# Análise de dados com SQL

## Resumo
Neste breve projeto com foco em colocar em prática os conhecimentos adiquiridos com os estudos em SQL, irei fazer análises dos dados sobre crédito de clientes de um banco, retirados de um repositório do Kaggle, o objetivo dessas análises é gerar insights rápidos e eficientes. Para a criação desse projeto foram usadas algumas plataformas, tais como AWS athena, S3, Google Colab e Kaggle.

## Dados
As informações dos clientes deste banco estão distribuídas da seguinte maneira:

**Query:** 

           select * from credito limit 10; 
![Print dados](https://github.com/Nicollas-str/SQL-Project/blob/main/print_dados.png)

Tipos dos dados de cada coluna:

**Query:** 

           DESCRIBE credito
![Print-tipo-dado](https://github.com/Nicollas-str/SQL-Project/blob/main/print_tipodado.png)

Com apenas duas querys para visualização dos dados notamos que temos dados nulos como por exemplo em escolaridade e estado civil.
Será que a escolaridade ou estado civil tem alguma relação com o credito do usuário? Veremos!

## Análise dos dados

Quantidade de pessoas para o respectivo salário anual:
**Query:** 

           select count(*), salario_anual from credito group by salario_anual
![Print-salário-anual](https://github.com/Nicollas-str/SQL-Project/blob/main/print_salarioquantidade.png)

Vemos que existe um equilibrio entre os salários até chegar em 120mil+ mostrando que existem bem menos pessoas com uma renda tão alta anualmente.

E sobre a escolaridade e o seu respectivo tipo de cartão?
           
**Query:** 

           select max(limite_credito) as limite_credito, escolaridade, tipo_cartao, sexo from credito 
           where escolaridade != 'na' and tipo_cartao != 'na' 
           group by escolaridade, tipo_cartao, sexo 
           order by limite_credito desc 
           limit 10
![Print-escolaridade-tipocartao](https://github.com/Nicollas-str/SQL-Project/blob/main/print_tipocartao.png)
Olhando apenas para essas linhas nota-se que tem sim uma separação por escolaridade, onde pessoas com altas graduações podem sim ter um cartão mais basico, porém pessoas com baixa escolaridade não possuem um cartão mais alto como platinum, mas vamos nos aprofundar um pouco mais nisso.

**Query:** 

           SELECT
           escolaridade,
           AVG(limite_credito) AS media_limite_credito
           FROM credito
           GROUP BY escolaridade
           ORDER BY media_limite_credito DESC;
![Print-escolaridade-limitecredito](https://github.com/Nicollas-str/SQL-Project/blob/main/print_limite.png)

Acima notamos que graduação está com a média mais alta de limite de crédito do que os demais, porém isso pode se dar por que existem bem mais pessoas graduadas do que as que possuem mestrado por exemplo.

**Query:** 

           select max(valor_transacoes_12m) as maior_valor_gasto, avg(valor_transacoes_12m) as media_valor_gasto, min(valor_transacoes_12m) as min_valor_gasto, sexo 
           from credito 
           group by sexo
![Print-escolaridade-gastamais](https://github.com/Nicollas-str/SQL-Project/blob/main/print_sexo.png)

Aqui notamos que mulheres gastam pouca coisa a mais que homem, um valor quase que irrelevante.

**Query:** 

           select avg(qtd_produtos) 
           as qts_produtos, avg(valor_transacoes_12m) as media_valor_transacoes, avg(limite_credito) 
           as media_limite, sexo, salario_anual 
           from credito 
           where salario_anual != 'na' 
           group by sexo, salario_anual 
           order by avg(valor_transacoes_12m) 
           desc
![Print-escolaridade-limiteesalario](https://github.com/Nicollas-str/SQL-Project/blob/main/print_medialimite.png)  
Como avaliação final entendemos que sim, o salário impacta diretamente no limite do cartão, como vemos acima! Outra análise interessante que podemos ver sobre a query acima é que não existem mulheres com salários acima de 60 mil.

## Conclusão

Essas forão algumas análises rapidas dos dados, nada muito complexo pois o foco é apresentar meu conhecimento utilizando SQL, mas ainda sim deu para termos bons aproveitamentos desses dados.
Alguns insights interessantes:

- a maior parte dos clientes possui renda até 40K
- a maior parte dos clientes é masculino!
- a escolaridade não parece influenciar no limite nem no tipo do cartão
- os clientes com maiores limites são em sua maioria homens
- os clientes com menores limites são em sua maioria mulheres
- dentre os menores limites não há presença de cartão platinum
- a faixa salarial impacta diretamente no limite de crédito
- nao existem clientes com salário anual acima de 60K do sexo feminino

Uma ótima exploração breve de dados que foram utilizadas querys com funções muito uteis no dia a dia, com certeza conseguiriamos entender melhor todas essas análises com um aprofundamento maior nos dados ou até mesmo com mais dados sobre esses clientes, com isso poderiamos entender por exemplo o por que de a escolaridade não afetar tanto no limite e tipo do cartão.



