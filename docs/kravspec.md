# Kravspec: Deadlines och påminnelser

## Problemet

> Vi är ett team på åtta personer som använder er uppgiftsapp varje dag. Problemet är att vi missar
> deadlines hela tiden, och ingen märker det förrän kunden ringer och är arg.
>
> /Sara, teamledare

> Appen säger att saker är försenade samma dag som de ska vara klara. Klockan nio på morgonen står det
> att "Skicka offert" är en dag sen, fast den ska vara klar idag. Folk har slutat lita på listan.
>
> /Sara, buggrapport två dagar efter demon

## Mål

| Del | Värde |
|---|---|
| Mätvärde | Andel uppgifter som blir klara i tid |
| Nuläge | Ungefär 60 % (6 av 10) |
| Mål | 85 % |
| Tidsram | Inom fyra veckor |
| Hur vi mäter | Systemet sparar när en uppgift blev klar och jämför med förfallodatumet (US-5) |

En uppgift är klar i tid om den markeras som klar senast 23:59 svensk tid på förfallodagen.

## Frågor och svar

| # | Fråga | Svar |
|---|---|---|
| 1 | Vad händer idag när en deadline missas? | Ingen märker det förrän kunden ringer och är arg. |
| 2 | Hur många använder appen, och hur ofta? | Åtta personer, varje dag. |
| 3 | Vad är fel med listan över försenade uppgifter? | Den visar uppgifter som försenade samma dag som de ska vara klara. Folk har slutat lita på den. |
| 4 | När räknas en uppgift som försenad? | När förfallodagen är slut. En uppgift med förfallodatum idag är inte försenad klockan 23:59 svensk tid. |
| 5 | Kan en uppgift som är klar vara försenad? | Nej, aldrig, oavsett datum. |
| 6 | Hur många uppgifter blir klara i tid idag? | Ungefär 6 av 10. |
| 7 | Hur vet du att vi har lyckats? | När 85 % av uppgifterna blir klara i tid, inom fyra veckor. |
| 8 | Vad är viktigast för dig? | Notiser. |
| 9 | Hur vill du få notiserna? | Både SMS och e-post. |
| 10 | När ska notisen komma? | En dag innan deadline, klockan 08:00 svensk tid. |
| 11 | Ska notisen skickas på helger? | Nej. Den skickas sista vardagen före förfallodagen, så en uppgift som ska vara klar på måndag ger en notis på fredagen. |
| 12 | Vad händer om en uppgift läggs in efter att notisen skulle ha skickats? | Då skickas notisen direkt, om förfallodagen inte har passerat. |
| 13 | Ska en ny notis skickas om förfallodatumet ändras efter att notisen har gått ut? | Ja, inför det nya förfallodatumet. |
| 14 | Vem ska få notisen? | Den som är ansvarig för uppgiften, och Sara. |
| 15 | Vad händer om uppgiften inte har någon ansvarig? | En uppgift med förfallodatum kan inte sparas utan ansvarig. |
| 16 | Vad händer om den ansvariga är sjuk eller på semester? | Då går notisen till Sara i stället. |
| 17 | Vem markerar att någon är frånvarande? | Personen själv. |
| 18 | Vad händer om Sara själv är borta? | Då går hennes notis till en ersättare som hon har utsett. |
| 19 | Vad händer om både Sara och ersättaren är borta, eller om ingen ersättare är utsedd? | Då får hela teamet notisen. |
| 20 | Vad händer om någon byter mobil utan att uppdatera sitt nummer? | Både SMS och e-post skickas alltid, så mejlet når ändå fram. |
| 21 | Ska ett nytt mobilnummer eller en ny e-postadress bekräftas med kod? | Nej. |
| 22 | Vad händer om en notis inte går fram? | Sara får veta det, med vilken uppgift och vilken mottagare det gällde. |
| 23 | Vad händer om Saras egen notis inte går fram? | Då får hennes ersättare veta det. |
| 24 | Hur snabbt måste listan över försenade uppgifter laddas? | På under 200 ms, även när alla åtta öppnar den samtidigt. |

