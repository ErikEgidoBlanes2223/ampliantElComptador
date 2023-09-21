# Ampliant El Comptador

## 1. Anàlisi de l’estructura del projecte 

Es tracta d'un projecte creat en Kotilin desde Android Studio, aquest projecte esta dissenyat per crear un comptador, el qual te  3 botons amb diferents funcionalitats cadascún.
Sumar 1 (+), Restar 1 (-), Resetejar 0.

### Visualització carpetes - Project

L'escructura de carpetes de ***projecte*** es tracta del arbre de subcarpetes del mateix, les quals están estructurades de la següent manera:
* Comptador (Carpeta del projecte)
    <img src="https://github.com/ErikEgidoBlanes2223/ampliantElComptador/assets/126054869/db0bbb2a-67c2-4431-b839-c300367a9556" alt="Texto alternativo" width="200" align="right">
    * .gradle
    * .idea
    * app
    * gradle
* External Libreries
* Scratches and Consoles

Amb aquest tipus de configuració tenim tota l'escructura del projecte, però al hora d'accedir a arxius principals ens fa més complicat d'accedir.
Per això es va desenvolupar la segona opció de visualització de carpetes, aquesta es la de ***Android***.

### Visualització carpetes - Android

L'escructura de carpetes de ***Android*** es tracta del arbre de subcarpetes del mateix, les quals están estructurades d'una forma més amigable i amagant la llarga quantitat de subcarpetes de les que no anem a treballar sobre elles. Aquestes están estucturades de la següent forma:
<img src="https://github.com/ErikEgidoBlanes2223/ampliantElComptador/assets/126054869/1b329efc-0bc3-49ea-9061-0c8d762b6239" alt="Texto alternativo" width="200" align="right">

 
* app
    * manifests
    * java
    * res
    * gradle Scripts

D'aquesta forma se'ns fa mes fàcil accedir als arxius i carpetes principals del programa (AndroidManifest, MainActivity.kt, Res, Gradle ).
Així el que podem fer es interactuar de manera més comode.
