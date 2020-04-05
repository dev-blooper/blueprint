---
layout: post
title:  "Welcome to Jekyll!"
date:   2020-04-05 18:25:33 -0500
categories: jekyll update
---

Primeros pasos[¶](#Primeros-pasos) {#Primeros-pasos}
==================================

En este tutorial vamos a conocer los usos mas utilizados con pandas para
explorar nuestros datasets.

Recordemos que el análisis exploratorio de datos (EDA del inglés
Exploratory Data Analysis) se realiza con el fin de:

-   Resumir las principales características del conjunto de datos.
-   Entender mejor el conjunto de datos que se está tratando.
-   Establecer relaciones entre variables.
-   Determinar si una variables es un buen predictor de una variable
    blanco.
-   Extraer las variables más importantes.

En primer lugar, vamos a cargar el dataset de caractarísticas de carros.

In [0]:

    # importamos librerias
    import pandas as pd
    import numpy as np

    # librerias para graficar
    import seaborn as sns
    import matplotlib.pyplot as plt

In [0]:

    file = 'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/automobileEDA.csv'

El primer paso es cargar el dataset que esta en formato csv y el segundo
paso es visualizar las primeras 5 filas con el metodo head

In [3]:

    # creamos un dataframe y visualizamos el dataset
    df = pd.read_csv(file)
    df.head()

Out[3]:

symboling

normalized-losses

make

aspiration

num-of-doors

body-style

drive-wheels

engine-location

wheel-base

length

width

height

curb-weight

engine-type

num-of-cylinders

engine-size

fuel-system

bore

stroke

compression-ratio

horsepower

peak-rpm

city-mpg

highway-mpg

price

city-L/100km

horsepower-binned

diesel

gas

0

3

122

alfa-romero

std

two

convertible

rwd

front

88.6

0.811148

0.890278

48.8

2548

dohc

four

130

mpfi

3.47

2.68

9.0

111.0

5000.0

21

27

13495.0

11.190476

Medium

0

1

1

3

122

alfa-romero

std

two

convertible

rwd

front

88.6

0.811148

0.890278

48.8

2548

dohc

four

130

mpfi

3.47

2.68

9.0

111.0

5000.0

21

27

16500.0

11.190476

Medium

0

1

2

1

122

alfa-romero

std

two

hatchback

rwd

front

94.5

0.822681

0.909722

52.4

2823

ohcv

six

152

mpfi

2.68

3.47

9.0

154.0

5000.0

19

26

16500.0

12.368421

Medium

0

1

3

2

164

audi

std

four

sedan

fwd

front

99.8

0.848630

0.919444

54.3

2337

ohc

four

109

mpfi

3.19

3.40

10.0

102.0

5500.0

24

30

13950.0

9.791667

Medium

0

1

4

2

164

audi

std

four

sedan

4wd

front

99.4

0.848630

0.922222

54.3

2824

ohc

five

136

mpfi

3.19

3.40

8.0

115.0

5500.0

18

22

17450.0

13.055556

Medium

0

1

Si queremos seleccionar una columna del dataset solo es necesario
realizarlo de la siguiente manera `df['nombre_columna']`

In [11]:

    df['symboling']

Out[11]:

    0      3
    1      3
    2      1
    3      2
    4      2
          ..
    196   -1
    197   -1
    198   -1
    199   -1
    200   -1
    Name: symboling, Length: 201, dtype: int64

Para seleccionar mas de una columna se realiza de esta forma
`df[['columna1','columna2', .. ]]`

In [12]:

    df[['make','aspiration']]

Out[12]:

make

aspiration

0

alfa-romero

std

1

alfa-romero

std

2

alfa-romero

std

3

audi

std

4

audi

std

...

...

...

196

volvo

std

197

volvo

turbo

198

volvo

std

199

volvo

turbo

200

volvo

turbo

201 rows × 2 columns

Es muy importante saber que datos estan vacios (en Python lo
identificamos con *na*). Para saberlo realizamos lo siguiente

In [7]:

    df.isna().sum()

Out[7]:

    symboling            0
    normalized-losses    0
    make                 0
    aspiration           0
    num-of-doors         0
    body-style           0
    drive-wheels         0
    engine-location      0
    wheel-base           0
    length               0
    width                0
    height               0
    curb-weight          0
    engine-type          0
    num-of-cylinders     0
    engine-size          0
    fuel-system          0
    bore                 0
    stroke               4
    compression-ratio    0
    horsepower           0
    peak-rpm             0
    city-mpg             0
    highway-mpg          0
    price                0
    city-L/100km         0
    horsepower-binned    1
    diesel               0
    gas                  0
    dtype: int64

Ahora tenemos que averiguar que tipo de variables hay en el dataset

In [8]:

    df.dtypes

Out[8]:

    symboling              int64
    normalized-losses      int64
    make                  object
    aspiration            object
    num-of-doors          object
    body-style            object
    drive-wheels          object
    engine-location       object
    wheel-base           float64
    length               float64
    width                float64
    height               float64
    curb-weight            int64
    engine-type           object
    num-of-cylinders      object
    engine-size            int64
    fuel-system           object
    bore                 float64
    stroke               float64
    compression-ratio    float64
    horsepower           float64
    peak-rpm             float64
    city-mpg               int64
    highway-mpg            int64
    price                float64
    city-L/100km         float64
    horsepower-binned     object
    diesel                 int64
    gas                    int64
    dtype: object

Ademas, es importante realizar una exploración de los datos. La
estadística nos permite explorar los datos con el propósito de hallar
las características principales, mediante la implementación de gráficas
y el cálculo de algunas variable estadísticas

In [9]:

    # Para dar una descripción estadística de variables numéricas:
    df.describe()

Out[9]:

symboling

normalized-losses

wheel-base

length

width

height

curb-weight

engine-size

bore

stroke

compression-ratio

horsepower

peak-rpm

city-mpg

highway-mpg

price

city-L/100km

diesel

gas

count

201.000000

201.00000

201.000000

201.000000

201.000000

201.000000

201.000000

201.000000

201.000000

197.000000

201.000000

201.000000

201.000000

201.000000

201.000000

201.000000

201.000000

201.000000

201.000000

mean

0.840796

122.00000

98.797015

0.837102

0.915126

53.766667

2555.666667

126.875622

3.330692

3.256904

10.164279

103.405534

5117.665368

25.179104

30.686567

13207.129353

9.944145

0.099502

0.900498

std

1.254802

31.99625

6.066366

0.059213

0.029187

2.447822

517.296727

41.546834

0.268072

0.319256

4.004965

37.365700

478.113805

6.423220

6.815150

7947.066342

2.534599

0.300083

0.300083

min

-2.000000

65.00000

86.600000

0.678039

0.837500

47.800000

1488.000000

61.000000

2.540000

2.070000

7.000000

48.000000

4150.000000

13.000000

16.000000

5118.000000

4.795918

0.000000

0.000000

25%

0.000000

101.00000

94.500000

0.801538

0.890278

52.000000

2169.000000

98.000000

3.150000

3.110000

8.600000

70.000000

4800.000000

19.000000

25.000000

7775.000000

7.833333

0.000000

1.000000

50%

1.000000

122.00000

97.000000

0.832292

0.909722

54.100000

2414.000000

120.000000

3.310000

3.290000

9.000000

95.000000

5125.369458

24.000000

30.000000

10295.000000

9.791667

0.000000

1.000000

75%

2.000000

137.00000

102.400000

0.881788

0.925000

55.500000

2926.000000

141.000000

3.580000

3.410000

9.400000

116.000000

5500.000000

30.000000

34.000000

16500.000000

12.368421

0.000000

1.000000

max

3.000000

256.00000

120.900000

1.000000

1.000000

59.800000

4066.000000

326.000000

3.940000

4.170000

23.000000

262.000000

6600.000000

49.000000

54.000000

45400.000000

18.076923

1.000000

1.000000

la variable "drive-wheels" describe la tracción de los vehiculos
consignados en la tabla; son variables categóricas que representan:

1.  fwd - Front Wheel Drive: Tracción delantera.
2.  rwd - Rear Wheel Drive: Tracción Tracera.
3.  4wd - 4 Wheel Drive: Tracción de cuatro ruedas.

Para contabilizar esta variable usamos el método `.value_counts()`

In [10]:

    df["drive-wheels"].value_counts()

Out[10]:

    fwd    118
    rwd     75
    4wd      8
    Name: drive-wheels, dtype: int64

Con pandas tambien podemos graficar. Para ello vamos a graficar en una
torta la cantidad de tipos de traccion

In [15]:

    df["drive-wheels"].value_counts().plot(kind = "pie", autopct='%1.1f%%')

Out[15]:

    <matplotlib.axes._subplots.AxesSubplot at 0x7fe65810e3c8>

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAPwAAADnCAYAAAA6ujs/AAAABHNCSVQICAgIfAhkiAAAAAlwSFlz%0AAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjEsIGh0%0AdHA6Ly9tYXRwbG90bGliLm9yZy+j8jraAAAgAElEQVR4nO3deXiU5dn38e85W5ZJCKsssowouCuK%0A4gYuta3SuD1qrdsrVftY3Ku1dtradmwfbOpSba1ad0vRitVWwXGrG4uiqIigSEQkLLJJCEM2ss31%0A/nEPGpYkk5CZa2bu83McOcg2M79ozlz3fa1ijEEp5Q4e2wGUUumjBa+Ui2jBK+UiWvBKuYgWvFIu%0AogWvlItowSvlIlrwSrmIFrxSLqIFr5SLaMEr5SJa8Eq5iBa8Ui6iBa+Ui2jBK+UiWvBKuYgWvFIu%0AogWvlItowaeQiFwjIp+KyOOdfFyFiPRNVS7lXj7bAXLcFcC3jTGrbAdRCrSFTxkR+RswHHhRRIw4%0AeopIi4gcm/iemSIyQkT6iMgrIvKJiDwEiNXwKmdpwaeIMWYisBo4AXgZ2A8YC8wDxolIHjDEGLME%0A+C0w2xizP/AfYKid1CrXacGnxyzg2MTbH3AK/3DgvcTXjwWmABhjokCVhYzKBbTg02MmMA4YA7wA%0A9ASOx/lDoFTaaMGnx1zgaCBujNkCzAd+jPOHgMS/5wOIyHigl42QKvdpwaeBMaYBWAm8k/jULKAY%0AWJj4+GbgWBH5BDgTWJH2kMoVRI+aUso9dBw+R4XC0T7Avom3oUAREOzgTXA6DDcCldv92/r9L4El%0AFWWlzen7iVR30BY+i4XCUQGG8E1ht35L9Uy9RqAc+AT4GKdf4r2KstL1KX5dtQu04LNIKBz1AIcC%0A3wJOxOkILLIaakfLcTop5wKvV5SVzrOcR7WiBZ/hQuFof+AUoBRnEk9Pu4k6bSXwHPAsMENvA+zS%0Ags9AoXB0X5ze+lNxxu5zZaptFRDFKf6XKspKay3ncR0t+AwRCkcDwFnA5TiTdHLdFuBV4BlgakVZ%0Aab3lPK6gBW9ZKBwN4UzCuQTYzW4aayqBvwF/rSgrXWs7TC7Tgrcg0fn2PZzW/GR0AtRWjcA/gTsr%0Ayko/sh0mF2nBp1EoHA0CVwMTgWGW42S614E/AS9UlJXqL2k30YJPg1A46gUuxZlCO8BynGyzGLgT%0AeER7+HedFnyKhcLRUuBWnPXwqusWAddUlJW+ZjtINtOCT5FQOHoocDvO2LnqPs8A11eUleoCoy7Q%0Agu9moXB0GDAJZ7lrroyfZ5p6oAy4taKsdIvtMNlEC76bhMJRP/Br4GdAvuU4brEMuK6irPQ520Gy%0AhRZ8NwiFoyOAx3G2rVLp9zJwdUVZ6RLbQTKdjv/uolA4einwIVrsNp0EzE/8v1Dt0Ba+i0LhaG/g%0AAZzpsCpzPAlMrCgrjdkOkom04LsgFI5+C5gM7G47i9qpZcB5FWWl79oOkmm04Dsh0TE3CfgpejuU%0A6RqBn1SUld5nO0gm0YJPUigcHYCzrnuM7SyqUx4DLtfhO4cWfBJC4eh+OPvJ6/z37DQPOLOirHS5%0A7SC2acF3IBSOngD8m+zbaUZtazVwYkVZ6WLbQWzS+9B2hMLR84GX0GLPBYOAGaFw9CDbQWzSgm9D%0AKBy9Aue8t4DtLKrb7Aa8GQpHXTtnQgt+J0Lh6C+Be9C58LmoF/BqKBwdazuIDVrw2wmFo3/EGXpT%0AuasH8HIoHP227SDppgXfSigc/R1wo+0cKi0KgedD4egptoOkk/bSJyTmYT9kO4dKuybg/Iqy0qdt%0AB0kHLXggFI6eDExHz9pzq0bgWxVlpW/ZDpJqri/4UDh6CM757Jl2ZJNKr/XAmFyfnOPqe/jE7jRR%0AtNiVM2Q3LbGzcM5ybcGHwtGeONNlB9rOojLGQcCUxKm8OcmVBZ841ulZdCdZtaMzgP+zHSJVXHkP%0AHwpH/w5cZDtHe1bddwmeQAF4PIjHy8AJd9G47gsqX74H09KIeLz0/s7l5A3ae5vHbVm+gI2vP/j1%0Ax02Vq+h32o0UjjyKr6bfRtNXyynY83B6HTcBgE1vP0mg7zAKRx6V1p8vC1xQUVb6hO0Q3c11vdKh%0AcPQ8MrzYt+p/3i14C0u+/rjqzUfpecx5FOx5GPVL36PqzUcZcH7ZNo/JH3YQgy6+G4CW+mpWP/C/%0A5O9xCI3rl+Hx5THokr+y7smbiDfUEm9qoHF1OT2PPjetP1eWeDgUjn5eUVY613aQ7uSqS/pQOLo7%0AzpTZrBVvrHP+bajDW9Sn3e+tK3+L/OGj8fjzEY+PeHMDxsQx8WYQD7FZUygZe0E6YmejfODZUDia%0AUwd8uqaFT3TEPIYzlzrzibD+qd8AUDRqPMWjTqb3iZex7qnfUPXGI2DiDLjw9nafovbTmfQ4/AwA%0A/H2H4C0oYc1j11K0/wk0V63BGEPegL1S/qNksYHA3cAPbAfpLq65hw+Fo1cDf7GdI1nN1RvwFfel%0ApXYT66beRO/vTKSu/C3yhhxAcO9jqP10FjUfvUT/c3c+7b+5ZiNrHrmKwVdORrw7/l1f//TN9D7p%0AKmoXvkrj+mXkh0ZRPOrkVP9Y2eqMXNn73hWX9KFwdB/gj7ZzdIavuC8A3mBPCkceRcPqz6hZ+BqF%0AI48GoHCfsTSs+azNx9ctnkXhyKN2Wux1S94hMGAvTNMWmjatod8ZYerK3yLepLtAteG+xDBu1sv5%0Agg+Foz7gH0CB7SzJijduId5Q9/X7W5Z9SKDfMLxFvWlYuRCALcs/wt9rUJvPUbtoJsF9j9vh86al%0Amc3vP0ePI87CNDfw9QpgE4cWPZy1DQNxzgnMem64h/81cJjtEJ3RUreJr/6dGAqOxwnudxwFw0fT%0AJ5BP1asPYOItiC9A75OvBqBhzRJq5r9In/HXANAcW0dL9VfkDT1gh+eunhel6IAT8fjz8ffbA9Pc%0AwOqHr6Rgz8Pw5OuEw3ZcGgpH/5ntp9fm9D18KBw9DJiDO/6wqdRbBhxYUVZaaztIV+X6Jf1daLGr%0A7rMHWb45Ss628KFw9FRgmu0cKufEgbEVZaVzbAfpipxs4UPhqAe4xXYOlZM8OFeOWSknCx64ENix%0Ax0qp7jEmFI6ebjtEV+TcJX0oHM0DytFTYlRqLQRGVZSVxm0H6YxcbOEvR4tdpd6BZOGU25xq4UPh%0AaDGwFOhnO4tyhSXAPtnUyudaC38DWuwqfUYAZ9sO0Rk5U/ChcLQPcL3tHMp1fmE7QGfkTMEDl6Kb%0AUar0GxUKR8fbDpGsnCj4xLj7RNs5lGtlTSufEwUPjMeZ9qiUDeNC4ej+tkMkI1cK/krbAZTrXWg7%0AQDKyflgucZjEMvRoZ2XXCiBUUVaa0QWVCy38RWixK/uGAsfaDtGRXCl4pTLB/7MdoCNJFbyIBEXE%0Ak3h/pIicJiL+1EbrWCgcPQbQbVdVpjg7sZYjYyXbws8E8kVkd+AVnL9kj6UqVCdMsB1AqVZKgFNt%0Ah2hPsgUvxpg64EzgXmPM9wGrwxCJfeazcomiymkZ3VufdMGLyFHABTjHKwN4UxMpaQfiHPGrVCYZ%0AHwpHe9sO0ZZkC/4nOLOJ/mOM+UREhgNvpC5WUr5t+fWV2pkAzgm0GSmpDR6NMTOAGa0+/gK4JlWh%0AkqQFrzLVscAjtkPsTLsFLyLTgTYnEhhjTuv2REkIhaN+smDMU7nWWNsB2tJRC5+pp20cBQRth1Cq%0ADXuGwtEBFWWla20H2V67BZ+4lAdARAqAocaY8pSn6phezqtMNxZ42naI7SU78eZUYD7wUuLjUSJi%0Ac893LXiV6TLysj7ZXvoIMAbYBGCMmY+l5aihcLQHcLiN11aqE7K64JuMMbHtPmdrVdA49PgolflG%0AhcLRjNuBKdmC/0REzge8IjJCRO4G3k5hrvZkxUYDyvW8wJG2Q2wv2YK/GqfQGoAngBjOZBwbRlh6%0AXaU6a5ztANtLduJNHfArEZmUeN+mkZZfX6lkHWw7wPaS7aU/WkQWAYsTHx8sIvemNFnbtIVX2WKo%0A7QDbS/aS/k7gJKASwBjzERZmuiU6QQam+3WV6qKsLXiMMSu3+1RLN2dJhrbuKpv0CYWjhbZDtJZs%0Awa8UkaMBIyJ+EbkB+DSFudqiBa+yzRDbAVpLtuAn4mwFvTvwJTAKO1tDa8GrbJNRl/XJ9tJvwNn8%0AwjYteJVtsq/gRaQf8L9AqPVjjDGXpCZWm4an+fWU2lXZV/DAc8As4FXsdNZtlXFTFZXqQEbdwydb%0A8IXGmJ+nNElyMnoLYKV2IqNa+GQ77Z4Xke+lNEly8m0HUKqTMmpDy462uKrGWRUnwC9FpAFoSnxs%0AjDE9Uh9xG1rwKttYP7CltY52vClOV5Ak6SW9yjYZVfDJzqX/h4j8r4jsk+pAHdAWXmWb7Ct4nC13%0ABwJ3i8gXIvKMiFybwlxt0RZeZZuM2qwl6fPhRcSLs7XUCTgz7+qNMWlr8UPhqBdoTtfrucUgNqx5%0APHDLsrpAVdGzxT3WvxnMz1/r8ww3GL2a6hae1R//8KMDbafYKtmJN6/hbAs9B2c8/nBjzPpUBtsJ%0Abd27kZeW5t/5Hn3rfO/ro0U4mmbYv+orflUFjdDwdkHB4mnFwaq5+Xm9Yx7PPogEbGfOTvFNthO0%0AluzlxgJgNHAAzm43m0RkjjGmPmXJdpRR90LZ7HjP/AX3+e8qKJDG43b29QDkHV9ff/Dx9c7/3nqR%0AulkF+R9PKw5Wf5Cf36dGZB9ErFyqmrhhaWQp/l5+hl03bJuvxZvirHpwFVsqtuAt8jLk8iEE+gWo%0AXVLL6r+vRnzCkIlDyBuQR0ttCyvuXUHopyHEI6mM3JjKJ++sZOfSXwcgIsXAD4FHgQGkt9VtPUSo%0AuqAPsQ3/CPyhfF9ZcbRI8v8dC4wp/G5d/aHfrXP+ANSIVL8RLCh/Phis/TA/r3+9yEhEkl5qvSsq%0AX6kkb1Ae8fr4Dl+rmlmFt9DLyFtHsumdTaz911qGXjGUypcqCV0fonFDIxvf2MjA8wayfvp6+p3S%0AL9XFDs4wdsZI9pL+Kpz9uUYDFTideLNSF2tHFWWl8VA4uhnnDG7VCUI8fqNv6uwfe6cf5BGO2dXn%0AKzKm+NSausNOrXF2O4t5PJv+W1hQHi0KNizMCwxsENkLkW6vpKaNTVR/VE2/U/tR+XLlDl+v/rCa%0A3c5wDhQuObyENVPWYIwBL8Qb48Qb44hXaFjfQNPGJor2TctM7ewreJzhsD8BHxhjbHacVaEF3ymH%0ASfmnjwZujRdLfcp2KCqJx3ueXVN7xNk1tQBUejwbXioqXPJiMNi0KC8wpEmkW84wWPPEGgb8YAAt%0A9TtfztFU1YS/t3PnJ17BU+ChpaaFfqX9WPXAKjwBD4MvG8zaJ9fS/8z+3REpGVvS9ULJSPaS/usz%0A5kTkMmPMA6mL1K4qnBV7qgPF1MYeCdz+0WFSPlYk+Z2NukOfeLzvBZtr+l6wuQaAtV7v2heKCr94%0AKRhsWRLwD2sW6fT88s3zN+Pr4aMgVEDNpzWdemzBsAL2/M2eANSW1+Lr6fzar7h3BeIVBp47EF9J%0AyrokMup8ua78lBMBWwW/0dLrZpWJ3mlv/8w3dYRXTEacsDugpWXAJbHqAZfEqgFY6fOtihYVVrwS%0ALJSlfv/wuEiH+xTWLalj84ebqf6oGtNkaNnSwsr7VzLkx98sRvP38tO00WnlTYshXh/HW+T9+uvG%0AGNZPW8+Qy4ewZsoaBpwzgKYNTVT+t5L+Z6esxf8yVU/cFV0peJudZqstvnbG21eWL308cEt1b6k+%0A2naW9gxpbh48cdPmwRM3bQZgqd+3/Pmi4IpXCwu9y/2+EcbZf2EbA74/gAHfHwBAzac1VL5UuU2x%0AAxSPKqZqdhWFexUSey9GcN/gNl0Jm97aRPFBxfiKfMQb485vsjj39ymU9O9sYq7L+8CXxphTOvMi%0AIhICnjfGHNDe93Wl4E/twmO6S0b9tcwUBTTU3eP/83sneOYfLZJ9w5d7NjUPu7YqNuzaKuc0s08D%0A/qXTi4JfvlFYGPjS593biPRq67Hr/r2Ogj0K6HFID3od24tVD6zisxs/wxt0huW2ijfE2TR7E6Eb%0AQgD0Pakvy+9cjnidoboU6szv7LU4e0WmbFFaUjPtRKQ/cAswyBgzXkT2A44yxjycqmA7EwpHrwLu%0ATudrZrrzvK/N/b3v0d19Et/ddpZUMGAW5AWWTC8KrplRWFCw1uvdG5Fs6rg9ceGEha939E0iMhj4%0AOzAJuB64GfiFMeZMETkdeBKnw9oDLDLGDBeR0TgjZgCvAOO7q4V/DGfs/VeJjz8DpgJpLXi0hf9a%0ASNas/Gdg0tqBsnGM7SypJCAHNzSOPLihceRNlVW0QMu8/LxF04qCX80uKAhu8Hr2RSRoO2c7KpL8%0AvruAG4GtK1Q/xNksFpwh8Y9xprb7gHcTn38UuMoYM1NEbkvmRZIt+L7GmKdE5BcAxphmEbGx1dUK%0AC6+ZUfw0N97uv2/OaZ45Y0Qya/ukdPCC9/AtDfsdvqUBgCZoercgf+H0omDlnIL8nlXONOBMWQfQ%0ASBIFLyKnAOuNMR+IyPHwdY0tFZF9cY5q/xPO4S9eYJaI9AR6GmNmJp7mH8D4jl4r2YKvFZE+JI6I%0AFpEjcabYptsnOAtoMmoFUrp8z/PuvLv89/QKSPNOp8S6kR/8Y+u3HDi23hnuboSG2YUF86cXBWNz%0A8/N6bfZ49kXEVr/G0oUTFibTI3gMcFpiV6l8oIeITAFm4hRxE85+ko/hFPzPuhoo2Xv40cBfcObS%0Afwz0A842xizo6gt3VSgcnU8GHtKXSgOpXPt4YNKy4Z61R9nOkm3qRGpnFBYsfr4oWP1Bfl6/Wmcd%0AgLfjR3aLaQsnLDy9Mw9ItPA3GGNOSbw/GZhsjLlJRN4B+gPDjTFGRBYAVxhjZovIH4HSbrmHT1xq%0AHAfsjTOYUW6MsTVl8D1cUvAe4i03+x6bfaH31UNF0GLvgkJjguNr60aPr3WmAVeLbH4tWFgeLQrW%0AfZQXSPU6gM928fHv4hT41sv2BcAA800rfTHwiIgYnE67DiXbwi/A6SWcaoxZ2tnU3SkUjv4Y+JvN%0ADOkwzrNg4f3+PwUKpXFv21ly2SaPp+qVYGF5tKiw8ZNAYFCDx7NXNz79xQsnLHysG59vlyV7L3wq%0A8APgKRGJ4/TQP2WMsdGJ9r6F10yb3sQqJwf+uGh/qRjbmRVtqmt6xuO9zqmuOfKcame67gav56sX%0Ag8HPXwwWNi3OCwxtcia0dNVb3ZGxOyW9483XDxAZAfwauMAYk657oa+FwlE/zlLZHNsQw5if+Z6a%0Afbn3uQM8QpsTTVR6rfF617xQFPzipWChWRLwh1qc8fJkrF84YWHaVugkqzNbXA3DaeV/gHP6zFRj%0AzB0pzNamUDg6F2dMMiccIkvK/x4oa+oh9e12uCj7Vvh8q54vCla8EiyQZe2vA/jPwgkLz0xruCQk%0Aux7+XZwdZ/4FfN8Y80VKU3XsfXKg4Iuo2/xw4Pb5Y2TxMSKk/WpJdd7Q5ubBV2yKDb5ikzMq/bnf%0Av2x6UeHK14KF/hU+316t1gHMtpeybcnew19kjClPaZLOyfr7+Mu8z7/9c98/98qUFW2qa/Zqatrj%0AuqrYHtcl1gF8Egh8Pr2o8MvFgcAMy9F2qqOTZy40xkwBSkWkdPuvG2P+lLJk7cvIv57J2EdWfPF4%0AYFKsT4avaFNds39j4177b2zsC8y3nWVnOhp/3DpHubiNNysqyko/AxbZev2uKKCh7iH/7TNeDIQH%0A95HqQ2znUSn1BpGYzVOW29TRUVP3J9bobjbG3JmmTMl6GviN7RDJOMf7xtxbfA8P8klcp8S6Q1KT%0AYGzocIaRMaYFOC8NWTrrGdsBOjJM1q56K+/qubf6Hxzjk3iywzkqu8WB52yHaEuyM+3uxOmlnwrU%0Abv28MWZe6qJ1LBSOlgMjbWbYGT/Njbf6759zhuetMSIU2M6j0momkVjGXskl20u/dV3uzYl/BWfl%0A3Le6PVHnPAP8wnKGbZzseXfen/339MrTFW1u9ZTtAO3pqJf++sS7z7PjIRCdm6KXGk+TIQU/gI3r%0ApgQmLd3Ls0Z7390rjvM7mbE6uoff2hs/Grgc5wTZQcCPgUNTG61jFWWl8wCrk4A8xFsivsdmzsm7%0AqkCL3fVmEomtsx2iPR310t8MICIzgUONMdWJjyNANOXpkvMMu7AhwK44xvPxxw/67/AXSoNOnlGQ%0A4ZfzkPw9fH+2PRSvMfG5TPAv0lzwPamumhwo+/hAWaYr2tRWtcATtkN0JNmF/5OBuSISSbTu7+Js%0At2NdRVnpe8AH6Xk1Y67z/WvWvLyJ8YM8y8ZpsatWphCJ2dj2rVOS3fFmkoi8iLN7JsDFxpgPUxer%0A027D2aAjZUbJ5+WTA2WNPaRuXMffrVzoHtsBkpH0ZpCJMXer4+7teBqn8254dz9xkPrqh/x3fHik%0AZ5GuaFNtmUUkttB2iGSk9ZDBVKkoK23B2ca3W13qfWHOgrwf1R7lXXSsFrtqx19tB0hWLm33/AgQ%0AAfru6hONlJXLnghMquorm3XjSNWRL4H/2A6RrJxo4QEqykrr2cW/tPk01N/vv2PGy4Gf795XNluf%0AZ6CyQhmRmK0dnDstZwo+4a9AXVceeLZ3xtyFeT/acJL3g+NECHRzLpWbVgIP2g7RGZ3exDLThcLR%0AvwJXJvv9Q2XdqicCk1YPlg05fUabSonLicSyasv0XGvhAe7A2WSzXT6am+7w3zdjRuC63lrsqguW%0Ak/7DVHdZzhV8RVnpMjq4zPqu570PP8m7dMVZ3lnHiVCYpmgqt/xfNt27b5VLvfSt3YSznfY2+7v3%0AZ+P6KYE/fD7C86UuclG74lMyZKZpZ+VcCw9QUVZaCfx268ce4i2/8U2e8U7eVXla7KobXEkk1mw7%0ARFfkagsPcC9w2dGej+Uh/x3eQmnQDSlUd3iSSOwN2yG6Kud66VubetNpY8/xzpghkptXMirtqoF9%0AiMRW2w7SVTld8ABESh4DJtiOoXLC9URimbZ7c6e4oeW7Aai0HUJlvYXA3bZD7Krcb+EBIiVn42yU%0A4Wpbmg3HPlpLQws0x+HsfX3cfEI+4x6tpbrB+T1YX2sYs7uXZ8/ddrRy+aY4/zO1jriBpjhcPSbA%0AxMMCNDQbTn+yjlWbDVccHuCKw51JipdNr2fiYQEOHZgTa44agCOIxD6yHWRXuaPgASIljwAX245h%0AkzGG2iYoCghNLYaxj9by55PzOXLwN323Zz1Vx+l7+7jo4G1nFze2GIyBPJ9Q02g44N4a3r40yPur%0AW1iwLs4vxwU45pE65lwa5KO1Lfzl3UYePj1nduj+KZGYrWPVupUbLum3ugb43HYIm0SEooCzSU9T%0AHJpatt2GeHOD4fVlzZyxj3+Hxwa8Qp7P+e6GZkM80U74PVDXZGhqga1tx6/faOD338pL5Y+STq8C%0AWX3f3pp7Cj4SqwHOB7JudlR3aokbRv2tht1uq+Y7w30c0ap1f3ZxEyfu4aNH3s537loZi3PQfTUM%0AubOGnx+Tx6BiD9/Z00fFpjhHPlzLNUcEmFbexKEDPQwqzolfrY3ABCKxnLkMds8l/VaRkl8At9iO%0AYdumLYb/mVrH3ePzOWA35z57/OO1/OiQAGftt2ML39rq6jhnPFnH9PMK6V/0TWE3tRhOmlLHc+cW%0A8ts3G1gRi3PRwX5O27v958tgZxGJ/dt2iO6UE3+GO+mPwEu2Q9jWM184IeTjpc+dCWMb6uLM/TJO%0A6ciO52INKvZwwG5eZq3Ydo3Sve81ctHBft5Z1UJJnjD17ALumNPYxrNkvDtyrdjBjQUficWBc3Hm%0AQ7vKV7VxNm1xrujqmwz//aKZffo6vwJPL2rmlJE+8n07v5xftTlOfZPz2Kp6w+wVLezd55tfn6p6%0Aw/NLmrnoYD91TQaPgAhfPybLvAjcaDtEKuTy1Nq2RWIxIiWn4my33cd2nHRZU2OY8GwdLXGIGzhn%0Afz+njHQut5/8uInw2G072t5f3cLf3m/kodMK+PSrOD99ZQsiTufcDUcHOLD/N0Nuv5vRwK/G5eER%0A4aS9fNzzXh0H3tfExNFZt5fIYuC8RMOQc9x3D99apOR4nLO8s/YmU3WrKmAMkVjOjua475K+tUjs%0ATeAq2zFURmgGzsnlYge3FzxAJPYAMMl2DGVVHLiISOxV20FSTQseIBK7iRTsa6+yggEuIxL7p+0g%0A6aAFv1Uk9lPgPtsxVNpdSySWdXvTdZUW/LauBB61HUKlzS+IxLJ+BVxnaMG35kyh/BHwuO0oKuUi%0ARGJltkOkmxb89pzx14uAv9iOolLCAD8hErvZdhAb3D0O35FIyY1AGeg58DmiGbiUSGyy7SC2aMF3%0AJFJyIc5BlTo5J7tVA2cTib1iO4hNWvDJiJR8F3gGKLIdRXXJaqCUSGy+7SC26T18MpxW4Qig3HYU%0A1WlvAodqsTu04JMViS0CDkf3xssmtwHfJhJbZztIptBL+q6IlFwH3IpbVxtmvs3Axbm4nn1XacF3%0AVaRkLPAksLvtKGobC4DvE4l9ZjtIJtJL+q6KxGYDBwJ/tx1FAc6Q2++Bw7TY26YtfHeIlHwPuB8Y%0AbDuKSy0Afkgk9qHtIJlOW/juEIm9ABwAuGYRRoZo3aprsSdBW/juFin5NnAXsL/tKDnuDeC6XDgN%0AJp204FMhUuLFWYTzO2A3y2lyzRLgBiKxabaDZCMt+FSKlBQDvwR+AuRbTpPtqnD+gN5DJObqw0R2%0AhRZ8OkRKhgER4EJ07L6zNgP3ArcRiW20HSbbacGnU6QkhLPf+SVAzhy+liLrcfpC7iUSi9kOkyu0%0A4G2IlPTH2S33cly0L36SluNMiX2ESKzedphcowVvU6SkEPgBTos/1nIam5qBKM6w5otEYs2W8+Qs%0ALfhMESkZgXN+/UW4Z7puOc5eA5OJxNbaDuMGWvCZxhnS+w5wDlBK7g3rfQFMA54mEnvLdhi30YLP%0AZJESDzAGOAU4FTjIbqAuiQNzcYp8GpHYJ5bzuJoWfDaJlAwFTgSOBI7Cmc2XadOjG4EPgTnA28AM%0AIrH1diOprbTgs5kzsWcMTvGPBkYCe5K+Ib8GnPvwT4F5OAX+PpHYljS9vuokLfhc49wGDAFG8M0f%0AgH44w3+9E299gJ6At41naV6T3N0AAAF+SURBVAE2ApWJtw2t/q0APgeWAsuJxFpS9JOoFNCCd6tI%0AieDM+mv9C+C8r0Wcs7TglXKRTOvwUUqlkBa8Ui6iBa+sEpHjReR52zncQgtedStx6O9VhtL/MWqX%0AiUhIRMpFZDLwMYm9/UTkWhH5IvH+cBF5K/H+ySKyWETmAWdaC+5CWvCqu4zA2ajiRJwNPQHGAZUi%0Asnvi/Zkikg88iDNVeDQwwEJW19KCV91luTHmHWPMWqBIRIpxJgA9ARyLU/CzgH2AZcaYJcYZE55i%0ALbELacGr7lLb6v23cZb6luMU+Tic6b+6Os4yLXiVCrOAG4CZOAtpTgAajDExYDEQEpE9E997np2I%0A7qQbKqpUmIVzOT/TGNMiIitxCh1jzBYRuQyIikhd4nuL7UV1F51aq5SL6CW9Ui6iBa+Ui2jBK+Ui%0AWvBKuYgWvFIuogWvlItowSvlIlrwSrmIFrxSLqIFr5SLaMEr5SJa8Eq5iBa8Ui6iBa+Ui2jBK+Ui%0AWvBKucj/B7BPRCFEQC72AAAAAElFTkSuQmCC%0A)

Tambien podemos realizar filtros a nuestro dataset. Por ejemplo, vamos a
obtener los carros que el tamaño del motor (engine-size) sea mayor a 130

In [16]:

    df[ df['engine-size'] > 130 ]

Out[16]:

symboling

normalized-losses

make

aspiration

num-of-doors

body-style

drive-wheels

engine-location

wheel-base

length

width

height

curb-weight

engine-type

num-of-cylinders

engine-size

fuel-system

bore

stroke

compression-ratio

horsepower

peak-rpm

city-mpg

highway-mpg

price

city-L/100km

horsepower-binned

diesel

gas

2

1

122

alfa-romero

std

two

hatchback

rwd

front

94.5

0.822681

0.909722

52.4

2823

ohcv

six

152

mpfi

2.68

3.47

9.0

154.0

5000.0

19

26

16500.0

12.368421

Medium

0

1

4

2

164

audi

std

four

sedan

4wd

front

99.4

0.848630

0.922222

54.3

2824

ohc

five

136

mpfi

3.19

3.40

8.0

115.0

5500.0

18

22

17450.0

13.055556

Medium

0

1

5

2

122

audi

std

two

sedan

fwd

front

99.8

0.851994

0.920833

53.1

2507

ohc

five

136

mpfi

3.19

3.40

8.5

110.0

5500.0

19

25

15250.0

12.368421

Medium

0

1

6

1

158

audi

std

four

sedan

fwd

front

105.8

0.925997

0.991667

55.7

2844

ohc

five

136

mpfi

3.19

3.40

8.5

110.0

5500.0

19

25

17710.0

12.368421

Medium

0

1

7

1

122

audi

std

four

wagon

fwd

front

105.8

0.925997

0.991667

55.7

2954

ohc

five

136

mpfi

3.19

3.40

8.5

110.0

5500.0

19

25

18920.0

12.368421

Medium

0

1

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

196

-1

95

volvo

std

four

sedan

rwd

front

109.1

0.907256

0.956944

55.5

2952

ohc

four

141

mpfi

3.78

3.15

9.5

114.0

5400.0

23

28

16845.0

10.217391

Medium

0

1

197

-1

95

volvo

turbo

four

sedan

rwd

front

109.1

0.907256

0.955556

55.5

3049

ohc

four

141

mpfi

3.78

3.15

8.7

160.0

5300.0

19

25

19045.0

12.368421

High

0

1

198

-1

95

volvo

std

four

sedan

rwd

front

109.1

0.907256

0.956944

55.5

3012

ohcv

six

173

mpfi

3.58

2.87

8.8

134.0

5500.0

18

23

21485.0

13.055556

Medium

0

1

199

-1

95

volvo

turbo

four

sedan

rwd

front

109.1

0.907256

0.956944

55.5

3217

ohc

six

145

idi

3.01

3.40

23.0

106.0

4800.0

26

27

22470.0

9.038462

Medium

1

0

200

-1

95

volvo

turbo

four

sedan

rwd

front

109.1

0.907256

0.956944

55.5

3062

ohc

four

141

mpfi

3.78

3.15

9.5

114.0

5400.0

19

25

22625.0

12.368421

Medium

0

1

69 rows × 29 columns

Y si queremos guardar ese resultado a otro dataframe, solo es necesario
crear una nueva variable

In [17]:

    new_df = df[ df['engine-size'] > 130 ]
    new_df.head()

Out[17]:

symboling

normalized-losses

make

aspiration

num-of-doors

body-style

drive-wheels

engine-location

wheel-base

length

width

height

curb-weight

engine-type

num-of-cylinders

engine-size

fuel-system

bore

stroke

compression-ratio

horsepower

peak-rpm

city-mpg

highway-mpg

price

city-L/100km

horsepower-binned

diesel

gas

2

1

122

alfa-romero

std

two

hatchback

rwd

front

94.5

0.822681

0.909722

52.4

2823

ohcv

six

152

mpfi

2.68

3.47

9.0

154.0

5000.0

19

26

16500.0

12.368421

Medium

0

1

4

2

164

audi

std

four

sedan

4wd

front

99.4

0.848630

0.922222

54.3

2824

ohc

five

136

mpfi

3.19

3.40

8.0

115.0

5500.0

18

22

17450.0

13.055556

Medium

0

1

5

2

122

audi

std

two

sedan

fwd

front

99.8

0.851994

0.920833

53.1

2507

ohc

five

136

mpfi

3.19

3.40

8.5

110.0

5500.0

19

25

15250.0

12.368421

Medium

0

1

6

1

158

audi

std

four

sedan

fwd

front

105.8

0.925997

0.991667

55.7

2844

ohc

five

136

mpfi

3.19

3.40

8.5

110.0

5500.0

19

25

17710.0

12.368421

Medium

0

1

7

1

122

audi

std

four

wagon

fwd

front

105.8

0.925997

0.991667

55.7

2954

ohc

five

136

mpfi

3.19

3.40

8.5

110.0

5500.0

19

25

18920.0

12.368421

Medium

0

1

Box Plots[¶](#Box-Plots) {#Box-Plots}
------------------------

Los box plot representan gráficas en las que se pueden analizar varias
características de un conjunto de datos como:

-   La distribución de los datos.
-   Asimetría.
-   Los puntos aislados.

In [21]:

    plt.figure(figsize=(12, 8))
    sns.boxplot(x="body-style",y="price", data=df)

Out[21]:

    <matplotlib.axes._subplots.AxesSubplot at 0x7fe64de7f748>

![](data:image/png;base64,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%0A)

In [22]:

    plt.figure(figsize=(8, 8))
    sns.boxplot(x="engine-location",y="price", data=df)

Out[22]:

    <matplotlib.axes._subplots.AxesSubplot at 0x7fe64d66dc18>

![](data:image/png;base64,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%0A)

Groupby[¶](#Groupby) {#Groupby}
--------------------

con el método groupby podemos agrupar los datos en diferentes
categorías. Los datos son agrupados con base en una o varias
características y el análisis se realiza sobre los grupos individuales.

Ahora realicemos un nuevo dataframe con las columnas 'drive-wheels',
'body-style' y 'price' y agrupemos por 'drive-wheels' para calcular el
valor medio en cada categoria:

In [24]:

    df_group = df[['drive-wheels','body-style','price']]
    df_group.head()

Out[24]:

drive-wheels

body-style

price

0

rwd

convertible

13495.0

1

rwd

convertible

16500.0

2

rwd

hatchback

16500.0

3

fwd

sedan

13950.0

4

4wd

sedan

17450.0

In [27]:

    # Agrupamiento de los resultados
    df_grupo1 = df_group.groupby(['drive-wheels'], as_index = False).mean().sort_values(by = "price", ascending = False).reset_index(drop = True)
    df_grupo1

Out[27]:

drive-wheels

price

0

rwd

19757.613333

1

4wd

10241.000000

2

fwd

9244.779661

Podemos agrupar de acuerdo a varias variables. Por ejemplo, agrupemos
por 'drive-wheels' y 'body-style'. Este procedimento agrupara el
dataframe por combinaciones unicas de 'drive-wheels' y 'body-style'.
Guardemos el resultado en la variable de prueba 'grupo\_test'

In [28]:

    grupo_test = df_group.groupby(['drive-wheels','body-style'], as_index = False).mean().sort_values(by = "price", ascending = False).reset_index(drop = True)
    grupo_test

Out[28]:

drive-wheels

body-style

price

0

rwd

hardtop

24202.714286

1

rwd

convertible

23949.600000

2

rwd

sedan

21711.833333

3

rwd

wagon

16994.222222

4

rwd

hatchback

14337.777778

5

4wd

sedan

12647.333333

6

fwd

convertible

11595.000000

7

fwd

wagon

9997.333333

8

fwd

sedan

9811.800000

9

4wd

wagon

9095.750000

10

fwd

hatchback

8396.387755

11

fwd

hardtop

8249.000000

12

4wd

hatchback

7603.000000

In [29]:

    # tambien podemos cambiar el metodo en el que se ordenan
    df_group.groupby(['drive-wheels','body-style'], as_index = False).mean().sort_values(by = "drive-wheels", ascending = False).reset_index(drop = True)

Out[29]:

drive-wheels

body-style

price

0

rwd

convertible

23949.600000

1

rwd

hardtop

24202.714286

2

rwd

hatchback

14337.777778

3

rwd

sedan

21711.833333

4

rwd

wagon

16994.222222

5

fwd

convertible

11595.000000

6

fwd

hardtop

8249.000000

7

fwd

hatchback

8396.387755

8

fwd

sedan

9811.800000

9

fwd

wagon

9997.333333

10

4wd

hatchback

7603.000000

11

4wd

sedan

12647.333333

12

4wd

wagon

9095.750000

Correlación[¶](#Correlación) {#Correlación}
----------------------------

La correlación es una medida de la relación entre variables que se mide
en una escala de -1 a 1. Cuanto más cercano sea el valor de correlación
a -1 o 1, más fuerte será la relación, y mientras más cerca de 0, más
débil será la relación. Mide cómo el cambio en una variable está
asociado con el cambio en otra variable.

Para calcular el coeficiente de correlación podemos utilizar el método
`corr()` de Pandas

In [30]:

    df.corr()

Out[30]:

symboling

normalized-losses

wheel-base

length

width

height

curb-weight

engine-size

bore

stroke

compression-ratio

horsepower

peak-rpm

city-mpg

highway-mpg

price

city-L/100km

diesel

gas

symboling

1.000000

0.466264

-0.535987

-0.365404

-0.242423

-0.550160

-0.233118

-0.110581

-0.140019

-0.008245

-0.182196

0.075819

0.279740

-0.035527

0.036233

-0.082391

0.066171

-0.196735

0.196735

normalized-losses

0.466264

1.000000

-0.056661

0.019424

0.086802

-0.373737

0.099404

0.112360

-0.029862

0.055563

-0.114713

0.217299

0.239543

-0.225016

-0.181877

0.133999

0.238567

-0.101546

0.101546

wheel-base

-0.535987

-0.056661

1.000000

0.876024

0.814507

0.590742

0.782097

0.572027

0.493244

0.158502

0.250313

0.371147

-0.360305

-0.470606

-0.543304

0.584642

0.476153

0.307237

-0.307237

length

-0.365404

0.019424

0.876024

1.000000

0.857170

0.492063

0.880665

0.685025

0.608971

0.124139

0.159733

0.579821

-0.285970

-0.665192

-0.698142

0.690628

0.657373

0.211187

-0.211187

width

-0.242423

0.086802

0.814507

0.857170

1.000000

0.306002

0.866201

0.729436

0.544885

0.188829

0.189867

0.615077

-0.245800

-0.633531

-0.680635

0.751265

0.673363

0.244356

-0.244356

height

-0.550160

-0.373737

0.590742

0.492063

0.306002

1.000000

0.307581

0.074694

0.180449

-0.062704

0.259737

-0.087027

-0.309974

-0.049800

-0.104812

0.135486

0.003811

0.281578

-0.281578

curb-weight

-0.233118

0.099404

0.782097

0.880665

0.866201

0.307581

1.000000

0.849072

0.644060

0.167562

0.156433

0.757976

-0.279361

-0.749543

-0.794889

0.834415

0.785353

0.221046

-0.221046

engine-size

-0.110581

0.112360

0.572027

0.685025

0.729436

0.074694

0.849072

1.000000

0.572609

0.209523

0.028889

0.822676

-0.256733

-0.650546

-0.679571

0.872335

0.745059

0.070779

-0.070779

bore

-0.140019

-0.029862

0.493244

0.608971

0.544885

0.180449

0.644060

0.572609

1.000000

-0.055390

0.001263

0.566936

-0.267392

-0.582027

-0.591309

0.543155

0.554610

0.054458

-0.054458

stroke

-0.008245

0.055563

0.158502

0.124139

0.188829

-0.062704

0.167562

0.209523

-0.055390

1.000000

0.187923

0.098462

-0.065713

-0.034696

-0.035201

0.082310

0.037300

0.241303

-0.241303

compression-ratio

-0.182196

-0.114713

0.250313

0.159733

0.189867

0.259737

0.156433

0.028889

0.001263

0.187923

1.000000

-0.214514

-0.435780

0.331425

0.268465

0.071107

-0.299372

0.985231

-0.985231

horsepower

0.075819

0.217299

0.371147

0.579821

0.615077

-0.087027

0.757976

0.822676

0.566936

0.098462

-0.214514

1.000000

0.107885

-0.822214

-0.804575

0.809575

0.889488

-0.169053

0.169053

peak-rpm

0.279740

0.239543

-0.360305

-0.285970

-0.245800

-0.309974

-0.279361

-0.256733

-0.267392

-0.065713

-0.435780

0.107885

1.000000

-0.115413

-0.058598

-0.101616

0.115830

-0.475812

0.475812

city-mpg

-0.035527

-0.225016

-0.470606

-0.665192

-0.633531

-0.049800

-0.749543

-0.650546

-0.582027

-0.034696

0.331425

-0.822214

-0.115413

1.000000

0.972044

-0.686571

-0.949713

0.265676

-0.265676

highway-mpg

0.036233

-0.181877

-0.543304

-0.698142

-0.680635

-0.104812

-0.794889

-0.679571

-0.591309

-0.035201

0.268465

-0.804575

-0.058598

0.972044

1.000000

-0.704692

-0.930028

0.198690

-0.198690

price

-0.082391

0.133999

0.584642

0.690628

0.751265

0.135486

0.834415

0.872335

0.543155

0.082310

0.071107

0.809575

-0.101616

-0.686571

-0.704692

1.000000

0.789898

0.110326

-0.110326

city-L/100km

0.066171

0.238567

0.476153

0.657373

0.673363

0.003811

0.785353

0.745059

0.554610

0.037300

-0.299372

0.889488

0.115830

-0.949713

-0.930028

0.789898

1.000000

-0.241282

0.241282

diesel

-0.196735

-0.101546

0.307237

0.211187

0.244356

0.281578

0.221046

0.070779

0.054458

0.241303

0.985231

-0.169053

-0.475812

0.265676

0.198690

0.110326

-0.241282

1.000000

-1.000000

gas

0.196735

0.101546

-0.307237

-0.211187

-0.244356

-0.281578

-0.221046

-0.070779

-0.054458

-0.241303

-0.985231

0.169053

0.475812

-0.265676

-0.198690

-0.110326

0.241282

-1.000000

1.000000

In [31]:

    df.corr()['price']

Out[31]:

    symboling           -0.082391
    normalized-losses    0.133999
    wheel-base           0.584642
    length               0.690628
    width                0.751265
    height               0.135486
    curb-weight          0.834415
    engine-size          0.872335
    bore                 0.543155
    stroke               0.082310
    compression-ratio    0.071107
    horsepower           0.809575
    peak-rpm            -0.101616
    city-mpg            -0.686571
    highway-mpg         -0.704692
    price                1.000000
    city-L/100km         0.789898
    diesel               0.110326
    gas                 -0.110326
    Name: price, dtype: float64

Vemos que el precio del automóvil tiende a subir a medida que, por
ejemplo, aumenta el tamaño del motor (engine-size), el ancho (width) y
largo (length) del vehículo; no así de su altura (heigth) o del tipo de
combustible que utiliza

Otra forma de verificar la correlación entre los atributos es usar el
método `scatter_matrix`, que dibuja cada atributo numérico contra
cualquier otro atributo numérico. como tenemos tantas columnas solo
vamos a graficar algunas.

In [32]:

    from pandas.plotting import scatter_matrix

    attributes = ["engine-size","curb-weight","horsepower","bore"]
    scatter_matrix(df[attributes], figsize=(15, 10))

Out[32]:

    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d4e6048>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d4bdfd0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d4772b0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d427518>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d3dd780>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d38e9e8>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d3c6c50>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d379e80>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d379ef0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d2ee3c8>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d2a3630>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d255898>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d288b00>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d23dd68>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d1f1fd0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fe64d1b1278>]],
          dtype=object)

![](data:image/png;base64,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%0AQmCC%0A)

La diagonal principal estaría llena de líneas rectas si Pandas dibujara
cada variable contra sí misma, lo que no sería muy útil. En su lugar,
Pandas muestra un histograma de cada atributo.

Por ultimo, la librería `seaborn` nos permite realizar gráficos como el
anterior o, por ejemplo, en un mapa de calor, mediante las funciones
`pairplot()` y `heatmap()`, respectivamente.

In [47]:

    # podemos poner variable categoricas con el hue

    sns.pairplot(df, hue = "drive-wheels", vars = ["engine-size","curb-weight","horsepower","bore"],height=2.5, aspect=0.9) 

Out[47]:

    <seaborn.axisgrid.PairGrid at 0x7fe6450df780>

![](data:image/png;base64,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%0A)
