---
layout: post
title: "Intelbras inicia abertura das APIs de seus dispositivos"
description: "Imagine que incrível seria gerenciar dispositivos como roteadores, câmeras de monitoramento, centrais telefônicas ou rádios de transmissão por meio de chamadas de API."
date: 2018-01-10 00:00:00
comments: true
keywords: "API, IoT, Network"
category: post
image: ../images/ap360.webp
tags:
- IoT
- API
---

Imagine que incrível seria gerenciar dispositivos como roteadores, câmeras de monitoramento, centrais telefônicas ou rádios de transmissão por meio de chamadas de API. Então… A Intelbras está caminhando para isso. Nos últimos dias, a empresa abriu para a comunidade a [documentação da API](https://izeus.docs.apiary.io/#) de uma plataforma IoT (Zeus) que no futuro será integrada em todos os seus produtos.

<iframe src="https://giphy.com/embed/26ufdipQqU2lhNA4g" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/producthunt-mind-blown-blow-your-26ufdipQqU2lhNA4g">via GIPHY</a></p>

Eu particularmente fico muito feliz em divulgar iniciativas como essa, pois estou ativamente tentando nas comunidades mostrar para as pessoas e empresas a importância de abrir plataformas, códigos e ideias. ❤

Essa aproximação de grandes empresas da indústria com comunidades de tecnologia aumenta o potencial de criação de oportunidades, geração de renda e fomento à inovação.

Inicialmente, a empresa fez o lançamento da Plataforma Zeus somente para a linha de [Access Points](https://www.intelbras.com/pt-br/roteador-empresarial-com-tecnologia-wi-fi-4-ap-310).

<h2>Onde comprar?</h2>
Caso queira gastar seus dinheiros nos Access Points para brincar de IoT, além dos Canais Oficiais de Vendas da Intelbras, você pode conferir os produtos aqui: AP 360 e AP 310. \o/

<h2>Arquitetura</h2>
A arquitetura do projeto se divide em 3 camadas principais: IU (Interface do Usuário), API (Interface de Programação de Aplicativos) e Serviços.

A camada IU é responsável pela apresentação dos dados ao usuário na interface padrão web que se comunica com a API via requisições HTTPS (REST).

A API é responsável por receber as requisições IU e repassar para os serviços do sistema. A resposta dos serviços é filtrada antes de ser repassada, para atender o padrão de comunicação da API.

Os serviços são responsáveis pelo acesso aos recursos do sistema através do barramento. Dessa forma, quando for necessário acessar um recurso cujo acesso é dependente do hardware, este acesso poderá ser abstraído através de uma HAL (Camada de Abstração de Hardware).

<h2>Como consumir a API?</h2>
Assim que você estiver com um Access Point, basta retirá-lo da caixa, alterar a senha do usuário admin que vem definida por padrão de fábrica, conectá-lo na rede e pronto, a API já está disponível para você brincar :)

<iframe src="https://giphy.com/embed/RzKHvdYC3uds4" width="480" height="392" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/ministry-of-silly-walks-gif-monty-python-RzKHvdYC3uds4">via GIPHY</a></p>

Eu vou mostrar para vocês alguns códigos de exemplo, com chamadas para funções do Zeus, que fiz em Python. Para quem não conhece a linguagem, ela tem o nome inspirado em um grupo de comédia britânica chamado Monty Python. :P

Brincadeiras a parte, busquei fazer exemplos de códigos bem simples para focar apenas em como consumir a API. Para isso, usei uma biblioteca bem legal chamada [requests](https://docs.python-requests.org/en/latest/).

Para facilitar a gerência de chamadas, criei um dicionário para inserir todos os serviços de configuração acessíveis, tendo o cuidado de inserir o endereço IP de um dispositivo que esteja conectado na mesma rede do seu computador:
```BASE_URL = 'https://<ip-dispositivo>/cgi-bin'
API = { 'login': BASE_URL+'/api/v1/system/login',}```

À medida que forem implementadas outras funções de acesso à API, elas serão incluídas nessa estrutura de dados especificada acima.

<h3>Autenticação</h3>
A primeira função que irei apresentar é a de autenticação. Dessa forma, será obtido um token de acesso para execução das futuras chamadas. O token deverá ser inserido no header das requisições.

```
import json
import requests


BASE_URL = 'https://10.0.0.1/cgi-bin'
API = {
    'login': BASE_URL+'/api/v1/system/login',
}
headers = {'content-type': 'application/json'}


def auth(username, password):
    data = {'data': {'username': username, 'password': password}}
    response = requests.post(API['login'], data=json.dumps(data),
                             headers=headers, verify=False)
    if response.status_code == 200:
        token = json.loads(response.content.decode('utf-8'))['data']['Token']
        headers['Authorization'] = 'Bauer ' + token
        return True

    return False```

Dessa forma, para realizar a autenticação em seu script Python, basta executar a função auth conforme exemplo abaixo:
`auth('user', 'pass')`

<h3>Configurando a porta SSH</h3>
Após possuir o token de acesso no seu header (linha 23 - auth.py), a diversão irá começar de fato. Como um primeiro exemplo, podemos configurar o acesso via protocolo SSH, de acordo com a especificação disponível na documentação do Zeus.

O método ssh_config será o responsável por fazer a chamada da API. Dessa forma, caso ele seja chamado sem nenhum argumento, será habilitada comunicação via SSH na porta 22 do dispositivo.

```API = {
    'login': BASE_URL+'/api/v1/system/login',
    'service_ssh': BASE_URL+'/api/v1/service/ssh',
}


def ssh_config(enabled=True, port=22, wan_access=True):
    data = {'data': {'enabled': enabled, 'port': port, 'wan_access': wan_access}}
    requests.put(API['service_ssh'], data=json.dumps(data),
                 headers=headers, verify=False)```

Sendo assim, para configurar o acesso SSH na porta 33 por exemplo, apenas execute a função abaixo:
`ssh_config(port=33)`

<h3>Aplicando as alterações</h3>
Todas as configurações enviadas aos dispositivos são somente ativadas após uma chamada ao endpoint apply. Dessa forma, após o post ser enviado, esse método retorna um hash das alterações dentro do response.

```API = {
    'apply': BASE_URL+'/api/v1/system/apply',
    'login': BASE_URL+'/api/v1/system/login',
    'service_ssh': BASE_URL+'/api/v1/service/ssh',
}


def apply():
    response = requests.post(API['apply'], headers=headers, verify=False)
    result = json.loads(response.content.decode('utf-8'))
    if result['data']['sucess']:
        return result['data']['config_hash']

    return False```

Para aplicar as configurações no dispositivo, basta executar a seguinte linha de código:
`apply()`

<h3>Alterando as cores do LED</h3>
Um recurso clássico de quem curte brincar com esse universo IoT é sempre o serviço de LED. Além disso, é um bom teste para quem quer ter um retorno mais visual de um request à API.

![Opções disponíveis no serviço de LED](https://mariosergio.me/images/zeus_api.webp)

Todos os recursos possíveis de se fazer com o serviço de LED estão disponíveis na [documentação](https://izeus.docs.apiary.io/#reference/service-led/led/update).

Na imagem ao lado é possível verificar quais ações são possíveis de serem feitas com o LED do Access Point. Toda essa listagem de opções e ações podem ser obtitas por meio de um GET no endpoint /service/leds.

Para exemplificar a utilização do serviço, implementei uma função chamada change_led_color(‘color’). Ou seja, essa função apenas irá esperar como argumento uma das cores disponíveis na variável option_list, apresentada na imagem.

Abaixo a implementação da função:

```API = {
    'apply': BASE_URL+'/api/v1/system/apply',
    'login': BASE_URL+'/api/v1/system/login',
    'service_led': BASE_URL+'/api/v1/service/leds',
    'service_ssh': BASE_URL+'/api/v1/service/ssh',
}


def change_led_color(color):
    response = requests.get(API['service_led'], headers=headers, verify=False)
    led_options = json.loads(response.content.decode('utf-8'))
    if color == 'off':
        led_options['data']['action']['value'] = 'off'
    else:
        led_options['data']['color']['value'] = color

    requests.put(API['service_led'], data=json.dumps(led_options),
                 headers=headers, verify=False)```

Caso queira ter acesso a todo o código de exemplo que apresentei nesse post, é só acessar o arquivo nesse [gist público](https://gist.github.com/sergiomario/4b1999554365871413609bcc53e211db).

<h3>Quão segura é essa brincadeira de API pública nos dipositivos?</h3>

<iframe src="https://giphy.com/embed/Em2dkag0fCjwQ" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/chloe-chloegif-gifs-reactions-Em2dkag0fCjwQ">via GIPHY</a></p>

Como vocês viram nos exemplos de código Python apresentados, todas as requisições à API são feitas via protocolo [HTTPS](https://pt.wikipedia.org/wiki/Hyper_Text_Transfer_Protocol_Secure). Como sabemos, isso permite que os dados sejam transmitidos por meio de uma conexão cifrada e que verifica a autenticidade do servidor e do cliente por meio de certificados digitais.

**IMPORTANTE**: É imprescindível que antes de usar o dispositivo, seja alterada a senha do usuário admin, que já vem por padrão de fábrica definida.

Outro ponto a ser esclarecido é que os Access Points não possuem seus endereços IP expostos publicamente na internet, já que por padrão eles utilizam um IP local obtido via DHCP. Isso porque o dispositivo se conecta à uma rede cabeada servindo de ponto de acesso.

Em resumo as boas práticas para construção de uma topologia de rede são fundamentais para garantia de segurança:

- Manter sempre o firewall atualizado;
- Evitar expôr os IPs dos dispositivos publicamente;
- Alterar a senha que vem definida por padrão de fábrica (Sim! Falei de novo);

As boas práticas são a maior garantia. Na dúvida lembre-se dos conselhos do Tio Ben.
`“Com grande poderes vêm grandes responsabilidades” (Ben, tio)`

<h2>Considerações Finais</h2>
Fico otimista para o futuro, imaginando que iniciativas como essa continuarão surgindo no mercado. Não somente abertura de APIs, mas também projetos de código aberto, apoio à comunidades de tecnologia e outras coisas legais.

Abraços ❤
