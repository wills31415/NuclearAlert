# Nuclear Alert

## Introduction

Le but de ce projet est de simuler de maniere assez fidele le fonctionnement d'un centre de
production nucleaire (malgres quelques entorses avec la realite).

Le joueur aura le choix entre trois options :

    1. etre libre de faire ce qui lui plaît dans la salle de controle;
    2. Se Soumettre a des ordres provenent d'un centre directeur : "Le Dispatching National";
    3. etre en face d'un accident (cinq types dont un aleatoire) et arriver a empecher l'accident nucleaire.

Dans tous les cas, le joueur aura a sa disposition :

    - Une console qui regroupe toutes les commandes de la salle de controle;
    - Un poste securite radioprotection permettant de verifier par le detail l'etat de la centrale (et
        eventuellement intervenir)
    - un schema de la centrale ou clignotent les organes les plus touches

Des systemes de securite renseigneront l'utilisateur sur les risques et degats potentiels resultant de
certaines manoeuvres. Celui-ci restera malgre tout responsable des decisions a prendre. Une session se
terminera toujours par un bilan destine a evaluer l'ampleur des degats (materiels et humains) et noter
le joueur en consequence.

## Fonctionnement d'une centrale nucleaire

![Schema d'une centrale nucleaire](schema_centrale.png)

Une tranche de centrale nucleaire se compose d'une enceinte de confinement (Batiment reacteur sur le schema)
abritant l'ensemble du circuit primaire et protegeant l'exterieur (a la façon d'une cocotte-minute
en cas de surpression). La cuve du reacteur, abritee dans une piscine contient l'uranium (le combustible).
Une reaction nucleaire s'y produit, controlee par deux parametres :

    - les barres de controle, glissant dans des canaux, la freinent lorsqu'elles sont abaissees dans 
      le reacteur;
    - Le taux d'acide borique qui la freine lorsqu'il est eleve.

Ladite reaction nucleaire produit de l'energie calorifique servant a chauffer l'eau sous pression du
circuit primaire. Ce circuit est mis sous pression grace au pressuriseur afin d'eviter que l'eau ne
se transforme en vapeur, meme a 300° celcius. La circulation est assuree par une pompe.

L'eau chaude du circuit primaire va alors passer dans l'echangeur de chaleur ou elle va chauffer l'eau
d'un deuxieme circuit : le circuit secondaire.

Cette eau se transforme en vapeur dans le generateur de vapeur. Cette vapeur entraîne a son tour une
turbine, puis un alternateur produit l'energie electrique; c'est la production (chiffree en MW, jusqu'a
1400 MW). La vapeur passe ensuite dans un condensateur ou elle se condense de nouveau en eau (car refroidie par de l'eau provenant du fleuve) pour retourner au generateur et ainsi de suite (bouclage). Une pompe
sert bien entendu a la circulation de l'eau du circuit secondaire.

### La salle de controle

La salle de controle met a votre disposition toutes les commandes et les donnees physiques (temperatures, pressions, debits, radioactivites, etc.) qui vous seront utiles.

Figurent aussi les cadres reserves aux ordres du dispatching et aux avertissements--securite qui se compose d'un message donnant l'etat d'une partie de la centrale :

    - Degradation possible
    - Risque important de degradation
    - Degradation tres importante

l'organe concerne :

    - Circuit primaire
    - Circuit secondaire
    - Pompe du circuit primaire
    - (a continuer)

et la cause de cette degradation.

Par exemple, vous pouvez avoir comme message :

    Risque important de degradation du circuit primaire du a la formation de vapeur (N.B : pression trop faible... )

Les commandes disponibles sont actionnees par des touches precises. Le reglage d'un parametre s'effectue par les touches flechees haut et bas (montee, descente). Tous ces
ordres sont soumis evidemment aux etats des organes qu'ils concernent :

    - 1 : Fonctionnement de la pompe du circuit primaire
    - 2 : Fonctionnement de la pompe du circuit secondaire
    - B : Action sur les barres de controle
    - T : Action sur le taux d'acide borique
    - P : Fonctionnement pressuriseur
    - R : Fonctionnement pompe condenseur
    - U : Autorise en cas d'urgence l'enfoncement rapide des barres dans le reacteur. Cette procedure comporte des risques de degradation.
    - S (maintenu enfonce) : demande la fin de la session
    - Tab : Affiche le schema de la centrale
    - Espace : Passage en poste securite radioprotection

**Nota** : *Difference entree-sortie* designe la difference de temperature entre l'entree et la sortie du condensateur. Ceci permet d'evaleur sont efficacite.

### Le poste securite radioprotection

Donne les etats de tous les organes de la tranche. La valeur cent correspond a un etat intact, zero a une destruction complete ou a un etat entravant gravement le fonctionnement.

Le cadre "Activite" signale entre autres divers niveaux de contamination (piscine, air a l'interieur de l'enceinte, rejets atmospheriques et aqueux) en becquerels (activite reelle), en rems ou milirems par heure (correspondant a l'influence exercee en une heure sur un etre humain).

Le cadre "Ordinateur" donne l'etat courant de la centrale et des alentours : E.G.C (Etat general centrale), niveau d'alerte, ouvriers actifs ou non (max. sept), population evacuee/contaminee, etc.

La encore quelques commandes sont disponibles :

    - Tab : Affiche le schema de la centrale
    - Espace : Retour a la salle de controle
    - P : Demande l'evacuation de la population (celle-ci n'est effective que quelques temps plus tard)
    - B : Bilan de l'activie ouvriere. Cette commande affiche les differents organes ou sont potentiellements realisables des interventions humaines. Pour chacun d'eux peut etre affiche :
        o Si l'intervention est possible ou impossible
        o Le nombre possible d'ouvriers pouvant intervenir
        o Le nombre d'ouvriers en train d'intervenir en cours
    Le bilan reste affiche tant que la touche B est enfoncee.
    - O : Intervention ouvriers. Selectionnez l'organe concerne en appuyant sur la lettre correspondante. Si l'intervention est deja en cours, vous aurez la possibilite de l'annuler (et de recuperer l'effectif).
    Une intervention d'ouvrier permet de remettre en etat un organe defectueux. Elle n'est bien sur possible que si les conditions (pression, radioactivite, temperature) le permettent. Si celles-ci deviennent defavorables en cours d'intervention, les ouvriers affectes a la tache seront signales blesses et ne pourront rejoindre que petit a petit les effectifs disponibles.

### Quelques remarques

La temperature du circuit primaire (donc en bout de chaîne, la production electrique) est dans une certaine mesure liee au debit de ce meme circuit. En effet, plus l'eau stagne, plus sa temperature s'eleve au contact de l'uranium en fission. Le reglage de la pompe du circuit primaire et de a pression determine avec precision la production. En fait, le dispatching admet une marge de plus ou moins 10MW (a maintenir pendant que dure le bip-bip). 

Mise en divergence signifie faire demarrer la reaction en chaîne (lever des barres, baisse du taux d'acide borique, fonctionnement des pompes, pressurisation, etc.)
et let production de vapeur dans le generateur. Toute action sur un organe principal du circuit primaire (pressuriseur, barres, bore ) n'entraîne pas, on s'en doute une modification brutale des parametres. Une certaine inertie (montees ou descentes progressives) rend la simulation realiste... et le jeu plus ardu.
Donc procedez avec methode et sans precipitation.

## Le Dispatching

Uniquement disponible au niveau deux du jeu (le niveau un est un mode completement libre sans incidents exterieurs possibles)

Vous recevez des ordres de l'exterieur, a vous de les suivre les plus fidelement possible.

Le premier ordre sera toujours la mise en divergence de la centrale (le demarrage du reacteur, etc.)
Des que la temperature de la vapeur depasse 140°C  mise en service (et donc commence a produit electricite),
on recevra des ordres. Attention, si on ne produit plus de vapeur apres en avoir produit, on recevra quand meme des ordres.

A chaque tour, il y aura 40% de chance qu'on vous demandera de produire pour les besoins nationaux un certain nombre de MW (entre 900 et 1400 MW). Tant que ce but n'est pas atteint, il n'y aura pas d'autre ordres.
On compte alors le nombre de tour avant que le joueur arrive a produire
le nombre de MW demande (ave une tolerance de 10MW). Au bout de huit tours (un tour = 10 secondes ?), tant que le but n'est pas atteint, on soustrait un point du score du joueur (score = 100 en debut de partie). Au bout de seize tours, si le but n'est pas atteint, on a 20% de chance de recevoir un contre ordre qui demande de produire un certain nombre de MW entre 100 et 1400MW. Au bout de cinquante tours, on vous demande d'accelerez la procedure et vous perdez six points au score. Au bout de soixante cinq tours, score diminue de trois points

Si vous atteignez le but et le maintenez pendant quinze tours, l'ordre cessera et vous gagnerez 10 points au score. 

Si la centrale ne produit plus d'electricite pendant six tours, le jeu a 50% de s'arreter a chaque tour
et on affiche alors le bilan (voir bilan)


## Les catastrophes possibles

Les catastrophes n'interviennent que si on choisit le niveau trois du jeu.

Voici les scenarii possibles pour les catastrophes :

    1. Pour une raison inexplicable, le circuit primaire vient d'etre tres gravement endommage. Les degats s'etendent jusqu'au pressuriseur. L'echangeur est legerement touche. La piscine est fissuree. Etat d'alerte maximal.
    Etat circuit primaire : 30%+[0-15], pressuriseur : 65 + [0-15], Pompe circuit primaire : Etat circuit primaire + [0-3], tuyvap (?) -= (10 + [0-15]), piscine = piscine - 18, cuve -= (3+[0-10]), etat bore -= (40+[0-25]), etat barre d'uranium /= 1.5, resist (?) = pres

    2. La cuve et la piscine viennent de se degrader subitement. Les barres, les canaux et le circuit primair sont egalement touches. Le generateur est fissure mais l'echangeur est intact. La situration est tres alarmante.
    piscine = 50 - [0-15], cuve = 55 - [0-7], ebar -= [20+[0-2]], , etat canaux /= 1.5, circuit primaire -= (10+[0-13]), pressuriseur -= 3, resist -= 4, generateur -= (3+[0-10]), etat bore -= (8+[0-10])

    3. Une fuite vient d'endommager gravement le systeme producteur de vapeur. L'ensemble primaire est peu touche mais le secondaire et l'enceinte ont ete degrades. Situation dangereuse, contamination possible.
    gene = 40 + [0-10], tuyvap = 50 + [0-3], prot -= [0-3], cir 2 -= 25 +[0-3]%, econd -= 3, pmp2 -= 4+[0-3],
    ebore = [0-1.].ebore, ebar -= 20 + [0-10]

    4. Un avion vient de percuter l'enceinte de confinement. Elle est partiellement detruite. L'ensemble primaire est gravement touche. Des projections ont endommage le circuit secondaire et surtout le condenseur.
    prot /= 2.5, pisc /= 1.5, cuve -= 20, gene -= 14 + [0-3], tuyvap -=3+[0-12], cir1 -= 20+[0-15],
    ebar /= 1.2, pmp1 = [0-1.]pmp1, pmp2 /= 1.3, cir2 -= 8+[0-10], econd= econd/2 - [0-14], 
    ebore = ebore/1.4 - [0-10]

    5. Un tremblement de terre d'une violence exceptionnelle a frappe la region. La centrale est touchee. Les degats sont multiples et impossibles a localiser. La situation est catastrophique. 
    prot /= 2.6, econde /= 2.6, pisc -= 30+[0-30], cuve = 20+[0-30], gene = 10+[0-10], pmp1/= 1.6,
    cir1 -= 20+[0-8]. Chance 50% cir2/1.4 et pmp2/2. Chance 70% cir1/1.4. Chance 40% ebore/3.2.
    Chance 30% ecan/1.5, ebar/2.4

Gestion des incidents potentiels : Tant que la production est inferieure a 900MW, pas d'incidents possibles
Sinon a chaque tour de jeu (10 secondes), il y a 20% de chance qu'une des cinq catastrophes au dessus arrive.
Quand une catastrophe arrive, 

Remarque : Si la production d'electricite depasse 1600MW, il s'affichera un message d'alerte disant qu'on est en surproduction. Dans ce cas, le declenchement automatique permettant de plonger les barres d'uranium dans l'acide borique aura lieu.


## Modelisation numerique

Inertie : Lorsque l'utilisateur demandera par exemple de modifier la quantite de bore, on decrementera/incrementera de un la quantite de bore actuelle pour atteindre au bout d'un certain nombre de pas de temps la valeur souhaitee. On fera de meme avec les autres quantites.

Nom des variables dans le code basique : 

A l'initialisation :
-------------------
T1  = 25  : Temperature du circuit primaire (de l'eau en °C)
P1  = 1   : Pression de l'eau dans les canalisation circuit primaire (en bar)
BAR = 0   : % des barres plonges dans le circuit d'eau
TPRES = 25 : Regime en % du pressuriseur (a atteindre)
RAD1 = 200 : Radioactivite circuit primaire (en becquerel)
ZVAPRESS = -1 : Pression de la vapeur d'eau dans le circuit secondaire (en bar)
TVAP = -1 : Temperature de la vapeur d'eau dans le circuit secondaire 
DEB1 = 0 : Debit pompe circuit primaire
DEB2 = 0 : Debit pompe circuit secondaire
FP1  = 0 : Fonctionnement de la pompe primaire (a 0%, a 100%, etc.)
FP2  = 0 : Fonctionnement de la pompe secondaire (a 0%, a 100%, etc.)
ZENCPRES = 1 : pression subit par l'enceinte du reacteur
ZRADINT = 0.00002 : Radioactivite de l'enceinte de confinement en rem/h ou en mrem/h
RAD2 = 0 : Radioactivite circuit secondaire (en becquerel)
BORE=47 : % d'acide borique a atteindre (destine a freiner les neutrons pour ralentir la reaction nucleaire)
DEBREF = 0 : Debit du condensateur
RADPISC = 0 : Radioactivite de la piscine (en becquerel)
ZAIRRAD = 0 : Radioactivite atmospherique (en rem/h ou en mrem/h)
ZREFRAD = 0 : Radioactivite aquatique ( en rem/h ou en mrem/h)
MW = 0 : production electrique obtenue
DES = 0 : Difference de temperature entre l'entree et la sortie du condensateur
FPR = 0 : % de fonctionnement de la pompe du condensateur
DISP = 145 : Nombre d'ouvriers disponibles
OCC = 0 : Nombre d'ouvriers actifs
BLES = 0 : Nombre d'ouvriers blesses
ZIT2 = 0
ECAN = 100 : Etat des canaux guidant les barres d'uranium
EBAR = 100 : Etat des barres d'uranium
CUVE = 100 : Etat de la cuve contenant les canaux et les barres
PISC = 100 : Etat de la piscine ou sont plonges les barres
PMP1 = 100 : Etat de la pompe du circuit primaire
PMP2 = 100 : Etat de la pompe du circuit secondaire
TUYVAP = 100 : Etat de l'echangeur de chaleur
GENE = 100 : Etat du generateur de vapeur
PRES = 100 : Etat du presuriseur
RESIST = 100 : Etat de la resistance du pressuriseur
PROT = 100 : Etat de l'enceinte de confinement
CIR1 = 100 : Etat du circuit primaire
EBORE = 100 : Etat de la production d'acide borique
CIR2 = 100 : Etat du circuit secondaire
ECOND = 100 : Etat du condenseur
ZCENTRALE = 100 : Etat general de la centrale
PNT = 100 : Nombre de points gagnes (score)
ZIT1 = 0
OUV(8) : 8,"PMP1", 8,"PMP2", 20,"COND", 60,"GENE", 5,"BORE", 20,"CIR2", 10,"PRESS", 45, "CIR1" : nombre d'ouvriers par chantier (avec nom du chantier)
BAR2 = BAR   : % barre dans piscine actuel (inertie des commandes)
BORE2 = BORE : % acide borique actuel (inertie commande, on essaie d'atteindre la valeur bore)
TPRES2 = 0 : Regime actuel du presuriseur
F1 = 0 : Espece de pas de temps glissant (module 20)
EVPOP = 0 : % de la population evacuee
CONTAM = 0 : Contamination de la population par la radioactivite
FD = 0
FD1 = 0 => FD et FD1 deux etats pour gerer le dispatching
CD = -1  : COmpteur de tour depuis le dernier ordre (modifie les etats pour gerer l'urgence)
BUT = -1 : En dispatching, nombre de MW voulu pour alimenter la population
MPRO = 0  : Moyenne de la production en MW de la centrale (fenetre glissante de six derniers pas de temps)

### Enceinte du reacteur

Si l'enceinte de confinement est abîmee :
Pression subit par l'enceinte  = 1 en etat normal
    Si la pression de l'eau est > 8 bar, etat de la cuve < 100% et etat piscine < 100% 
    ou bien si etat cuve < 30% et etat piscine < 40% :
         pression subit = pression subit pas de temps avant + (200-cuve-pisc)/2300.
    Si etat circuit 1 < 60 et pression eau > 12 bar ou si circuit 1 < 20:
         pression subit += (100-circuit1)/3000
    Si l'etat du generateur de vapeur < 90 et pression vapeur d'eau dans generateur > 2:
         pression subit += (100-gene)/2000
    La pression subit ne peut pas depasser physiquement cinq bar
    Si la pression subit est > 1 :
        Si la etat protection confinement est compris entre 50 et 60 :
            pression subit -= ((100-prot)/200).(pression subit)
    Petite chance (moins de 30%) que la pression baisse de 0.13 bar mais ne peut etre en dessous
    de un bar.

Inertie des barres :  x = 100 - (100-bar).ebar/100 (= bar si ebar = 100%)
                      si bar2 < x bar2 += 1
                      Si bar2 > x bar2 -= 1


### Calcul circuit primaire

Temperature du circuit t1= (50-bore2)/50.((bar2/100).645-(deb1/90).140+2P1)+26+zit1
Si tuyvap<50 et bore<25 et bar2<50 alors zit1 += [0:26]
Si tvap < t1 : zit1 += (tvap-t1)/3
sinon zit1 = max(zit1-[0:16],0)
Si t1 < 25 : t1 = 25 + [0:15]
Pression circuit primaire : p1 = max(((tpres2-25)/3.24 + (t1-100)/83.3).(cir1/100+0.1).(tuyvap/100+0.1),1)
Debit circuit primaire : deb1 = cir1/100.cuve/100.fp1/100.90
x = min(1400, mw)
radiation circuit primaire rad1 = 98.(deb1+1)+[0:90]+(50-bore).(x+0.1).0.0654

### Circuit secondaire

Debit = (etat circuit secondaire).(etat condensateur+10).(etat generateur vapeur).(% fonctionnement
pompe circuit) x 0.00000085
Si le debit calcule est < 3, et si la pression de la vapeur > 3, alors :
debit = (etat circuit).(etat condensateur+10).(etat generateur vapeur) x 0.0000013
Le debit ne peut pas depasser 99 m^3/s

Si |zit2| < 3 alors z = 0 sinon z = zit2
Temperature vapeur = (etat echangeur chaleur).(t1/151.)+26+z
Si (Delta temp. entree sortie (=des))<= 11 et t1 > 190, zit2 += rnd(11-des) sinon zit2 -= [0:2]

si (fp2<55+[0:15]) et t1 > 200 alors zit2 += [0:t1/100]
sinon si zit2!=0 alors zit2 -= [0:3]. Si zit2 < 0 alors zit2 = 0

Si la temperature de la vapeur est inferieure a 120°C, on considere qu'il n'y a pas de vapeur

Si il y a de la vapeur, alors la pression exercee par la vapeur est (cir2+10).gene.(fp2/500000+(tvap-135)/100000)
avec une pression minimale de 1 bar et vaut au maximum 99 bar (!). 

La radioactivite dans le circuit secondaire depend de l'etat de l'echangeur de chaleur, et est calculee comme 
le max entre la radioactivite du circuit secondaire au pas de temps precedent et (100-tuyvap)/100.rad1.


### Le condensateur :

Debit condensateur = etat condensateur * % fonctionnement pompe condensateur * 0.015
Si il y a creation vapeur d'eau : Difference temperateur entree-sortie = debit/7.5

### Traitement production

Si pas de vapeur ou cir2 < 22, MW = 0
Si tvap < 3000 (!) alors mw = max(5.787.(tvap-120)+28.118.(zvappres-1)+P1,0) sinon mw = 30000
Si cir2 < 60 : mw = (cir2/100).mw
Si mw > 1400 et mw < 1412 => mw = 1400 ???

### Securite

Signale et gere d'eventuels problemes sur la centrale (effets cumulatifs !) :

mpro = (5mpro+mw)/6

    - Sur le circuit primaire : Si t1 < 40 : pas de degradation possible
                                Si 400 < t1 < 420 : Affichage temperature trop eleve circuit 1
                                Si t1 >= 420 : Affichage risque important degradation circuit 1 a cause de la temperature
                                    Si les barres plongees a plus de 20% : degradation des barres de [0-3]%
                                                                           Affichage degradation possible des barres
                                    Degradation circuit 1 de [0-2]%
                                    30% de chance que la pres et la resist de l'enceinte confinement degrade de [0-2]%
                                Si t1 >= 40p1 : Afficher risque important de degradation circuit 1/vapeur
                                                circuit1 degradation de [0-3]%
                                                pres de l'enceinte confinement degradation de [0-2]%
                                                30% degradation resist enceinte confinement de [0-2]%
                                Si t1 >= 50°C:
                                    Si etat circuit 1 < 50% : 40% chance degradation echangeur chaleur tuyvap -= [0-4]%
                                                              20% chance degradation generateur vapeur (gene)
                                    Si etat circuit 1 < 58% : 50% degradation pompe 1 de [0-3]%
                                    Si etat presuriseur < 50% : 80% chance enceinte confinement resist degradation de [0-3]%
                                    Si etat circuit 1 < 60% : 40% degradation cuve [0-2]
                                    Si etat circuit 1 < 30% : 30% degradation cuve [0-3]                
                                    Si etat circuit 1 < 20% : 80% degradation piscine [0-6]%, cuve : [0-6]%
                                    Si etat circuit 1 < 80% et pression > 10 : 15% degradation circuit 1 [0-2]%
                                    Si cuve < 70% et bar2 > 22 : 40% degradation barres [0-3]%
                                    Si cuve < 50% : 50% degradation canaux [0-5]%
                                    Si echangeur chaleur (tuyvap) < 60% : 30% degradation circuit 1 [0-1.5]%
                                    Si echangeur chaleur < 60% et pression > 3 : 50% degradation gene [0-2]%
                                    Si canaux < 60% et bar2 > 40 : 30% etats barres degradation [0-2]%
                                    Si cuve < 50% et circuit 1 < <50% : etat bore degradation [0-2]%

    - Sur le circuit secondaire : Si pas de vapeur, pas de degradations possibles
                                  Si echangeur chaleur < 70% : Affichage probleme echange chaleur entre circuit 1 et 2
                                  Si echangeur chaleur < 40% : Affichage risque important degradation echangeur/generateur
                                                               25% chance degradation generateur vapeur [0-3]%
                                  Si temperature vapeur d'eau >= 310°C, Afficher risque important degradation circuit 2 a cause de la chaleur
                                                                        25% chance degradation circuit 2 [0-4]%
                                  Si delta temp. < 11 et temp. vap >= 130 : afficher Degradation potentiel circuit 2 du au refroidissement
                                  Si circuit 2 < 50 et temp. vap. > 130 : 30% degradation circuit 2 [0-1.5]%
                                  Si circuit 2 < 60% : 30% chance degradation pompe 2 [0-2]%
                                  Si circuit 2 < 40% : 40% chance degradation generateur vapeur [0-2]%

    - Confinement/autre : Si delta temp.> 19 : Afficher degradation potentiel condenseur cause delta temp.
                                               40% degradation condenseur [0-3]%
                          Si pression subit confinement > 2 et < 3.4 alors Afficher degradation potentiel confinement du a pression
                                                                           Si protection > 50%, 30% protection degrader a [0-2]%
                          Si pression subit confinement >= 3.4 et < 4.5 : Afficher Risque important degradation confinement du a pression
                                                                         Si protection > 25%, 60% degradation protection a [0-6]%
                          Si protection confinement = 0 ou pression confinement >= 4.5, alors degradation totale de l'enceinte (voir explication plus bas), affichage alertes (voir plus bas)

## Traitement de la population autour de la centrale

evpop = 10 . pourcentage population evacuee.

Si evpop = 10, tout le monde est evacue

radiation piscine = (100-cuve).rad1/100+100+[0-45]
zradint = [0-1/55]+0.00002+(100-cir1).rad1/9898+(100-pres)/10
Si pisc < 55 et radpisc > 3000 : zradint = 1.25 zradint
Si prot < 90 zradint /= 1.3
Si prot < 10 zradint /= 1.5
Si prot > 97 zairrad = 0 sinon zairrad = (100-prot)/100.zradint+(100-circ2)/10
Si econd > 90 or rad2 < 2 : zrefrad = (100-econd).rad2/10000
Si evpop!=0 et evpop !=10 : 40% chance evpop += 1
Si evpop!=10 ou zradint>=10 :
    contam = contam - 5.(zairrad>6)-5.(zrefrad>1)-8.(zrefrad>12)-10.(zairrad>12)
    Si zairrad > 12 : contam += 4 + [0-15]
    Si zrefrad > 12 : contam += 5 + [0-20]
    Si zairrad > 20 : contam += 12 + [0-20]

Si contam entre 10 et 600 : Contamination radioactive legere de la population
Si contam entre 600 et 800 : Contamination radioactive importante de la population
Si contam superieur a 800  : Population gravement contaminee

## Autres formulations mathematiques :

Les etats ne peuvent etre negatifs. Resist ne peut etre superieur a pres et cuve ne peut pas etre plus degrade que piscine. 
Le regime des pompes ne peuvent etre superieurs a leur etat
tpres ne peut pas etre plus grand que pres + resist et tpres ne peut pas etre plus petit que 25 (seul cas ou il peut etre plus grand)
zvappres >= 1
La contamination radioactive ne peut pas etre plus grande que 30000

Enfin, l'etat total de la central est egal a : ecan+2ebar+8cuve+3pisc+pmp1+pmp2+5tuyvap+4gene+press+resist+4prot+8cir1+3cir2+ebore+econd)/44

**NB :** Si l'etat de la central est inferieure a 22%, la centrale sera completement detruite.

Si l'etat de la centrale est entre 50 et 60%, on entre dans l'etat d'urgence n°1 (DEFCOM 1)

Si l'etat de la centrale est entre 30 et 50%, on entre dans l'etat d'urgence n+2 (DEFCOM 2)

Si l'etat de la centrale est inferieure a 30%, sa destruction devrait etre imminente.



## Degradation total enceinte confinement

Afficher un message d'alerte disant que l'enceinte de confinement est totalement detruite

gene se degrade de 10 + [0-10]%
Dans ce cas, si gene < 40 : Affiche D.T.I echangeur
                            tuyvap se degrade de 10 + [0-10]%
80% degradation circuit primaire : msg D.T.I cir1/Press + cir1 degradation 10 + [0-10]%
                                                        + press de 10%
                                                        Si press < 90% : 80% resist degrade [0-10]%
65% degradation cuve et piscine : msg D.T.I cuve/piscine + piscine degradation 6+[0-16]%
                                                         + cuve degradation 5 +[0-10]%

## Tentative d'arret d'urgence

Pour eviter une catastrophe nucleaire, il est possible de tenter un arret d'urgence (qui consiste a
noyer les barres d'uranium dans l'acide borique afin d'absorber un max de neutron et arreter la reaction
nucleaire). Evidemment, si certaines parties de la centrale (surtout les canaux et les barres d'uranium)
sont abîmees, la tentative peut echouer :

La probabilite de reussite est  (en %) : cuve.ecan.ebar.0.00007+15
Si la tentative est reussie, les barres commencent a descentre (on met bar a zero et bar2 a z/2 (?))
Si la tentative echoue, on risque d'abimer une partie du circuit primaire :

    - 80% de chance d'abîmer les canaux entre 5 et 15% de degradation
    - 30% de chance d'abîmer les barres d'uranium entre 2 et 10% de degradation
    - 40% de chance d'abîmer la cuve entre 0 et 8%

## Travail des ouvriers

Lorsqu'on demande aux ouvriers d'aller reparer des parties de la centrale, le nombre d'ouvrier est fixe par avance. A savoir :

    - Huit ouvriers pour la pompe du circuit 1
    - Huit ouvriers pour la pompe du circuit 2
    - Vingt ouvriers pour le condenseur
    - Soixante ouvriers pour le generateur de vapeur
    - Cinq ouvriers pour l'injecteur d'acide borique
    - Ving ouvriers pour le circuit 2
    - Dix ouvriers pour le presuriseur
    - Quarante cinq ouvriers pour le circuit 1

Il y a au depart 145 ouvriers de disponibles.

Selon la qualite de l'environneent ou ils travaillent, il peuvent tomber malade ou non.
Tous les huit tours de jeu, il y a 40% de chance qu'un ouvrier guerisse et devient disponible.

Si l'etat du circuit 1 est < 20%, toute intervention est impossible
Tous les cinq tours, il y a 10% de (mal)chance que les ouvriers travaillant au generateur de vapeur soient blesses (si ils travaillent au generateur, bien entendu)

Si zradint > 12 ou zencpres>3 : les ouvriers travaillant sur la pompe 1, le generateur de vapeur, l'injecteur d'acide borique, le presuriseur ou le circuit 1 ne pourront pas y travailler. Si ils etaient deja sur le chantier, ils seront tous blesses

Si tvap > 300 ou mw > 1000 : les ouvriers travaillant sur la pompe 2, le condeseur ou le circuit 2 ne pourront pas y travailler. Si ils etaient deja sur le chantier, ils seront tous blesses.

A chaque tour, il y a 30% que leur intervention n'ameliore rien.
Sinon, 

    - Pour les pompes : si etat >= 97%, on arrive alors a 100%
                        sinon etat += [0-3]%
    - Pour condenseur : Si etat >= 98%, on arrive a 100%
                        sinon etat += [0-2]%
    - Pour generateur vapeur : Si etat < 89%, etat += [0-5]% sinon considere comme repare (mais pas a 100%)
    - Pour injecteur de bore : Si etat < 96%, etat += [0-4]% sinon considere comme repare (pas forcement 100%)
    - Pour circuit n°2 : Si etat < 78%, etat += [0-2]% sinon considere comme repare
    - Pour circuit n°1 : Si etat < 80%, etat += [0-2]% sinon considere comme repare
    - Pour presuriseur : Si etat < 97%, etat += [0-3]%, resist = etat -[0-4]% sinon tout a 100% (pres et resist)

Lorsqu'un module est considere comme repare, les ouvriers sont de nouveau disponibles! 
