# Small-Project-about-LM35



A. Etude du capteur de température______________________________________________ On désire réaliser un thermomètre qui déclenche une alarme lorsque la température mesurée  dépasse la valeur d’une température consigne. 
Pour ce faire, le capteur de température utilisé est un circuit intégré spécialisé LM 35. Lorsqu’il  est alimenté sous une tension de 5 V, la tension de sortie est proportionnelle à la température  du milieu dans lequel est plongé ce capteur.  
1. Déterminer la relation mathématique entre la tension de sortie US du capteur et la température Ɵ. 

T min to T max 
MIN : -55°C
MAX : 150°C
°C



Us = a T + b avec T : Température  en Ɵ .. et a = 10 mv/ °C et b  c’est égale à 0 
⇒ Us = a T + b avec a  = 10 mV et b = 0 


2. Déterminer la sensibilité de ce capteur. 

La sensibilities  : S = ⲇU / ⲇt  

3. Si l’on place le capteur à l’air ambiant de la salle, on mesure la tension de sortie US. Pour une tension Us = 230mV, déduire théoriquement la température de la salle. 
US Tension d’alimentation 


Théoriquement : on a US = 230 mv ⇒ donc a T = 230 mV avec a = 10 mV ⇒ T = 230 mV/10 mV = 23 °C

Pratique :            sans échauffement on a  : 24°C ⇒ Us ~ 255 mV  
avec échauffement on a : 40°C   ⇒ Us ~ 400 mV


B. Réalisation du thermomètre__________________________________________________ On se propose d’amplifier la tension de sortie US pour obtenir : 
● Une lecture de 0 V lorsque la température Ɵ est égale à 0 °C. 
● Une lecture de 10 V lorsque la température Ɵ est égale à 100 °C. 
1. Déterminer la valeur du coefficient d'amplification A pour satisfaire ces 2 conditions ? 

Pour satisfaire ces 2 conditions la valeur du coefficient d’amplification doit être égale À= 10

On utilise pour cette amplification le montage de la figure 2.  
Figure2 



Matériel utilisé 
● Un AOP TL081 (Alimentation ±Vcc = ±9V) 
● Un capteur de température LM35 
● Une résistance R1 de 1 KΩ 
● Un potentiomètre 
● Un multimètre










Montage Sur ISIS ( Simulation )




1. Donner l’expression du gain pour ce montage.

on a  V+ = V- et V- = ( (US/R + 0/R1 ) / (1/R)+(1/R1) )*US’  donc US = US’*R1 + 0 *R / R + R1
US = R1/R1+R * US’ ⇒  US’ = R1+R/R1 = 1 +R/R1    on varie le R pour qu’on obtient un coefficient du on total sur cette expression ( 1 +R/R1) = 10 
R = 9 Kohm 

2. En déduire la valeur de la résistance R sachant que R1=1 KΩ

 on varie le R pour qu’on obtient un coefficient du on total sur cette expression ( 1 +R/R1) = 10 
R = 9 Kohm 

3. Pour tester ce thermomètre, relever les valeurs affichées par le voltmètre à la sortie du  TL081 puis les convertir en températures pour les différents cas suivants : 


 (Vmtr1) 
 (Vmtr2) 
Ɵ
Air ambiant de la salle 
236 mV
2.35 V
23 °C
Paume de la main
327 mV
3.145V
32 °C
Présence de flamme
398 mV
3.989 V
40 °C



Les Valeurs Sur la Simulation ISIS : 




Montage Sur DIGILENT : 












Captures de WaveForms : 


C. Réalisation d’une alarme 
A partir du thermomètre précédent, on ajoute un étage " alarme " qui déclenche un signal  lumineux (LED) lorsque la température dépasse une valeur affichée (consigne). Pour ce faire, on utilise un second AOP : La tension Us’ du thermomètre est comparée à une  tension de référence Uref que l’on pourra faire varier à l’aide d’un diviseur de tension. q
Figure 30

1. Calculer les valeurs minimale et maximale de la résistance réglable r2 du diviseur de  tension pour que la tension de référence Uref puisse varier de 0 V (soit 0°C) à 4 V (soit 40°C)  en sachant que r = 500Ω. 

Sachant que la tension d’alimentation du 9V  
on a Vref = (Valim*r) / (r2 +r ) 
Donc r2 = 400 ohm pour qu’on puisse varie la tension entre 0V et 4V sachant que la tension d’alimentation doit être 9V 



Simulation Sur ISIS : 



















Montage Sur DIGILENT : 

2. Préciser la valeur de la tension de référence pour afficher une consigne de 30°C.  Déterminer alors la valeur de r2.
r2 Doit être égale à 3V pour que notre consigne soit correspond à 30°C

3. Remplir le tableau suivant : 
Noter à quel moment il y a déclenchement de l’alarme (quelle est la LED qui s’allume ?) 


���� 
(Vmtr1)
����′ 
(Vmtr2)
Ɵ 
Uref 
(Vmtr3)
Us ‘’ (sortie AOP2) (Vmtr4)
LED  
allumée
Air ambiant de la salle 
223 mV
2.215 V
 22 °C
3.012 V
VSAT = - 9V 
Vert 
Présence de flamme
335 mV
3.319 V
33 °C
3.014 V 
VSAT = 9V 
Rouge


Simulation Sur ISIS : 







4. Quelle est la fonction assurée par le 2ème AOP ? 

Le 2ème AOP joue le rôle de comparateur pour s'assurer que la valeur de tension récupérée par la capture (la tension amplifiée) et ne dépasse pas la valeur de consigne, si la valeur est supérieure à la consigne alors la led rouge s'allumera indiquant qu'il y a une présence de flamme et de ce fait on délivre le +VSAT de l'AOP et si la tension est inférieure à la consigne la led verte s'allumera indiquant que l'on est bon et c'est de ce fait on délivrant le -VSAT de l'AOP qui va donner une tension négative est assuré que la LED verte s'allume


