# Agente de IA

Agente de IA são sistemas de inteligencia artificial com algum nível de autonomia.

Esses sistemas podem perceber o ambiente, processar informações, aprender e agir de forma autonoma para atingir objetivos específicos.

## Funcionamento de um agente de IA

- [ ] **Percepção**: coleta de informações do ambiente (testo, vozm vídeom áudio, dados de sistemas)

- [ ] **Processamento Raciocínio**: pode ser alimentado por grandes modelos de LLMs(Modelos de linguagem Machine Learning), processamento dos dados, acessar conhecimentos armazenados, elaborar planos para analisar dados, identificar padrões, fazer previsões e/ ou tomar decisões.

- [ ] **Ação**: conforme a decisão o agente vai executar ações em formato: texto, uso de ferramentas, interação com sistemas ou operar ambientes(robôs).

### Exemplos de aplicação:

Agente para avaliar curriculo, Agente para criar roteiros de viagens, Agente para analisar dados e encontrar padrões.

Esse Agentes podem executar cadeias de tarefas pequenas para atingir o objetivo final, tomam decisões e conseguem decompor atividades maiores para menores.

**Chatbots** - linguagem conversacional (ChatGPT, Claude)

**Raciocinadores** - modelo mais avançado de IA, indicados para resolver problemas em nível humano com raciocínio complexo.

**Agente de IA** - pode realizar ações autonomas, tem memória persistente e integração com ferramentas externas. 

## Prática

Para essa primeira prática vamos utilizar:

VisualStudio Code:

1. Criar uma pasta para o projeto(meu caso pasta IA)

2. Criar o ambiente virtual de desenvolvimento comando: `python -m venv .venv` isso vai facilitar o deploy e controle das versões das bibliotecas

3. Ver lista de bibliotecas que temos no projeto, comando:` pip list`

