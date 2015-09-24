# Inversão gravimétrica do relevo da Moho em coordenadas esféricas

Apresentado nos seminários anuais da pós-graduação em geofísica do Observatório
Nacional por
[Leonardo Uieda](http://www.leouieda.com).

Slides podem ser vistos online no
[SpeakerDeck](https://speakerdeck.com/leouieda/inversao-gravimetrica-do-relevo-da-moho-em-coordenadas-esfericas).

## Resumo

A descontinuidade de Mohorovičić (ou Moho), que separa a crosta do manto
terrestre, é estudada quase exclusivamente através de métodos geofísicos.
Os principais métodos utilizados para estimar a profundidade da Moho são a
sismologia (com fontes naturais ou artificiais) e a gravimetria.
A sismologia geralmente produz estimativas pontuais (através da análise de
funções do receptor ou da dispersão de ondas de superfície) ou em áreas muito
restritas (através de levantamentos sísmicos ou inversões tomográficas).
Já a gravimetria é capaz de produzir estimativas regionais ou até mesmo
globais dependendo da cobertura de dados disponível.
O advento da gravimetria por satélite facilitou o acesso a dados de qualidade
com cobertura aproximadamente homogênea em áreas tradicionalmente pobres na
cobertura de dados terrestres.
No caso da América do Sul, a cobertura de dados sismológicos e de gravimetria
terrestre é heterogênea e geralmente concentrada em torno de centros urbanos e
da região costeira.
Neste trabalho, utilizamos dados de gravimetria por satélite para mapear a
profundidade da Moho na América do Sul.
Para isso, desenvolvemos um método de inversão não-linear computacionalmente
eficiente e capaz de levar em consideração a curvatura da Terra.

Existem na literatura diversos métodos de inversão gravimétrica para estimar o
relevo de uma interface, como o embasamento de uma bacia sedimentar ou a Moho.
A maioria desses métodos discretizam o relevo em prismas retangulares retos
justapostos com densidade homogênea e conhecida.
O problema inverso é estimar a espessura desses prismas que melhor ajusta os
dados observados.
O uso de prismas retangulares implica em uma aproximação plana para a Terra,
que não é adequada para estudos em escala continental.
Uma melhor aproximação seria a de uma Terra esférica.
Nessa aproximação, o relevo da interface deve ser discretizado em tesseroides,
ou prismas esféricos.
Para ambas aproximações, o problema inverso resultante é computacionalmente
custoso por que requer a construção de grandes matrizes densas e a solução de
grandes sistemas lineares.
Exitem métodos que buscam aumentar a eficiência computacional dessa classe de
inversão gravimétrica.
Um desses métodos utiliza a Transformada Rápida de Fourier (FFT) para estimar o
relevo no domínio da frequência.
Outro método aproxima as matrizes envolvidas na inversão por matrizes
diagonais.
Essa aproximação elimina a necessidade efetuar operações matriciais e de
construir e resolver sistemas lineares, acelerando consideravelmente a
computação do resultado.
O método desenvolvido neste trabalho discretiza o relevo da Moho em tesseroides
e é baseado na aproximação por matrizes diagonais.
Além disso, nossa formulação utiliza regularização de suavidade para
estabilizar o problema inverso.
Nossa implementação acelera as operações matriciais e a solução de sistemas
lineares através do uso de matrizes esparsas.


A solução do problema inverso depende de diversos parâmetros auxiliares
(hyperparâmetros):
(1) o contraste de densidade ao longo da interface,
(2) a profundidade do nível de referência (i.e., a Moho da Terra Normal)
e
(3) o valor do parâmetro de regularização, que controla o balanço entre
suavidade da solução e o ajuste dos dados observados.
Os valores utilizados para esses hyperparâmetros tem um impacto direto sobre a
estimativa do relevo da Moho.
Logo, é crucial determinar valores ótimos (ideais) para esses hyperparâmetros.
Para isso, utilizamos um método estatístico de avaliação de modelos denominado
validação cruzada.
Utilizamos um tipo de validação cruzada para determinar o parâmetro de
regularização e outro para determinar o contraste de densidade e o nível de
referência.

A validação cruzada para determinar o parâmetro de regularização é a variante
denominada ``holdout''.
Nesse método, separamos o conjunto de dados em dois: um para a inversão e outro
para avaliar a performance do modelo estimado (conjunto de teste).
Para um determinado valor do parâmetro de regularização, realizamos a inversão
utilizando exclusivamente o conjunto de dados para inversão.
Em seguida, utilizamos a estimativa dessa inversão para prever os dados
referentes ao conjunto de teste.
Esse processo é repetido para diversos valores do parâmetro de regularização.
Ao final, o parâmetro de regularização ideal é aquele que produz uma estimativa
que melhor prevê os dados do conjunto de teste.
Enfatizamos que o conjunto de teste não é utilizado na inversão.

Na validação cruzada para determinar o contraste de densidade e o nível de
referência, utilizamos dados sismológicos para o conjunto de teste.
Para determinados valores dos dois hyperparâmetros, realizamos a inversão com o
conjunto de dados separado para inversão na validação cruzada para o parâmetro
de regularização.
Em seguida, comparamos a estimativa obtida do relevo da Moho com estimativas
pontuais provenientes da sismologia.
Repetimos esse processo para diferentes combinações dos dois hyperparâmetros.
Os valores ideais são aqueles que produzem uma estimativa que mais se ajusta
aos vínculos sismológicos.

Realizamos testes com dados sintéticos para validar a metodologia descrita
acima.
O primeiro teste foi baseado em um modelo simples para o relevo da Moho.
Para o segundo teste, utilizamos o modelo crustal
CRUST1.0 (http://igppweb.ucsd.edu/~gabi/rem.html)
para gerar os dados sintéticos.
Após essses dois testes, aplicamos o método desenvolvido para estimar a
profundidade da Moho na América do Sul.
Utilizamos dados provenientes do modelo de harmônicos esféricos GOCO5S, que é
baseado em dados de satélite.
Os dados utilizados na inversão foram dispostos em uma malha regular com
espaçamento de 0.4º e a 50 km de altitude.
Os resultados obtidos estão de acordo com estimativas anteriores e com as
principais províncias geológicas do continente.

O código para gerar este resumo
e a apresentação que o acompanha
estão disponíveis em um repositório no site
Github (https://github.com/leouieda/seminario-on-2015).

## License

[![Creative Commons
License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
This work is licensed under a
[Creative Commons Attribution 4.0 International
License](http://creativecommons.org/licenses/by/4.0/).
