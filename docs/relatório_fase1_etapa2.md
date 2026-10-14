# Relatório de Execução - Fase 1, Etapa 2
**Projeto:** MESAFARTAI  
**Módulo:** Motor NLU e Trava de Threshold (AC-3)

### 1. Informe quantos número de árvores foram utilizados no motor NLU.
Foram utilizadas **80 árvores** de decisão no modelo Random Forest, configuradas por meio do parâmetro `n_estimators=80` na inicialização do classificador.

### 2. Informa qual o valor de threshold foi utilizado no processo de limiar de confiança.
O valor de threshold (limiar de confiança) configurado foi de **0.60** (`limiar_threshold=0.60`). Mensagens com nível de confiança abaixo deste valor ou categorizadas explicitamente como `fora_de_escopo` acionam a resposta de fallback.

### 3. Coloque o resultado da primeira execução.
Abaixo está o log real retornado pelo terminal durante a bateria de testes automatizados:

```text
 [NLU] Modelo Random Forest e Vetorizador TF-IDF treinados com sucesso!

--- BATERIA DE TESTES DE ESTRESSE NLU ---

Entrada: 'Tenho 30 kg de banana para doar'
Intenção: cadastrar_doacao | Confiança: 0.93
Retorno: Intenção 'cadastrar_doacao' identificada com 92.5% de confiança.

Entrada: 'Nossa instituição precisa de mantimentos'
Intenção: fallback | Confiança: 0.41
Retorno: Desculpe, não consegui entender com clareza o seu pedido.
Você pode refazer a mensagem informando se deseja **doar alimentos** ou **solicitar doações para uma ONG**?

Entrada: 'Qual é a receita de bolo de cenoura?'
Intenção: fallback | Confiança: 0.49
Retorno: Desculpe, não consegui entender com clareza o seu pedido.
Você pode refazer a mensagem informando se deseja **doar alimentos** ou **solicitar doações para uma ONG**?

Entrada: 'coisa comida doar la'
Intenção: fallback | Confiança: 0.42
Retorno: Desculpe, não consegui entender com clareza o seu pedido.
Você pode refazer a mensagem informando se deseja **doar alimentos** ou **solicitar doações para uma ONG**?
```

### 4. Descreva como você poderia fazer para os resultados de testes serem melhores, aumentando o grau de confiança dos resultados.
Para elevar o grau de confiança e mitigar falsos fallbacks (como ocorreu no teste da frase *"Nossa instituição precisa de mantimentos"*), podemos adotar as seguintes estratégias:
* **Expandir o Dataset de Treino:** Adicionar mais variações de frases e sinônimos nas listas `frases_treino` e `intencoes_treino`, incluindo palavras-chave como "instituição", "mantimentos" e "necessidade" na classe `solicitar_alimentos`.
* **Pré-processamento de Texto:** Implementar etapas de limpeza de dados antes da vetorização, tais como conversão para minúsculas, remoção de pontuações, remoção de *stopwords* (palavras irrelevantes como "de", "para", "o") e aplicação de *lemmatization* ou *stemming* (redução de palavras ao seu radical).
* **Ajuste de Hiperparâmetros:** Testar variações no balanceamento de classes e calibrar o número de árvores do Random Forest para melhorar a distribuição de probabilidades no cálculo do `predict_proba`.

### 5. Descreva por que o Random Forest foi o melhor método de Machine Learning para essa fase.
O Random Forest se destacou como uma excelente escolha para esta fase inicial pelos seguintes motivos:
* **Robustez a Ruídos e Overfitting:** Por ser um método de aprendizado baseado em um conjunto (*ensemble*) de múltiplas árvores de decisão independentes, ele reduz drasticamente o risco de sobreajuste (*overfitting*), lidando muito bem com pequenas bases de dados e termos irrelevantes presentes nas frases dos usuários.
* **Saída Probabilística Direta:** O algoritmo fornece nativamente probabilidades mapeadas para cada classe via método `predict_proba`. Isso tornou a implementação da nossa trava de segurança (Threshold) extremamente simples, confiável e precisa.
* **Facilidade de Configuração:** Diferente de algoritmos mais complexos como Redes Neurais ou SVMs, o Random Forest exige pouca parametrização inicial para apresentar uma excelente acurácia em tarefas de classificação de texto multiclasse associadas ao TF-IDF.
