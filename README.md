# Video Transcriber .NET 8

Uma aplicação desktop moderna e de alto desempenho desenvolvida em **C# (.NET 8 Windows Forms)** para transcrição **100% off-line** de áudio e vídeo utilizando a biblioteca **Vosk** e o **FFmpeg**. 

O projeto tem foco em produtividade, privacidade e facilidade de uso, extraindo o áudio de arquivos de mídia locais e convertendo-os em texto, sem enviar nenhum dado para a nuvem.

## 🚀 Principais Recursos

- **Transcrição 100% Offline:** Todo o processamento de áudio e reconhecimento de fala (Speech-to-Text) ocorre localmente no seu computador, garantindo privacidade total dos dados.
- **Extração Automática de Áudio:** Integração com FFmpeg para extrair e converter automaticamente streams de áudio de vídeos (MP4, MKV, etc.) e áudios diversos (MP3, M4A) para o formato WAV compatível com o Vosk.
- **Exportação Multiformato:**
  - **Texto Puro (TXT):** O texto contínuo da transcrição.
  - **Legendas Sincronizadas (SRT):** Arquivo de legenda pronto para ser anexado ao vídeo, com *timestamps* precisos.
  - **Documentos Word (RTF/DOCX):** Texto formatado para relatórios e edição.
- **Interface Moderna (Dark Mode):** Construída com Windows Forms, mas fugindo do padrão antigo, apresentando uma UI elegante, reativa, com barra de progresso e logs em tempo real.
- **Arquitetura Modular:** Separação clara de responsabilidades (Serviço de Interface, FFmpeg, Vosk e Exportação).

## 📋 Pré-requisitos

Para compilar e executar o projeto, você precisará ter instalado em sua máquina:

- **[.NET 8.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)**
- **Visual Studio 2022** (Recomendado) ou Visual Studio Code
- Sistema Operacional Windows (O projeto utiliza Windows Forms nativo).

## 🛠️ Como Executar o Projeto

1. **Faça o Download / Clone o Repositório:**
   Baixe os arquivos gerados ou faça o clone via Git.

2. **Abra a Solução:**
   Dê um duplo clique no arquivo `VideoTranscriber.sln` para abri-lo no Visual Studio.

3. **Restaurar Pacotes NuGet:**
   O Visual Studio deve restaurar os pacotes automaticamente. O projeto depende primariamente do pacote `Vosk`. Se necessário, force a restauração no console do gerenciador de pacotes:
   ```bash
   dotnet restore
   ```

4. **Execute (F5):**
   Aperte `F5` ou clique em "Start" no Visual Studio.
   > **Nota:** No primeiro uso, a aplicação fará automaticamente o download do FFmpeg (executável) e do modelo leve do Vosk para o idioma Português (aprox. 50MB no total) para dentro da pasta do projeto.

## 🛠️ Como Executar diretamente o programa da pasta

   > Baixe o arquivo start.zip, extraia para uma pasta e execute VideoTranscriber.exe 

## 🧩 Arquitetura do Código

A base de código foi estruturada com serviços bem definidos:

- `MainForm.cs`: A classe principal da interface gráfica. Gerencia eventos, arrastar/soltar arquivos, invoca as tarefas em *background* (`Task.Run`) e atualiza a UI (`Invoke`).
- `FFmpegService.cs`: Responsável pelo download e orquestração do executável do FFmpeg para converter a mídia de entrada em um fluxo `WAV Mono PCM de 16kHz`.
- `VoskService.cs`: Cuida do carregamento do modelo de rede neural, leitura do arquivo WAV decodificado e transformação das frequências em texto e timestamps.
- `ExportService.cs`: Trata a persistência da transcrição em arquivos estruturados (TXT, SRT, RTF).
- `TranscriptionSegment.cs`: Modelo de dados simples contendo início, fim e o texto de cada segmento falado.

## 📦 Modelos de Linguagem

O projeto vem configurado para baixar automaticamente o modelo `vosk-model-small-pt-0.3` (Português Brasileiro). 
Você pode alterar isso no código-fonte para baixar modelos maiores (mais precisos, porém mais lentos) ou para outros idiomas (Inglês, Espanhol, etc.), consultando os modelos disponíveis no site oficial: [Vosk Models](https://alphacephei.com/vosk/models).

## 🤝 Contribuições

Sinta-se livre para abrir *Issues*, reportar bugs e enviar *Pull Requests*. Toda melhoria na arquitetura, suporte a novos formatos de exportação ou melhorias na interface são super bem-vindas!

## 📜 Licença

Este projeto é disponibilizado sob a licença **MIT**. Você é livre para utilizar, modificar e distribuir o código. A biblioteca Vosk segue a licença Apache 2.0 e o executável do FFmpeg segue as diretrizes da GNU GPL / LGPL.
