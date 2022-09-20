# Batman

### Observation des ports

On utilise nmap pour observer les ports de la machine

```basg
nmap -vv ip -p-
```

Et on tombe sur

![Untiled](assets/nmap.png)

On peut voire les ports suivant : 21, 22 et 3000

On observe que le port 21 est un ftp

### Connection ftp

Pour pouvoir nous connecter en ftp on utilise la commande suivante

```bash
ftp ip 21
```

On doit ensuite se connecter en tant qu'anonymous
Et on peut récuperer alert.py via cette commande 

```bash
get alert.py
```

Puis on peut observer comment fonctionne alert.py

![Untiled](assets/alert.png)

### Connection sur le server

On peut se connecter sur le server via la commade ncat, puis via ce que l'on a observer par rapport a alert.py, on peut constater que l'on peut lancer des commades dans la machine. On utilise la méthode suivante pour récuperer le premier flag


```bash
ncat ip 3000
    >[ALERT]
    >a; ls;
    >a; bash;
>cat /home/bruce_wayne/user.txt
```
Avec cela on trouve ce qui est a l'intérieur de user.txt qui est le premier flag


### Connection ssh a la machine


Ensuite pour pouvoir acceder au dernier flag on va devoire se connecter en ssh a la machine.
Pour ce faire on va devoir ajouté notre clé ssh publique au fichier authorized_host, pour ce faire on fait :

```bash
mkdir /home/bruce_wayne/.ssh
touch /home/bruce_wayne/.ssh/authorized_host
echo "ssh" > /home/bruce_wayne/ssh/authorized_host
```

Puis on peut se connecter en ssh avec

```bash
ssh bruce_wayne@ip
```

### Récupération du dernier flag

Maintenant que l'on est connecter en ssh, on va observer si bruce_wayne a un mot de passe, pour ce faire on utilise la commande suivante

```bash
sudo -l
```

![Untiled](assets/sudo-l.png)

On peut voire que bruce_wayne peut executer un programme python en root sans devoir noter son mot de passe

Donc on va modifier le programme python via vim pour pouvoire le force write avec :w!
Voici le code 

![Untiled](assets/python.png)

Ensuite on le lance est on tombe sur le dernier flag qui se trouvé dans le dossier root de la machine comme sont nom pouvez nous l'annoncé.
