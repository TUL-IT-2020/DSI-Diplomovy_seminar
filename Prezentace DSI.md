---
marp: true
paginate: true
theme: gaia
tags:
  - slide
  - mermaid
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .hw-diagram {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: relative;
  }
  .hw-diagram img {
    margin: 0.5rem;
  }
  .hw-diagram svg {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
  }
  .flex-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4rem;
  }
  .flex-container img {
    width: 20%;
  }
---

# Redundantní uložiště pro CubeSat
## Návrh praktického řešení

<br><br><br>

Téma: Magisterská práce
Datum: 16. 2. 2025
Autor: Jaroslav Körner
Vedoucí práce: Ing. Lenka Kosková Třísková, Ph.D.

---
## Zadání: 
### Realizace úložiště souborového systému Linux odolného proti poruchám určeného pro CubeSat

Cíle práce:
1. Seznámit se s problematikou malých satelitů - CubeSat.
2. Navrhnout řešení vhodné pro malý satelit na LEO.
3. Provést analýzu FMECA daného řešení.
4. Implementovat a otestovat řešení na demonstračním HW s OS Linux.

---
## Problém: 
### CubeSatů obecně
![bg right 100%](assets/Satelity_statistiky-bez_pozadi.png)

- Okolo 50% misí skončí neúspěchem.
- Až 20% selhání nastane po vynesení na oběžnou dráhu.
  - Selhání elektroniky je nejčastější příčinou.

---
## Problém: 
### úložiště satelitu
Jedno SD/MMC uložiště není dostatečně spolehlivé pro misi CubeSatu.

### Stávající řešení (VZLUSAT-2):
- 2 SD/MMC uložiště
- Modifikovaný Bootloader

![bg right 70%](assets/Boot.png)

---
## Myšlenka

- Nahrazení 2 SD karty za 3 SD karty.
- Vytvoření rozhraní řadiče
  - Ten zprostředkovává přístup k uložišti, jako by to byla jedna karta.
- Implemetnace algoritmu odolného proti chybám čtení poškozených dat.

---
## Možná řešení:

- Softwarové řešení
  - Přidání uCPU a vytvoření SW pro ovládání SD karet
- Hardwarové řešení
  - Vytvoření IP jádra pro FPGA

<div class="flex-container">
  <img src="assets/Integrated%20circuit.png" alt="Integrated Circuit">
  <img src="assets/xilinx-logo.png" alt="Xilinx Logo">
</div>

---
## SW řešení
- Softwarové řešení
- uCPU
  - SPI / SD
- Rozhraní:
  - SPI slave

![bg right 70%](assets/uCPU.png)

---
## HW řešení (IP core)

- IP jádro pro FPGA
- FPGA
  - PMOD - na SD
- Rozhraní:
  - AXI-MM / SPI slave

![bg right 70%](assets/FPGA.png)

---
## Algoritmus:
- Při poškození dat -> majority vote
- Při poškození 1 karty -> přestane z ní číst a odešle data pokud jsou shodná na obou kartách
- Při poškození 2 karet -> přestane z nich číst a odešle data z jedné karty 

![bg right 50%](assets/3SD_2Data.png)

---
## Analýza FMECA

TODO...

---
## Demonstrace na HW

TODO...


---
## Dekuji za pozornost

---
## Zdroje:
- [Statistiky misí: Otto F. Koudelka - Nanosatellites for Technological and Science Missions]()
