# T05:Connexió via SSH

El primer que farem serà crear dues màquines virtuals: una amb Windows i l’altra amb Linux (Ubuntu). La primera interfície serà NAT i la segona serà Host-Only.  

![](img.md/1.png)

![](img.md/2.png)

# SSH Linux

El primer que farem serà entrar a la màquina d’Ubuntu i executar la comanda : sudo apt install ssh

![](img.md/3.png)

Com que l’hem posat des del principi, la xarxa es configurarà automàticament. Després la comprovarem amb la comanda `ip addr show` per veure la IP del servidor.  

![](img.d/4.png)

I després comprovarem que l’SSH s’ha instal·lat correctament. 

![](img.md/5.png)

Després, dins de la màquina de Windows, anirem a “Ver conexiones de red” per poder editar la configuració i, tot seguit, comprovarem que s’ha assignat correctament.

![](img.md/6.png) 

![](img.md/7.png)

![](img.md/8.png)

Després d’haver fet l’anterior, ja ens podrem connectar a la màquina d’Ubuntu des de la terminal de Windows. Quan ens ho demani, haurem d’acceptar amb `yes`. Finalment, farem la connexió amb la comanda `ssh nom@ip`.  

![](img.md/9.png)

Després d’entrar, configurarem l’arxiu `/etc/ssh/sshd_config` amb l’editor `sudo nano`.

![](img.md/10.png)

Després, dins l’arxiu, podrem configurar diferents opcions, com per exemple: permetre o denegar la connexió per a l’usuari root, canviar el port de connexió i definir la llista d’usuaris autoritzats per a connexió remota.

Per deshabilitar l’accés SSH per a l’usuari root, modificarem el mateix arxiu anterior i afegirem les línies corresponents.

![](img.md/11.png)  

Després, establirem una contrasenya per a l’usuari root amb la comanda `sudo passwd root`.  

![](img.md/12.png)

Després, intentarem connectar-nos per SSH com a root amb `ssh root@ip` i veurem que no ens deixarà.

![](img.md/13.png)

Però, localment, sí que podrem entrar com a root sense problemes.

![](img.md/14.png)

Després, per veure com permetre la connexió remota només a usuaris autoritzats, crearem un nou usuari anomenat `usuari2`.

![](img.md/15.png)

Després, establirem la contrasenya per a aquest usuari amb la comanda `passwd`.

![](img.md/16.png)

Després, haurem d’editar l’arxiu `sshd_config`.

![](img.md/17.png)

I afegirem la línia `AllowUsers` amb el nom de l’usuari que volem autoritzar, en aquest cas `usuari2`. Tot seguit, ho comprovarem.

![](img.md/18.png)

Finalment, reiniciarem el servei SSH per aplicar els canvis.

![](img.md/19.png)

Comprovem que amb l’usuari autoritzat podem connectar-nos per SSH.

![](img.md/20.png)

Després, comprovarem que l’usuari `usuari2` no es pot connectar, ja que no li hem donat permisos.

![](img.md/21.png)

Finalment, com a últim pas, accedirem mitjançant un certificat en lloc d’utilitzar l’usuari i la contrasenya.  


Per fer això, el primer pas serà obrir el PowerShell del client i escriure la següent comanda: ssh-keygen -t rsa

![](img.md/22.png)

Després, entrarem a la carpeta `.ssh` i farem un `ls` per veure els fitxers que conté.

![](img.md/23.png)

Farem un `cat` per llegir el contingut de la clau que s’ha generat.

![](img.md/24.png)

Copiem el contingut de la clau i fem un `scp` cap a `usuari@192.168.56.102`.

![](img.md/25.png)

Després, entrarem dins de l’usuari i farem un `cat` a `/home/usuari/.ssh/id_rsa.pub` per comprovar que hem fet una còpia segura.

![](img.md/26.png)

Després, transferirem la informació a `.ssh/authorized_keys`.

![](img.md/27.png)

Ara veurem que podem entrar sense necessitat d’utilitzar cap contrasenya.

![](img.md/28.png)

# SSH Windows

El primer serà instal·lar l’OpenSSH. Per això executarem la comanda següent: Add-WindowsCapability -Online -Name OpenSSH.Server

![](img.md/29.png)

Després, iniciarem el servei amb la comanda: Start-Service sshd

![](img.md/30.png)

Per fer que s’iniciï automàticament, executarem la comanda: Set-Service -Name sshd -StartupType Automatic

![](img.md/31.png)

Després, comprovarem que des de la màquina Linux podem connectar-nos per SSH a la de Windows.

![](img.md/32.png)  

![](img.md/33.png)


# Tunel

El primer serà instal·lar el Wireshark.

![](img.md/34.png)

Entrem i comprovem que podem veure tot correctament.

![](img.md/35.png)

Entrem a les propietats, a la secció de connexió.

![](img.md/36.png)

A la configuració de LAN, habilitem el servidor proxy i fem clic a “Opcions avançades” per configurar-lo.

![](img.md/37.png)

A la configuració del proxy, establim el SOCKS a `127.0.0.1` i el port a `9876`.

![](img.md/38.png)

Després, connectem el túnel amb la comanda: ssh -D 9876 usuari@10.0.2.15

![](img.md/39.png)

Desactivem el tallafocs perquè es pugui visualitzar.  
Això s’ha de fer abans de crear el túnel:

![](img.md/40.png)

Després, activem el proxy.

Fem una cerca a Google i, tot seguit, obrim el Wireshark; haurem de veure com tot el tràfic passa pel túnel.  

![](img.md/41.png)

- [Tornar al enunciat](readme.md)
