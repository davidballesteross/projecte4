# Servidor NFS

Per començar, hem de crear 2 maquines virtuals, en aquesta practica hem de crear una maquina **ubuntu server** i una **zorin** per simular el **servidor i el client**.
Les dues maquines han d'estar en: la primera en **NAT** i la segona en **HOST ONLY**.

![Captura 1](img/1.png)
![Captura 2](img/2.png)

---
Un cop que ja tenim les dues maquines configurades començem configuran el servidor (ubuntu base)

La primera comanda que utilitzarem servira per actualitzar els paquets.

```bash
sudo apt update && sudo apt upgrade -y 
```
![Captura 3](img/3.png)

Cuan hem executat la comanda, hem de tornar a executarla per comprobar que no quedin actualitzacions.

---
Un cop que ja tenim actualitzat tots els paquets i ho haguem comprobat, el seguent pas sera començar amb la creació de l'estructura de carpetas, de grups i usuaris.

El primer que farem sera crear els grups neccesaris, en aquest cas en demana que creem 2 grups, el primer **devs** i el segon **admin**

Per crear aquest grups farem la seguent comanda 

```bash
groupadd devs
```

```bash
groupadd admin
```
![Captura 4](img/4.png)

---
Per poder comprovar que els grups s'han creat correctament farem servir la comanda greep per buscar els 2 grups, el grup **devs** i el grup **admin**, hem d'entrar dins de l'arxiu /etc/groups, per fer-ho farem la seguent comanda:

```bash
grep devs /etc/group
```

```bash
grep admin /etc/group
```

En la qual com podrem veure en la captura els 2 grups d'han creat correctament

![Captura 5](img/5.png)

Un cop que ja tenim els grups creats el seguent pas sera crear l'usuari **dev01** que formi part del grup **devs**, per fer això farem servir la seguent comanda

```bash
useradd -G devs -m -s /bin/bash dev01
```

Per confirmar que esta creat l'usuari dev01 correctament fem servir el grep

```bash
grep dev01 /etc/passwd
```

![Captura 6](img/6.png)

Un cop que ja tenim l'usuari dev01 el seguent pas sera crear l'usuari **admin01** que formi part del grup **admin**, per fer això farem servir la seguent comanda

```bash
useradd -G admin -m -s /bin/bash admin01
```

Per confirmar que esta creat l'usuari **admin01** correctament fem servir la comanda grep com anteriorment

```bash
grep admin01 /etc/passwd
```
![Captura 7](img/7.png)

Un cop que ja hem creat els grups i els usuaris, el seguent pas sera crear el directori per als projectes de desenvolupament en la qual la ruta que ens demana és la seguent /srv/nfs/dev_projects, per crear les totes les carpetas d'una sola comanda farem el seguent:

```bash
mkdir /srv/nfs/dev_projects -p
```
![Captura 8](img/8.png)

Un cop fet això crearem el directori per a les eines d'administració en la qual la ruta sera /srv/nfs/admin_tools

```bash
mkdir /srv/nfs/admin_tools
```

![Captura 9](img/9.png)

Per ultim configurarem els permisos de les carpetas, en aquest utilitzare la comanda Chown per canviar la propietat de la carpeta.

```bash
chown root:devs /srv/nfs/dev_projects
```

```bash
chown root:admin /srv/nfs/admin_tools
```
![Captura 10](img/10.png)

Un cop fet això hem d'assignar els permisos de la carpeta amb la comanda chmod 770

```bash
chmod 770 /srv/nfs/dev_projects
```

```bash
chmod 770 /srv/nfs/admin_tools
```

![Captura 11](img/11.png)

Per comprobar que els permisos estan correctament farem ls -l per poder veure els permisos de cada carpeta

![Captura 12](img/12.png)

Per poder continuar amb el servidor hem de crear els grups i usuaris dins de la maquina client (Zorin)
Per poder crear els grups i usuaris farem instalem la aplicació "users and groups"

![Captura 13](img/13.png)

![Captura 14](img/14.png)

![Captura 15](img/15.png)

![Captura 16](img/16.png)

![Captura 17](img/17.png)

Hem de comprobar que els numeros UID i GID (els números d'identificació) coincideixin a les dues màquines.

Un cop fet això instalarem els paquets neccesairs del servei NFS al servidor, per fer això farem la seguent comanda

```bash
apt install nfs-kernel-server -y
```
Per comprobar que s'ha instalat correctament podem fer un systemctl status

```bash
systemctl status nfs-kernel-server
```

![status](img/8.png)

---

A continuació farem una prova 1 (L'error comú)
