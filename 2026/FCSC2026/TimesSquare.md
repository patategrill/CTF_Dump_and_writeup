## WriteUp Times Square catégorie MISC du FCSC2026 :  

**Nom :** Times Square
**Catégorie :** Misc
**Points :** 150
**Niveau de difficulté :** Facile


**voici l'énoncé :** On vous donne accès à un terminal d'accès distant, trouvez vite son flag avant que le système ne se bloque. 

commande pour avoir accès au terminal : ssh -o StrictHostKeyChecking=no -p 2051 challenges.fcsc.fr 

Premièrement, on se connecte au challenge avec la commande ssh -o StrictHostKeyChecking=no -p 2051 challenges.fcsc.fr qui nous donne : 

<pre>
 ┌ FCSC ACCESS TERMINAL ────────────────────────────────────────┐
 │You've been waiting 0 seconds for a flag to appear...         │
 │Maybe your TTY is too small? 🦕                               │
 │                                                              │
 │uint16_t X = 115, Y = 26, t = 0                               │
 └ Press q to exit ─────────────────────────────────────────────┘
</pre>

Le X correspond à la "hauteur" du terminal 
Le Y correspond à la largeur du terminal 
Le t est un compteur qui augmente de 1 chaque sec

Il est dit "Maybe your TTY is too small ?" ce qui traduit en français veut dire "Peut-être que votre TTY (terminal) est trop petit ?"

Donc on commence par augmenter la largeur du terminal jusqu'a ce que le terminal nous donne : 

<pre>
 ┌ FCSC ACCESS TERMINAL ────────────────────────────────────────┐
 |Wow you have a laaaaarge screen! Impressive!! 🤯              │
 │Maybe it is time to make me a bit taller?                     │
 │                                                              │
 │uint16_t X = 354, Y = 26, t = 238                             │
 └ Press q to exit ─────────────────────────────────────────────┘
</pre>

Il est dit "Maybe it is time to make me a bit taller ?" ce qui traduit veut dire "Peut-être est-il temps de me faire grandir un peu ?"

Alors on augmente la hauteur sauf qu'on finit par ne plus voir le message donc on quitte le terminal avec q et on observe le message :

<pre>
 ┌ FCSC ACCESS TERMINAL ────────────────────────────────────────┐
 │So much screen space, you seem serious about getting the flag!│
 │Pass the following C condition to print the flag:             │
 │X + Y + t = 42 && X > 300 && Y > 200                          │
 │uint16_t X = 354, Y = 302, t = 409Connection to challenges.fcsc.fr closed.
</pre>

On voit alors qu'il y a une condition à l'apparition du flag qui est X + Y + t = 42 && X > 300 && Y > 200 sauf que cette condition est 
impossible à valider car X doit être supérieur à 300 et Y doit être supérieur à 200 ce qui nous donne 300 + 200 = 500 soit beaucoup trop, 
sans compter le timer qui augmente de 1 par seconde.

Or il y a la fonction uint16_t donc toutes les valeurs sont mod 65536 donc il est possible de valider la condition avec ces éléments.
Il nous faut donc calculer les bonnes valeurs à trouver pour X,Y et t pour valider la condition, 
on veut trouver (X + Y + t) mod 65536 = 42, après calcul, on trouve que X doit être égale à 65328, Y à 250 et donc t a 0 
car 65328 + 250 + 0 = 65578 et 65578 mod 65536 = 42

Il nous faut maintenant tromper le terminal avec stty qui va nous permettre de faire croire au terminal que la hauteur et la largeur sont des 
valeurs qu'on lui a renseignés (X = 65328 et Y = 250) avec stty columns 65328 rows 250, on se connecte en même temps au terminal avec 
ssh -o StrictHostKeyChecking=no -p 2051 challenges.fcsc.fr ce qui nous donne une ligne de commande qui ressemblent à :

stty columns 65328 rows 250 && ssh -o StrictHostKeyChecking=no -p 2051 challenges.fcsc.fr

On obtient alors un terminal bugué mais le flag est là !:
<pre>
┌ FCSC ACCESS TERMINAL ────────────────────────────────────────┐ 
│Wow you did theimpossible and got the flag! │
  FCSC{2b1150bfd7ad93f72a184764bcae0f51521fcaf796b0997288} 
  │uint16_t X = 65328, 250, └ Press q to exi─────────────────────────────────────────────┘ 
  S much screen space, you seem serious about getting the flag! 
  Pass the following C condition to print the flag: X + Y + t = 42 && 300 && 200
</pre>
