# ffmpeg-compartilhamento-audio
Repositório com informações para compartilhamento de áudio entre computadores conectados na mesma rede.

## Problema
Utilizar 2 (dois) computadores na mesma rede (Sistemas Operacionais: Windows 10 Pro - Versão 22H2 e Ubuntu 24.04.3 LTS), sendo que apenas 1 (um) computador tem caixa de som (SO: Windows 10 Pro).

## Ferramentas utilizadas
FFMPEG (https://ffmpeg.org/): Uma solução completa e multiplataforma para gravar, converter e transmitir áudio e vídeo.

## Instalação no Windows (que será chamada de máquina Server)
No link oficial da ferramenta FFMPEG (https://ffmpeg.org/), é possivel acessar a aba Download (https://ffmpeg.org/download.html), selecionar o sistema operacional Windows e acessar o primeiro link (https://www.gyan.dev/ffmpeg/builds/). Deve ser baixado a Compilação mestre do Git na versão full (https://www.gyan.dev/ffmpeg/builds/ffmpeg-git-full.7z).

Após realizar o download do arquivo zipado, a pasta deve ser extraída e renomeada para "ffmpeg". A pasta pode ser movida para o caminho padrão dos Arquivos de Programas (C:\Program Files (x86)).

## Instalação no Ubuntu (que será chamada de máquina Client)
A ferramenta FFMPEG pode ser instalada diretamente utilizando o comando a seguir:
```
sudo apt install ffmpeg
```

## Comando para envio do áudio
O comando a seguir deverá ser executado na máquina Client que enviará a saída de áudio.

```
ffmpeg -f pulse -i default -c:a libmp3lame -f rtp rtp://<endereço IP da máquina server>:<porta>
```

**`default`**: Representa a entrada de áudio padrão do PulseAudio.

**`libmp3lame`**: Codifica o áudio para MP3.

**`rtp://<endereço IP da máquina server>:<porta>`**: O endereço IP da máquina Server e a porta onde estará escutando, geralmente se utiliza a porta `1234` é importante que seja utilizado o mesmo endereço IP e Porta nos comandos de envio e recebimento do áudio.

### Script de Automação (Envio)
Arquivo: `EnvioAudio.sh`

O arquivo deve ser baixado, deve ser configurado o endereço IP e porta e deve executar o comando a seguir, para tornar o arquivo executável: ```chmod +x ./EnvioAudio.sh```

Ao executar o arquivo, será aberto o terminal e exibirá as informações sobre a transmissão do áudio.

## Comando para recebimento do áudio
O comando a seguir deverá ser executado na máquina Server que receberá a saída de áudio da máquina Client.

```
ffplay rtp://<endereço IP da máquina server>:<porta>
```

O endereço e porta devem ser o mesmo utilizado na máquina Client.

### Script de Automação (recebimento)
Arquivo: `RecebimentoAudio.bat`

O arquivo deve ser baixado, deve ser configurado o endereço IP e porta e ao ser executado, abrirá o terminal e exibirá as informações sobre a transmissão do áudio.
