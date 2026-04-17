## General

- CAD ERC: Warnings de Conectivitate ("Only one pin on net"): Exista 26  de avertismente care indica faptul ca pinii microcontrolerului nRF52840 (ex: P0.26, P0.25, P0.24, P0.03 etc) sunt "in aer".

## Debugging

- Marcaj Silkscreen: Test pad-urile (TP) din schema trebuie să aiba etichete clare (ex: TP_SDA, TP_SCL). In raportul ERC, pinii de masa (VSS, EP, CTG) apar conectati la GND, dar trebuie verificat daca au test point-uri accesibile pentru depanare.

## Mechanical & Layout

- Components placement: In fisierul pcb, componentele sunt plasate in afara conturului placii. In acest moment, PCB-ul nu poate fi asamblat în carcasa. Butoanele si mufa USB trebuie să fie pe marginea placii, aliniate cu modelul 3D furnizat.

- Net Connectivity in Layout: Companentele nu sunt plasate in coturul pacii, astfel nu exista conexiuni electrice catre restul circuitului ceea ce duce la 259 de erori critice.
