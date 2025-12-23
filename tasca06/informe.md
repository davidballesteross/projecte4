# Guia d'Accés i Configuració d'Escriptori Remot 

Aquesta guia documenta el procés de configuració i connexió mitjançant RDP (Remote Desktop Protocol) entre un client (usuari final) i un suport tècnic. El procediment s'ha realitzat seguint les directrius de la tasca **T06: Accés remot. Escriptori remot (RDP)**.

---

## Objectiu

Permetre la connexió remota entre un equip client i un equip de suport, per tal de visualitzar i controlar l'escriptori remot i resoldre incidències en temps real.

---

## Pas 1: Habilitar l'Escriptori Remot a l'Equip Client (Windows)

- Accedir a **Configuració → Sistema → Escriptori remot**.
- Activar l’opció **Escriptori remot**.
- Afegir usuaris amb accés remot (per exemple, l'usuari *David*).
- Confirmar amb **Acceptar**.

![solucio](/tasca06/img/cap1.png)
![solucio](/tasca06/img/cap2.png)
![solucio](/tasca06/img/cap3.png)
![solucio](/tasca06/img/cap4.png)

---

## Pas 2: Configurar l'Escriptori Remot a l'Equip de Suport (GNU/Linux amb Zorin/GNOME)

- Obrir **Configuració → Compartir**.
- Activar **Compartició d'escriptori** i **Inici de sessió remot**.
- Configurar els detalls de connexió:
  - **Nom de l'equip:** `usuari-VirtualBox`
  - **Port RDP:** `3389` (per defecte) o `3390` (segons configuració)
  - **Usuari i contrasenya locals**

![solucio](/tasca06/img/cap5.png)
![solucio](/tasca06/img/cap6.png)
![solucio](/tasca06/img/cap7.png)
![solucio](/tasca06/img/cap8.png)
![solucio](/tasca06/img/cap9.png)
![solucio](/tasca06/img/cap10.png)
![solucio](/tasca06/img/cap11.png)

---
