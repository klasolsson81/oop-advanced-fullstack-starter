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
| Hur vi mäter | Systemet sparar när en uppgift blev klar och jämför med förfallodatumet (US-6) |

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
| 11 | Vem ska få notisen? | Den som är ansvarig för uppgiften, och Sara. |
| 12 | Vad händer om den ansvariga är sjuk eller på semester? | Då går notisen till Sara i stället. |
| 13 | Vad händer om Sara själv är borta? | Då går hennes notis till en ersättare som hon har utsett. |
| 14 | Vad händer om någon byter mobil utan att uppdatera sitt nummer? | Både SMS och e-post skickas alltid, så mejlet når ändå fram. Ett nytt nummer eller en ny e-postadress måste bekräftas med en kod innan det används. |
| 15 | Vad händer om en notis inte går fram? | Sara får veta det, med vilken uppgift och vilken mottagare det gällde. |
| 16 | Hur snabbt måste listan över försenade uppgifter laddas? | På under 200 ms, även när alla åtta öppnar den samtidigt. |

### Frågor som saknar svar

- Ska notisen skickas på helger, till exempel på söndagen när förfallodagen är en måndag?
- Vad händer om en uppgift skapas, eller får sitt förfallodatum, efter klockan 08:00 dagen innan?
- Vem får notisen om uppgiften inte har någon ansvarig?
- Vem markerar att någon är frånvarande: personen själv eller Sara?
- Vad händer om både Sara och ersättaren är borta, eller om ingen ersättare är utsedd?
- Ska en ny notis skickas om förfallodatumet ändras efter att notisen har gått ut?
- Vart går SMS:et innan ett nytt nummer är bekräftat: till det gamla numret eller ingenstans?
- Vem får veta det om Saras egen notis inte går fram?

## User stories

Storyerna står i prioritetsordning.

### US-1: Påminnelse dagen innan deadline

Som teamledare vill jag att både den ansvariga och jag får en påminnelse via SMS och e-post dagen innan en deadline, så att uppgiften hinner bli klar innan kunden ringer.

- **AK-1.1** Givet en uppgift, när en teammedlem sätts som ansvarig, så är hen ansvarig för uppgiften.
- **AK-1.2** Givet en ej klar uppgift med förfallodatum imorgon, när klockan är 08:00 svensk tid, så får den ansvariga ett SMS och ett mejl med uppgiftens titel och förfallodatum.
- **AK-1.3** Givet en ej klar uppgift med förfallodatum imorgon, när klockan är 08:00 svensk tid, så får Sara ett SMS och ett mejl om uppgiften.
- **AK-1.4** Givet en ej klar uppgift med förfallodatum imorgon, när klockan är 07:59 svensk tid, så har ingen notis skickats.
- **AK-1.5** Givet en klar uppgift med förfallodatum imorgon, när klockan är 08:00 svensk tid, så skickas ingen notis.
- **AK-1.6** Givet en uppgift utan förfallodatum, så skickas aldrig någon notis.
- **AK-1.7** Givet att notisen för en uppgift redan har skickats, när systemet kontrollerar igen samma dag, så skickas ingen ny notis.
- **AK-1.8** Givet att servern kör i UTC och en ej klar uppgift har förfallodatum imorgon, när klockan är 08:00 svensk tid, så skickas notisen.

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

- **AK-3.1** Givet att den ansvariga är markerad som frånvarande, när påminnelsen skickas, så får den ansvariga ingen notis och Sara får den.
- **AK-3.2** Givet att Sara är markerad som frånvarande och har utsett en ersättare, när påminnelsen skickas, så får ersättaren Saras notis.
- **AK-3.3** Givet att både den ansvariga och Sara är markerade som frånvarande, när påminnelsen skickas, så får ersättaren notisen.
- **AK-3.4** Givet att den ansvarigas frånvaro har tagit slut, när nästa påminnelse skickas, så får den ansvariga den igen.

### US-4: Besked när en påminnelse inte når fram

Som teamledare vill jag få veta när en påminnelse inte når fram, så att jag själv kan kontakta den ansvariga innan deadline.

- **AK-4.1** Givet att SMS:et till den ansvariga inte går fram, när påminnelsen skickas, så skickas mejlet ändå.
- **AK-4.2** Givet att SMS:et till den ansvariga inte går fram, så får Sara ett meddelande med uppgiftens titel och mottagarens namn.
- **AK-4.3** Givet att mejlet till den ansvariga inte går fram, så får Sara ett meddelande med uppgiftens titel och mottagarens namn.
- **AK-4.4** Givet att både SMS och mejl går fram, så får Sara inget sådant meddelande.

### US-5: Bekräftade kontaktuppgifter

Som teammedlem vill jag bekräfta ett nytt mobilnummer eller en ny e-postadress med en kod, så att påminnelser inte går till fel person.

