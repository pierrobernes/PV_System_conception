## 1. Description de l'installation

Le client projette une consommation de 6000 Kwh.

Les surfaces de toiture exploitables sont les suivantes :     

| Surface | Inclinaison (°)| Orientation | Repartition (%) |
|---------|---------------|-------------|---------------|
| 1       | 30          | Ouest   | 50.0        |
| 2       | 30          | Est   | 50.0        |


## 2. Estimation de la puissance crete nécessaire

L'estimation de la puissance crete nécessaire est réalisée sur base de la consommation annuelle,     une production forfaitaire de 1000Kwh/Kwc de panneaux et un facteur correctif $F_c$ fonction de l'inclinaison et de l'orientation.     <br>    Afin de tenir compte de toitures d'orientation différentes, un facteur de répartition $F_r$ pondère le calcul par orientation    

$$ Puissance\ crete = \frac{Consommation\ annuelle * F_r}{1000 * F_c} $$

### 2.1 Calcul

#### Toiture 1

La surface de toiture a les caractéristiques suivantes :  <li> Inclinaison 30°, <li> Orientation Ouest, <li> Répartition : 50.0% de la production

Détermination du facteur de correction $F_c$ en fonction de l'orientation et l'inclinaison

$$F_c = 0.85 + (30-25) * \frac{ 0.82-0.85 }{35-25} = 0.835$$

Estimation de la puissance crete nécessaire

$$ Puissance\ crete = \frac{ 6000* 0.5 } { 1000 * 0.835} = 3.59 (Kwc)$$

#### Toiture 2

La surface de toiture a les caractéristiques suivantes :  <li> Inclinaison 30°, <li> Orientation Est, <li> Répartition : 50.0% de la production

Détermination du facteur de correction $F_c$ en fonction de l'orientation et l'inclinaison

$$F_c = 0.85 + (30-25) * \frac{ 0.83-0.85 }{35-25} = 0.84$$

Estimation de la puissance crete nécessaire

$$ Puissance\ crete = \frac{ 6000* 0.5 } { 1000 * 0.84} = 3.57 (Kwc)$$

<br>

**La puissance crete totale requise est de 7.16 Kwc**

## 2.2 Détermination du nombre de panneaux nécessaires

Les panneaux utilisés sont de marque **Hyundai** et série **HiT-H455LE-FB(ZB)**.

Leur puissance crete maximale est de 455 W.  Le nombre de panneaux peut donc être calculé comme suit : 

$$ Puissance\ crete = \frac{7160.0\ (W)}{455\ (W)} = 16\ (arrondi\ superieur)$$

<br>

**Le nombre de panneaux nécessaires est de 16**; ce qui permettra de délivrer une puissance crete cumulée de **7.28 Kwc.**

## 3. Analyse de compatibilité avec le matériel utilisé

### 3.1 Description du matériel

#### 3.1.1 Panneaux

Les panneaux utilisés sont de marque **Hyundai** et série **HiT-H455LE-FB(ZB)**. Leurs caractéristiques sont reprises dans la table ci-dessous : 

| Caractéristique | Valeur STC | Valeur NOCT |
|---|---|---| 
| V<sub>oc</sub> (V) | 36.82 | 35.14 |
| I<sub>sc</sub> (A) | 15.64 | 12.5 |
| V<sub>mpp</sub> (V) | 30.94 | 29.55 |
| I<sub>mpp</sub> (A) | 14.71 | 11.76 |


Coefficient de température V<sub>oc</sub>: **-0.22** %/°C

#### 3.1.2 Onduleur

L'onduleur utilisé est de marque **Huawei** et de série **Sun2000-4KTL-M1 (Haute intensité)**. Ses caractéristiques sont reprises dans la table ci-dessous : 

| Caractéristique                     | Valeur              |
|-------------------------------------|---------------------|
| Puissance PV Max (W)                | 6000                 |
| Tension d'entrée maximum (V)        | 1100                 |
| Plage de tension de fonctionnement - Min (V) | 140                  |
| Plage de tension de fonctionnement - Max (V) | 980                  |
| Tension minimum de démarrage (V)    | 200                  |
| Tension nominale de fonctionnement (V) | 600                  |
| Courant maximum par MPPT au MPP(A)  | 13.5                 |
| Courant maximum par MPPT en court-circuit(A) | 13.5                 |
| Type de sortie AC                   | Tri                  |
| Courant de sortie maximum (A)       | 16.7                 |
| Nombre de MPPT                      | 2                    |


