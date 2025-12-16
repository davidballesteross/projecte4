# Part 1: Còpia seguretat dels equips clients Windows

Per comneçar el primer pas sera tindre una maquina client windows amb un disc principal on tindrem el sistema operatiu i despres un segon disc de 10 Gb en el qual farem la copia.

![Captura 1](img/t02.1.png)

**A dins de la màquina obrirem l'administrador de discos i farem click dret sobre ell, li donarem a siguiente fins que quedi així**

![image](./img/14.png)

**Ara crearem documents per fer les proves de copa de seguretat**

![image](./img/15.png)


**El primer pas serà entrar al nostre navegador i entrar a la Web de duplicati, seguidament instal·larem segons el nostre sistema operatiu, en aquest cas Windows**

![image](./img/1.png)


**Un cop instal·lat obrim el descarregable i començem amb la instal·lació**

![image](./img/2.png)


**Acceptem y continuem**

![image](./img/3.png)


**Seguim amb la instal·lació com a les següents captures**

![image](./img/4.png)


![image](./img/5.png)


**Haurem de donar-li permisos per fer canvis al dispositiu**

![image](./img/6.png)


**Esperem a que es completi**

![image](./img/7.png)


**Un cop completat, li donarem a Finish**

![image](./img/8.png)


**Al donar-li a finish ens obrirà una pàgina al nostre navegador, podrem canviar la contrasenya, però en aquest cas no la canviarem**

![image](./img/9.png)


**Afagirem un backup**

![image](./img/10.png)

![image](./img/11.png)


**Ara posarem la informació del disc**

![image](./img/12.png)

**Posarem que el backup es fagi al disc secundari**

![image](./img/16.png)


**El següent serà seleccionar el que volem que es fagi un backup, en aquest cas seran els 4 documents que hem creat abans**

![image](./img/17.png)

**Posarem que es fagi cada 1 hora**

![image](./img/18.png)


**Per últim li donarem a Submit i ja estarà creat**

![image](./img/19.png)


**Ara farem el mateix pero amb Google Drive**

![image](./img/20.png)

**La farem cada dia a les 6 de la tarda**

![image](./img/21.png)


![image](./img/22.png)


**Ara borrarem els documents per veure si es fa el backup**

![image](./img/23.png)

**Anirem a Restore a la part esquerra i despres farem click a restore i start**

![image](./img/24.png)

![image](./img/25.png)

**Ja ho tindriem fet**

![image](./img/26.png)

![image](./img/27.png)


**Ara pasarem a la part de Ubuntu**

**Farem servir Duplicaty**

**Primer de tot farem la següent comanda**

```
mkdir /media/backup 
```

![image](./img/28.png)

**Ara haurem de donar-li forma al disc**

```
sudo apt install fdisk
```

**Ara veurem el disc que tenim**

```
fdisk -l
```

![image](./img/29.png)

**Ara haurem d'instal·lar lvm2**

```
sudo apt install lvm2
```

**I ara crearem el volum**

```
pvcreate /dev/sdb
```

![image](./img/30.png)

**El següent pas serà formategar-lo**

```
mkfs.xfs -f /dev/sdb
```

![image](./img/31.png)

**Ara muntarem el disc a la carpeta que hem creat abans**

```
mount /dev/sdb /media/backup
```

![image](./img/32.png)

**Ara instal·larem el Duplicity**

```
apt install duplicity -y
```

**Un cop tinguis això llest, el següent pas és crear un parell d’usuaris amb la seva carpeta personal i posar quatre arxius de 10 MB al home del teu usuari.**

```
useradd -m -s /bin/bash user1
```

```
useradd -m -s /bin/bash user2
```

![image](./img/33.png)

```
fallocate -l 10MB file1
fallocate -l 10MB file2
fallocate -l 10MB file3
fallocate -l 10MB file4
```

![image](./img/34.png)

**Ara ja tenim els arxius creats, amb la següent comanda fem una copia de seguretat a la carepta home**

```
duplicity full /home/user file:///media/backup/
```

**Jo he escollit la passphrase prova1**

![image](./img/35.png)

**Amb la comanda ls podem veure que s'ha fet**

![image](./img/36.png)

**Ara borrarem els documents que hem fet abans**

![image](./img/37.png)

```
duplicity restore file:///media/backup/ /home/user/copia
```

![image](./img/38.png)
