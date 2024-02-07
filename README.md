# zabbix_telegram
Integrando o Zabbix com o Telegram: Uma Abordagem Passo a Passo

# Introdução

O Zabbix é uma poderosa ferramenta de monitoramento de código aberto que permite o acompanhamento em tempo real da performance e disponibilidade de redes, servidores e outros dispositivos de TI. Uma das características mais valiosas do Zabbix é sua capacidade de alertar os administradores sobre eventos críticos. Uma forma eficaz de receber esses alertas é através do Telegram, uma popular plataforma de mensagens instantâneas.

## Passo 1: Preparando o Ambiente

Antes de começarmos, é importante garantir que você tenha acesso ao servidor Zabbix e ao Telegram. Certifique-se de ter as permissões necessárias em ambos os sistemas.

## Passo 2: Criando um Bot no Telegram

Abra o aplicativo Telegram e procure o BotFather - o bot oficial do Telegram para criar outros bots. Inicie uma conversa com o BotFather e use o comando /newbot para criar um novo bot.
Siga as instruções para escolher um nome e um username para o seu bot.
Ao finalizar, o BotFather irá fornecer um token de acesso. Mantenha este token seguro, pois ele será necessário para a integração.

## Passo 3: Configurando o Media Type no Zabbix

Acesse o painel do Zabbix e vá para "Administração" -> "Tipos de Mídia".
Crie um novo tipo de mídia e selecione "Script" como tipo.
Em "Nome", coloque um rótulo descritivo, como "Telegram Bot".
No campo "Script Nome", insira o caminho do script que iremos criar no próximo passo.
Adicione o token do Bot do Telegram como parâmetro (pode ser feito diretamente no script, conforme detalharemos).

## Passo 4: Criando o Script de Envio para o Telegram

Vamos criar um script Python para enviar mensagens para o Telegram. Use o exemplo abaixo como ponto de partida:

```script Python
import requests

def send_telegram_message(bot_token, chat_id, message):
    url = f"https://api.telegram.org/bot{bot_token}/sendMessage"
    data = {"chat_id": chat_id, "text": message}
    requests.post(url, data=data)

if __name__ == "__main__":
    bot_token = "SEU_TOKEN_AQUI"
    chat_id = "SEU_CHAT_ID_AQUI"
    message = "Testando integração Zabbix-Telegram"

    send_telegram_message(bot_token, chat_id, message)
```

Lembre-se de substituir "SEU_TOKEN_AQUI" pelo token do seu bot e "SEU_CHAT_ID_AQUI" pelo ID do chat para onde as mensagens serão enviadas.

## Passo 5: Automatizando os Alertas no Zabbix

No Zabbix, vá até "Configuração" -> "Ações".
Crie uma nova ação e configure os critérios de disparo conforme a necessidade.
Em "Operações de Recuperação", adicione uma operação do tipo "Enviar mensagem para o usuário" e selecione o tipo de mídia "Telegram Bot" que criamos anteriormente.
Adicione o script Python como "Script Nome".
