# Monitorizare Litieră Pisică

## Introducere
Acest proiect utilizează un modul de greutate și un senzor de gaz pentru a monitoriza activitatea pisicii în litieră, oferind informații despre tipul și frecvența utilizării acesteia. Datele generate sunt transmise către ThingSpeak, o platformă cloud care permite stocarea, analiza și vizualizarea acestora prin grafice, precum și trimiterea de notificări automate în funcție de condiții predefinite. 

Informațiile colectate includ cantitatea de reziduuri lichide și solide eliminate, durata petrecută în litieră și frecvența utilizării. Analizând aceste date, sistemul poate identifica tipul de activitate desfășurat de pisică, trimite notificări pentru curățarea litierei și ajută la detectarea eventualelor probleme de sănătate.

## Descrierea soluției tehnice adoptate

### Detectarea utilizării litierei
Sistemul este construit pe baza unui Raspberry Pi 3 Model B+, la care sunt conectați un modul de greutate și un senzor de gaz. Aceste componente colectează date privind utilizarea litierei, care sunt prelucrate și transmise către ThingSpeak.

- **Intrare în litieră:** O creștere bruscă a greutății (~4 kg), corespunzătoare greutății pisicii.
- **Ieșire din litieră:** O scădere semnificativă a greutății, revenind aproape la valoarea inițială.

### Determinarea tipului de activitate
- **Eliminare de reziduuri lichide (urină):**
  - Senzorul de gaz detectează prezența amoniacului.
  - Se înregistrează o greutate reziduală după ieșirea pisicii.
  - Cantitatea de urină se determină prin diferența dintre greutatea maximă detectată și greutatea pisicii (~4 kg).

- **Eliminare de reziduuri solide (fecale):**
  - Senzorul de gaz nu detectează prezența amoniacului.
  - Se înregistrează o greutate reziduală semnificativă după ieșirea pisicii.

- **Fără activitate semnificativă:**
  - Senzorul de gaz nu detectează gaze.
  - Nu există variații semnificative de greutate, ceea ce sugerează că pisica doar a intrat și a ieșit fără a lăsa reziduuri.

## Utilizarea platformei ThingSpeak
Sistemul utilizează ThingSpeak pentru stocarea, analiza și vizualizarea datelor colectate.

### Caracteristici platformă:
- Suportă trimiterea datelor prin HTTP/MQTT.
- Permite setarea de alerte automate în funcție de condiții predefinite.
- Oferă un API flexibil pentru extragerea și procesarea datelor.
- Versiunea gratuită permite utilizarea a 4 canale și gestionarea a până la 3 milioane de mesaje pe an.

### Utilizarea datelor colectate
- Monitorizarea frecvenței utilizării litierei pentru a detecta schimbări în comportamentul pisicii.
- Evaluarea posibilelor probleme de sănătate.
- Vizualizarea datelor sub formă de grafice pentru interpretare rapidă.

### Alarme și notificări
Sistemul trimite notificări automate prin e-mail când:
- Greutatea reziduală indică acumularea semnificativă de reziduuri solide, sugerând necesitatea curățării litierei.

## Modul de selecție și caracteristicile componentelor
- **Raspberry Pi 3 Model B+:** Mini computer pentru gestionarea senzorilor și colectarea datelor.
- **Modul de greutate:**
  - *Load Cell 5 kg*: Detectează modificările de greutate.
  - *Convertor HX711*: Amplifică semnalul de la senzor și permite conectarea la Raspberry Pi.
- **Senzor de gaz:** *MH MQ-135 Flying Fish* - Detectează gazele specifice, inclusiv amoniacul.
![litiera](https://github.com/user-attachments/assets/6d472b10-e882-47a1-a232-631d1f364ad7)
