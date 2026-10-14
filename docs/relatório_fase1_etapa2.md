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
Para elevar o grau de confiança e mitigar falsos fallbacks, podemos adotar as seguintes estratégias:
* **Expandir o Dataset de Treino:** Adicionar mais frases e sinônimos para a classe `solicitar_alimentos`, incluindo termos como "instituição", "mantimentos", "necessidade" e "abrigo".
* **Pré-processamento de Texto:** Aplicar limpeza de texto, conversão para minúsculas, remoção de pontuação e stopwords, além de stemização ou lematização.
* **Ajuste de Hiperparâmetros:** Testar diferentes valores de `n_estimators`, balanceamento de classes e variações no `TfidfVectorizer`.

### 5. Descreva por que o Random Forest foi o melhor método de Machine Learning para essa fase.
O Random Forest foi a melhor escolha porque:
* **é robusto a ruídos e pequenos datasets**;
* **oferece probabilidades com `predict_proba`**, o que facilita a trava de segurança;
* **é fácil de configurar e interpretar** para uma etapa inicial do projeto;
* **funciona bem com vetorização TF-IDF para classificação de textos curtos**.

### Checklist da etapa concluída
- [X] Arquivo `src/nlu.py` salvo e executado sem erros no terminal.
- [X] Trava de Threshold (< 0.60) funcionando nos testes para mensagens incertas/fora de escopo.
- [X] Arquivo `requirements.txt` atualizado na raiz do repositório.
- [X] Comandos `git add`, `git commit` e `git push` executados com sucesso.
- [X] Inserção de dados no `docs/regras.txt` e relatório de execução construído.

### Observação
O que parecia ser um "!" no editor foi causado por conflito de merge do Git e não por erro de código no `nlu.py`.
A correção foi feita pela resolução do conflito e pela consolidação do conteúdo da etapa 2 no arquivo de regras e no relatório final.
