# Cronometru Digital - Proiect Practica

Acesta este proiectul meu realizat in cadrul stagiului de practica din anul 2 de facultate. Reprezinta un cronometru digital proiectat in KiCad, capabil sa numere crescator si descrescator (0-99), afisand valorile pe doua display-uri cu 7 segmente.

![Randare 3D a proiectului](img/pcb_3d1.png)

### Descriere Tehnica

Circuitul a fost gandit modular, avand la baza urmatoarele etaje:
1.  **Semnal de ceas:** Generat de un **NE555** configurat ca oscilator astabil.
2.  **Numarare:** Se realizeaza cu doua numaratoare binare sincrone pe 4 biti, model **74LS193** (U7 si U8). Acestea permit numararea in ambele sensuri (UP/DOWN).
3.  **Decodificare si Afisare:** Semnalul binar este convertit pentru afisajul cu 7 segmente folosind decodificatoare **CD4511** (U6 si U10).

**Alte componente logice utilizate:**
* **74LS73 (U2):** Flip-flop JK pentru control.
* **74LS08 (U3):** Porti SI (AND).
* **CD4071 (U4):** Porti SAU (OR).

### Schema Electrica
Schema finala, care include corectiile necesare pentru buna functionare:

![Schema electrica KiCad](img/schema.png)

### Iteratia v1.0 si Rezolvarea Problemelor (Debug)

Dupa producerea PCB-ului si lipirea componentelor, am identificat o eroare in schema initiala: pinul 11 (Load) al numaratoarelor nu era conectat la 5V, iar condensatorul C4 (47uF) nu era legat la rezistenta R17.

**Solutia (The Fix):**
Am remediat problema direct pe placa prin adaugarea a doua fire ("jumpers") pe stratul de jos (Bottom Layer).
* Firele rosii vizibile in poza de mai jos asigura conexiunea pinilor la 5V si traseul corect pentru condensator.
* Dupa aceasta modificare, circuitul functioneaza perfect conform specificatiilor.

| Fata Componente | Spate (Fix-ul cu fire rosii) |
|:---:|:---:|
| ![PCB Fata](img/pcb_fata_2.jpg) | ![PCB Spate cu fire](img/pcb_spate_2.jpg) |

### Lista de Materiale (BOM)

Costul total al proiectului (componente + PCB + transport) a fost de aproximativ 140 Lei.

| Referinta | Componenta | Detalii |
|:---|:---|:---|
| U9 | **NE555P** | Timer precizie |
| U7, U8 | **SN74LS193N** | Numarator binar sincron UP/DOWN |
| U6, U10 | **CD4511BE** | Decodificator BCD la 7 segmente |
| U5, U11 | **HDSP-5601** | Afisaj 7 segmente |
| U1 | **L7805** | Regulator tensiune 5V |
| U2 | **SN74LS73AN** | Dual JK Flip-Flop |
| U3 | **SN74LS08N** | Quad 2-Input AND Gate |
| U4 | **CD4071BE** | Quad 2-Input OR Gate |
| - | **Baterie 9V** | Sursa de alimentare |

### Structura Repo
* `/kicad` - Fisierele sursa ale proiectului (.sch, .kicad_pcb)
* `/img` - Imagini si randari