### Frågor som saknar svar

- Räknas helgdagar, som juldagen eller midsommarafton, som helg?
- En uppgift läggs in på en lördag med förfallodatum måndag. Ska notisen skickas direkt, trots att det är helg?
- Vad händer med befintliga uppgifter som har förfallodatum men ingen ansvarig?

## User stories

### US-1: Påminnelse före deadline

Som teamledare vill jag att både den ansvariga och jag får en påminnelse via SMS och e-post vardagen före en deadline, så att uppgiften hinner bli klar innan kunden ringer.

- **AK-1.1** Givet en ny uppgift med förfallodatum men utan ansvarig, när den sparas, så sparas den inte och appen visar att en ansvarig krävs.
- **AK-1.2** Givet en ej klar uppgift med förfallodatum torsdag, när klockan är 08:00 svensk tid på onsdagen, så får den ansvariga ett SMS och ett mejl med uppgiftens titel och förfallodatum.
- **AK-1.3** Givet en ej klar uppgift med förfallodatum torsdag, när klockan är 08:00 svensk tid på onsdagen, så får Sara ett SMS och ett mejl om uppgiften.
- **AK-1.4** Givet en ej klar uppgift med förfallodatum torsdag, när klockan är 07:59 svensk tid på onsdagen, så har ingen notis skickats.
- **AK-1.5** Givet en ej klar uppgift med förfallodatum måndag, när klockan är 08:00 svensk tid på fredagen, så skickas notisen.
- **AK-1.6** Givet en klar uppgift med förfallodatum torsdag, när klockan är 08:00 svensk tid på onsdagen, så skickas ingen notis.
- **AK-1.7** Givet en uppgift utan förfallodatum, så skickas aldrig någon notis.
- **AK-1.8** Givet att notisen för en uppgift har skickats och förfallodatumet inte har ändrats, när systemet kontrollerar igen, så skickas ingen ny notis.
- **AK-1.9** Givet att servern kör i UTC och en ej klar uppgift har förfallodatum torsdag, när klockan är 08:00 svensk tid på onsdagen, så skickas notisen.

### US-2: Rätt lista över försenade uppgifter

Som teammedlem vill jag se vilka uppgifter som är försenade, så att jag kan agera innan kunden ringer.

- **AK-2.1** Givet en uppgift med förfallodatum idag, när klockan är 23:59 svensk tid, så är den inte försenad.
- **AK-2.2** Givet en uppgift som är klar, så är den aldrig försenad, oavsett datum.
- **AK-2.3** Givet uppgiften "Skicka offert" med förfallodatum idag, när klockan är 09:00 svensk tid, så finns den inte i listan över försenade uppgifter.
- **AK-2.4** Givet en ej klar uppgift med förfallodatum igår, när klockan är 00:00 svensk tid idag, så är den försenad.
- **AK-2.5** Givet en uppgift utan förfallodatum, så är den aldrig försenad.
- **AK-2.6** Givet försenade och ej försenade uppgifter, när uppgiftslistan visas, så står de försenade överst.
- **AK-2.7** Givet att inga uppgifter är försenade, när listan över försenade uppgifter hämtas, så är den tom.
- **AK-2.8** Givet att API:t inte svarar, när listan ska visas, så visar appen att den inte kunde laddas, och inte en tom lista.

### US-3: Påminnelse när någon är frånvarande

Som teamledare vill jag att påminnelsen når någon även när den ansvariga eller jag är borta, så att ingen deadline missas för att någon är sjuk eller på semester.

