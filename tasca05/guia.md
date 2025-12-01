# T05:Connexió via SSH


Primer de tot hem de crear dues màquines virtuals, una amb Windows i l’altra amb Linux (Zorin). Una vegada dins de la màquina virtual de Zorin, executarem les següents comandes per instal·lar SSH:

<img src="img.md/0.png">

I després comprovem que s’ha instal·lat correctament.

<img src="img.md/1.png">

---

Apaguem la màquina i afegim una segona interfície en **Host Only** perquè les màquines es vegin entre elles.

<img src="img.md/2.png">

Arranquem la màquina i editem el netplan per assignar-li una IP a la interfície:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

<img src="img.md/3.png">

Una vegada amb l’arxiu modificat, apliquem els canvis:

```bash
sudo netplan apply
```

I comprovem que s’ha assignat correctament.

<img src="img.md/4.png">

---

Encenem la màquina Windows i afegim la segona interfície en **Host Only** perquè es puguin veure les dues màquines.  

A dins de Windows, ens dirigim a “Ver conexiones de red” per editar la configuració de l'adaptador i comprovem que s’ha assignat correctament.

<img src="img.md/5.png">

I comprovem que **s’ha assignat correctament** i que es **veuen entre elles**.

<img src="img.md/6.png">

---

Un cop completades les passes anteriors, ja ens podem connectar a la màquina Ubuntu des de la terminal de Windows amb:

```bash
ssh usuari@192.168.56.200
```

Ens apareix un missatge de seguretat ja que és la primera vegada que ens connectem, i ens demana confirmar l'autenticitat de la clau pública.  

<img src="img.md/7.png">

L’acceptem i ens connectem correctament, apareixent el terminal de la màquina Ubuntu.

<img src="img.md/8.png">

---

Un cop dins de la màquina a través de SSH, podem editar l’arxiu de configuració:

```bash
sudo nano /etc/ssh/sshd_config
```
<img src="img.md/9.png">

Per exemple, podem:
- Permetre o no connexions de root.
- Canviar el port de connexió (per defecte el 22).
- Fer una llista d’usuaris autoritzats per connexió remota.

Per deshabilitar l'accés SSH per a l'usuari root, modifiquem l’arxiu `/etc/ssh/sshd_config` i canviem les següents línies.

<img src="img.md/10.png">

Comprovem que només es pot iniciar sessió en root localment i no per SSH. Per a fer-ho haurem de canviar la contrasenya del root amb la següent comanda:

```bash
sudo passwd root
```

<img src="img.md/11.png">

Si intentem fer SSH com a root, no ens deixarà.  

<img src="img.md/12.png">

Però podem iniciar sessió de manera local sense problemes.

<img src="img.md/13.png">

---

Per permetre connexió remota només a usuaris autoritzats:

Creem un nou usuari `usuari2`:

```bash
sudo useradd -m -s /bin/bash usuari2
```

<img src="img.md/14.png">

Assignem una contrasenya:

```bash
sudo passwd usuari2
```

Afegim l'usuari autoritzat a l’arxiu SSH:

```bash
sudo nano /etc/ssh/sshd_config
```

Afegim la línia:

```text
AllowUsers usuari
```

<img src="img.md/15.png">

Reiniciem el servei per aplicar els canvis:

```bash
sudo systemctl restart ssh
```

Ara, si intentem iniciar sessió amb `usuari2` no podrem, mentre que amb l’usuari `usuari` sí que funciona.

<img src="img.md/16.png">
<img src="img.md/17.png">
