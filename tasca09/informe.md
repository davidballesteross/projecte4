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

Cuan hem executat la comanda, hem de tornar a executarla per comprobar que no qieden actualitzacions.

Un cop que ja tenim actualitzat els paquets, el seguent pas sera començar amb la creació de l'estructura de carpetas, de grups i usuaris.

El primer que farem sera crear els grups neccesaris, en aquest cas en demana que crem 2 grups, el primer devs i el segon admin

Per crear aquest grups farem la seguent comanda 

```bash
groupadd devs
```

```bash
groupadd admin
```
![Captura 4](img/4.png)

Per comporbar que l'arxiu s'ha creat correctament farem servir el greep per buscar tant el grup devs com admin dins de l'arxiu /etc/groups, per fer-ho farem la seguent comanda

```bash
grep devs /etc/group
```

```bash
grep admin /etc/group
```

En la qual podrem veure que els grups d'han creat correctament

![Captura 5](img/5.png)

Un cop que ja tenim els grups creats el seguent pas sera crear l'usuari dev01 que formi part del grup devs, per fer això farem servir la seguent comanda

```bash
useradd -G devs -m -s /bin/bash dev01
```

Per confirmar que esta creat l'usuari dev01 correctament fem servir el grep

```bash
grep dev01 /etc/passwd
```
![Captura 5](img/5.png)

Un cop que ja tenim l'usuari dev01 el seguent pas sera crear l'usuari admin01 que formi part del grup admin, per fer això farem servir la seguent comanda

```bash
useradd -G admin -m -s /bin/bash admin01
```

Per confirmar que esta creat l'usuari admin01 correctament fem servir el grep

```bash
grep admin01 /etc/passwd
```
![Captura 6](img/6.png)

Un cop que ja hem creat els grups i els usuaris, el seguent pas sera crear el directori per als projectes de desenvolupament en la qual la ruta que ens demana és la seguent /srv/nfs/dev_projects, per crear les totes les carpetas d'una sola comanda farem el seguent:

```bash
mkdir /srv/nfs/dev_projects -p
```

Un cop fet això crearem el directori per a les eines d'administració en la qual la ruta sera /srv/nfs/admin_tools

```bash
mkdir /srv/nfs/admin_tools
```

![Creació de carpetas](img/3.png)

Per ultim configurarem els permisos de les carpetas, en aquest cas seran els seguent.

Chown per canviar la propietat de la carpeta

```bash
chown root:devs /srv/nfs/dev_projects
```

```bash
chown root:admin /srv/nfs/admin_tools
```

Un cop fet això assignare els permisos de la carpeta amb la comanda chmod

```bash
chmod 770 /srv/nfs/dev_projects
```

```bash
chmod 770 /srv/nfs/admin_tools
```

Per comprobar que els permisos estan correctas farem ls -l per poder veure els permisos de cada carpeta

![Permisos de la carpeta](img/4.png)

Avans de continuar amb el servidor crearem els grups i usuaris dins de la maquina client, en aquest cas una maquina zorin.

Per poder crear els grups i usuaris farem servir la aplicació "users and groups"

![aplicació](img/5.png)

Per comporbar que tots els grups s'han creat correctament farem servir el grep tal i com hem fet avans

![grups](img/6.png)

![usuaris](img/7.png)

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
