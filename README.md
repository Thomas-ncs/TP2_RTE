#quelle est la part des énergie renouvelable par rapport aux autres energies en france durant l'annés 2022
import csv 
import os
import matplotlib.pyplot as plt
table = []
données = []
chiffre = 0 
renouvelable = []
n_renouvelable = []
temp = []
c = 0
nr = 0
r = 0
nr2 = 0
r2 = 0
courbe_nr  = [] #  non renouvelable
courbe_r  = [] # renouvelable
with open ("/home/etudiant/Bureau/RTE_2022.csv",'r') as fichier:
	a = csv.reader(fichier,delimiter=",")
	for i in a:
		table.append(i)
for i in table: # supprimer tout les élément paire de notre liste 
	if c % 2 == 1:
		données.append(i)
		c = c+1
	else:
		table = table
		c = c+1
données[0] = données[1] # supprimer notre premier element de liste
données.remove(données[len(données)-1]) # supprimer notre dernier element de liste car vide
for i in range(365): 	#création de la variable temps
	temp.append(chiffre) #crée une liste temp en jour de 0 à 364 jours
	chiffre = chiffre + 1
for i in range(len(données)):  #pour tout les i je met tout les element 7-13 en int
	données[i][7] = int(données[i][7])
	données[i][8] = int(données[i][8])
	données[i][9] = int(données[i][9])
	données[i][10] = int(données[i][10])
	données[i][11] = int(données[i][11])
	données[i][12] = int(données[i][12])
	données[i][13] = int(données[i][13])
	nr = nr + données[i][7]+données[i][8]+données[i][9]+données[i][10] 
	r = r + données[i][11]+données[i][12]+données[i][13]
	n_renouvelable.append(nr) 
	renouvelable.append(r)
for i in range(len(n_renouvelable)):
	if i%48 == 0: # dans 1 jour il y'a 48 cycle de 30 minute
		for u in range(i):
			nr2 = nr2 + n_renouvelable[u]
		courbe_nr.append(nr2)
for i in range(len(renouvelable)):
	if i%48 == 0:
		for u in range(i):
			r2 = r2 + renouvelable[u]
		courbe_r.append(r2)
plt.plot(temp, courbe_nr)
plt.plot(temp, courbe_r)
plt.show()
plt.close
	

	
