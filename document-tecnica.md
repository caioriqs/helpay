> Especialista Digital Analytics: Caio Gomes<br />
> Documento de Especificação Técnica - Helpay

<br />

## Implementação da Camada de dados
Última atualização: 15/02/2019<br />
Em caso de dúvidas, entrar em contato com: [rkwebanalytics@gmail.com](mailto:rkwebanalytics@gmail.com)

<br />

## Índice
- [Objetivo](#objetivo)
- [Overview e Descrições Técnicas](#overview-e-descrições-técnicas)
- [Especificação de Micro-conversões](#especificação-de-micro-conversões)
- [Especificação de Conversões](#especificação-de-conversões)
- [Considerações Finais](#considerações-finais)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação do Google Tag Manager, da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [Helpay](https://www.helpay.com.br/).

<br />

## Overview e Descrições Técnicas



### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	}];
</script>
```

OU

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	});
</script>
```

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página que permite a inclusão de dados adicionais.

**Instalação**
1. Elementos de link: ```<a href="..." class="minha_classe">Link</a>``` <br />
Elementos do tipo link que foram mapeados, precisam receber a classe **gtm-link-event** e os data attributes em sua estrutura.

```html
<a href="http://www.meudominio.com.br/page2"
	class="minha_classe gtm-link-event"
 	gtm-event-data-category="[[exemplo:valor-categoria]]"
  	gtm-event-data-action="[[exemplo:valor-acao]]"
  	gtm-event-data-label="[[exemplo:valor-rotulo]]">Texto do link</a>
```

2. Elementos comuns: ```<div class="minha_classe">Elemento</div>``` <br />
Todos os elementos comuns do html que não são links e que foram mapeados, precisam receber a classe **gtm-element-event** em sua estrutura.

```html
<div 	class="minha_classe gtm-element-event"
  	gtm-event-data-category="[[exemplo:valor-categoria]]"
 	gtm-event-data-action="[[exemplo:valor-acao]]"
 	gtm-event-data-label="[[exemplo:valor-rotulo]]">Texto do elemento</div>
```

#### Importante:
> Todos os links e botões citados nesta documentação devem ter em sua estrutura `html` a classe `gtm-link-event` se for um link `<a>` ou `gtm-element-event` se o elemento não for um link `<a>` conforme demonstraremos nos exemplos específicos.<br />

> Devem ter também os data-attributes `gtm-event-data-category`, `gtm-event-data-action` e `gtm-event-data-label` preenchidos conforme instruções específicas.

<br />	 	

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente [Helpay](https://www.helpay.com.br/).


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar 'nao_disponivel'. - Mudar de acordo com o projeto

---

<br />

### Especificação de Micro-conversões:


**1 - Clique no Menu:**<br />

- **Quando:** Ao clicar em qualquer item do menu;
- **Onde:** Menu principal;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Botão</i>
```

| Variável 			| Exemplo 											| Descrição				|
| :----------------	| :------------------------------------------------	| :-------------------	|
| [[nome-item]]		| 'sobre-nos', 'blog', 'quero-ser-helpay' e etc		| Nome do item no Menu	|

<br />

**2 - Cadastre-se:**<br />

- **Quando:** Ao clicar em "Cadastre-se";
- **Onde:** Menu principal;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="minha-conta:cadastrar"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="minha-conta:cadastrar"
>Botão</i>
```

<br />

**3 - Acessar Minha Conta:**<br />

- **Quando:** Ao clicar em "Minha Conta";
- **Onde:** Menu principal;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="minha-conta:acessar"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="minha-conta:acessar"
>Botão</i>
```

<br />


**4 - Clique Buscar:**<br />

- **Quando:** Ao clicar no botão "Buscar";
- **Onde:** Content Principal - consulte débitos do veículo;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:buscar"
	gtm-event-data-action="clique:buscar"
	gtm-event-data-label="consulte-debitos"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:buscar"
	gtm-event-data-action="clique:buscar"
	gtm-event-data-label="consulte-debitos"
>Botão</i>
```

<br />

**5 - Clique "Perguntas":**<br />

- **Quando:** Ao clicar em "Acessar central de dúvidas" ;
- **Onde:** Sessão de dúvidas;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:duvidas"
	gtm-event-data-label="acessar-central-de-duvidas"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:duvidas"
	gtm-event-data-label="acessar-central-de-duvidas"
>Botão</i>
```

<br />

**6 - Clique nas dúvidas:**<br />

- **Quando:** Ao clicar nas dúvidas;
- **Onde:** Sessão de dúvidas frequentes;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:duvidas-frequentes"
	gtm-event-data-label="[[nome-duvida]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:duvidas-frequentes"
	gtm-event-data-label="[[nome-duvida]]"
>Botão</i>
```

| Variável 		| Exemplo 						| Descrição								|
| :-----------	| :--------------------------	| :----------------------------------	|
| nome-duvida	| 'porque-utilizar-o-helpay' 	| Nome da dúvida clicada, sanitizada	|

<br />


**7 - Clique Rodapé:**<br />

- **Quando:** Ao clicar em algum item/link;
- **Onde:** Rodapé;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:rodape"
	gtm-event-data-label="link:[[nome-link]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:home"
	gtm-event-data-action="clique:rodape"
	gtm-event-data-label="link:[[nome-link]]"
>Botão</i>
```

| Variável 		| Exemplo 									| Descrição							|
| :-----------	| :-------------------------------------	| :-------------------------------	|
| nome-link		| 'quero-ser-helpay', 'consultar-veiculos' 	| Nome do link clicado, sanitizado	|

<br />


**8 - Baixar APP:**<br />

- **Quando:** Ao clicar no botão da "AppStore/GooglePlay";
- **Onde:** Na sessão de informações sobre aplicativo;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:consultar"
	gtm-event-data-action="clique:baixar-app"
	gtm-event-data-label="app:[[nome-loja]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:consultar"
	gtm-event-data-action="clique:baixar-app"
	gtm-event-data-label="app:[[nome-loja]]"
>Botão</i>
```

<br />

**9 - Blog - Clique Menu:**<br />

- **Quando:** Ao clicar nos itens
- **Onde:** Menu Blog

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="helpay:blog"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="helpay:blog"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Botão</i>
```

| Variável 			| Exemplo 					| Descrição				|
| :----------------	| :---------------------	| :-------------------	|
| [[nome-item]]		| 'cnh', 'multas' e etc		| Nome do item no Menu	|

<br />

---

### Especificação de Conversões:

**Sucesso Consulta:**<br />

- **Onde:** No callback de sucesso;

```html
<script>
	dataLayer.push({
		'event': 'conversion',
		'eventCategory': 'helpay:consultar',
		'eventAction': 'sucesso:consulta'
	});
</script>
```

<br />

**Sucesso Cadastro:**<br />

- **Onde:** No callback de sucesso de cadastro;

```html
<script>
	dataLayer.push({
		'event': 'login',
		'eventCategory': 'helpay:login',
		'eventAction': 'sucesso:cadastro'
	});
</script>
```

<br />

---

### Especificação de E-commerce:

**1 - Clique Continuar - Selecionar modo de pagamento:**<br />

- **Quando:** Ao selecionar se irá pagar por "cartão", "boleto" ou "cartão + boleto";
- **Onde:** No clique do botão "Continuar";

```html
<script>
	dataLayer.push({
		'event': 'event',
		'eventCategory': 'helpay:ecommerce',
		'eventAction': 'clique:continuar:pagamento',
		'eventLabel': 'modo-pagamento:[[tipo-pagamento]]'
	});
</script>
```

| Variável 				| Exemplo 								| Descrição																	|
| :-------------------	| :----------------------------------	| :------------------------------------------------------------------------	|
| [[tipo-pagamento]]	| 'cartao', 'boleto' e 'cartao+boleto'	| Retornar o modo de pagamento selecionado, ao clicar no botão "continuar"	|


<br />

### 2 - Checkout:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da páginas página de checkout. Deve existir um array de produto para cada tipo/categoria adicionada na compra/assinatura.

```html
<script>
dataLayer.push({
	'event': 'checkout',
	'eventCategory': 'helpay:ecommerce',
	'eventAction': 'checkout-etapa:[[checkout-name]]',
	'ecommerce': {
		'checkout': {
			'actionField': {'step': '[[passo-checkout]]'},
			'products': [{
				'name': '[[nome-debito]]',		//Nome ou ID do produto é obrigatório
				'id': '[[id-consulta]]',
				'price': '[[preco-debito]]',
				'brand': 'helpay',
				'category': 'debitos',
				'quantity': '[[quantidade-debitos]]'
			}]
		}
	}
});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 													| Descrição 							|
| :------------	| :------------------------ | :-------------------------------------------------------	| :----------------------------------	|
| eventAction 	| [[checkout-name]]			| 'modo-pagamento', 'dados-pessoais', 'dados-de-pagamento' 	| Nome do passo de checkout				|
| actionField 	| [[passo-checkout]]		| 'step-1', 'step-2', 'step-3' 								| Passo atual do checkout 	 			|
| name 			| [[nome-debito]] 			| 'ipva', 'documentacao' e etc				 				| Nome do debito 						|
| id			| [[id-consulta]] 			| '1234567'													| ID de consulta 						|
| price			| [[preco-debito]] 			| '1279.90'										 			| Preço do debito						|
| quantity		| [[quantidade-debitos]]	| '1', '2' e etc											| Quantidade de debitos no checkout		|


<br />

### 3 - Purchase:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da página de transação, e se o usuário acessar novamente o link ou atualizar a página, o objeto não deve ser disparado novamente. Deve existir um array de produto para cada tipo/categoria adicionada na compra/assinatura.

```html
<script>
dataLayer.push({
	'event': 'purchase',
	'eventCategory': 'helpay:ecommerce',
	'eventAction': 'sucesso:pagamento',
	'ecommerce': {
		'purchase': {
			'actionField': {
				'id': '[[id-transacao]]',	//ID da transação é obrigatório
				'revenue': '[[valor-total-transacao]]',
				'tax': '[[taxa-transacao]]'
			},
			'products': [{
				'name': '[[nome-debito]]',	//Nome ou ID do produto é obrigatório
				'id': '[[id-consulta]]',
				'price': '[[preco-debito]]',
				'brand': 'helpay',
				'category': 'debitos',
				'quantity': '[[quantidade-debitos]]'
			}]
		}
	}
});
</script>
```

*Descrição Purchase:*

| Nome 			| Variável 					| Exemplo 				| Descrição 															|
| :------------	| :------------------------	| :----------------		| :----------------------------------------------------------------		|
| id 			| [[id-transacao]] 			| 'abc1234d56' 			| ID da Transação														|
| revenue 		| [[valor-total-transacao]] | '1779.90'	 			| Valor total da transação incluindo taxas								|
| tax 	 		| [[taxa-transacao]] 		| '123.90'	 			| Taxas de pagamento. Caso não exista, preecher com "nao_disponivel"	|

<br />

*Descrição Produtos:*

| Nome 			| Variável 					| Exemplo 							| Descrição 								|
| :------------	| :------------------------	| :------------------------ 		| :------------------------------------		|
| name 			| [[nome-debito]] 			| 'ipva', 'documentacao' e etc		| Nome do debito 						|
| id			| [[id-consulta]] 			| '1234567'							| ID de consulta 						|
| price			| [[preco-debito]] 			| '1279.90'							| Preço do debito						|
| quantity		| [[quantidade-debitos]]	| '1', '2' e etc					| Quantidade de debitos no checkout		|

<br />

## Considerações Finais:

> Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
