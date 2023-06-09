---
title: 1.Bakgrund
publishDate: 7 Jun 2023
description: My graduation thesis from Chas Academy
---

## <a name="top"></a> Table of Contents

1. [Inledning](#Inledning)

   1.1 [Bakgrund](#Bakgrund)

   1.2 [Syfte](#Syfte)

   1.3 [Avgränsning](#Avgränsning)

---

# <a name="Inledning"></a>Inledning

Projektet kommer av att jag under min praktik såg möjligheten att utveckla en så kallad “Dashboard” som en del av en startsida för en inloggad användare. Idéen med denna funktion är att ge den inloggade användaren en informativ överblicksbild av appens tjänster och administrativa möjligheter.
<br />
<br />

Utmaningen för mig som utvecklare är att bygga denna funktion:

-  Läsbar
-  Skalbar
-  Och med återanvändbart modulärt tänk
   <br />
   <br />

För att skapa förutsättningar för framtida ändringar, utbyggnad och underhåll.

<br />
<br />
<br />

![Super wide](/assets/figma1.jpg)

[[Top]](#top)
<br />
<br />
<br />

## <a name="Bakgrund"></a>Bakgrund

En av de mest intressanta delarna med webbutveckling och de webbprojekt som jag hittills arbetat i och sett, är skillnaden i hur effektivt och modulärt byggda de är. Har sedan man började i skolan verkligen börjat se komplexiteten i webbproduktioner och även hur viktigt det är att modularisera detta, för att på bästa sätt “skiva elefanten” och separera segment som funktioner och moduler/komponenter i mindre beståndsdelar.
<br />
<br />
Fördelarna är många och uppenbara:

-  Enklare för utvecklare att hitta och arbeta i strukturen.
-  Slippa skriva upprepad kod och många gånger uppfinna hjulet på nytt på flera ställen i projektet.
-  Mindre kodbas och mer konsekvent kod och produktion.
-  Lättare att testa och förstå mindre kundsegment.
-  Flexibel återanvändning av komponenter med mera.

<br />
<br />

Jag har genom utbildningen lite burit med mig att React är något att försöka bli bekväm med, men även att det är det biblioteket “som gäller”. Även om det under senare tid har dykt upp nya liknande bibliotek i stor utsträckning. För att citera en barndomskamrat som jobbar i branchen.

> Om du kan React, så har du jobb sen.

Samtidigt är det ett komplext bibliotek med fri struktur på gott och ont, och det finns många sätt att uppnå samma mål med sin kod.

Jag har upplevt att man i komplexiteten i ett så flexibelt bibliotek måste hitta mönster att följa i sitt användande. Gångbara mönster att följa, bli trygg med och återanvända för att inte uppfinna hjulet på nytt varje gång man sätter sig med React.
I konceptet och fördelarna med att hela tiden försöka jobba med modularisering ingår även att försöka skriva så kallad “ren kod”. Regler för detta kan sammanfattas med konceptet kallat S.O.L.I.D.

[[Top]](#top)
<br />
<br />

## <a name="Syfte"></a>Syfte

Har tagit tillfället i akt att sätta målet för projektet till att försöka öka min personliga utveckling i att träna på effektiv modularitet och struktur. Min förmåga att återanvända kod och funktioner, få bättre känsla för överblick, struktur och möjligheter att jobba smartare/snabbare och förhoppningsvis med större trygghet.

> Ipsum et cupidatat mollit exercitation enim duis sunt irure aliqua reprehenderit mollit. Pariatur Lorem pariatur laboris do culpa do elit irure. Eiusmod amet nulla voluptate velit culpa et aliqua ad reprehenderit sit ut.

Dashboard:en bör kunna utformas olika för varje användarroll. Jag har förutom detta begränsat mitt arbete till att främst undersöka och ta fram en lämplig fil- och datastruktur för ändamålet. De enskilda widgets som skulle vara intressanta att göra har lite fått stå åt sidan och har inte hunnit göras klara pga tidsbrist eller att projektet i stort inte är utbyggt nog för att registrera viss nödvändig användardata.

En önskan från företaget var om användaren skulle kunna lägga till och ta bort Widgets efter eget tycke och smak och spara denna layout för användaren. Detta skulle vara grundfunktionalitet som så det fick viss prioritering.

[[Top]](#top)
<br />
<br />

## <a name="Avgränsning"></a>Avgränsning

Projektet är skrivet i Next.js som är ett React-ramverk. Projektet innehåller ett antal “widgets” (komponenter, moduler) för olika info för respektive användarroll. Någon widget kan vara mer unik för respektive användarroll. Andra kan påminna om varandra men inneha olika data. En användare kan ha 3 olika roller:

<br />

### En användare registreras med en av följande användarroller

-  Inköpare
-  Återförsäljare
-  Bud

Dashboard:en bör kunna utformas olika för varje användarroll. Jag har förutom detta begränsat mitt arbete till att främst undersöka och ta fram en lämplig fil- och datastruktur för ändamålet. De enskilda widgets som skulle vara intressanta att göra har lite fått stå åt sidan och har inte hunnit göras klara pga tidsbrist eller att projektet i stort inte är utbyggt nog för att registrera viss nödvändig användardata.
<br />
<br />
En önskan från företaget var om användaren skulle kunna lägga till och ta bort Widgets efter eget tycke och smak och spara denna layout för användaren. Detta skulle vara grundfunktionalitet som så det fick viss prioritering.
<br />
<br />
![Super wide](/assets/layout.png)

<br />
[[Top]](#top)
