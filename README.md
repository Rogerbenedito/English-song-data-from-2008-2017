# Classificació Binària de 17.7K cançons Angleses d'entre el 2008 i 2017
Linck: https://www.kaggle.com/rashikrahmanpritom/177k-english-song-data-from-20082017
(Aquest document a estat generat a partir de **Codi.ipynb** on trobareu tot el codi utilitzat)
## Objectiu
Poder classificar cançons entre els estils (Gèneres) de Rock i de Hip-Hop

## Introducció
En aquest document trobareu els resultats generats per fer un aprenentatge computacional de classificació i analitzarem els següents punts:
```
Analitzar les dades de més de 17.000 cançons
Netejar les dades incompletes o innecessàries de 21 atributs.
Identificar els atributs rellevants i l'atribut objectiu
Manipular dades no numèriques per poder visualitzar possibles correlacions
Comprovar els beneficis de balancejar les dades
Analitzar diferents models de classificació
Diferenciar cançons entre Rock i Hip-Hop.
```

## Llibreries necessàries:
```
numpy
scikit-learn
matplotlib
scipy
imbalanced-learn
sklearn
```

## Anàlisis dels atributs:

 Dimensionalitat de la BBDD: (17734, 21)
    
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_id</th>
      <th>bit_rate</th>
      <th>comments</th>
      <th>composer</th>
      <th>date_created</th>
      <th>date_recorded</th>
      <th>duration</th>
      <th>favorites</th>
      <th>genre_top</th>
      <th>genres</th>
      <th>...</th>
      <th>information</th>
      <th>interest</th>
      <th>language_code</th>
      <th>license</th>
      <th>listens</th>
      <th>lyricist</th>
      <th>number</th>
      <th>publisher</th>
      <th>tags</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>135</td>
      <td>256000</td>
      <td>1</td>
      <td>NaN</td>
      <td>2008-11-26 01:43:26</td>
      <td>2008-11-26 00:00:00</td>
      <td>837</td>
      <td>0</td>
      <td>Rock</td>
      <td>[45, 58]</td>
      <td>...</td>
      <td>NaN</td>
      <td>2484</td>
      <td>en</td>
      <td>Attribution-NonCommercial-ShareAlike 3.0 Inter...</td>
      <td>1832</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>[]</td>
      <td>Father's Day</td>
    </tr>
    <tr>
      <th>1</th>
      <td>136</td>
      <td>256000</td>
      <td>1</td>
      <td>NaN</td>
      <td>2008-11-26 01:43:35</td>
      <td>2008-11-26 00:00:00</td>
      <td>509</td>
      <td>0</td>
      <td>Rock</td>
      <td>[45, 58]</td>
      <td>...</td>
      <td>NaN</td>
      <td>1948</td>
      <td>en</td>
      <td>Attribution-NonCommercial-ShareAlike 3.0 Inter...</td>
      <td>1498</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>[]</td>
      <td>Peel Back The Mountain Sky</td>
    </tr>
    <tr>
      <th>2</th>
      <td>151</td>
      <td>192000</td>
      <td>0</td>
      <td>NaN</td>
      <td>2008-11-26 01:44:55</td>
      <td>NaN</td>
      <td>192</td>
      <td>0</td>
      <td>Rock</td>
      <td>[25]</td>
      <td>...</td>
      <td>NaN</td>
      <td>701</td>
      <td>en</td>
      <td>Attribution-NonCommercial-ShareAlike 3.0 Inter...</td>
      <td>148</td>
      <td>NaN</td>
      <td>4</td>
      <td>NaN</td>
      <td>[]</td>
      <td>Untitled 04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>152</td>
      <td>192000</td>
      <td>0</td>
      <td>NaN</td>
      <td>2008-11-26 01:44:58</td>
      <td>NaN</td>
      <td>193</td>
      <td>0</td>
      <td>Rock</td>
      <td>[25]</td>
      <td>...</td>
      <td>NaN</td>
      <td>637</td>
      <td>en</td>
      <td>Attribution-NonCommercial-ShareAlike 3.0 Inter...</td>
      <td>98</td>
      <td>NaN</td>
      <td>11</td>
      <td>NaN</td>
      <td>[]</td>
      <td>Untitled 11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>153</td>
      <td>256000</td>
      <td>0</td>
      <td>Arc and Sender</td>
      <td>2008-11-26 01:45:00</td>
      <td>2008-11-26 00:00:00</td>
      <td>405</td>
      <td>5</td>
      <td>Rock</td>
      <td>[26]</td>
      <td>...</td>
      <td>NaN</td>
      <td>354</td>
      <td>en</td>
      <td>Attribution-NonCommercial-NoDerivatives (aka M...</td>
      <td>424</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>[]</td>
      <td>Hundred-Year Flood</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>


### Descripció dels atributs:
Com podem observar, la nostra base de dades consta 17734 cançons i cada cançó conste de 21 atributs que la defineixen.
Els atributs són:

**track_id**: ID de la cançó. (Int)

**bit_rate**: Freqüència amb què les dades s'emmagatzemen o es transmeten en un medi, medides en BPM.(Int)

**comments**: Nombre de comentaris en la plataforma de Spoty .(Int)

**composer**: Nom del compositor. (String)

**date_created**: Data en què es va crear. (Date)

**date_recorded**: Data en què es va gravar. (Date)

**duration**: Duració de la cançó en segons. (Int)

**favorites**: Número de "Favorits" en la plataforma Spoty. (Int)

**genre_top**: Gènera de la cançó (**Serà el nostre Atribut Objectiu**). (String)

**genres**: Gènera de la llista de cançons que apareix. (Array Int)

**genres_all**: Tots els generes assignats de cada cançó. (Array Int)

**information**: Informació extra que poden incorporar a Spoty. (String)

**interest**: Valor de la cançó directament proporcional a les reproduccions del últim més. (Int)

**language_code**: Idioma de la cançó (String)

**license**: Llicències que de la cançó (String)

**listens**: Nombre de reproduccions (int)

**lyricist**: Lletra de la cançó. (String)

**number**: Número de la cançó dintre del disc (Int)

**publisher**: Nom de l'editora (String)

**tags**: Anotacions de cada canso (Array String)

**title**: Nom de cada cançó (String)

### Neteja d'atributs amb informació nul·la:


    track_id             0
    bit_rate             0
    comments             0
    composer         17568
    date_created         0
    date_recorded    15836
    duration             0
    favorites            0
    genre_top            0
    genres               0
    genres_all           0
    information      17252
    interest             0
    language_code    13645
    license             20
    listens              0
    lyricist         17681
    number               0
    publisher        17682
    tags                 0
    title                0
    dtype: int64
    

    Dimensionalitat de la BBDD: (17734, 21)
    

Observem que dels 21 atributs hi ha 6 que no tenim informació introduïda, així que eliminarem aquestes columnes innecessàries (composer, date_recorded, information, language_code, lyricist, publisher)


    track_id         0
    bit_rate         0
    comments         0
    date_created     0
    duration         0
    favorites        0
    genre_top        0
    genres           0
    genres_all       0
    interest         0
    license         20
    listens          0
    number           0
    tags             0
    title            0
    dtype: int64
    

També observem que en l'atribut **"license"** tenim 20 valors com a NaN així que també eliminarem les files que corresponents.
Això provocarà que passa'm de tenir 17734 cançons a 17714


    track_id        0
    bit_rate        0
    comments        0
    date_created    0
    duration        0
    favorites       0
    genre_top       0
    genres          0
    genres_all      0
    interest        0
    license         0
    listens         0
    number          0
    tags            0
    title           0
    dtype: int64
    
Mirant una mica més a fons la base de dades, observem que hi ha l'atribut **"Tags"** que també consta amb un 87,9% de valors NaN (15579), però camuflats com a "[]", ja que són Arrays de String.
Així que també el treure'm del nostre dataset.

També traurem atributs que són irrellevants com; **track_id**, **number**, **date_created**, **license** i **title**


Dimensionalitat de la BBDD: (17714, 9)
    

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bit_rate</th>
      <th>comments</th>
      <th>duration</th>
      <th>favorites</th>
      <th>genre_top</th>
      <th>interest</th>
      <th>listens</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>256000</td>
      <td>1</td>
      <td>837</td>
      <td>0</td>
      <td>Rock</td>
      <td>2484</td>
      <td>1832</td>
    </tr>
    <tr>
      <th>1</th>
      <td>256000</td>
      <td>1</td>
      <td>509</td>
      <td>0</td>
      <td>Rock</td>
      <td>1948</td>
      <td>1498</td>
    </tr>
    <tr>
      <th>2</th>
      <td>192000</td>
      <td>0</td>
      <td>192</td>
      <td>0</td>
      <td>Rock</td>
      <td>701</td>
      <td>148</td>
    </tr>
    <tr>
      <th>3</th>
      <td>192000</td>
      <td>0</td>
      <td>193</td>
      <td>0</td>
      <td>Rock</td>
      <td>637</td>
      <td>98</td>
    </tr>
    <tr>
      <th>4</th>
      <td>256000</td>
      <td>0</td>
      <td>405</td>
      <td>5</td>
      <td>Rock</td>
      <td>354</td>
      <td>424</td>
    </tr>
  </tbody>
</table>
</div>



### Anàlisis de correlació
Un cop netejada la base de dades, intentarem passar l'atribut "genre_top", que es String, a Int per poder visualitzar si hi ha una correlació entre ells amb la **Taula de correlacions** i la funcio **pairplot** i comprovarem si les dades estan balancejades per evitar una mala interpretació de les dades i que a l'hora de generar el model no pugui provocar una mala classificació.

![alt text](img/AtributObjectiuCount.PNG)
![alt text](img/TaulaCorrelacio_1.PNG)


Observem que hi ha una alta correlació entre els atributs "listens" i "interest". Això ja ens ho esperavem, ja que si el número de reproduccions d'una cançó augmenta, l'interès que se li assigna aquesta cançó, també augmenta.
També passa una cosa similar amb els "comments" i els "favorites", ja que si t'agrada una canso, la comentes i li dónes 'like'.

Però al mirrar si hi ha alguna correlació entre els atributs numèrics i l'atribut objectiu, no apareix res realment significatiu.
Dels atributs numèrics, el que ens dóna més informació, és el de "bit_rate", ja que ens dóna el número de BPM. Això te logica, ja que el Hip-Hop acostuma a utilitzar uns BPM entre els 60 i els 120, cosa que el Rock no té tan marcat. Però com el número de cançons de Rock forme el 80% de les dades, pot ser que ens provoqui aquesta poca correlació entre BPM i Hip-Hop.
Així que balancegarem el número de cançons de cada classe.

Tot hi això si no aconseguim ningun resultat, també podem mirar els atributs "genres" i "genres_all", ja que ens indican, en quin tipus de disc/àlbum està i els gèneres musicals que té associat. Però abans també haurem d'adaptar el nostre dataset, ja que estan en format strting.
    

![alt text](img/AtributObjectiuCountBalansed.PNG)
![alt text](img/TaulaCorrelacio_2.PNG)
    

Un cop balancejats el número de valors de cada classe, observem que la correlació entre els BPM (bit_range) a augmentat, però no tant com esperàvem, per tant, la nostra hipòtesi de poder classificar la música segons unicament el seu BPM no semble que pugui funcionar.

### Selecció d'atributs

Intentarem generar la classificació utilitzant també els atributs **genres** i **genres_all**, però abans haurem de tractar les dades, ja que, com ja hem dit, les dades estan en format String. A sobre no sabem quina de les ID utilitzades, dintre d'aquests atributs, fan referència al genera osubgenera de Rock i de Hip-Hop i per finalitzar una cançó pot tindre més d'una ID referenciada a un gènera.  

Per començar utilitzarem una tècnica per seleccionar el primer gènera que tenen assignades cadascuna dels atributs anomenats anteriorment.

Llegirem el primer valor del String, l'aïllarem i el passarem a Int. Això ho farem amb la funció "selectFirst", i ho aplicarem tant a l'atribut **genres** com el **genres_all**.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>bit_rate</th>
      <th>comments</th>
      <th>duration</th>
      <th>favorites</th>
      <th>genre_top</th>
      <th>genres</th>
      <th>genres_all</th>
      <th>interest</th>
      <th>listens</th>
    </tr>
    <tr>
      <th>genre_top</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Hip-Hop</th>
      <th>0</th>
      <td>320000</td>
      <td>0</td>
      <td>250</td>
      <td>0</td>
      <td>1</td>
      <td>21</td>
      <td>21</td>
      <td>479</td>
      <td>335</td>
    </tr>
    <tr>
      <th>1</th>
      <td>320000</td>
      <td>0</td>
      <td>134</td>
      <td>1</td>
      <td>1</td>
      <td>21</td>
      <td>21</td>
      <td>181</td>
      <td>228</td>
    </tr>
    <tr>
      <th>2</th>
      <td>160000</td>
      <td>0</td>
      <td>101</td>
      <td>6</td>
      <td>1</td>
      <td>21</td>
      <td>21</td>
      <td>1284</td>
      <td>825</td>
    </tr>
    <tr>
      <th>3</th>
      <td>320000</td>
      <td>0</td>
      <td>172</td>
      <td>1</td>
      <td>1</td>
      <td>21</td>
      <td>21</td>
      <td>109</td>
      <td>57</td>
    </tr>
    <tr>
      <th>4</th>
      <td>320000</td>
      <td>0</td>
      <td>175</td>
      <td>3</td>
      <td>1</td>
      <td>21</td>
      <td>21</td>
      <td>1404</td>
      <td>1179</td>
    </tr>
  </tbody>
</table>
</div>

![alt text](img/TaulaCorrelacio_3.PNG)

Com observem, amb l'atribut **genres_all** tenim una correlació amb l'atribut objectiu encara més alta que amb el dels BPM i també observem que hi ha una alta correlació entre l'atribut **genres_all** i **genres**

Començarem combinant els atributs amb una major correlació amb l'atribut objectiu per intentar generar una classificació.

Aquests atributs són; **genres_all** i **bit_rate**.

Però més endavant veurem els resultats de combinar els atributs **genres_all** i **genres**

Dimensionalitat de la BBDD: (7104, 3)
    
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>genre_top</th>
      <th>genres_all</th>
      <th>bit_rate</th>
    </tr>
    <tr>
      <th>genre_top</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Hip-Hop</th>
      <th>0</th>
      <td>1</td>
      <td>21</td>
      <td>320000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>21</td>
      <td>320000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>21</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>21</td>
      <td>320000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>21</td>
      <td>320000</td>
    </tr>
  </tbody>
</table>
</div>


## Anàlisis de models de Classificació
Ara que ja tenim el nostre Dataset només amb els atributs que volem, provarem de gènera unes classificacions Logística i SVM amb diferents conjunts d'aprenentatge i test per veure el tant per cent de classificació correcte que podem obtenir amb aquests mètodes.

(El mètode SVM, l'utilitzarem amb el tipus de kernel 'rpf')


    Correct classification Logistic  0.5 % of the data:  0.7043918918918919
    Correct classification SVM       0.5 % of the data:  0.7730855855855856
    Correct classification Logistic  0.7 % of the data:  0.6937148217636022
    Correct classification SVM       0.7 % of the data:  0.7650093808630394
    Correct classification Logistic  0.8 % of the data:  0.7065446868402533
    Correct classification SVM       0.8 % of the data:  0.796622097114708
    

Observem que utilitzar els mètodes d'hiperplans, obtenim una millor classificació, aixi que intentarem provar diferents kernels amb el mètode SVM per veure les diferents generacions de classificacions que poden produir i seleccionarem els que ens doni una major taxa de classificació correcte.

![alt text](img/Classificador_1.PNG)

Com podem veure, les classificacions lineals sembla que no són les més indicades, en canvi les que compten amb una Lambda (Λ) major, ens generen una classificació més encertada. Tot i això i per asseguren-se, també generarem un rànquing amb els mètodes segons el seu radi d'encert amb la classificació.


</style>
<table id="T_c00bb_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >model</th>
      <th class="col_heading level0 col1" >cv_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_c00bb_level0_row0" class="row_heading level0 row0" >3</th>
      <td id="T_c00bb_row0_col0" class="data row0 col0" >SVC(kernel='linear')</td>
      <td id="T_c00bb_row0_col1" class="data row0 col1" >0.577777</td>
    </tr>
    <tr>
      <th id="T_c00bb_level0_row1" class="row_heading level0 row1" >4</th>
      <td id="T_c00bb_row1_col0" class="data row1 col0" >LinearSVC()</td>
      <td id="T_c00bb_row1_col1" class="data row1 col1" >0.702777</td>
    </tr>
    <tr>
      <th id="T_c00bb_level0_row2" class="row_heading level0 row2" >2</th>
      <td id="T_c00bb_row2_col0" class="data row2 col0" >LogisticRegression()</td>
      <td id="T_c00bb_row2_col1" class="data row2 col1" >0.704999</td>
    </tr>
    <tr>
      <th id="T_c00bb_level0_row3" class="row_heading level0 row3" >1</th>
      <td id="T_c00bb_row3_col0" class="data row3 col0" >SVC(kernel='poly')</td>
      <td id="T_c00bb_row3_col1" class="data row3 col1" >0.723148</td>
    </tr>
    <tr>
      <th id="T_c00bb_level0_row4" class="row_heading level0 row4" >0</th>
      <td id="T_c00bb_row4_col0" class="data row4 col0" >SVC()</td>
      <td id="T_c00bb_row4_col1" class="data row4 col1" >0.766667</td>
    </tr>
  </tbody>
</table>




Observan aquesta taula, valem que el mètode de classificació amb una major tassa d'encerts és el SVM amb el kernels de tipus 'rpf', seguit per al SVM amb els kernels de tipus polinomial.
A més a més, veiem que el model de classificació Logística dona millors resultats que els models SVM lineals.

## Beneficis de balancejar les dades
En aquest punt podem dir que podem classificar les cançons segons si són del gènera musical Rock o Hip-hop, amb una precisió del 76,7% i sempre que la quantitat de cançons de cada estil estigui balancejada, però que passaria si intentéssim classificar una llista de cançons on el 80% d'elles són de Rock i el 20% de Hip-hip? (Llista original)

Nosaltres hem suposat que en haver una diferència tan gran entre classes, a l'hora d'intentar generar una classificació, el model classificaria totes les cançons del tipus Rock i això provocaria una tassa de falsos negatius de 20%, obtenint així una classificació amb una tassa d'encerts del 80%. Però realment passaria?

Ara intentarem classificar les 17.000 cançons sense balancejar-les.

![alt text](img/Classificador_2.PNG)

<table id="T_20710_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >model</th>
      <th class="col_heading level0 col1" >cv_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_20710_level0_row0" class="row_heading level0 row0" >3</th>
      <td id="T_20710_row0_col0" class="data row0 col0" >SVC(kernel='linear')</td>
      <td id="T_20710_row0_col1" class="data row0 col1" >0.572493</td>
    </tr>
    <tr>
      <th id="T_20710_level0_row1" class="row_heading level0 row1" >4</th>
      <td id="T_20710_row1_col0" class="data row1 col0" >LinearSVC()</td>
      <td id="T_20710_row1_col1" class="data row1 col1" >0.698613</td>
    </tr>
    <tr>
      <th id="T_20710_level0_row2" class="row_heading level0 row2" >2</th>
      <td id="T_20710_row2_col0" class="data row2 col0" >LogisticRegression()</td>
      <td id="T_20710_row2_col1" class="data row2 col1" >0.700924</td>
    </tr>
    <tr>
      <th id="T_20710_level0_row3" class="row_heading level0 row3" >1</th>
      <td id="T_20710_row3_col0" class="data row3 col0" >SVC(kernel='poly')</td>
      <td id="T_20710_row3_col1" class="data row3 col1" >0.712433</td>
    </tr>
    <tr>
      <th id="T_20710_level0_row4" class="row_heading level0 row4" >0</th>
      <td id="T_20710_row4_col0" class="data row4 col0" >SVC()</td>
      <td id="T_20710_row4_col1" class="data row4 col1" >0.770399</td>
    </tr>
  </tbody>
</table>




Observant els resultats veiem que, en utilitzar tot el dataset sense balancejar el nombre de cada classe, obtenim un rati d'encerts amb un 0,6% major que balanceja'n-ho. Si no interpretéssim bé les dades, podríem pensar que això implica que usant el 100% del dataset, podem generem una millor classificació, però realment és així?

El que realment està passant és que el nombre de cançons de Rock ha augmentat tant que el percentatge de falsos negatius en comparació als certs negatius sa descompensat prou per a obviar l'existència de falsos negatius. Si aquest model l'uséssim amb un dataset on la quantitat de cançons de cala classe fos similar, ens donaria una tassa d'èxit pitjor a la que havíem generat amb el model balancejat. Per tant, podem dir que la nostra hipòtesi de balancejar les classes, era certa.

Podem dir que llavors, el model generat anteriorment, és el millor possible quan les dades estan balancejades?
No ho podem assegurar, ja que és possible obtenir una major tassa de classificació utilitzant un mètode diferent de seleccionar els valors de **genres_all**.
També podríem obtenir un millor model, ajustant correctament els atributs de la funció SVM i optimitzant el seu funcionament.

## Mètodes ensemble

També podem provar d'utilitzar models **'ensemble'** per veure si podem generar una bona classificació i sense que ens generi Overfitting.
Per fer-ho utilitzarem el model SVM amb els kernels de tipus 'rpf' amb el metode **BaggingClassifier**, ja que és els que ens generen la millor classificació i així provem si podem optimitzar-ho, però també el compararem amb el mètode **GradientBoostingClassifier** utilitzant el model de Regressió Logística. (Opció per defecte de la fonació GradientBoostingClassifier)
(Com hem vist que balancejar les classes és necessari, tornarem a utilitzar les dades balancejades)

![alt text](img/Classificador_3.PNG)


<table id="T_19334_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >model</th>
      <th class="col_heading level0 col1" >cv_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_19334_level0_row0" class="row_heading level0 row0" >0</th>
      <td id="T_19334_row0_col0" class="data row0 col0" >BaggingClassifier(base_estimator=SVC(C=0.2, gamma=0.7))</td>
      <td id="T_19334_row0_col1" class="data row0 col1" >0.767239</td>
    </tr>
    <tr>
      <th id="T_19334_level0_row1" class="row_heading level0 row1" >1</th>
      <td id="T_19334_row1_col0" class="data row1 col0" >GradientBoostingClassifier()</td>
      <td id="T_19334_row1_col1" class="data row1 col1" >0.999717</td>
    </tr>
  </tbody>
</table>




Veiem que utilitzant el mètode BaggingClassifier amb el model SVC, obtenim uns resultats molt similars als obtinguts utilitzen només SVC. En canvi, a l'utilitzar un mètode ensemble amb el model de Regresio Logistica, observem un canvi dràstic, en la classificació. Veiem que només utilitza l'eix horitzontal per diferenciar entre classes i aconsegueix genera una classificació molt més precisa. Aquest eix horitzontal representa els diferents valors de l'atribut **genres_all**. Això implica que estem sent capaços de classificar per ID de subclasse (subgènere). Però és molt probable que això hagi sorgit per culpa d'un sobre entrenament i que a l'hora d'intentar incorpora noves dades de test, ens acabi donant una tassa d'error superior. 

## Utilització de diferents atributs

Un cop vist això deixarem d'utilitzar l'atribut **bit_rate** que té una correlació baixa amb l'atribut **genres_all** i utilitzarem l'atribut **genres**, que com ja hem vist anteriorment, té una correlació del 56% i mirarem si podem genera una dispersió major de les dades.

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>genre_top</th>
      <th>genres</th>
      <th>genres_all</th>
    </tr>
    <tr>
      <th>genre_top</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Hip-Hop</th>
      <th>0</th>
      <td>1</td>
      <td>21</td>
      <td>21</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>21</td>
      <td>21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>21</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>21</td>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>21</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>



![alt text](img/Classificador_4.PNG)



<table id="T_4d150_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >model</th>
      <th class="col_heading level0 col1" >cv_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_4d150_level0_row0" class="row_heading level0 row0" >2</th>
      <td id="T_4d150_row0_col0" class="data row0 col0" >LogisticRegression()</td>
      <td id="T_4d150_row0_col1" class="data row0 col1" >0.511664</td>
    </tr>
    <tr>
      <th id="T_4d150_level0_row1" class="row_heading level0 row1" >4</th>
      <td id="T_4d150_row1_col0" class="data row1 col0" >LinearSVC()</td>
      <td id="T_4d150_row1_col1" class="data row1 col1" >0.553333</td>
    </tr>
    <tr>
      <th id="T_4d150_level0_row2" class="row_heading level0 row2" >3</th>
      <td id="T_4d150_row2_col0" class="data row2 col0" >SVC(kernel='linear')</td>
      <td id="T_4d150_row2_col1" class="data row2 col1" >0.567408</td>
    </tr>
    <tr>
      <th id="T_4d150_level0_row3" class="row_heading level0 row3" >1</th>
      <td id="T_4d150_row3_col0" class="data row3 col0" >SVC(kernel='poly')</td>
      <td id="T_4d150_row3_col1" class="data row3 col1" >0.583150</td>
    </tr>
    <tr>
      <th id="T_4d150_level0_row4" class="row_heading level0 row4" >0</th>
      <td id="T_4d150_row4_col0" class="data row4 col0" >SVC()</td>
      <td id="T_4d150_row4_col1" class="data row4 col1" >0.696113</td>
    </tr>
  </tbody>
</table>




Com podem veure, en comptes de gènera una dispersió de les dades, hem acabat ajuntant la gran part d'elles el que dificulta genera una bona classificació i tot i que podríem utilitzar mètodes ensemble, acabaria donant resultats molt similars als obtinguts amb la selecció d'atributs anteriors.

Per aquest motiu i perquè el temps computacional comença a ser bastant alt, he decidit deixar-ho en aquest punt.

## Conclusions
Hem pogut veure com el balanceja les dades ens serveix per no generar classificacions errònies.

Hem vist també, que els atributs amb major importància són 'genres_all', 'bit_rate' i 'genres'.

També hem sigut capaços de generar una classificació del 76,7% utilitzant els atributs 'genres_all' i 'bit_rate'.

Hem vist que és possible generar classificacions només utilitzant l'atribut 'genres_all', però que té altra probabilitat de ser culpa d'un sobreentrenament de les dades.

I finalment, que podríem segui intenten genera un millor classificador si som capaços d'especificar un segon atribut el qual dispersi les dades més agrupades.