- **AK-3.1** Givet en teammedlem, när hen markerar sig själv som frånvarande, så räknas hen som frånvarande.
- **AK-3.2** Givet en teammedlem, när hen försöker markera någon annan som frånvarande, så går det inte.
- **AK-3.3** Givet att den ansvariga är frånvarande, när påminnelsen skickas, så får den ansvariga ingen notis och Sara får den.
- **AK-3.4** Givet att Sara är frånvarande och har utsett en ersättare, när påminnelsen skickas, så får ersättaren Saras notis.
- **AK-3.5** Givet att både den ansvariga och Sara är frånvarande, när påminnelsen skickas, så får ersättaren notisen.
- **AK-3.6** Givet att Sara är frånvarande och inte har utsett någon ersättare, när påminnelsen skickas, så får alla i teamet som inte är frånvarande notisen.
- **AK-3.7** Givet att både Sara och ersättaren är frånvarande, när påminnelsen skickas, så får alla i teamet som inte är frånvarande notisen.
- **AK-3.8** Givet att den ansvarigas frånvaro har tagit slut, när nästa påminnelse skickas, så får den ansvariga den igen.

### US-4: Besked när en påminnelse inte når fram

Som teamledare vill jag få veta när en påminnelse inte når fram, så att jag själv kan kontakta den ansvariga innan deadline.

- **AK-4.1** Givet att SMS:et till den ansvariga inte går fram, när påminnelsen skickas, så skickas mejlet ändå.
- **AK-4.2** Givet att SMS:et till den ansvariga inte går fram, så får Sara ett meddelande med uppgiftens titel och mottagarens namn.
- **AK-4.3** Givet att mejlet till den ansvariga inte går fram, så får Sara ett meddelande med uppgiftens titel och mottagarens namn.
- **AK-4.4** Givet att SMS:et eller mejlet till Sara inte går fram, så får Saras ersättare ett meddelande med uppgiftens titel.
- **AK-4.5** Givet att både SMS och mejl går fram, så skickas inget sådant meddelande.

### US-5: Andel uppgifter klara i tid

Som teamledare vill jag veta hur stor andel av uppgifterna som blir klara i tid, så att jag ser om vi når målet på 85 %.

- **AK-5.1** Givet en uppgift, när den markeras som klar, så sparas datum och tid då den blev klar.
- **AK-5.2** Givet en uppgift som markerades som klar 23:59 svensk tid på förfallodagen, så räknas den som klar i tid.
- **AK-5.3** Givet en uppgift som markerades som klar dagen efter förfallodagen, så räknas den som klar för sent.
- **AK-5.4** Givet en ej klar uppgift vars förfallodag har passerat, så räknas den som inte klar i tid.
- **AK-5.5** Givet en uppgift utan förfallodatum, så räknas den inte med.
- **AK-5.6** Givet tio uppgifter vars förfallodag har passerat, varav sex blev klara i tid, när andelen räknas fram, så är den 60 %.

### US-6: Påminnelse när förfallodatumet sätts sent eller ändras

Som teamledare vill jag att påminnelsen kommer även när en uppgift läggs in sent eller får ett nytt förfallodatum, så att ingen uppgift blir utan påminnelse.

- **AK-6.1** Givet att klockan är 10:00 svensk tid på onsdagen, när en uppgift sparas med förfallodatum torsdag, så skickas notisen direkt.
- **AK-6.2** Givet att klockan är 10:00 svensk tid på torsdagen, när en uppgift sparas med förfallodatum torsdag, så skickas notisen direkt.
- **AK-6.3** Givet att klockan är 10:00 svensk tid på onsdagen, när förfallodatumet för en befintlig uppgift ändras till torsdag, så skickas notisen direkt.
- **AK-6.4** Givet en uppgift som sparas med ett förfallodatum som redan har passerat, så skickas ingen notis.
- **AK-6.5** Givet att notisen för en uppgift med förfallodatum torsdag har skickats, när förfallodatumet ändras till torsdag veckan efter, så skickas en ny notis klockan 08:00 svensk tid onsdagen före det nya datumet.

## Use case: Påminnelse före deadline

