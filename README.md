# Venda cruzada de seguro de saúde

Este é um projeto fictício. A empresa, o contexto e as perguntas de negócios não são reais. Este portfólio está seguindo as recomendações do blog da [Comunidade DS](https://www.comunidadedatascience.com/como-usar-data-science-para-fazer-a-empresa-vender-mais/).

O notebook com todos os passos realizados está disponivel [aqui](https://github.com/douglasaturnino/health-insurance-cross-sell).
O google sheets com os produtos de dados em produção pode ser acessado clicando [aqui](https://docs.google.com/spreadsheets/d/1ptqAWq9TaIQbTEto8UnVbwrJkEHBi_qmmWFlWckOJ8E/edit#gid=0). Ao enviar uma mensagem para o BOT, a resposta pode haver uma lentidão para aparecer, pois, o Render depois de um tempo sem uso desliga a aplicação.
O dataset está disponivel no [Kaggle](https://www.kaggle.com/datasets/anmolkumar/health-insurance-cross-sell-prediction).

Este projeto foi feito por Douglas Saturnino.

# 1. Problema de negócio

A Insurance All é uma empresa que fornece seguro de saúde para seus clientes e o time de produtos está analisando a possibilidade de oferecer aos assegurados, um novo produto: Um seguro de automóveis.

Assim como o seguro de saúde, os clientes desse novo plano de seguro de automóveis precisam pagar um valor anualmente à Insurance All para obter um valor assegurado pela empresa, destinado aos custos de um eventual acidente ou dano ao veículo.

A Insurance All fez uma pesquisa com cerca de 380 mil clientes sobre o interesse em aderir a um novo produto de seguro de automóveis, no ano passado. Todos os clientes demonstraram interesse ou não em adquirir o seguro de automóvel e essas respostas ficaram salvas em um banco de dados junto com outros atributos dos clientes.

O time de produtos selecionou 127 mil novos clientes que não responderam a pesquisa para participar de uma campanha, no qual receberão a oferta do novo produto de seguro de automóveis. A oferta será feita pelo time de vendas através de ligações telefônicas.

Contudo, o time de vendas tem uma capacidade de realizar 20 mil ligações dentro do período da campanha.

Nesse contexto, você foi contratado como um consultor de Ciência de Dados para construir um modelo que prediz se o cliente estaria ou não interessado no seguro de automóvel. 

Com a sua solução, o time de vendas espera conseguir priorizar as pessoas com maior interesse no novo produto e assim, otimizar a campanha realizando apenas contatos aos clientes mais propensos a realizar a compra.

Como resultado da sua consultoria, você precisará entregar um relatório contendo algumas análises e respostas às seguintes perguntas:

1. Principais Insights sobre os atributos mais relevantes de clientes interessados em adquirir um seguro de automóvel.
2. Qual a porcentagem de clientes interessados em adquirir um seguro de automóvel, o time de vendas conseguirá contatar fazendo 20.000 ligações?
3. E se a capacidade do time de vendas aumentar para 40.000 ligações, qual a porcentagem de clientes interessados em adquirir um seguro de automóvel o time de vendas conseguirá contatar?
4. Quantas ligações o time de vendas precisa fazer para contatar 80% dos clientes interessados em adquirir um seguro de automóvel?

# 2. Premissas de Negócios

Cada linha representa um cliente e cada coluna contém alguns atributos que descrevem esse cliente, além da sua resposta à pesquisa, na qual ela mencionou interesse ou não ao novo produto de seguros. 

O conjunto de dados inclui as seguintes informações:
Variável | Definição
------------ | -------------
|Id| Identificador único do cliente.|
|Gender| Gênero do cliente.|
|Age| Idade do cliente.|
|Driving License| 0, o cliente não tem permissão para dirigir e 1, o cliente tem para dirigir ( CNH – Carteira Nacional de Habilitação )|
|Region Code| Código da região do cliente.|
|Previously Insured| 0, o cliente não tem seguro de automóvel e 1, o cliente já tem seguro de automóvel.|
|Vehicle Age| Idade do veículo.|
|Vehicle Damage| 0, cliente nunca teve seu veículo danificado no passado e 1, cliente já teve seu veículo danificado no passado.|
|Anual Premium| Quantidade que o cliente pagou à empresa pelo seguro de saúde anual.|
|Policy sales channel| código anônimo para o canal de contato com o cliente.|
|Vintage| número de dias que o cliente se associou à empresa através da compra do seguro de saúde.|
|Response| 0, o cliente não tem interesse e 1, o cliente tem interesse.|

# 3. Estratégia de solução

Para conseguir o resultado da pesquisa no google sheets e ordenar a lista de clientes com maior probabilidade de adquirir um seguro, foi feita as etapas descrita abaixo:

**Step 01. Descrição dos Dados:**

Etapa onde foi renomeado as variaveis para o padrão onde os espaços são substituidos por underline( _ ) e todas as palavras são em letra minuscula. Também verificou-se a quantidade de linhas e colunas do dataset e o seu tipo de dados

**Step 02. Engenharia de Atributo**

Nessa etapa as respostas do atributos "vehicle age" foram alteradas para o padrão snake_case e as respostas do atributo "vehicle damage" também foram alteradas: os originais "Yes" e "No" por 1 e 0, respectivamente.

**Step 03. Filtragem dos Dados:**

Nessa etapa ocorre a manipulação dos valores ausentes e autliers, nesse conjunto de dados não foi encontrado valores ausentes por essa razão essa etapa não foi feita nada.

**Step 04. Análise exploratória de dados:**

Nessa etapa foram relizadas as análises específicas para entender a influencia de algumas caracteristicas na decisão final do cliente em adquirir um seguro.

**Step 05. Preparação dos dados:**

Nessa etapa foi feita a padronização, reescala e transformação dos dados

**Step 06. Seleção de variaveis:**

Nessa etapa foi feita a identificação das variaveis mais importantes para o treinamento do modelo de aprendizado de maquina. Para isso, foi utilizado o pacote Boruta e o modelo ExtraTreesClassifier para selecionar os atributos.

**Step 07. Machine Learning Modelling:**

Nessa etapa é utilizada para avaliar e testar os algoritmos de aprendizado de máquina KNN Classifier, logistic regression, Extra Trees classifier, Random Forest, XGBoost Regressor.

**Step 08. Performece do modelo:**

Nessa etapa é verifiicada a performance de cada modelo criado e foi escolhido o modelo XGBoost, para a etapa de Hyperparameter.

**Step 09. Hyperparameter Fine Tuning:**

Nesse etapa foi escolhodo o modelo de xgboost apesar dele não ser o modelo com os melhores  resultados é o modelo que com menor peso e o modelo que tem a menor variação conforme o aumento de numeros k. Sendo assim foi o modelo usando para escolher os melhores parametros.

**Step 10. Converter o modelo em valores de negócios:**

O gerente recebeu uma lista ordenada de clientes com maior probabilidade de adquirir um seguro de veículo. Ao entrar em contato com os 20% melhores da lista, espera-se que haja uma conversão de pelo menos 90% do total de interessados no produto.

**Step 11. Deploy Modelo to Production:**


# 4. Modelos de Machine Learning

Nessa etapa é utilizada para avaliar e testar os algoritmos de aprendizado de máquina KNN Classifier, logistic regression, Extra Trees classifier, Random Forest, XGBoost Regressor e Gaussian Naive Bayes.

# 5. Performance do Modelo de Machine Learning
A performance de cada modelo escolhido está na tabela abaixo usando a Accuracia, precisão e reacall com as suas medias e desvios padrão. O @k representa os dados de 20 mil ligações.

|Model Name	|Accuracy Mean	| Accuracy STD| Precision Mean	|Precision STD	|Recall Mean	|Recall STD	|Precision@K Mean	|Precision@K STD	|Recall@K Mean	|Recall@K STD|
|:-------| :----------:	| :---------:| :--------: | :---------:| :---------: | :-------: | :-------: | :--------: | :----------:| :----------:|
|LogisticRegression	    |0.7889	|0.0008 |0.7096	|0.0008	|0.9781	|0.0004	|0.7623 |0.0018	|0.2902	|0.0017|
|GaussianNB	            |0.7889	|0.0008	|0.7096	|0.0008	|0.9781	|0.0004	|0.7700	|0.0028	|0.2932	|0.0011|
|KNeighborsClassifier	|0.8625	|0.0008	|0.7951	|0.0009	|0.9767	|0.0007	|0.9177	|0.0125	|0.3494	|0.0047|
|XGBClassifier	        |0.8093	|0.0011	|0.7389	|0.0010	|0.9569	|0.0009	|0.9491	|0.0020	|0.3614	|0.0008|
|ExtraTreesClassifier	|0.9264	|0.0009	|0.9059	|0.0010	|0.9516	|0.0013	|0.9982	|0.0003	|0.3801	|0.0001|
|RandomForestClassifier	|0.9218	|0.0012	|0.9170	|0.0015	|0.9277	|0.0009	|0.9998	|0.0001	|0.3807	|0.0000|

# 6. Business Results
Agora será mostrado o relatório com as análises e responder as perguntas de negocios.


## 1. Principais Insights sobre os atributos mais relevantes de clientes interessados em adquirir seguro de automóvel.

**Hypothesis 01:**
Quanto mais antigo o carro, maior o interesse do proprietário em adquirir um seguro de veículo.

|Vehicle age|Interested in vehicle insurance|Not interested in vehicle insurance|
|----------------|:----------------:|:-------------:|
|Below 1 year|4.4%|95.6%|
|Between 1 and 2 years|17.4%|82.6%|
|Over 2 years|29.5%|70.5%|



**Hypothesis 02:**

A idade do proprietario é relevante na decisão de contratar o seguro do veículo.

<img src="https://user-images.githubusercontent.com/95532957/204141903-a65532e0-a0e7-489d-8826-7b3f90bc5aae.png" title="age vs response" align="center" 
height="400" class="center"/>

**True/False.**

Hipótese verdadeira quanto mais velho for a pessoa, maior a chances dela adquirir um seguro de 
Veículo.

**Hypothesis 03:**

O interesse é maior em clientes que possuem veículos mais novos.



<img src="https://user-images.githubusercontent.com/95532957/204142020-bf4c35c6-b81e-429a-81c5-03e03b0ca98f.png" title="Interesse vs Idade do Veículo" 
align="center" height="400" class="center"/>

Hipótese falsa. Quando mais velho o veículo, maior é o interesse em seguro veicular:

4% dos clientes com veículos abaixo de 1 ano possuem interesse.
17% dos clientes com veículos entre 1 e 2 anos possuem interesse.
29% dos clientes com veículos com mais de 2 anos possuem interesse.


Insight de negócio: Buscar dados de acionamento de seguro por clientes com veículos mais 
velhos, a fim de validar esta possível correlação. Havendo correlação, avaliar necessidade de 
reajustes no preço dos seguro ofertados a estes clientes.

## 2. Qual a porcentagem de clientes interessados em adquirir um seguro de automóvel, o time de vendas conseguirá contatar fazendo 20.000 ligações?

Com 20.000 ligações o time de vendas terá ligado para 26% da base de clientes e dassa teria encontrado 60% dos clientes que estão interesado em um seguro de automoves.

<img src="https://user-images.githubusercontent.com/95532957/204142099-56a08fdf-8883-44be-9ea9-8425b5a4e7a1.png" title="gains and lift curve" lign="center" height="400" class="center"/>


## 3. E se a capacidade do time de vendas aumentar para 40.000 ligações, qual a porcentagem de clientes interessados em adquirir um seguro de automóvel o time de vendas conseguirá contatar?

Com 40.000 ligações o time de vendas terá ligado para 52% da base de clientes e dassa teria 
encontrado 99% dos clientes que estão interesado em um seguro de automoves.

<img src="https://user-images.githubusercontent.com/95532957/204142129-5e4b368c-00b0-41ab-be6d-d80f4bac2470.png" title="gains and lift curve" 
lign="center" height="400" class="center"/>

# 7. Conclusão

De acordo com os critérios definidos, foi feita uma lista de clientes com o maior interesse em adquirir um seguro de automoveis. Como resultado para o negocio foram criados:

* Uma API onde será feita a previsão dos clientes com o maior interesse.

* Uma planilha no google sheats que mostrar em porcentagem a chances desses clientes com interese em adquirir um seguro de automoveis.

Abaixo mostra como usar o google sheats para fazer a previsão de clientes.

<img src="https://user-images.githubusercontent.com/95532957/204161999-a38a8305-51b6-4a53-b4e8-e8dd2d38efc0.gif" title="Exemplo de uso" 
lign="center" height="400" class="center"/>

# 8. Próximos passos

Algumas melhorias no projeto podem ser incrementadas no futuro:

* Colocar as classes das linhas do grafico e a porcentagem
* Testes novos modelos e fazer o balanciamento de classe para melhorar a performance do modelo
* No google sheats poder fazer a previsão selecionando as linhas
* Fazer uma validação no google sheats, pois da forma que está aparece um erro se não for colocado os dados corretamente.
