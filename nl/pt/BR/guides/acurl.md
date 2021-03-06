---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Curl autorizado: `acurl`

_(Este guia se baseia em um artigo do Blog de Samantha Scharr: [
"Curl autorizado, também conhecido como acurl" ![Ícone de link externo](../images/launch-glyph.svg "Ícone de link externo")](https://cloudant.com/blog/authorized-curl-a-k-a-acurl/){:new_window},
publicado originalmente em 27 de novembro de 2013.)_

`acurl` é um alias prático que permite executar `curl` de comandos do Cloudant para URLs
sem ter que inserir seu nome de usuário e senha para cada solicitação.
Isso significa que um simples `GET` para um banco de dados não precisa mais ser gravado como
`https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com/foo`;
em vez disso, basta usar `https://$ACCOUNT.cloudant.com/foo`.

Isso não apenas diminui URLs muito longas,
como também o alias `acurl` é mais seguro.
Ele evita que alguém leia sua senha sobre seus ombros enquanto você digita
e, o mais importante,
ele garante que sua senha não seja enviada em texto sem formatação pela rede, utilizando HTTPS.

São necessárias apenas três etapas simples:

1.	[Codificar o nome do usuário e a senha](#encode-username-and-password).
2.	[Criar um alias](#create-an-alias)
3.	[Ativar o alias](#activate-the-alias).

## Codificar o nome do usuário e a senha

Primeiramente, codificaremos seu nome de usuário e senha do Cloudant com base64.
Isso nos dá uma sequência de caracteres base64 como saída.

O comando para codificar alguns dados com base64 é semelhante ao exemplo a seguir:

```python
python -c 'import base64; print base64.urlsafe_b64encode("$ACCOUNT:$PASSWORD")'
```
{:codeblock}

Supomos que a saída seja chamada `<OUTPUT-OF-BASE64>`.

Por exemplo,
se você usar o comando:

```python
python -c 'import base64; print base64.urlsafe_b64encode("$ACCOUNT:$PASSWORD")'
```
{:codeblock}

Você obterá a saída a seguir:

```
bXl1c2VybmFtZTpteXBhc3N3b3Jk
```
{:codeblock}

>	**Nota**: lembre-se de que sua senha continua armazenada em texto sem formatação em seu computador;
a codificação base64 _não_ é criptografia.
	Se você usar a codificação base64 na mesma sequência de caracteres,
sempre obterá a mesma sequência de saída de caracteres correspondente.

## Criar um alias

Agora criaremos um alias para `curl` que inclua essas credenciais para que não seja necessário inseri-las
sempre que um comando `curl` for gravado.

Inclua a linha a seguir em seu `~/.bashrc` ou `~/.bash_profile`:

```sh
alias acurl="curl -s --proto '=https' -g -H 'Authorization: Basic <OUTPUT-OF-BASE64>'"
```
{:codeblock}

Esse alias inclui um cabeçalho de Autorização em vez de incluir as
credenciais de autorização na URL inserida na linha de comandos.
Ele também força o uso de HTTPS, que é altamente recomendável sobre HTTP simples,
uma vez que criptografa seus dados e credenciais em trânsito e o ajuda a ter certeza de que está se conectando a sistemas Cloudant.

## Ativar o alias

Agora inicie um novo shell ou execute `source ~/.bash_profile` (ou `~/.bashrc`, se isso tiver sido usado) para tornar o alias funcional.

## Testando `acurl`

Agora vamos nos certificar de que tudo está configurado corretamente.
Vá em frente e execute:

```sh
acurl https://$ACCOUNT.cloudant.com/_all_dbs
```
{:codeblock}

Se você obtiver a lista de seus bancos de dados de volta,
incrível!
`acurl` estará configurado e pronto para execução.

Boa codificação!
