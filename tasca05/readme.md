# Tasca 05: SSH (Secure Shell)

A la màquina ubuntu, configurem una interfície en NAT i l’altre en Host-Only.

![Captura 1](img/i1.png)

---
Modifiquem el netplan.

```
sudo nano /etc/netplan/50-cloud-init.yaml
```

![Captura 2](img/i2.png)

---
Instal·lem el servei ssh.

```
sudo apt install ssh
```

![Captura 3](img/i3.png)

---
Ens connectem al servei ssh.

```
ssh usuari@192.168.56.101
```

![Captura 4](img/i4.png)

---
Comprovem que estem connectats al servidor des de la màquina client.

```
hostname
```

![Captura 5](img/i5.png)

---
Li posem contrasenya a l’usuari root.

```
sudo passwd root
```

![Captura 6](img/i6.png)

---
Entrem a l’arxiu /etc/ssh/sshd_config i afegim l’última línia.

```
sudo nano /etc/ssh/sshd_config
```

![Captura 7](img/i7.png)

---
Entrem a l’usuari root amb “sudo - root” per comprovar que ens deixa i després sortim.

```
su - root
exit 
```

![Captura 8](img/i8.png)

---
Intentem fer ssh des de la màquina client cap a l’usuari d’administrador del servidor i veurem com ens denega l’accés.

```
ssh root@192.168.56.101
```
![Captura 9](img/i9.png)

---
Des de la màquina client, introduïm la comanda “ssh-keygen -t rsa” perquè ens generi codis RSA.

```
ssh-keygen -t rsa
```

![Captura 10](img/i10.png)

---
Amb la comanda “ls .\.ssh\” mirarem dins del directori de la carpeta ssh els arxius que hi ha creats, amb la data, el temps, mida i nom.

```
ls .\.ssh\
```
![Captura 11](img/i11.png)
![Captura 12](img/i12.png)

---
Dins de la carpeta ssh a la màquina del servidor, creem un arxiu.

```
touch .ssh/authorized_keys
```

![Captura 13](img/i13.png)

---
Copiem la clau que hem generat anteriorment a la carpeta ssh. 

```
cat id_rsa.pub >> .ssh/authorized_keys
```

![Captura 32](img/i32.png)

---
Des de la màquina client, comprovem que podem fer ssh sense necessitat de la contrasenya.

```
ssh usuari@192.168.56.101
```

![Captura 14](img/i14.png)

---
Per tenir el servidor OpenSSH hem d’anar a configuració, característiques opcionals i activar el client OpenSSH.

![Captura 15](img/i15.png)
![Captura 16](img/i16.png)

També podem instal·lar l'OpenSSH des del PowerShell, amb la seguent comanda:
```
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```
---

Desactivem el firewall, per això buscarem “Windows Defender Firewall” i seleccionarem l’opció de la configuració que es mostra.

![Captura 17](img/i17.png)

---
Entrem a xarxa pública.

![Captura 18](img/i18.png)

---
Desactivem el Firewall de Microsoft Defender.

![Captura 19](img/i19.png)

---
Executem com administrador el PowerShell.

![Captura 20](img/i20.png)

---
Iniciem el servei sshd.

```
Start-Service sshd
```

![Captura 21](img/i21.png)

---
Posem aquesta comanda perquè cada vegada que encenem la màquina s’inici el servei.

```
Set-Service -Name sshd -StartupType "Automatic"
```

![Captura 22](img/i22.png)

---
Fem ipconfig per veure l’ip de l’interfície Host-Only de la màquina ubuntu per poder-nos connectar.

```
ipconfig
```

![Captura 23](img/i23.png)

---
Fem un ping a la màquina client per comprovar que les dos màquines es veuen.

```
ping google.com
```

![Captura 24](img/i24.png)

---
Ens connectem a la màquina client.

```
ssh -D 9876 usuari@192.168.56.101
```

![Captura 25](img/i25.png)

---
Per configurar el Proxy al Windows, primer hem d’anar al panell de control i a xarxes.


![Captura 26](img/i26.png)

---
Anirem a opcions d’internet.

![Captura 27](img/i27.png)

---
A dins, anem a connexions i a configuració de LAN.

![Captura 28](img/i28.png)

---
Habilitem el servidor proxy, i després anem a opcions avançades.

![Captura 29](img/i29.png)

---
Posem l’IP local i el port amb el qual hem connectat el servei ssh.

![Captura 30](img/i30.png)

---
Comprovem els paquets en Wireshark.

![Captura 31](img/i31.png)

---

[Tornar pàgina del projecte](../README.md)

