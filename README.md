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

## 2.Análisi del clicle de vida i el problema de la pèrdua d’estat

        import androidx.appcompat.app.AppCompatActivity
        import android.os.Bundle
        import android.widget.Button
        import android.widget.TextView
        
        class MainActivity : AppCompatActivity() {
    
        var comptador=0
    
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(R.layout.activity_main)
    
            // Referencia al TextView
            val textViewContador=findViewById<TextView>(R.id.textViewComptador)
    
            // Inicialitzem el TextView amb el comptador a 0
            textViewContador.setText(comptador.toString())
    
            // Referencia al botón
            val btAdd=findViewById<Button>(R.id.btAdd)
    
            // Asociaciamos una expresióin lambda como
            // respuesta (callback) al evento Clic sobre
            // el botón
                btAdd.setOnClickListener {
                    comptador++
                    textViewContador.setText(comptador.toString())
                }
        }
    }


Pel que fa a la pèrdua d'estat, aquesta versió no maneja l'estat de l'aplicació quan l'activitat es destrueix i es recrea (com en una rotació de pantalla). Això significa que si l'usuari rota l'aparell, el comptador es reiniciarà a zero.

Per manejar la pèrdua d'estat, es pot implementar el mètode onSaveInstanceState per desar l'estat actual del comptador en un Bundle, i onRestoreInstanceState per restaurar aquest estat quan l'activitat es recrea.

En resum, aquesta versió té una funcionalitat senzilla de comptador i mostra com configurar un listener de clic per al botó. No obstant això, no tracta la pèrdua d'estat en canvis de configuració, la qual cosa pot ser millorada mitjançant l'ús de onSaveInstanceState i onRestoreInstanceState per mantenir l'estat del comptador en aquests casos.


## 3. Solució a la pèrdua d’estat

    class MainActivity : AppCompatActivity() {
        var comptador=0
        lateinit var binding: ActivityMainBinding
    
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)  
            binding = ActivityMainBinding.inflate(layoutInflater)
            setContentView(binding.root)
    
            // Referencia al TextView
            binding.textViewComptador.setText(comptador.toString())
    
            // Definim els botons de sumar, restar i reset
            // amb les funcions pertinents
            binding.btAdd.setOnClickListener {
                comptador++
                binding.textViewComptador.setText(comptador.toString())
            }
            
            // BOTONS DE RESTAR I RESET
            
            binding.btMenys.setOnClickListener {
                comptador--
                binding.textViewComptador.setText(comptador.toString())
            }
            binding.btReset.setOnClickListener {
                comptador=0
                binding.textViewComptador.setText(comptador.toString())
            }
        }
    
        override fun onSaveInstanceState(estat: Bundle) {
            super.onSaveInstanceState(estat)
            // Codi per a guardar l'estat
            estat.putInt("compt", comptador)
        }
    
        override fun onRestoreInstanceState(estat: Bundle) {
            super.onRestoreInstanceState(estat)
            // Codi per a guardar l'estat
            comptador=estat.getInt("compt")
            var text1=findViewById<TextView>(R.id.textViewComptador)
            text1.setText(comptador.toString())
    
        }
    }

Amb la millora d'aquest codi, s'implementa una solució per a la pèrdua d'estat en una activitat d'Android quan hi ha canvis de configuració, com la rotació de la pantalla. S'utilitzen els mètodes onSaveInstanceState i onRestoreInstanceState per guardar i restaurar l'estat del comptador.

* **onCreate(savedInstanceState: Bundle?)**
    * Aquest mètode s'executa quan l'activitat es crea. Ací, es configura la interfície d'usuari, es vinculen les vistes a les variables de l'enllaç (binding) i s'estableixen els listeners dels botons per a les operacions de sumar, restar i reset.

* **onSaveInstanceState(estat: Bundle)**
    * Aquest mètode s'executa abans que l'activitat siga destruïda (per exemple, en una rotació de pantalla). S'utilitza per desar l'estat actual del comptador en el Bundle proporcionat com a paràmetre.

* **onRestoreInstanceState(estat: Bundle)**
    * Aquest mètode s'executa quan l'activitat es recrea després d'una rotació de pantalla o altres canvis de configuració. Es fa servir per restaurar l'estat del comptador des del Bundle i actualitzar la interfície d'usuari amb aquest valor.

Amb aquesta implementació, quan hi ha un canvi de configuració, com una rotació de pantalla, l'estat actual del comptador es guarda amb onSaveInstanceState, i quan l'activitat es torna a crear, aquest estat es restaura amb onRestoreInstanceState, evitant així la pèrdua de l'estat del comptador.

## 4. Ampliant la funcionalitat amb decrements i Reset


    binding.btMenys.setOnClickListener {
                    comptador--
                    binding.textViewComptador.setText(comptador.toString())
                }
                binding.btReset.setOnClickListener {
                    comptador=0
                    binding.textViewComptador.setText(comptador.toString())
    }

Hem afegit dues accions més als botons:

* **binding.btMenys.setOnClickListener**
    * Quan es fa clic en el botó "Restar", es decrementa el comptador en -1.
* **binding.btReset.setOnClickListener**
    * Quan es fa clic en el botó "Reset", es reinicia el comptador a 0.

Ara, l'aplicació permet augmentar, disminuir i restablir el comptador mitjançant els botons corresponents.
També hem implementat binding per a poder utilitzar totes les vistes i objectes de forma més senzilla i poder implementar View Binding.

    binding = ActivityMainBinding.inflate(layoutInflater)

## 5. Té alguna implicació crear una nova activitat?

Si afegim una nova activitat al projecte, és important seguir les mateixes bones pràctiques i utilitzar View Binding per accedir a les vistes de la nova activitat. Això ens permetrà mantenir un codi més net i eficient.

Pero si l'afegim manualment, hem de anar en compte perquè açò implica accedir a les vistes del layout mitjançant findViewById, que és menys eficient i pot conduir a errors si s'incorrectament. L'ús de View Binding evita aquestes errades i millora la llegibilitat del codi en proporcionar un accés segur i tipat a les vistes. És recomanable utilitzar View Binding en lloc de findViewById sempre que sigui possible per a evitar aquestes errades i optimitzar l'accés a les vistes

Altres errades són per exemple no afeigr la activitat creada de forma manual al nostre arxiu AndroidManifest, la qual cosa pot provocar errors greus al programa, que la nova activitat creada o funcione perque no a sigut descrita al manifest o problemes de rendiment inclús de colapsament de l'aplicació.
