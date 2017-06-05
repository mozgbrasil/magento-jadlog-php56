[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/logo_32_32.png "MOZG"
![valid XHTML][checkmark]

[url-method]: http://www.jadlog.com.br/
[requerimentos]: http://mozgbrasil.github.io/requerimentos/
[contact-jadlog]: http://www.jadlog.com.br/faleconosco.html
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[github-boxpacker]: https://github.com/mozgbrasil/magento-boxpacker-php56#mozgboxpacker
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove

# Mozg\Jadlog

## Sinopse

Integração a [Jadlog][url-method]

## Demonstração

<a href="http://mozg.com.br/assets/images/docs/2017-02-06-magento-jadlog.pdf" target="_blank"><img src="http://mozg.com.br/assets/images/docs/2017-02-06-magento-jadlog.gif" /></a>

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Recursos

- Definir dimensões para os produtos

- Definir dimensões, peso e valor da Embalagem/Caixa

- Opção para embalar os produtos separadamente ou combinar na mesma Embalagem/Caixa

- Embalagem do produto inteligente, exibe como os produtos serão agrupados e calcula o peso dimensional fazendo o envio fracionado se necessário

- Armazenamento das requisições em Cache

~~- Definir como diferentes combinações de produtos são embalados em conjunto # TODO~~

~~- Atribuir produtos a determinadas caixas (produtos múltiplos podem ser atribuídos à mesma caixa) # TODO~~

## Característica técnica

Atualmente diversos módulos de terceiros relativo a métodos de entrega sempre soma o peso e dimensões dos produtos gerando falha na requisição a transportadora devido não terem um sistema que separa os produtos em sua devida embalagem distribuindo seu peso.

O nosso módulo foi desenvolvido visando total transparência dos processos executados, para efeito de análise visualize os processos armazenado em log.

A extensão permite você definir as dimensões de seus produtos, as dimensões de suas embalagens e regras de como empacotar diferentes combinações de produtos em conjunto.

A extensão escolhe qual embalagem será utilizado para embalar os produtos para o pedido.

A extensão pode distribuir os produtos em diversas embalagens até o peso máximo suportado para a embalagem.

Como será cadastrado a embalagem com as dimensões e peso suportado pelas transportadoras não deve ocorrer falha relativa as dimensões ou peso.

A primeira coisa a se levar em consideração no uso do módulo é o [Gerenciamento de Embalagem/Caixa][github-boxpacker], como já vem alguns registros pré inseridos certifique se de atualizar os registros conforme sua necessidade.

Certifique se ter cadastrado as devidas dimensões para os produtos.

Para cada embalagem é feito uma requisição a transportadora onde é passado os devidos parâmetros

O módulo possui armazenamento de cache

Na finalização do pedido é armazenado no histórico do pedido um comentário contendo um identificador único que poderá ser usado para consulta no arquivo de log a discriminação dos pacotes seus itens e a visualização de cada pacote com seus itens em 3D

Sempre confira as informações de frete antes de processar cada pedido, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

Para o rastreamento do pacote é feito acesso ao WebService onde é passado os devidos parâmetros e exibido o devido retorno

## Instalação - Atualização - Desinstalação - Desativação

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Antes de executar os processos, [clique aqui][requerimentos] e leia os pré-requisitos e sugestões

--

Certique se da existencia do arquivo composer.json na raiz do projeto Magento e que o mesmo tenha os trechos "minimum-stability", "prefer-stable", "repositories" e '"magento-root-dir":"./"', conforme https://gist.github.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba

Caso não exista o arquivo composer.json na raiz do projeto Magento, efetue o download

	wget https://gist.githubusercontent.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba/raw/9b514bc896171b6d75833b6f165065356f62ca59/composer.json

--

Para qualquer atualização no Magento sempre mantenha o Compiler e o Cache desativado

--

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

	composer require mozgbrasil/magento-jadlog-php56:dev-master

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

Antes de efetuar qualquer processo que envolva atualização no Magento é recomendado manter o Compiler e Cache desativado

	composer clear-cache && composer update

Na ocorrência de erro, renomeie a pasta /vendor/mozgbrasil e execute novamente

Para checar a data do módulo execute o seguinte comando

	grep -ri --include=*.json 'time": "' ./vendor/mozgbrasil

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

	composer remove mozgbrasil/magento-jadlog-php56 && composer clear-cache && composer update

--

### Para desativar o módulo

Renomeie a pasta do módulo

Cada módulo tem a sua pasta no diretório /vendor/mozgbrasil/

## Como configurar o método de entrega

Antes de configurar o módulo você deve cadastrar o CEP de origem, indo ao backend em:

	STORES -> Configuration -> Sales/Shipping Settings -> Origin

Para configurar o método de entrega, acesse no backend em:

	STORES -> Configuration -> Sales/Shipping Methods -> Jadlog (powered by MOZG)

Você terá os campos a seguir

### • **Ativar**

Para "ativar" ou "desativar" o uso do método

### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

### • **Título**

Nome do método que deve ser exibido

### • **Serviços**

Selecione os serviços desejado, para selecionar mais de um, segure a tecla "Ctrl" e clique nos serviços

### • **Serviço Para Entrega Gratuita**

Quando houver um desconto de frete grátis, esse serviço terá o valor zero

### • **Calcular taxa de manuseio**

Podendo ser fixo ou percentual

### • **Taxa de Manuseio**

Será adicionado o valor ao frete

### • **Mostrar método se não aplicável**

Quando configurado como "Não", caso seja retornado algum serviço com erro, não será exibido o método de entrega

### • **Debug**

Deve ser armazenado os processos do módulo em var/log/

O arquivo 

DATE_mozg.log

se trata de log do módulo sendo um log mais detalhado contendo todos os processos inclusive das execuções realizadas pelas bibliotecas externas do módulo

O arquivo

shipping_METHOD.log

se trata de log nativo do magento relativo ao método de entrega

### • **Identificador do atributo largura dos produtos**

Permite definir o nome do atributo de largura dos produtos usado no projeto

### • **Identificador do atributo comprimento dos produtos**

Permite definir o nome do atributo de comprimento dos produtos usado no projeto

### • **Identificador do atributo altura dos produtos**

Permite definir o nome do atributo de altura dos produtos usado no projeto

### • **Unidade de medida**

Sendo o padrão do peso do produto como kilo

Caso esteja usando a unidade de massa em gramas, tanto os produtos como as embalagens devem respeitar o mesmo padrão

Ao informar na configuração do método o uso da unidade de massa em gramas é feito a conversão do peso de grama para kilo

1 Kg no formato "Kilo" será "1.000", já em "Gramas" será "1000.000"

### • **Mostrar serviço com retorno de erro**

Quando configurado como "Não", caso seja retornado algum serviço com erro, o mesmo não deve ser exibido no método de entrega

### • **Tipo de entrega**

Informe o seu Tipo de entrega

### • **Tipo de Seguro**

Informe o seu Tipo do Seguro

### • **Frete a pagar no destino**

Informe o modelo de pagamento do frete

### • **Valor da coleta**

Informe o Valor da coleta

### • **CNPJ do cliente que será responsável pelo pagamento**

Preencha nesse campo o número do CNPJ vinculado ao contrato com a Jadlog

### • **Senha**

Informe a Senha

<!--
### • **Código do Cliente**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação

### • **Remetente**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação

### • **Inscrição Estadual**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação

### • **CEP**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação

### • **Endereço**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação

### • **Bairro**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação

### • **Telefone**

Esse atributo deve ser usado na integração ao sistema de solitação de coleta on-line oferecido pela transportadora, o atribuito foi criado mas não foi desenvolvido essa automação
-->

## Quais os recursos do módulo

- [✓] Cálculo do frete
- [✓] Rastreamento

## Perguntas mais frequentes "FAQ"

### Como conferir os valores dos fretes junto a transportada

Você pode visualizar no log os parâmetros enviado a transportada

Quando finalizado o pedido é armazenado no historico as dimensões da caixa que foi usada para o obter o frete

#### Simulação da requisição do preço

Ao efetuar o calculo do frete do produto

É usado as dimensões da embalagem para cálculo do peso cúbico

Caso o valor do peso cúbico seja maior que o peso esse deve ser enviado

A fórmula do peso cúbico é "(largura_embalagem)×(comprimento_embalagem)×(altura_embalagem)/coeficiente" sendo o coeficiente 6000 ou 3333 de acordo com o serviço

Temos o devido retorno ao processar a seguinte requisição 

	curl --header 'Content-Type: text/xml;charset=UTF-8' --header 'SOAPAction:valorar' --data '<?xml version="1.0" encoding="UTF-8"?>
	<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://jadlogEdiws">
	<SOAP-ENV:Body>
	    <ns1:valorar>
	        <ns1:vModalidade>0</ns1:vModalidade>
	        <ns1:Password>C2o0E1m3</ns1:Password>
	        <ns1:vSeguro>N</ns1:vSeguro>
	        <ns1:vVlDec>1</ns1:vVlDec>
	        <ns1:vVlColeta>10,00</ns1:vVlColeta>
	        <ns1:vCepOrig>08215430</ns1:vCepOrig>
	        <ns1:vCepDest>08215430</ns1:vCepDest>
	        <ns1:vPeso>1.05</ns1:vPeso>
	        <ns1:vFrap>N</ns1:vFrap>
	        <ns1:vEntrega>D</ns1:vEntrega>
	        <ns1:vCnpj>17977285000118</ns1:vCnpj>
	    </ns1:valorar>
	</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>' http://jadlog.com.br/JadlogEdiWs/services/ValorFreteBean?wsdl

ou

	http://wsdlbrowser.com/

#### Simulação da requisição da consulta

Temos o devido retorno ao processar a seguinte requisição 

	curl --header 'Content-Type: text/xml;charset=UTF-8' --header 'SOAPAction:consultar' --data '<?xml version="1.0" encoding="UTF-8"?>
	<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://jadlogEdiws">
	<SOAP-ENV:Body>
	    <ns1:consultar>
	        <ns1:CodCliente>17977285000118</ns1:CodCliente>
	        <ns1:Password>C2o0E1m3</ns1:Password>
	        <ns1:NDs>123</ns1:NDs>
	    </ns1:consultar>
	</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>' http://jadlog.com.br/JadlogEdiWs/services/TrackingBean?wsdl

ou

	http://wsdlbrowser.com/soapclient?wsdl_url=http%3A%2F%2Fjadlog.com.br%2FJadlogEdiWs%2Fservices%2FTrackingBean%3Fwsdl&function_name=consultar

### Como aplicar o Frete Grátis

Na configuração do módulo para o método de entrega é possível definir o "Serviço Para Entrega Gratuita" recurso que deve ser aplicado quando definido a ação de "Frete Grátis" nas "Regras da Promoção"

No Backend do Magento, acesse o menu: Promoções -> Regras de Promoção -> Criar regra -> Crie uma regra e defina na aba "Ações" o uso do Frete Grátis

Dessa forma na exibição do cálculo do frete será exibido para o serviço escolhido o valor zerado

Esse recurso se trata de regra nativa do Magento caso tenha algum problema sugiro desativar todas as regras de promoção e ativar uma de cada vez até encontrar o motivo da ocorrência

### Serviço Para Entrega Gratuita pré-selecionado como EXPRESSO

O "Serviço Para Entrega Gratuita" só deve funcionar quando definido na regra de promoção o frete grátis

Sobre o "Serviço Para Entrega Gratuita" já estar pré-selecionado como "EXPRESSO" isso está ocorrendo pois esse serviço tem o seu identificador sendo zero, e o identificador nativo do Magento para "Nenhuma das opções" também é zero ou vazio

Devido a está ocorrência não está sendo possível aplicar o "Serviço Para Entrega Gratuita" para o Serviço "EXPRESSO"

### Sobre o retorno de erro "Could not connect to host"

Se trata de bloqueio imposto no seu servidor de hospedagem para acesso a Jadlog

No Firewall crie uma condição liberando as portas no servidor "80" e "8080" e adicione na WHITE LIST o ip 187.93.97.51 da jadlog

### Serviço retornando "Nao existe tarifa para parametros solicitados"

Caso queira na configuração do método altere a opção "Mostrar serviço com retorno de erro" para Não

### Dados de contato - Jadlog

Para que sejam encaminhadas as solicitações ao webservice da JADLOG.  
O cliente deverá efetuar o seu cadastro com o Departamento Comercial.  
Telefone: 11 3563 2000  
Contatos: Vera Ramos / Debora / Simone / Flavia / João Pedro

Comercial - JadLog <comercial@jadlog.com.br>

Suporte - JadLog <helpdesk@jadlog.com.br>

Programador - Ricardo Fernandes <ricardo.fernandes@jadlog.com.br> +55 11 3563-2000 ramal 2067

ricardo.azevedo@jadlog.com.br

ou acesse

Para entrar em contato com a [Jadlog][contact-jadlog]

## Manual

http://www.youblisher.com/p/641712-Manual-de-integracao-JADLOG/

## Contribuintes

Equipe Mozg

## License

[Comercial License](LICENSE.txt)

## Badges

[![Join the chat at https://gitter.im/mozgbrasil](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mozgbrasil/)
[![Latest Stable Version](https://poser.pugx.org/mozgbrasil/magento-jadlog-php56/v/stable)](https://packagist.org/packages/mozgbrasil/magento-jadlog-php56)
[![Total Downloads](https://poser.pugx.org/mozgbrasil/magento-jadlog-php56/downloads)](https://packagist.org/packages/mozgbrasil/magento-jadlog-php56)
[![Latest Unstable Version](https://poser.pugx.org/mozgbrasil/magento-jadlog-php56/v/unstable)](https://packagist.org/packages/mozgbrasil/magento-jadlog-php56)
[![License](https://poser.pugx.org/mozgbrasil/magento-jadlog-php56/license)](https://packagist.org/packages/mozgbrasil/magento-jadlog-php56)
[![Monthly Downloads](https://poser.pugx.org/mozgbrasil/magento-jadlog-php56/d/monthly)](https://packagist.org/packages/mozgbrasil/magento-jadlog-php56)
[![Daily Downloads](https://poser.pugx.org/mozgbrasil/magento-jadlog-php56/d/daily)](https://packagist.org/packages/mozgbrasil/magento-jadlog-php56)
[![Reference Status](https://www.versioneye.com/php/mozgbrasil:magento-jadlog-php56/reference_badge.svg?style=flat-square)](https://www.versioneye.com/php/mozgbrasil:magento-jadlog-php56/references)
[![Dependency Status](https://www.versioneye.com/php/mozgbrasil:magento-jadlog-php56/1.0.0/badge?style=flat-square)](https://www.versioneye.com/php/mozgbrasil:magento-jadlog-php56/1.0.0)

:cat2:
