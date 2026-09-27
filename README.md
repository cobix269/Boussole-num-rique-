# NORHALO

NORHALO est un projet de boussole numérique réalisé à l’aide d’un PCB qui permet à son utilisateur de retrouver le nord magnétique même dans le noir. Un écran lumineux affiche une flèche qui indique le nord grâce à un magnétomètre, des LEDs s’allument en fonction de la direction dans laquelle pointe la flèche.



Figure 1 & 2 :     <img width="221" height="174" alt="image" src="https://github.com/user-attachments/assets/7652ea36-8b13-480d-88f8-444b1e5ff32d" />

  <img width="209" height="175" alt="image" src="https://github.com/user-attachments/assets/93d80f8e-d5fb-4357-ba00-c13d786a4074" />

À propos :

Le projet est réalisé sous KiCad et comprend actuellement la conception du schéma électronique ainsi que celle du circuit imprimé et le code a implémenté dans le microcontrôleur.

## Composantes principales

| Type de composant | Référence / Modèle |
| :--- | :--- |
| **Accéléromètre** | MPU-6050 |
| **Alimentation** | USB-C |
| **Ecran** | *Non spécifié* |
| **LEDs** | WS2812B |
| **Level shifter** | 74AHCT1G125 |
| **Magnétomètre** | MMC5883MA |
| **Microcontrôleur** | STM32G071KBTxN |
| **Régulateur 3,3V** | AP2112K-3.3 |

---

**Fonctionnement** :
<img width="454" height="257" alt="image" src="https://github.com/user-attachments/assets/dc220699-66c4-4177-a8e4-c060b684831f" />


Le MMC5883MA est utilisé comme capteur magnétique pour mesurer le champ magnétique terrestre.

Le MPU-6050 apporte les informations inertielles permettant de prendre en compte l'orientation et les mouvements de la carte par rapport au sol.

Les données des capteurs sont traitées par le STM32G071KBTxN, qui peut déterminer la représentation de la direction à afficher.

Le code permet de fusionner ces données pour calculer un cap précis (compensé en inclinaison), puis met à jour l'écran central et pilote les LEDs (WS2812B) afin d'indiquer l'orientation.

Alimentation :

La carte est prévue pour être alimentée via USB-C.

L'alimentation est ensuite régulée par un AP2112K-3.3 afin de fournir le domaine d'alimentation aux circuits fonctionnant en 3,3 V comme le microcontrôleur.

Le 74AHCT1G125 est utilisé dans la chaîne de commande des LED afin d'assurer l'interface logique entre le microcontrôleur et les WS2812B.

Les résistances sont utilisées comme résistance de pull-up pour le bus I2C, pour la configuration USB-C et pour la chaîne de commande des LEDs

Les condensateurs sont utilisés pour assurer le découplage local des circuits intégrés, la stabilisation de l’alimentation et le filtrage des variations rapides de tension.

Pour le placement des composants il est important que les condensateurs de découplage soient placés au plus près des composants qu’ils doivent découpler afin de réduire la longueur des connexions.

Structure du projet :

.            
    ├── Projet1.kicad_sch      # Schéma principal
    ├── Projet1.kicad_pcb      # Circuit imprimé
    ├── LED20.kicad_sch        # Schéma de l'affichage LED
    ├──README.md              # Documentation du projet
    └── Code_boussole 	       # code du projet 


Améliorations futures :

Passer sur batterie (LiPo / Li-Ion) : Ajoute un régulateur de charge USB et un circuit de basculement automatique entre l'USB et la batterie

Mesure de tension batterie : Ajoute un pont diviseur de tension connecté à une entrée ADC du STM32 pour afficher le pourcentage de batterie restant sur l'écran rond

Fusible réarmable : Ajoute une protection contre les surintensités juste après VBUS.

Visualisation du projet généré par IA : 
<img width="375" height="296" alt="image" src="https://github.com/user-attachments/assets/7f48481f-e096-4c55-aa78-1f7d685874d8" />
<img width="376" height="256" alt="image" src="https://github.com/user-attachments/assets/d52474ad-9076-405f-9b37-3621759e0d5b" />

