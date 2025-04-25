# Aplicação de Chats e Configurações API no Azure OpenAI

## Objetivos

Este artigo tem como objetivo fornecer uma visão prática sobre como integrar a API do Azure OpenAI em diferentes tipos de aplicações, explorando suas funcionalidades, configurações e como utilizar os principais modos disponíveis: **Chat, Completar, Imagens e Áudio**.

Você aprenderá:

- Como realizar chamadas à API para diversos fins (chat, completar, gerar imagens e áudio).
- Como configurar e estruturar as chamadas de API.
- A importância do Semantic Kernel e como ele pode ser usado para construir IA de agentes inteligentes.
- Exemplos práticos em Python para facilitar a compreensão e implementação das funcionalidades.


## API do Azure OpenAI

A API do Azure OpenAI fornece acesso a uma série de modelos poderosos baseados na GPT (Generative Pre-trained Transformer) e outros modelos treinados, para execução de tarefas de processamento de linguagem natural, geração de imagens, transcrição de áudio e muito mais.

### Modos Suportados

- **Chat**: Permite interagir de forma conversacional com a IA, mantendo o estado da conversa e gerando respostas contextualizadas. Ideal para assistentes virtuais e chatbots.
- **Completar**: Usado para gerar ou completar textos com base em um prompt. Perfeito para completar frases, parágrafos ou até artigos.
- **Imagens**: Gera imagens a partir de uma descrição textual (*text-to-image*), utilizando IA para criar gráficos, ilustrações e fotos realistas.
- **Áudio**: Permite transcrever fala para texto ou gerar áudio a partir de texto, além de interpretar áudio de maneira eficaz.


## Exemplo de Uso com Python

Abaixo, um exemplo prático utilizando Python para interagir com os modos disponíveis na API do Azure OpenAI. O script cria um menu simples para o usuário selecionar entre as funcionalidades.

### Instalação das Bibliotecas Necessárias

No terminal, execute:

```bash
pip install openai requests
```


### Código Exemplo

```python
import openai
import os

# Substitua pelo seu Azure OpenAI key
openai.api_key = "SUA_CHAVE_API"

def chat_mode():
    prompt = input("Digite sua mensagem para o chat: ")
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    print("Resposta do Chat: ", response['choices'][0]['message']['content'])

def complete_mode():
    prompt = input("Digite o prompt para completar: ")
    response = openai.Completion.create(
        model="text-davinci-003",
        prompt=prompt,
        max_tokens=100
    )
    print("Texto Completo: ", response.choices[0].text)

def image_mode():
    prompt = input("Digite a descrição para gerar a imagem: ")
    response = openai.Image.create(
        prompt=prompt,
        n=1,
        size="1024x1024"
    )
    image_url = response['data'][0]['url']
    print("Imagem gerada: ", image_url)

def audio_mode():
    audio_file_path = input("Digite o caminho do arquivo de áudio: ")
    with open(audio_file_path, "rb") as audio_file:
        response = openai.Audio.transcribe(
            model="whisper-1",
            file=audio_file
        )
    print("Texto Transcrito: ", response['text'])

def main():
    while True:
        print("\nSelecione uma opção:")
        print("1. Chat")
        print("2. Completar")
        print("3. Gerar Imagem")
        print("4. Transcrever Áudio")
        print("5. Sair")
        
        choice = input("Escolha uma opção: ")

        if choice == '1':
            chat_mode()
        elif choice == '2':
            complete_mode()
        elif choice == '3':
            image_mode()
        elif choice == '4':
            audio_mode()
        elif choice == '5':
            break
        else:
            print("Opção inválida! Tente novamente.")

if __name__ == "__main__":
    main()
```


### Explicação do Código

- O código permite ao usuário selecionar uma funcionalidade específica (chat, completar, gerar imagem ou transcrever áudio).
- O modelo de chat `gpt-4` é utilizado para interações conversacionais.
- Para completar textos, o modelo `text-davinci-003` é usado para gerar novos conteúdos a partir de um prompt.
- No modo de imagem, o modelo DALL-E é chamado para gerar uma imagem baseada na descrição do usuário.
- O modo de áudio utiliza o modelo `whisper-1` para transcrever áudio para texto.

Este código pode ser facilmente adaptado para um chatbot ou assistente virtual mais avançado.

## Introdução ao Semantic Kernel

O **Semantic Kernel** é um framework desenvolvido pela Microsoft para auxiliar na criação de agentes inteligentes e aplicações de IA, permitindo a integração de modelos de linguagem como o OpenAI, serviços de nuvem e outras ferramentas de IA.

### Principais Componentes do Semantic Kernel

- **Agentes**: Entidades que realizam tarefas, como responder perguntas ou gerar conteúdo. Podem agir de forma autônoma ou sob controle do usuário.
- **Kernel**: Camada central que coordena e organiza as interações entre diferentes componentes da aplicação, integrando serviços e APIs externas, incluindo o Azure OpenAI.
- **Planos**: Representam as tarefas ou objetivos que o agente precisa atingir, podendo ser divididos em múltiplos passos para execução sequencial.

Ao integrar o Semantic Kernel com a API do Azure OpenAI, é possível criar sistemas sofisticados que executam interações contextuais baseadas em IA, como chatbots que aprendem com as conversas ou sistemas de automação de atendimento.

## Considerações Finais

A API do Azure OpenAI oferece uma ampla gama de funcionalidades para construir aplicações poderosas com IA. Com simples chamadas de API, é possível criar chatbots, gerar texto, produzir imagens e transcrever áudio. A combinação com o Semantic Kernel proporciona uma base sólida para o desenvolvimento de agentes inteligentes e aplicações mais complexas.

**Boas práticas incluem:**

- Proteger as chaves da API.
- Definir limites para evitar abuso do serviço.
- Para projetos de maior escala, explorar modelos especializados ou realizar treinamentos adicionais para personalizar o comportamento da IA.

A integração da API do Azure OpenAI com o Semantic Kernel é uma excelente forma de impulsionar suas aplicações de IA.

---

## Referências Bibliográficas

- Microsoft. (2024). Azure OpenAI Documentation. Disponível em: https://learn.microsoft.com/en-us/azure/cognitive-services/openai/
- Microsoft. (2023). Semantic Kernel Documentation. Disponível em: https://learn.microsoft.com/en-us/azure/ai-services/semantic-kernel/
- OpenAI. (2023). API Documentation. Disponível em: https://platform.openai.com/docs

