## FireBot-STS
FireBot je autić-robot dizajniran od strane učenika Srednje tehničke škole Bugojno u svrhu rješavanja problema gašenja požara na miniranim i nepristupačnim prostorima. FireBot opremljen je sa PP aparatom, prskalicom za vodu, dvije kamere, a upravljanje se vrši pomoću Remotexy aplikacije povezane sa Arduinom putem bluetooth modula.

## Članovi tima
Članovi tima su učenici 4. razreda Srednje tehničke škole Bugojno, a to su: Ajdin Letica, Hamza Petrović, Merjem Mešan, Sajra Ajkunić.

## Problem koji rješavamo

U julu 2024. godine, veliki požar zahvatio je 50 ha šume na nepristupačnom terenu kod Bugojna, ugrozivši arheološko nalazište i tražeći intervenciju helikoptera Oružanih snaga BiH. Ljudi ne mogu pristupiti takvim lokacijama bez velikog rizika, a tradicionalne metode gašenja su spore i ograničene. Više informacija: [RTV Slon – Požar kod Bugojna](https://www.rtvslon.ba/pozar-u-blizini-bugojna-jos-aktivan-jutros-stigao-helikopter-oruzanih-snaga-bih/)

## Naš pristup: FireBot

FireBot omogućava daljinsko upravljanje gašenjem požara bez potrebe da ljudi ulaze u opasne zone.

### Ključne karakteristike:
- **Domet upravljanja:** 15 metara
- **Kretanje:** Dva glavna motora (naprijed) + pomoćni točkići (nazad) za stabilnost na neravnom terenu
- **Upravljanje:** Laptop → Remote XY aplikacija → Bluetooth modul → Arduino 
- **Vizuelna kontrola:** Prednja kamera (pokretna u 4 smjera) + zadnja kamera
- **Gašenje požara:**
  - **Prskalica za vodu** (povezana relejem na Arduino, snabdijeva se iz kanistera)
  - **Protivpožarni aparat** (pokreće ga aktuator preko Arduina)

## Tehnologije koje koristimo

- **Raspberry Pi** – omogućava pregled vizuelnog sistema
- **Remote XY** - aplikacija koja šalje komande na arduino preko bluetooth modula
- **Bluetooth modul** - povezuje aplikaciju i arduino 
- **Arduino Mega** – izvršava komande, upravlja motorima, prskalicom i PP aparatom
- **Motori + H-most** – omogućuju kretanje vozila
- **Relej modul** – za aktivaciju pumpe prskalice, reflektora i aktuatora
- **Aktuator** – za aktivaciju PP aparata
- **2 kamere** – prednja pokretna i zadnja statična
- **C/C++ (Arduino IDE)** – za kontrolu hardvera
- **Baterijsko napajanje** – omogućava autonomno kretanje
 
## Funkcionalnosti

- Daljinsko upravljanje iz sigurne zone
- Gašenje požara vodom ili PP aparatom
- Vizuelna povratna informacija putem kamera
- Rotacija prskalice u 4 smjera (gore, dolje, lijevo, desno)
- Stabilno kretanje na neravnom terenu


