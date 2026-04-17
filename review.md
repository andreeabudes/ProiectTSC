## General

- CAD ERC: Warnings de Conectivitate ("Only one pin on net"): Exista 26  de avertismente care indica faptul ca pinii microcontrolerului nRF52840 (ex: P0.26, P0.25, P0.24, P0.03 etc) sunt "in aer".

## Debugging

- Marcaj Silkscreen: Test pad-urile (TP) din schema trebuie să aiba etichete clare (ex: TP_SDA, TP_SCL). În raportul ERC, pinii de masă (VSS, EP, CTG) apar conectați la GND, dar trebuie verificat dacă au test point-uri accesibile pentru depanare.

## Mechanical & Layout

- Components placement: In fisierul bcd, componentele sunt plasate în afara conturului placii. In acest moment, PCB-ul nu poate fi asamblat în carcasa. Butoanele si mufa USB trebuie să fie pe marginea placii, aliniate cu modelul 3D furnizat.

- Net Connectivity in Layout: Companentele nu sunt plasate in coturul pacii, astfel nu exista conexiuni electrice catre restul circuitului ceea ce duce la 259 de erori critice.