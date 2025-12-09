# T05: Accés Remot. Connexió SSH

---

Es creen dues màquines virtuals: una amb Windows i una altra amb Ubuntu.

A la màquina ubuntu, configurem una interfície en NAT i l’altre en Host-Only.

![Captura 1](img/imagen1.png)

---
Modifiquem el netplan. : sudo nano /etc/netplan/50-cloud-init.yaml

![Captura 2](img/imagen2.png)

---
Ara instal·lem el servei ssh. : sudo apt install ssh

![Captura 3](img/imagen3.png)

---
Ens connectem al servei ssh: ssh usuari@192.168.56.101

![Captura 4](img/imagen4.png)

---
Ara comprovem que estem connectats al servidor des de la màquina client. Amb la comanda: hostname

![Captura 5](img/imagen5.png)

---
Li posem contrasenya a l’usuari root: sudo passwd root

![Captura 6](img/imagen6.png)

---
Entrem a l’arxiu /etc/ssh/sshd_config i afegim l’última línia.

sudo nano /etc/ssh/sshd_config

![Captura 7](img/imagen7.png)

---
Entrem a l’usuari root amb “sudo - root” per comprovar que ens deixa i després sortim. 1: su - root 2:exit 

![Captura 8](img/imagen8.png)

---
Intentem fer ssh des de la màquina client cap a l’usuari d’administrador del servidor i veurem com ens denega l’accés: ssh root@192.168.56.101

![Captura 9](img/imagen9.png)

---
Des de la màquina client, introduïm la comanda “ssh-keygen -t rsa” perquè ens generi codis RSA: ssh-keygen -t rsa

![Captura 10](img/imagen10.png)

---
Amb la comanda “ls .\.ssh\” mirarem dins del directori de la carpeta ssh els arxius que hi ha creats, amb la data, el temps, mida i nom: ls .\.ssh\

![Captura 11](img/imagen11.png)
![Captura 12](img/imagen12.png)

---
Dins de la carpeta ssh a la màquina del servidor, creem un arxiu: touch .ssh/authorized_keys

![Captura 13](img/imagen13.png)

---
Copiem la clau que hem generat anteriorment a la carpeta ssh: cat id_rsa.pub >> .ssh/authorized_keys

![Captura 32](img/imagen32.png)

---
Des de la màquina client, comprovem que podem fer ssh sense necessitat de la contrasenya: ssh usuari@192.168.56.101

![Captura 14](img/imagen14.png)

---
Per tenir el servidor OpenSSH hem d’anar a configuració, característiques opcionals i activar el client OpenSSH.

![Captura 15](img/imagen15.png)
![Captura 16](img/imagen16.png)

També podem instal·lar l'OpenSSH des del PowerShell, amb la seguent comanda: 
``
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```
---

Desactivem el firewall, per això buscarem “Windows Defender Firewall” i seleccionarem l’opció de la configuració que es mostra.

![Captura 17](img/imagen17.png)

---
Entrem a xarxa pública.

![Captura 18](img/imagen18.png)

---
Desactivem el Firewall de Microsoft Defender.

![Captura 19](img/imagen19.png)

---
Executem com administrador el PowerShell.

![Captura 20](img/imagen20.png)

---
Iniciem el servei sshd: Start-Service sshd

![Captura 21](img/imagen21.png)

---
Posem aquesta comanda perquè cada vegada que encenem la màquina s’inici el servei.

```
Set-Service -Name sshd -StartupType "Automatic"
```

![Captura 22](img/imagen22.png)

---
Fem ipconfig per veure l’ip de l’interfície Host-Only de la màquina ubuntu per poder-nos connectar.

```
ipconfig
```

![Captura 23](img/imagen23.png)

---
Fem un ping a la màquina client per comprovar que les dos màquines es veuen.

```
ping google.com
```

![Captura 24](img/imagen24.png)

---
Ens connectem a la màquina client.

```
ssh -D 9876 usuari@192.168.56.101
```

![Captura 25](img/imagen25.png)

---
Per configurar el Proxy al Windows, primer hem d’anar al panell de control i a xarxes.


![Captura 26](img/imagen26.png)

---
Anirem a opcions d’internet.

![Captura 27](img/imagen27.png)

---
A dins, anem a connexions i a configuració de LAN.

![Captura 28](img/imagen28.png)

---
Habilitem el servidor proxy, i després anem a opcions avançades.

![Captura 29](img/imagen29.png)

---
Posem l’IP local i el port amb el qual hem connectat el servei ssh.

![Captura 30](img/imagen30.png)

---
Comprovem els paquets en Wireshark.

![Captura 31](img/imagen31.png)

---
- [Tornar al enunciat](README.md)