### 3.2 Calculs

#### 3.2.1 Compatibilité en tension

Les tensions dans les conditions de températures au niveau de la cellule les plus défavorables pour l'onduleur sont considérées :<li> par temps froid (cellule PV à -10°C) - la tension augmente et pourrait induire des tensions trop importantes sur le string<li> par temps chaud (cellule PV à 70°C) - la tension diminue et la limite basse de démarrage de l'onduleur pourrait ne pas être atteinte

<br>

En effet, les tensions renseignées au niveau de la norme STC le sont pour une température de 25°C.

Le coefficient de variation de la tension à vide $V_oc$ appelé ci-après $C_t$ est utilisé dans les formules ci-dessous pour déterminer les tensions à vide au niveau de température de cellule souhaité: 

$$V_{oc(temp°C)} = V_oc - (V_oc*C_t*(25-temp))$$

Par température de cellule de -10°C, le $V_{oc}$ devient : 

$$V_{oc(-10°C)} = 36.82 - (36.82*-0.22*(25--10)) = 39.66\ (V)$$

<br>

A cette température, le $V_{mpp}$ devient :  

$$V_{mpp(-10°C)} = 30.94 - (36.82*-0.22*(25--10)) = 33.78\ (V)$$

<br>

Tandis que par température de cellule de 70°C, le $V_{oc}$ devient : 

$$V_{oc(70°C)} = 36.82 - (36.82*-0.22*(25-70)) = 33.17\ (V)$$

<br>

Grâce à ces valeurs, on peut déterminer le nombre maximum de panneau par string :

$$\frac{DC_{max\ onduleur\ a\ vide}}{V_{oc(-10°C)}} = \frac{1100\ (V)} {39.66\ (V)} = 27.74 \Rightarrow Max.\ 27\ Panneaux\ par\ string$$

<br>

**Attention** cependant car la tension max. admissible à vide de l'onduleur (1100 V) est supérieure à la tension admissible sur toiture résidentielle (750 V).

Le nombre de panneaux maximum à vide doit donc être revu sur base de cette tension : 

$$\frac{Tension\ Max\ sur\ toiture}{V_{oc(-10°C)}} = \frac{750\ (V)} {39.66\ (V)} = 18.91 \Rightarrow Max.\ 18\ Panneaux\ par\ string$$

<br>

Pour garantir le démarrage de l'onduleur par temps chaud, le nombre minimum de panneaux est de :

$$\frac{DC_{min\ démarrage\ onduleur}}{V_{oc(70°C)}} = \frac{140\ (V)} {33.17\ (V)} = 4.22 \Rightarrow Min.\ 5\ Panneaux\ par\ string$$

<br>

En fonctionnement par temps froid, le nombre de panneaux par string ne pourra pas dépasser :

$$\frac{Tension\ Max\ sur\ toiture}{V_{mpp(-10°C)}} = \frac{750\ (V)} {33.78\ (V)} = 22.2 \Rightarrow Max.\ 22\ Panneaux\ par\ string$$

##### Conclusions

| Description                          | Valeur |
|--------------------------------------|--------|
| Min. panneaux / string  | 5      |
| Max. panneaux / string  | 18     |

La puissance DC maximum recommandée (sans optimiseur) est donnée par le fabricant à 6000.  Mettre 18 panneaux produirait 8190 W.  Idéalement il faudrait se limiter à 13 - 14 panneaux tous strings confondus.

8190

#### 3.2.2 Compatibilité en courant

Les panneaux dans les strings étant tous raccordés en série, le courant maximum DC produit sera de 

| Courant panneaux                        | Norme | Test | Compatibilité|
|--------------------------------------|--------|----|----|
| $$I_{sc}$$  | NOCT | 12.5 A <= 13.5 A ? | OK|
| $$I_{mpp}$$ | NOCT| 11.76 A <= 13.5 A ?| OK|

#### 3.3 Optimisation

L'onduleur fonctionnera de manière optimum avec une tension d'entrée de 600.

Dans les conditions NOCT, l'onduleur fournira une tension $V_{mpp}$ de 29.55; le nombre optimum de panneaux par string est dès lors de :

$$Optimum = \frac{600 (V)}{29.55 (V)} = 20.0\ Panneaux$$

Ce nombre étant supérieur au nombre maximum de panneaux par string calculé précédemment, nous ne retiendrons pas cette valeur **(maximum 18 panneaux)**.