- **AK-5.1** Givet att en teammedlem har ändrat sitt mobilnummer men inte bekräftat det, när en påminnelse skickas, så skickas inget SMS till det nya numret.
- **AK-5.2** Givet att en teammedlem har angett rätt kod för sitt nya mobilnummer, när nästa påminnelse skickas, så går SMS:et till det nya numret.
- **AK-5.3** Givet att en teammedlem anger fel kod, så används inte det nya numret.
- **AK-5.4** Givet att en teammedlem har ändrat sin e-postadress men inte bekräftat den, när en påminnelse skickas, så skickas inget mejl till den nya adressen.
- **AK-5.5** Givet att en teammedlem har angett rätt kod för sin nya e-postadress, när nästa påminnelse skickas, så går mejlet till den nya adressen.

### US-6: Andel uppgifter klara i tid

Som teamledare vill jag veta hur stor andel av uppgifterna som blir klara i tid, så att jag ser om vi når målet på 85 %.

- **AK-6.1** Givet en uppgift, när den markeras som klar, så sparas datum och tid då den blev klar.
- **AK-6.2** Givet en uppgift som markerades som klar 23:59 svensk tid på förfallodagen, så räknas den som klar i tid.
- **AK-6.3** Givet en uppgift som markerades som klar dagen efter förfallodagen, så räknas den som klar för sent.
- **AK-6.4** Givet en ej klar uppgift vars förfallodag har passerat, så räknas den som inte klar i tid.
- **AK-6.5** Givet en uppgift utan förfallodatum, så räknas den inte med.
- **AK-6.6** Givet tio uppgifter vars förfallodag har passerat, varav sex blev klara i tid, när andelen räknas fram, så är den 60 %.

## Use case: Påminnelse före deadline

**Aktörer:** den ansvariga, Sara (teamledare), systemet
**Förutsättning:** uppgiften har en ansvarig och är inte klar.
**Mål:** uppgiften blir klar i tid.

### Huvudflöde

1. Klockan 08:00 svensk tid dagen före förfallodagen skickar systemet ett SMS och ett mejl till den ansvariga.
2. Systemet skickar samma påminnelse till Sara.
3. Den ansvariga öppnar appen och ser uppgiften.
4. Den ansvariga gör uppgiften och markerar den som klar senast på förfallodagen.
5. Systemet sparar när uppgiften blev klar och räknar den som klar i tid.

### Alternativa flöden

- **A1 Uppgiften är redan klar.** Vid steg 1 är uppgiften klar. Ingen påminnelse skickas.
- **A2 Uppgiften saknar förfallodatum.** Ingen påminnelse skickas, och uppgiften blir aldrig försenad.
- **A3 Den ansvariga är frånvarande.** I steg 1 får den ansvariga ingen påminnelse. Sara får den i steg 2.
- **A4 Sara är frånvarande.** I steg 2 går påminnelsen till Saras ersättare.
- **A5 Den ansvariga har bytt mobil utan att uppdatera numret.** SMS:et går till det gamla numret, men mejlet når ändå fram i steg 1. Går SMS:et inte fram fortsätter flödet i U1.
- **A6 Det är fortfarande förfallodagen.** Den ansvariga öppnar listan över försenade uppgifter på förfallodagen. Uppgiften finns inte där, eftersom den inte är försenad förrän dagen är slut.
- **A7 Uppgiften blir klar för sent.** I steg 4 markeras uppgiften som klar efter förfallodagen. Fram till dess visas den som försenad. Systemet räknar den som klar för sent.

### Undantagsflöden

- **U1 SMS eller mejl går inte fram.** Den andra kanalen skickas ändå. Sara får ett meddelande om vilken uppgift och vilken mottagare det gällde.
- **U2 API:t svarar inte.** I steg 3 visar appen att uppgifterna inte kunde laddas. Den visar inte en tom lista.
- **U3 Uppgiften har tagits bort av någon annan.** Före steg 1 skickas ingen påminnelse. I steg 4 visar appen att uppgiften inte finns längre.

## Icke-funktionella krav

| Id | Krav | Hur vi mäter |
|---|---|---|
| IFK-1 | Listan över försenade uppgifter laddas på under 200 ms, även när alla åtta öppnar den samtidigt. | Lasttest med 8 samtidiga anrop. |
| IFK-2 | 0 misslyckade anrop mot listan över försenade uppgifter. | Samma lasttest. |
| IFK-3 | Alla datumregler räknas i svensk tid (Europe/Stockholm), oavsett serverns tidszon och även vid byte mellan sommar- och vintertid. | Tester med en fejkad klocka och servern i UTC. |

## Utanför scope

- Påminnelser på förfallodagen eller efter att en uppgift har blivit försenad. Bara dagen innan.
- Andra kanaler än SMS och e-post, till exempel push-notiser.
- Prioritet på uppgifter.
- Påminnelser till hela teamet.
- Att välja egen tid eller kanal för påminnelser.
- Grafer och rapporter för mätvärdet. Vi räknar bara fram andelen.
