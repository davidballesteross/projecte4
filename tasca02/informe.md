# Sistema de Còpies de Seguretat  
**Client:** Muntatges i Serveis Tècnics SL

## Introducció
El client **Muntatges i Serveis Tècnics SL** necessita una política de còpies de seguretat robusta i fiable.  
Per donar resposta a aquesta necessitat, s’ha dissenyat i implementat un sistema de backups dividit en dues parts:

- Còpia de seguretat en equips **Windows 11** utilitzant **Duplicati**.
- Còpia de seguretat en un **servidor Ubuntu Linux** utilitzant **Duplicity** i **cron**.

---

## Part 1: Còpia de seguretat dels equips clients Windows

### Creació de la VM amb Windows 11
Configuració inicial de la màquina virtual amb Windows 11.  
**Objectiu:** Disposar d’un entorn Windows que simuli un client real.

### Afegir un segon disc de 10 GB
S’afegeix un disc dur addicional a la màquina virtual.  
**Objectiu:** Simular un dispositiu local dedicat exclusivament a còpies de seguretat.

![solucio](/tasca02/img/cap1.png)
![solucio](/tasca02/img/cap2.png)
![solucio](/tasca02/img/cap3.png)
![solucio](/tasca02/img/cap4.png)
![solucio](/tasca02/img/cap5.png)
![solucio](/tasca02/img/cap6.png)
![solucio](/tasca02/img/cap7.png)

### Instal·lació de Duplicati
Descàrrega i instal·lació de l’eina Duplicati.  
**Objectiu:** Disposar d’una eina de còpies de seguretat programades i xifrades.

![solucio](/tasca02/img/cap8.png)

### Primera execució de Duplicati
Accés a la interfície web de Duplicati.  
**Objectiu:** Configurar els plans de còpia de seguretat.

![solucio](/tasca02/img/cap9.png)

### Configuració del destí de còpia (disc secundari)
Definició del disc addicional com a destí de les còpies.  
**Objectiu:** Verificar que el disc secundari funciona com a repositori local.

![solucio](/tasca02/img/cap10.png)
![solucio](/tasca02/img/cap11.png)
![solucio](/tasca02/img/cap12.png)
![solucio](/tasca02/img/cap13.png)
![solucio](/tasca02/img/cap14.png)
![solucio](/tasca02/img/cap15.png)

### Configuració del destí de còpia (Google Drive)
Connexió amb un compte de Google Drive.  
**Objectiu:** Complir la regla **3-2-1**, mantenint una còpia fora de l’empresa.

![solucio](/tasca02/img/cap16.png)
![solucio](/tasca02/img/cap17.png)
![solucio](/tasca02/img/cap18.png)
![solucio](/tasca02/img/cap19.png)

---

## Part 2: Còpia de seguretat del servidor Linux

![solucio](/tasca02/img/cap20.png)

### Detecció del disc amb `lsblk`
Identificació del disc **/dev/sdb** de 10 GB.  
**Objectiu:** Localitzar el dispositiu destinat a les còpies de seguretat.

![solucio](/tasca02/img/cap21.png)

### Particionament amb `parted`
Creació d’una partició amb sistema de fitxers XFS.  
**Objectiu:** Utilitzar un sistema de fitxers robust per a backups.

![solucio](/tasca02/img/cap22.png)

### Format amb `mkfs.xfs`
Formatatge de la partició creada.  
**Objectiu:** Preparar el disc per emmagatzemar dades.

![solucio](/tasca02/img/cap23.png)

### Muntatge del disc a `/media/backup`
Creació i muntatge del punt de muntatge.  
**Objectiu:** Definir el destí de les còpies de seguretat.

![solucio](/tasca02/img/cap24.png)

### Instal·lació de `duplicity` i `xfsprogs`
Instal·lació dels paquets necessaris.  
**Objectiu:** Disposar de les eines imprescindibles per gestionar backups.

![solucio](/tasca02/img/cap25.png)
![solucio](/tasca02/img/cap28.png)

### Creació d’usuaris de prova
Creació dels usuaris `usuari1` i `usuari2`.  
**Objectiu:** Simular un entorn multiusuari real.

![solucio](/tasca02/img/cap26.png)
![solucio](/tasca02/img/cap29.png)
![solucio](/tasca02/img/cap30.png)

### Creació de fitxers de prova
Generació de fitxers de 10 MB amb `fallocate`.  
**Objectiu:** Validar el funcionament de les còpies.

![solucio](/tasca02/img/cap31.png)

### Primera còpia completa amb Duplicity
Còpia completa del directori `/home`.  
**Objectiu:** Establir el punt inicial de la cadena de còpies.

![solucio](/tasca02/img/cap27.png)
![solucio](/tasca02/img/cap32.png)
![solucio](/tasca02/img/cap33.png)

### Restauració de fitxers
Prova de restauració de fitxers eliminats.  
**Objectiu:** Comprovar que les còpies són recuperables.

![solucio](/tasca02/img/cap35.png)

### Còpia incremental
Creació d’un nou fitxer i execució d’un backup incremental.  
**Objectiu:** Verificar que només es copien els canvis.

![solucio](/tasca02/img/cap37.png)

### Estat de la col·lecció (`collection-status`)
Visualització de còpies completes i incrementals.  
**Objectiu:** Validar la coherència de la cadena de backups.

![solucio](/tasca02/img/cap34.png)

### Script `fullbackup.sh`
Script per automatitzar la còpia completa.  
**Objectiu:** Facilitar l’execució del backup complet.

![solucio](/tasca02/img/cap36.png)

### Script `incrementalbackup.sh`
Script per automatitzar les còpies incrementals.  
**Objectiu:** Optimitzar l’ús d’espai i temps.

![solucio](/tasca02/img/cap39.png)
![solucio](/tasca02/img/cap40.png)

### Configuració de `cron`
Programació de les tasques automàtiques.  
**Objectiu:** Garantir còpies diàries sense intervenció manual.

![solucio](/tasca02/img/cap40.png)

### Verificació dels fitxers de backup
Comprovació dels fitxers `.difftar.gpg` i manifests.  
**Objectiu:** Evidenciar que les còpies s’han realitzat correctament.

![solucio](/tasca02/img/cap41.png)
![solucio](/tasca02/img/cap42.png)

### Restauració puntual d’un fitxer
Recuperació del fitxer `fitxer1.bin`.  
**Objectiu:** Validar la restauració selectiva de dades.

![solucio](/tasca02/img/cap43.png)
![solucio](/tasca02/img/cap44.png)

---
