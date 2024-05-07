# Análise de Mercado de Games :video_game:
Uma análise de vendas de games para PS4, compreendidos no período de 2013-2018, na América do Norte, Europa, Japão e Resto do Mundo.<br>
Os dados foram obtidos do site Kaggle.<br>
Link do Dataset: https://www.kaggle.com/datasets/sidtwr/videogames-sales-dataset<br>
Código completo: https://colab.research.google.com/github/FranciscoAlveJr/Mercado-de-games/blob/main/Mercado_de_Games.ipynb
## Importando Bibliotecas
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import warnings

warnings.filterwarnings('ignore')
```
## Importando o banco de dados do dataset
```
df = pd.read_csv('PS4_GamesSales.csv', encoding='latin-1')
```
|index|Game|Year|Genre|Publisher|North America|Europe|Japan|Rest of World|Global|
|---|---|---|---|---|---|---|---|---|---|
|1|Grand Theft Auto V|2014\.0|Action|Rockstar Games|6\.06|9\.71|0\.6|3\.02|19\.39|
|2|Call of Duty: Black Ops 3|2015\.0|Shooter|Activision|6\.18|6\.05|0\.41|2\.44|15\.09|
|3|Red Dead Redemption 2|2018\.0|Action-Adventure|Rockstar Games|5\.26|6\.21|0\.21|2\.26|13\.94|
|4|Call of Duty: WWII|2017\.0|Shooter|Activision|4\.67|6\.21|0\.4|2\.12|13\.4|
|5|FIFA 18|2017\.0|Sports|EA Sports|1\.27|8\.64|0\.15|1\.73|11\.8|
## Visualizando o número de linhas e colunas
```
df.shape
```
Resultado: (1034, 9)<br>
Ou seja, a tabela possui 1034 linhas e 9 colunas
<br>
<br>
## Visualizando os nomes das colunas
```
df.columns
```
Colunas: 'Game', 'Year', 'Genre', 'Publisher', 'North America', 'Europe', 'Japan', 'Rest of World', 'Global'
## Verficando valores nulos
```
df.isnull().sum()
```
|Game|Year|Genre|Publisher|North America|Europe|Japan|Rest of World|Global|
|---|---|---|---|---|---|---|---|---|
|0|209|0|209|0|0|0|0|0|

Foram encontrados 209 valores nulos
<br>
![grafico_nulos](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/dec30739-9ac0-464e-b8bd-f6a5e949bffc)

## Removendo valores nulos
```
df.dropna(inplace=True)
```
|index|Game|Year|Genre|Publisher|North America|Europe|Japan|Rest of World|Global|
|---|---|---|---|---|---|---|---|---|---|
|1|Grand Theft Auto V|2014\.0|Action|Rockstar Games|6\.06|9\.71|0\.6|3\.02|19\.39|
|2|Call of Duty: Black Ops 3|2015\.0|Shooter|Activision|6\.18|6\.05|0\.41|2\.44|15\.09|
|3|Red Dead Redemption 2|2018\.0|Action-Adventure|Rockstar Games|5\.26|6\.21|0\.21|2\.26|13\.94|
|4|Call of Duty: WWII|2017\.0|Shooter|Activision|4\.67|6\.21|0\.4|2\.12|13\.4|
|5|FIFA 18|2017\.0|Sports|EA Sports|1\.27|8\.64|0\.15|1\.73|11\.8|
|---|---|---|---|---|---|---|---|---|---|
|1026|Biomutant|2019\.0|Action|THQ Nordic|0\.0|0\.0|0\.0|0\.0|0\.0|
|1027|de Blob|2017\.0|Platform|THQ Nordic|0\.0|0\.0|0\.0|0\.0|0\.0|
|1028|Chaos on Deponia|2017\.0|Adventure|Daedalic Entertainment|0\.0|0\.0|0\.0|0\.0|0\.0|
|1029|Code Vein|2018\.0|Action|Bandai Namco Entertainment|0\.0|0\.0|0\.0|0\.0|0\.0|
|1031|Radial G Racing Revolved|2017\.0|Racing|Tammeka Games|0\.0|0\.0|0\.0|0\.0|0\.0|

Usando o `df.shape` novamente, o número de linhas cai para 825, após a remoção dos valores nulos.
<br>
<br>
Foi preciso tirar valores com anos de 2019 e 2020, pois existem valores desprezíveis
```
df = df.loc[(df['Year'] != 2019) & (df['Year'] != 2020)]
```
## Convertendo os anos, de decimal para inteiro
Os valores dos anos estão apresentando ponto Flutuante.
<br>
|1|2|3|4|5|---|1025|1026|1027|1028|1029|
|---|---|---|---|---|---|---|---|---|---|---|
|2014\.0|2015\.0|2018\.0|2017\.0|2017\.0|---|2018\.0|2017\.0|2017\.0|2018\.0|2017\.0|
```
df = df.astype({'Year': int})
```
|1|2|3|4|5|---|1025|1026|1027|1028|1029|
|---|---|---|---|---|---|---|---|---|---|---|
|2014|2015|2018|2017|2017|---|2018|2017|2017|2018|2017|

Agora os valores dos anos não apresentam mais ponto flutuante.
## Verificando Vendas Globais

![grafico_vendas_globais](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/97de76d1-e2e1-463b-a374-a0e4ae45c184)<br>
É possível analisar que, houve um pico de vendas entre 2015 e 2016. Vendo pelo ponto de vista do mercado, o PlayStation 4 foi lançado em 2013, então é fácil presumir que o aumento nas vendas dos jogos se deve ao aumento das vendas do console nos anos seguintes.
<br>
<br>
Os jogos que venderam mais de 10 milhões de cópias<br>
|index|Game|Year|Genre|Publisher|North America|Europe|Japan|Rest of World|Global|
|---|---|---|---|---|---|---|---|---|---|
|1|Grand Theft Auto V|2014|Action|Rockstar Games|6\.06|9\.71|0\.6|3\.02|19\.39|
|2|Call of Duty: Black Ops 3|2015|Shooter|Activision|6\.18|6\.05|0\.41|2\.44|15\.09|
|3|Red Dead Redemption 2|2018|Action-Adventure|Rockstar Games|5\.26|6\.21|0\.21|2\.26|13\.94|
|4|Call of Duty: WWII|2017|Shooter|Activision|4\.67|6\.21|0\.4|2\.12|13\.4|
|5|FIFA 18|2017|Sports|EA Sports|1\.27|8\.64|0\.15|1\.73|11\.8|
|6|FIFA 17|2016|Sports|Electronic Arts|1\.26|7\.95|0\.12|1\.61|10\.94|
|7|Uncharted \(PS4\)|2016|Action|Sony Interactive Entertainment|4\.49|3\.93|0\.21|1\.7|10\.33|
## Análise por continente
![grafico_continentes](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/b27a3aef-4bda-4ef8-ad77-ce9abad6d10f)<br>
Aqui é possível ver um certo equilíbrio nas vendas na América do Norte e Europa. Sendo o segundo, levemente maior.
## Desenvolvedoras
Top 10 Desenvolvedoras que mais venderam no PS4 (2013-2018)<br>
|index|Publisher|Global|
|---|---|---|
|1|Activision|72\.44|
|2|Ubisoft|59\.16|
|3|Electronic Arts|54\.96|
|4|Sony Interactive Entertainment|54\.85|
|5|EA Sports|47\.550000000000004|
|6|Sony Computer Entertainment|42\.26|
|7|Rockstar Games|33\.93|
|8|Square Enix|29\.92|
|9|Bethesda Softworks|28\.96|
|10|Warner Bros\. Interactive Entertainment|27\.83|

![grafico_publisher](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/9355f77b-05a0-495c-9558-80aebb765f87)
<br>
## Gêneros
Top 10 gêneros mais vendidos no PS4 (2013-2018)
|index|Genre|Global|
|---|---|---|
|1|Action|136\.82|
|2|Shooter|134\.99|
|3|Sports|92\.85|
|4|Role-Playing|62\.73|
|5|Action-Adventure|61\.86|
|6|Racing|25\.29|
|7|Fighting|19\.36|
|8|Platform|17\.85|
|9|Adventure|15\.22|
|10|Misc|12\.47|

![grafico_generos](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/f86eeff7-ebeb-4a26-8f46-f9e1bf9656a0)
<br>
## Top 10 Jogos
Top 10 jogos mais vendidos para PS4 no mundo (2013-2018)<br>
|index|Game|Global|
|---|---|---|
|1|Grand Theft Auto V|19\.39|
|2|Call of Duty: Black Ops 3|15\.09|
|3|Red Dead Redemption 2|13\.94|
|4|Call of Duty: WWII|13\.4|
|5|FIFA 18|11\.8|
|6|FIFA 17|10\.94|
|7|Uncharted \(PS4\)|10\.33|
|8|Spider-Man \(PS4\)|8\.76|
|9|Call of Duty: Infinite Warfare|8\.48|
|10|Fallout 4|8\.48|

![grafico_jogos](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/acbff48a-f447-4968-bbda-db7856a777d4)
## Top 10 América do Norte
Top 10 jogos mais vendidos para PS4 na América do Norte (2013-2018)<br>
|index|Game|North America|
|---|---|---|
|1|Call of Duty: Black Ops 3|6\.18|
|2|Grand Theft Auto V|6\.06|
|3|Red Dead Redemption 2|5\.26|
|4|Call of Duty: WWII|4\.67|
|5|Uncharted \(PS4\)|4\.49|
|6|Spider-Man \(PS4\)|3\.64|
|7|Star Wars Battlefront 2015|3\.31|
|8|Call of Duty: Infinite Warfare|3\.11|
|9|Fallout 4|2\.91|
|10|Call of Duty: Advanced Warfare|2\.84|

![grafico_america](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/b387940b-ff76-48fa-b98d-74735e1545f3)
<br>
## Top 10 Europa
Top 10 jogos mais vendidos para PS4 na Europa (2013-2018)
|index|Game|Europe|
|---|---|---|
|1|Grand Theft Auto V|9\.71|
|2|FIFA 18|8\.64|
|3|FIFA 17|7\.95|
|4|Red Dead Redemption 2|6\.21|
|5|Call of Duty: WWII|6\.21|
|6|Call of Duty: Black Ops 3|6\.05|
|7|FIFA 16|5\.77|
|8|FIFA 15|4\.49|
|9|Fallout 4|3\.97|
|10|Uncharted \(PS4\)|3\.93|

![grafico_europa](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/b577597e-7ffe-44da-8fb2-9cca3054d460)
<br>
## Top 10 Japão
Top 10 jogos mais vendidos para PS4 no Japão (2013-2018)
|index|Game|Japan|
|---|---|---|
|1|Monster Hunter: World|2\.17|
|2|Dragon Quest XI|1\.43|
|3|Final Fantasy XV|1\.05|
|4|Grand Theft Auto V|0\.6|
|5|Metal Gear Solid V: The Phantom Pain|0\.5|
|6|Persona 5|0\.48|
|7|Dark Souls III|0\.44|
|8|Knack|0\.42|
|9|NieR Automata|0\.42|
|10|Resident Evil VII: Biohazard|0\.41|

![grafico_japao](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/d9c7243a-8bbd-4d7b-a039-385091b36d76)
<br>
Aqui vale ressaltar que no Japão se diferencia dos outros países, tanto nos jogos, quanto nos gêneros.
<br>
## Top 10 Resto do Mundo
Top 10 jogos mais vendidos para PS4 no resto do mundo (2013-2018)
|index|Game|Rest of World|
|---|---|---|
|1|Grand Theft Auto V|3\.02|
|2|Call of Duty: Black Ops 3|2\.44|
|3|Red Dead Redemption 2|2\.26|
|4|Call of Duty: WWII|2\.12|
|5|FIFA 18|1\.73|
|6|Uncharted \(PS4\)|1\.7|
|7|FIFA 17|1\.61|
|8|Spider-Man \(PS4\)|1\.41|
|9|Call of Duty: Infinite Warfare|1\.36|
|10|Fallout 4|1\.34|

![grafico_resto](https://github.com/FranciscoAlveJr/Mercado-de-games/assets/65497402/6383f3c8-0a48-42f2-b563-9526c180fdd3)
<br>
# CONCLUSÃO
## A CAMPEÃ 🥇 DAS DESENVOLVEDORAS FOI...
![activision](https://tm.ibxk.com.br/2020/12/30/30130926491100.jpg?ims=704x264)<br>
Seja pela popularidade da franquia Call of Duty, seja pela quantidade de jogos publicados, a Activision ultrapassou a marca de mais de 70 milhões de cópias vendidas.
<br>
## O GÊNERO MAIS VENDIDO 🥇 FOI DE...
![ps4_action](https://sm.ign.com/t/ign_nordic/lists/2/25-best-ps/25-best-ps4-games-to-play-right-now_yyka.1280.jpg)<br>
Com quase 140 milhões de cópias vendidas, o gênero de **AÇÃO**, foi o mais vendido do console. Maior parte destas vendas se deve a um fenômeno do mundo dos games...
<br>
## O CAMPEÃO 🥇 DOS JOGOS...
![gta_v](https://static0.gamerantimages.com/wordpress/wp-content/uploads/GTA-V-Protagonists.jpg?q=50&fit=crop&w=1500&dpr=1.5)<br>
Com quase 20 milhões de cópias vendidas, Grand Theft Auto V (ou GTA V) foi o jogo que mais vendeu cópias no console PS4.<br>
Lembrando que esses dados compreendem os anos de 2013-2018