**Aktörer:** den ansvariga, Sara (teamledare), systemet
**Förutsättning:** uppgiften är inte klar. En uppgift med förfallodatum har alltid en ansvarig.
**Mål:** uppgiften blir klar i tid.

### Huvudflöde

1. Klockan 08:00 svensk tid sista vardagen före förfallodagen skickar systemet ett SMS och ett mejl till den ansvariga.
2. Systemet skickar samma påminnelse till Sara.
3. Den ansvariga öppnar appen och ser uppgiften.
4. Den ansvariga gör uppgiften och markerar den som klar senast på förfallodagen.
5. Systemet sparar när uppgiften blev klar och räknar den som klar i tid.

### Alternativa flöden

- **A1 Uppgiften är redan klar.** Vid steg 1 är uppgiften klar. Ingen påminnelse skickas.
- **A2 Uppgiften saknar förfallodatum.** Ingen påminnelse skickas, och uppgiften blir aldrig försenad.
- **A3 Förfallodagen är en måndag.** Påminnelsen i steg 1 skickas på fredagen.
- **A4 Uppgiften läggs in efter tiden för steg 1.** Påminnelsen skickas direkt när uppgiften sparas, om förfallodagen inte har passerat.
- **A5 Förfallodatumet ändras.** Flödet börjar om från steg 1 med det nya datumet.
- **A6 Den ansvariga är frånvarande.** I steg 1 får den ansvariga ingen påminnelse. Sara får den i steg 2.
- **A7 Sara är frånvarande.** I steg 2 går påminnelsen till Saras ersättare. Finns ingen ersättare, eller är ersättaren också borta, går den till alla i teamet som inte är frånvarande.
- **A8 Den ansvariga har bytt mobil utan att uppdatera numret.** SMS:et går till det gamla numret, men mejlet når ändå fram i steg 1. Går SMS:et inte fram fortsätter flödet i U1.
- **A9 Det är fortfarande förfallodagen.** Den ansvariga öppnar listan över försenade uppgifter på förfallodagen. Uppgiften finns inte där, eftersom den inte är försenad förrän dagen är slut.
- **A10 Uppgiften blir klar för sent.** I steg 4 markeras uppgiften som klar efter förfallodagen. Fram till dess visas den som försenad. Systemet räknar den som klar för sent.

### Undantagsflöden

- **U1 SMS eller mejl går inte fram.** Den andra kanalen skickas ändå. Sara får ett meddelande om vilken uppgift och vilken mottagare det gällde. Gäller det Saras egen notis får hennes ersättare meddelandet.
- **U2 API:t svarar inte.** I steg 3 visar appen att uppgifterna inte kunde laddas. Den visar inte en tom lista.
- **U3 Uppgiften har tagits bort av någon annan.** Före steg 1 skickas ingen påminnelse. I steg 4 visar appen att uppgiften inte finns längre.

## Icke-funktionella krav

| Id | Krav | Hur vi mäter |
|---|---|---|
| IFK-1 | Listan över försenade uppgifter laddas på under 200 ms, även när alla åtta öppnar den samtidigt. | Lasttest med 8 samtidiga anrop. |
| IFK-2 | 0 misslyckade anrop mot listan över försenade uppgifter. | Samma lasttest. |
| IFK-3 | Alla datumregler räknas i svensk tid (Europe/Stockholm), oavsett serverns tidszon och även vid byte mellan sommar- och vintertid. | Tester med en fejkad klocka och servern i UTC. |

## Utanför scope

- Påminnelser på förfallodagen eller efter att en uppgift har blivit försenad. Bara sista vardagen före.
- Andra kanaler än SMS och e-post, till exempel push-notiser.
- Prioritet på uppgifter.
- Att hela teamet får varje påminnelse. Teamet får den bara när varken Sara eller hennes ersättare är på plats.
- Att välja egen tid eller kanal för påminnelser.
- Bekräftelse av mobilnummer och e-postadress med kod.
- Grafer och rapporter för mätvärdet. Vi räknar bara fram andelen.
