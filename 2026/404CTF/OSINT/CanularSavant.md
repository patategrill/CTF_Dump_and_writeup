# Write-up Canular Savant [1/3]  
  
**- Nom :** Canular Savant [1/3]  
**- Catégorie :** OSINT  
**- Points :** 100  
**- Niveau de difficulté :** Facile  
  
### **Description :**  

Je (1.85m) me baladais à Paris, jusqu'à me retrouver à un rond-point bordé de plusieurs fontaines.  
De quel rond-point s'agissait-il ?  
Format du flag : 404CTF{carrefour-etoile_du_porte-avion-charles-de-gaulle}  
_(Les flags de cette série ne comportent pas d'accents)_

On sait alors que l'on doit chercher un rond-point dans Paris bordé de plusieurs fontaines, alors on commence par une simple recherche sur google `rond-point bordé de plusieurs fontaines - Paris`   


On tombe sur plusieurs images parlant du rond-point des Champs Elysées alors on recherche son nom complet : `Rond-point des Champs-Élysées Marcel-Dassault`   

Alors on peut construire le flag en remplacant les espaces par des _, retirer les majuscules et les accents.  
On obtient alors `404CTF{rond-point_des_champs-elysees-marcel-dassault}`

Flag :  
```
404CTF{rond-point_des_champs-elysees-marcel-dassault}
```
