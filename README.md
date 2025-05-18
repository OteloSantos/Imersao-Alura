# 🧠 Sistema de Informação e Apoio para Famílias com Síndromes Raras

Este projeto utiliza uma cadeia de Agentes de Inteligência Artificial para buscar, organizar e apresentar informações sobre síndromes raras de forma empática para famílias.

## 🌟 Propósito

Diagnósticos de síndromes raras podem ser momentos de muita incerteza e necessidade de informação para as famílias. O objetivo deste projeto é fornecer uma ferramenta automatizada que auxilie os pais a obter informações iniciais relevantes sobre a síndrome diagnosticada em seus filhos, incluindo aspectos da condição, opções de apoio e tratamento paliativo, e sugestões de perguntas importantes para a equipe médica, tudo apresentado de maneira acolhedora e humana.

## ✨ Como Funciona

O sistema opera como um pipeline de três Agentes de IA, cada um com uma função específica:

1.  **🕵️ Agente Buscador:**
    * **Entrada:** Nome da síndrome rara.
    * **Função:** Utiliza a ferramenta Google Search para pesquisar extensivamente sobre a síndrome, buscando o máximo de fontes relevantes e confiáveis possíveis.
    * **Saída:** Uma compilação de informações e referências encontradas na pesquisa.

2.  **📚 Agente Organizador:**
    * **Entrada:** Nome da síndrome e os resultados da pesquisa do Agente Buscador.
    * **Função:** Atuando como um pesquisador científico, processa os resultados da busca, utilizando o Google Search novamente se necessário para aprofundar. Extrai e organiza os pontos mais importantes da síndrome, formas de amparo à família, tratamentos paliativos e perguntas essenciais para os pais fazerem aos médicos.
    * **Saída:** Informações estruturadas e organizadas sobre a síndrome com foco nos aspectos relevantes para a família.

3.  **🫂 Agente Acolhedor:**
    * **Entrada:** Nome da síndrome e as informações organizadas pelo Agente Organizador.
    * **Função:** Assumindo a persona de um Psicólogo do Serviço Social virtual, este agente recebe as informações organizadas e as reescreve em uma mensagem empática, clara, amorosa e encorajadora, validando os sentimentos dos pais e reforçando a importância do diálogo com a equipe médica.
    * **Saída:** Uma mensagem final humanizada e de apoio direcionada aos pais.

## 🛠️ Tecnologias Utilizadas

* **Python:** Linguagem de programação principal.
* **Google AI / Gemini Models:** Modelos de linguagem utilizados pelos agentes (`gemini-1.5-flash-latest`, `gemini-1.5-pro-latest` ou outros modelos suportados - *verificar modelos disponíveis*).
* **Agential Framework (Google):** Biblioteca para construção e orquestração dos agentes.
* **Google Search Tool:** Ferramenta utilizada pelos agentes Buscador e Organizador para realizar pesquisas online.
* **Google Colab / Jupyter Notebooks:** Ambiente de desenvolvimento e execução.

## ⚙️ Configuração e Instalação

1.  **Clone o Repositório:**
    ```bash
    git clone [https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git](https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git)
    cd SEU_REPOSITORIO
    ```
    *(Substitua `SEU_USUARIO` e `SEU_REPOSITORIO` pelo seu usuário e nome do repositório no GitHub)*

2.  **Crie um Ambiente Virtual (Recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate # No Windows use `venv\Scripts\activate`
    ```

3.  **Instale as Dependências:**
    ```bash
    pip install -r requirements.txt
    ```
    *(Crie um arquivo `requirements.txt` na raiz do seu projeto com as seguintes linhas):*
    ```
    agential
    google-generativeai
    markdown
    textwrap
    ipython
    ```

4.  **Obtenha sua Chave de API do Google AI:**
    Você precisa de uma chave de API para usar os modelos Gemini. Obtenha a sua no [Google AI Studio](https://aistudio.google.com/app/apikey).

5.  **Configure a Chave de API e Ferramentas no Código:**
    No seu notebook Colab ou script Python, adicione as configurações necessárias no início (geralmente na primeira célula):

    ```python
    import google.generativeai as genai
    from agential.tools.Google Search import Google Search # Verifique a documentação exata da Agential para inicialização da tool

    # Configure a API Key
    # Substitua 'YOUR_API_KEY' pela sua chave real ou use variáveis de ambiente
    genai.configure(api_key='YOUR_API_KEY')

    # Inicialize a ferramenta Google Search (forma pode variar ligeiramente dependendo da versão da Agential)
    try:
        Google Search = Google Search()
    except Exception as e:
        print(f"Erro ao inicializar a ferramenta Google Search: {e}")
        print("Certifique-se de que a ferramenta está configurada corretamente (verifique a documentação da Agential).")
        Google Search = None # Garante que o código não falhe completamente se a tool não inicializar
    ```
    **Nota:** Lembre-se do erro `404 NOT_FOUND` que vimos. Verifique a lista de modelos disponíveis (`genai.list_models()`) e use nomes de modelos válidos e suportados (`gemini-1.5-flash-latest`, `gemini-1.5-pro-latest`, etc.) nas definições dos seus agentes nas células 03, 04 e 05.

## ▶️ Como Executar

Este projeto foi desenvolvido para ser executado em um ambiente de notebook como o Google Colab.

1.  Abra o arquivo do notebook (`seu_projeto.ipynb`) no Google Colab.
2.  Execute as células em ordem:
    * Célula de instalação de dependências (se não usou `pip install -r`).
    * Célula de configuração da API Key e inicialização da ferramenta Google Search.
    * Células que definem as funções auxiliares (`call_agent`, `to_markdown`).
    * Células que definem cada um dos agentes (`agente_buscador`, `agente_organizador`, `agente_acolhedor`).
    * A Célula final de orquestração (Célula 06 no seu exemplo).
3.  Quando solicitado na Célula 06, digite o nome da síndrome rara e pressione Enter.
4.  Aguarde a execução sequencial dos agentes. O resultado de cada agente será exibido, seguido pela mensagem final do Agente Acolhedor.