4. Execute o comando em terminal PowerShell: `.\.venv\Scripts\activate`. Resultado esperado:![93b0e4b3-cebb-45a7-9368-7ff0141de335](file:///C:/Users/Jacqueline/Pictures/Typedown/93b0e4b3-cebb-45a7-9368-7ff0141de335.png)

5. Agora ao executar o comando: `pip list`, vamos ver apenas os pacotes instalados para esse projeto em particular.

6. Criar o arquivo para indicar as extensões que vamos trabalhar no projeto: na raiz do projeto arquivo requirements.txt conteúdo do arquivo: 

```
crewai
ipykernel
python-dotenv
```

### `crewai`

A biblioteca `crewai` é uma estrutura (framework) para construir e gerenciar **agentes de IA colaborativos**. Pense nela como uma ferramenta que permite criar equipes de "trabalhadores" de IA, onde cada trabalhador (agente) tem um papel, um objetivo e uma história de fundo, e eles podem colaborar para resolver problemas complexos.

**O que ela faz:**

* **Orquestração de Agentes:** Permite definir múltiplos agentes de IA, cada um com sua especialidade (`role`), seu propósito (`goal`) e sua personalidade (`backstory`).
* **Gestão de Tarefas:** Você pode definir tarefas específicas (`Task`) e atribuir essas tarefas a agentes específicos.
* **Fluxo de Trabalho:** A `crewai` permite definir como as tarefas serão executadas:
  * **Sequencial (`Process.sequential`):** Uma tarefa é concluída antes que a próxima comece, e a saída de uma tarefa pode servir de entrada para a próxima. É o que você usou no seu exemplo.
  * **Hierárquico (`Process.hierarchical`):** Um agente "gerente" ou "supervisor" delega e supervisiona as tarefas de outros agentes.
* **Colaboração:** Facilita a comunicação e a passagem de informações entre os agentes, permitindo que eles trabalhem juntos para atingir um objetivo comum.
* **Integração com LLMs:** Por baixo dos panos, ela se integra com Modelos de Linguagem Grandes (LLMs) como o GPT da OpenAI (o que você está usando), Gemini, etc., para que os agentes possam "pensar", "raciocinar" e gerar respostas.

### `ipykernel`

`ipykernel` é o **kernel IPython para Jupyter e outros front-ends compatíveis**.

**O que ele faz:**

* **Motor de Execução:** Ele é o "motor" que executa o código Python que você escreve em ambientes como notebooks Jupyter (ou JupyterLab, Google Colab, etc.).
* **Comunicação:** Ele estabelece uma comunicação bidirecional entre o ambiente onde você escreve seu código (o notebook, por exemplo) e o ambiente onde o código é realmente processado (o Python interpreter).
* **Interatividade:** Permite que você execute células de código individualmente, veja os resultados imediatamente e mantenha o estado das variáveis e funções entre as execuções de células.

### `python-dotenv`

A biblioteca `python-dotenv` é uma ferramenta simples para **carregar variáveis de ambiente de arquivos `.env`**.

**O que ela faz:**

* **Segurança de Credenciais:** Permite que você armazene informações sensíveis, como chaves de API, senhas, tokens, etc., em um arquivo separado chamado `.env` (ou qualquer outro nome que você configurar).
* **Separação de Configuração:** Mantém suas configurações específicas de ambiente (como sua chave da OpenAI) separadas do seu código-fonte principal. Isso é uma prática recomendada de desenvolvimento de software.
* **Carregamento Simples:** A função `load_dotenv()` lê o arquivo `.env` e automaticamente adiciona as variáveis definidas nele ao ambiente do seu sistema (ou ao ambiente do seu processo Python).

---

7. Executa comando para instalar as bibliotecas do arquivo requirements.txt: `pip install -r ./requirements.txt`

8. Criar o arquivo .env, adicionar a chave da sua OPENAI:
    `OPENAI_API_KEY=sk-proj-Oq42ij3H--------`

9. Criar o arquivo agent.ipynb

10. Clique em selecionar o Kernel - escolher Python Enveronments
    
    1. Caso não tenha opções de Kernel pode instalar as kernels padrão
    
    2. Escolher Python Enveronments
    
    3. Escolher opção .venv(Python versão..)

11. Clique em code e adicione o seguinte código:

```
from dotenv import load_dotenv
_ = load_dotenv()
from crewai import Crew, Process, Agent, Task
```

Entendendo o código:
`from dotenv import load_dotenv`: Esta linha importa a função load_dotenv da biblioteca dotenv. Essa biblioteca é super útil para carregar variáveis de ambiente de um arquivo .env para o seu ambiente de execução. Isso é crucial para manter informações sensíveis, como chaves de API, seguras e fora do seu código-fonte principal.
`_ = load_dotenv()` #carrega o arquivo com a variavel de ambiente e chave da api: Aqui, a função load_dotenv() é chamada. Quando você tem um arquivo .env (que, no seu caso, provavelmente contém sua chave da OpenAI), essa função lê esse arquivo e disponibiliza as variáveis ali definidas para o seu programa. O _ = é apenas uma convenção para indicar que o valor de retorno da função não será usado diretamente, mas a ação de carregar as variáveis já ocorreu.

**`from crewai import Crew, Process, Agent, Task`**: Esta linha importa quatro classes principais da biblioteca `crewai`:

* **`Crew`**: A "equipe" ou "tripulação" principal que orquestra os agentes e as tarefas.
* **`Process`**: Define o fluxo de trabalho entre as tarefas (neste caso, `Process.sequential` significa que uma tarefa será executada após a outra).
* **`Agent`**: A classe base para definir cada agente individual.
* **`Task`**: A classe para definir as tarefas que os agentes irão executar.

---

12. Execute esse comando:
       Objetivo do codigo será informar o arquivo onde inputamos as variáveis de ambiente.
       ![a8054bdd-c472-4771-a871-403b3ed4d7ca](file:///C:/Users/Jacqueline/Pictures/Typedown/a8054bdd-c472-4771-a871-403b3ed4d7ca.png)
    
    * **`from dotenv import load_dotenv`**: Esta linha importa a função `load_dotenv` da biblioteca `dotenv`. Essa biblioteca é super útil para carregar variáveis de ambiente de um arquivo `.env` para o seu ambiente de execução. Isso é crucial para manter informações sensíveis, como chaves de API, seguras e fora do seu código-fonte principal.
    * **`_ = load_dotenv() #carrega o arquivo com a variavel de ambiente e chave da api`**: Aqui, a função `load_dotenv()` é chamada. Quando você tem um arquivo `.env` (que, no seu caso, provavelmente contém sua chave da OpenAI), essa função lê esse arquivo e disponibiliza as variáveis ali definidas para o seu programa. O `_ =` é apenas uma convenção para indicar que o valor de retorno da função não será usado diretamente, mas a ação de carregar as variáveis já ocorreu.
    * **`from crewai import Crew, Process, Agent, Task`**: Esta linha importa quatro classes principais da biblioteca `crewai`:
      * **`Crew`**: A "equipe" ou "tripulação" principal que orquestra os agentes e as tarefas.
      * **`Process`**: Define o fluxo de trabalho entre as tarefas (neste caso, `Process.sequential` significa que uma tarefa será executada após a outra).
      * **`Agent`**: A classe base para definir cada agente individual.
      * **`Task`**: A classe para definir as tarefas que os agentes irão executar.
    
    ---
    
    

13. Criar nova célula em +Code adicionar o seguinte comando
    
    O código a seguir define algumas caracteristicas da task do agent

```
planejador_de_viagem = Agent(
    role="Planejador de viagem",
    goal="Planejar todos os detalhes de uma viagem, incluindo roteiros e atividades",
    #as tres aspas duplas permite incluir um texto de mais de uma linha
    backstory="""
    Você é um especialista em planejamento de viagens, sempre em busca de
    novas aventuras e experiências. Seu objetivo é garantir os detalhes da viagem
    para que sejam organizados de maneira eficiente e agradável.
    """,
    verbose=True
)
```

* **`planejador_de_viagem = Agent(...)`**: Esta linha cria uma instância de um agente, chamando-o de `planejador_de_viagem`.
* **`role="Planejador de viagem"`**: Define o papel ou a função principal desse agente dentro da equipe. É como o seu título profissional.
* **`goal="Planejar todos os detalhes de uma viagem, incluindo roteiros e atividades"`**: O objetivo específico que este agente deve alcançar. Isso ajuda a direcionar seu comportamento e suas respostas.
* **`backstory="""..."""`**: Esta é uma descrição detalhada do "passado" ou da personalidade do agente. É como dar uma história de fundo que o ajuda a se comportar de forma mais coerente e "inteligente" dentro de seu papel. As três aspas duplas (`"""`) permitem que você escreva um texto com múltiplas linhas, o que é ótimo para descrições mais longas.
* **`verbose=True`**: Se definido como `True`, este agente fornecerá saídas mais detalhadas sobre o seu processo de pensamento e as ações que está realizando durante a execução. É útil para depuração e para entender como ele está trabalhando.

---



14. Adicionar mais uma célula, agora com o seguinte comando:

```
orcamentista = Agent(
    role="Orçamentista da viagem",
    goal="Estimar o custo total de uma viagem, considerando transporte, hospedagem, alimentação e atividades",
    backstory="""
    Você é um analista financeiro focado em viagem. Sua missão é garantir que os custos estejam
    dentro do orçamento, criando estimativas precisas para cada parte da viagem.
    """
)
```

* **`orcamentista = Agent(...)`**: Semelhante ao agente anterior, esta linha cria uma nova instância de agente, chamada `orcamentista`.
* **`role="Orçamentista da viagem"`**: Seu papel é ser o especialista em orçamento.
* **`goal="Estimar o custo total de uma viagem, considerando transporte, hospedagem, alimentação e atividades"`**: Seu objetivo é calcular os custos de forma abrangente.
* **`backstory="""..."""`**: Sua história de fundo o define como um analista financeiro focado em viagens, com a missão de criar estimativas precisas. Observe que `verbose` não foi definido aqui, então o padrão será `False`, o que significa que ele será menos "tagarela" em sua saída.
  
  ---
  
  

 15. Criar mais uma cédula, agora para a task:

Note que esse código acessa o agente que criamos anteriormente para executar a task em questão, aqui estamos relacionando o script com a ação.

```
planeja_roteiro=Task(
    description="Crie um roteiro detalhado para uma viagem para Europa, incluindo as cidades, atividades e transporte",
    agent=planejador_de_viagem,
    expected_output="""
    Um roteiro com a sequência de cidades a serem visitadas, as principais atividades
    e o tipo de transporte a ser utilizado.
    """
)
```

  

* **`planeja_roteiro=Task(...)`**: Esta linha cria uma tarefa específica, nomeada `planeja_roteiro`.
* **`description="Crie um roteiro..."`**: A descrição detalhada do que a tarefa envolve. É a instrução principal para o agente que a executará.
* **`agent=planejador_de_viagem`**: Esta é uma associação crucial! Ela informa qual agente é responsável por executar esta tarefa. Neste caso, o `planejador_de_viagem` será o encarregado.
* **`expected_output="""..."""`**: Define o formato e o conteúdo esperado da saída desta tarefa. Isso ajuda o agente a saber o que deve produzir e também permite que outros agentes ou o sistema avaliem a qualidade da saída. 

---



 16. Crie mais uma célula e adicione o seguinte código:

```
estima_orcamento=Task(
    description="Calcule o orçamento total para a viagem , levando em consideração as cidades, transporte, hospedagem e atividades",
    agent=orcamentista,
    expected_output="""
    Uma estimativa detalhada com os custos detalhados para cada item da viagem.
    """
)
```

* **`estima_orcamento=Task(...)`**: Cria uma segunda tarefa, `estima_orcamento`.
* **`description="Calcule o orçamento total..."`**: A descrição da tarefa, focada no cálculo do orçamento.
* **`agent=orcamentista`**: Esta tarefa é atribuída ao agente `orcamentista`.
* **`expected_output="""..."""`**: Define o tipo de saída esperada, uma estimativa detalhada dos custos.

---



17. Crie mais uma célula e vamos adicionar agora o código que vai ordenar as ações em forma sequencial: 

```
viagem_crew=Crew(
    agents=[planejador_de_viagem, orcamentista],
    tasks=[planeja_roteiro,estima_orcamento],
    process=Process.sequential
)
```

* **`viagem_crew=Crew(...)`**: Esta linha inicializa a equipe principal, chamada `viagem_crew`.
* **`agents=[planejador_de_viagem, orcamentista]`**: Uma lista de todos os agentes que farão parte desta equipe. Neste caso, são os dois agentes que você definiu.
* **`tasks=[planeja_roteiro,estima_orcamento]`**: Uma lista de todas as tarefas que esta equipe deve executar. As tarefas serão executadas na ordem em que aparecem na lista.
* **`process=Process.sequential`**: Define como as tarefas serão executadas. `Process.sequential` significa que as tarefas serão executadas uma após a outra, em ordem. A `crewai` também oferece `Process.hierarchical`, onde um agente supervisor delega tarefas a outros.

---



18. Por fim, vamos criar o código em nova célula, para executar todo nosso script:

```
result=viagem_crew.kickoff()
```

**`result=viagem_crew.kickoff()`**: Esta é a linha que dá início à execução da equipe! Quando `kickoff()` é chamado, a `viagem_crew` começa a trabalhar. Ela vai:

> 1. Delegar a tarefa `planeja_roteiro` ao `planejador_de_viagem`.
> 2. Uma vez que o `planejador_de_viagem` tenha concluído sua tarefa e produzido o `expected_output` (o roteiro), a equipe passará para a próxima tarefa.
> 3. Delegar a tarefa `estima_orcamento` ao `orcamentista`.
> 4. O `orcamentista` usará (se necessário, o que é ideal neste caso) as informações geradas pelo `planejador_de_viagem` para calcular o orçamento.
> 5. O resultado final de todas as tarefas será armazenado na variável `result`.

O resultado esperado pode vir truncado, mas após um tempo de processamento será gerado:

![a693595f-af29-44da-9136-5adc8519d33e](file:///C:/Users/Jacqueline/Pictures/Typedown/a693595f-af29-44da-9136-5adc8519d33e.png)

Resultado:

```
# Agent: Planejador de viagem
## Task: Crie um roteiro detalhado para uma viagem para Europa, incluindo as cidades, atividades e transporte


# Agent: Planejador de viagem
## Final Answer: 
**Roteiro Detalhado para uma Viagem à Europa (14 dias)**  

**Cidades a serem visitadas:**  
1. Lisboa, Portugal  
2. Madrid, Espanha  
3. Paris, França  
4. Amsterdã, Países Baixos  
5. Roma, Itália  

**Dia 1: Chegada em Lisboa**  
- **Atividades:**  
  - Check-in no hotel  
  - Passeio pelo Bairro Alto  
  - Jantar em um restaurante local (Experimente a culinária portuguesa)   
- **Transporte:** Carro do aeroporto para o hotel ou táxi

**Dia 2: Lisboa**  
- **Atividades:**  
  - Visita à Torre de Belém e Mosteiro dos Jerônimos  
  - Almoço no Mercado da Ribeira  
  - Passeio de bonde 28  
  - Visita ao Castelo de São Jorge  
- **Transporte:** Metrô e bonde local

**Dia 3: Lisboa - Madrid**  
- **Atividades:**  
  - Manhã livre  
  - Viagem de trem para Madrid (aproximadamente 3 horas)  
- **Transporte:** Trem (Renfe)  

**Dia 4: Madrid**  
- **Atividades:**  
  - Visita ao Museu do Prado  
  - Passeio pela Plaza Mayor e mercado de San Miguel  
  - Jantar com tapas em um bar local  
- **Transporte:** Metrô e a pé

**Dia 5: Madrid - Paris**  
- **Atividades:**  
  - Manhã livre e visita ao Parque do Retiro  
  - Viagem de trem para Paris (aproximadamente 2h30)  
- **Transporte:** Trem (Renfe/SNCF)  

**Dia 6: Paris**  
- **Atividades:**  
  - Visita à Torre Eiffel  
  - Passeio pelo Champs-Élysées  
  - Visita ao Arco do Triunfo  
  - Jantar em um bistrô francês  
- **Transporte:** Metrô e a pé

**Dia 7: Paris**  
- **Atividades:**  
  - Visita ao Museu do Louvre  
  - Almoço no Jardim das Tulherias  
  - Passeio pelo bairro de Montmartre e visita à Basílica de Sacré-Cœur  
- **Transporte:** Metrô e ônibus

**Dia 8: Paris - Amsterdã**  
- **Atividades:**  
  - Manhã livre para compras  
  - Viagem de trem para Amsterdã (aproximadamente 3 horas)  
- **Transporte:** Trem (Thalys)  

**Dia 9: Amsterdã**  
- **Atividades:**  
  - Visita ao Museu Van Gogh  
  - Passeio pelos canais de barco  
  - Jantar em um restaurante à beira do canal  
- **Transporte:** Bicicleta ou a pé

**Dia 10: Amsterdã - Roma**  
- **Atividades:**  
  - Manhã livre  
  - Voar para Roma (aproximadamente 2h30)  
- **Transporte:** Avião

**Dia 11: Roma**  
- **Atividades:**  
  - Visita ao Coliseu e Fórum Romano  
  - Almoço em Trastevere  
  - Visita ao Vaticano - Basílica de São Pedro e Capela Sistina  
- **Transporte:** Metrô e a pé

**Dia 12: Roma**  
- **Atividades:**  
  - Visita à Praça Navona e Panteão  
  - Passeio pela Fontana di Trevi  
  - Jantar em uma trattoria italiana  
- **Transporte:** Metrô e a pé

**Dia 13: Roma - Retorno**  
- **Atividades:**  
  - Manhã livre para compras ou atividades de último minuto  
  - Check-out do hotel  
- **Transporte:** Carro do hotel para o aeroporto ou táxi   

**Dia 14: Retorno para Casa**  
- Vôo de volta para casa  

Este roteiro proporciona uma mistura rica de cultura, história e gastronomia, acompanhada de transporte eficiente entre as principais cidades da Europa. Todas as atividades sugeridas permitem uma experiência imersiva em cada destino. Boa viagem!

```


