# Escopo do Projeto - MESAFARTAI

## 1. Problema de negócio

O desperdício de alimentos é um problema que afeta tanto os estabelecimentos que possuem alimentos disponíveis quanto as instituições que precisam desses alimentos.

Supermercados, restaurantes, feirantes e outros estabelecimentos podem possuir alimentos próprios para consumo que acabam sendo descartados por excesso de estoque ou proximidade da validade.

Ao mesmo tempo, ONGs, abrigos e cozinhas comunitárias precisam de alimentos para atender pessoas em situação de vulnerabilidade.

O MESAFARTAI busca facilitar a comunicação entre esses dois lados.

## 2. Público-alvo

### Doadores

São pessoas ou estabelecimentos que possuem alimentos disponíveis para doação.

Exemplos:

* Supermercados
* Restaurantes
* Feirantes
* Produtores
* Outros estabelecimentos

### ONGs

São instituições que podem receber as doações e encaminhar os alimentos para pessoas que precisam.

Exemplos:

* ONGs
* Abrigos
* Cozinhas comunitárias
* Instituições sociais

## 3. Funcionamento geral

O usuário poderá enviar uma mensagem de forma natural pelo chat.

Exemplo:

"Tenho 20 kg de arroz para doar e ele vence amanhã."

O sistema deverá identificar a intenção da mensagem e posteriormente extrair informações importantes utilizando NLU e Regex.

Essas informações poderão ser armazenadas no banco de dados e utilizadas para auxiliar na escolha de uma ONG próxima.

## 4. Intenções tratadas

### cadastrar_doacao

Utilizada quando o usuário deseja informar que possui alimentos para doar.

Exemplo:

"Tenho 15 kg de arroz para doar."

### solicitar_alimentos

Utilizada quando uma ONG ou usuário deseja solicitar alimentos.

Exemplo:

"Estamos precisando de alimentos para o nosso abrigo."

### consultar_status

Utilizada para consultar o andamento de uma doação ou coleta.

Exemplo:

"Quero saber onde está minha doação."

### fora_de_escopo

Utilizada quando a mensagem não possui relação com as funções do MESAFARTAI ou quando a confiança do modelo estiver abaixo do limite definido.

## 5. Dados coletados no chat

O sistema deverá trabalhar com informações como:

* Tipo de alimento
* Quantidade
* Unidade ou peso
* Data ou prazo de validade
* Informações do doador
* Localização
* Informações relacionadas à ONG

A extração de algumas dessas informações será feita utilizando Regex.

## 6. Tecnologias

* Python
* Scikit-Learn
* SQLite3
* Regex
* NLU
* KNN
* Streamlit

## 7. Banco de dados

O projeto utilizará SQLite3 para armazenar informações sobre usuários, doações e matches logísticos.

As principais tabelas serão:

* usuarios
* doacoes
* matches

## 8. Matchmaking

O sistema deverá utilizar informações de localização para auxiliar na escolha da ONG mais próxima da doação.

O objetivo é reduzir a distância entre o doador e a instituição receptora, tornando a logística mais eficiente.

## 9. Identidade visual

O logotipo será criado utilizando um gerador de imagens por Inteligência Artificial.

### Prompt utilizado

Criar um logotipo moderno e simples para um projeto chamado MESAFARTAI, uma plataforma de tecnologia voltada ao combate ao desperdício de alimentos e à conexão entre doadores e ONGs. O símbolo deve unir visualmente conceitos de alimento, acolhimento, solidariedade e Inteligência Artificial. Utilizar um estilo profissional, amigável e tecnológico, com formas simples, boa leitura em tamanhos pequenos e aparência adequada para um projeto acadêmico e futuro portfólio profissional. Não utilizar excesso de elementos ou detalhes.

### Arquivo

O logotipo deverá ser salvo como:

`assets/logo_mesafartai.png`
