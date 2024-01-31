<h1 align="center"> Serviço YOLO na Google Cloud Platform (GCP) </h1>

## Índice

1. INTRODUÇÃO
2. VANTAGENS
3. YOLO
4. GCP Setup
5. Configuração do Sistema
6. Comandos Systemctl

## INTRODUÇÃO

Este repositório contém um projeto que utiliza o algoritmo YOLO (You Only Look Once) para detecção de objetos com integração ao serviço configurado na GCP. Este README fornece informações essenciais para configurar, executar e gerenciar o serviço usando o systemctl, proporcionando facilidade de gerenciamento e automação.

O systemctl é uma ferramenta de controle e gerenciamento central para o sistema e o gerenciador de serviços systemd. Ele desempenha um papel crucial em sistemas operacionais baseados em systemd, como muitas distribuições Linux modernas, tais como o Ubuntu 16.04 e posteriores.

## VANTAGENS
	
  - O systemctl fornece uma interface de linha de comando simples e consistente para gerenciar serviços, tornando as operações de inicialização, parada e reinicialização intuitivas.
  - Automatiza a resolução de dependências entre unidades (serviços), garantindo que serviços dependentes sejam iniciados ou parados na ordem apropriada.
  - Facilita o monitoramento do status de unidades com o comando status, fornecendo informações detalhadas, mensagens de log associadas e indicadores visuais do estado da unidade.
  - Integra-se ao journalctl, consolidando logs de sistema e permitindo que os usuários obtenham informações detalhadas sobre o histórico de eventos do sistema.
  - Utiliza arquivos de configuração padronizados para definir propriedades de unidades, simplificando a leitura, escrita e manutenção das configurações do sistema.
  - Permite facilmente habilitar ou desabilitar serviços para serem iniciados automaticamente durante a inicialização do sistema, proporcionando flexibilidade na configuração do ambiente.
  - Além de serviços, systemctl gerencia timers (tarefas agendadas), sockets (comunicação entre serviços) e outras unidades, proporcionando uma gestão completa do sistema.

O systemctl se destaca como uma ferramenta poderosa e versátil para administradores de sistemas, oferecendo controle robusto sobre o ambiente do sistema operacional.


## YOLO

YOLO é uma técnica de detecção de objetos em imagens e vídeos que se destaca pela sua eficiência, processando a imagem inteira de uma vez, em vez de dividir a imagem em grades. Ele fornece resultados rápidos e precisos, sendo amplamente utilizado em diversas aplicações.

## GCP Setup

1. Crie uma Conta na GCP

Se ainda não tiver uma conta na GCP, crie uma em https://console.cloud.google.com/.

2. Crie um Projeto

Na Console da GCP, crie um novo projeto para hospedar seus recursos.
Aqui você pode encontrar um tutorial detalhado sobre esse tópico: https://cloud.google.com/resource-manager/docs/creating-managing-projects?hl=pt-br

## Configuração do Sistema

Primeiro, configure o ambiente para a aplicação. Neste caso, o YOLOv8

Instalando as dependências
```
pip install ultralytics
```

Crie arquivo de serviço
```
sudo nano /etc/systemd/system/detect_object.service
```

Altere o arquivo com seu respectivo diretório
```
[Unit]
Description=Object_Detection

[Service]
Type=simple
ExecStart=/home/projects/detect_object.py
Restart=always

[Install]
WantedBy=default.target
```

Recarregue o systemd, inicie e verifique o status
```
sudo systemctl daemon-reload
sudo systemctl start detect_object
sudo systemctl enable detect_object
sudo systemctl status detect_object
```
