---
title: 2.Metod
publishDate: 7 Jun 2023
description: My graduation thesis from Chas Academy
---

## <a name="top"></a> Table of Contents

2. [Metod och genomförande](#Method)

   2.1 [Planering](#Planning)

   2.2 [Kund och användarbehov](#Needs)

   2.3 [Dataflöde och struktur](#Dataflow)

   2.4 [Component composition study](#Composition)

---

# <a name="Method"></a>Metod

Arbetet har gjorts efter en grov planering. Det är alltid svårt att veta hur lång tid vissa saker kan ta och hur det kan komma att påverka planeringen i stort.

<br />

## <a name="Planering"></a>Planering

Arbetet har utförts under 4 stycken sprintar där arbetet är uppdelat enligt nedan.
<br />
<br />

### Sprint 1

-  Research och val kring arbetssätt/pattern i React (Component composition, Higher-Order Components (HOCs), Render Props eller Hooks).
-  Definiera filstrukturer och dashboard-komponenter.
-  Definiera några exempel på respektive användarrolls widgets.
-  Definiera grafiskt återanvändbara komponenter/moduler som är oberoende av widgets innehåll.

### Sprint 2

-  Skapa återanvändbar frontend-struktur och komponenter efter definition.
-  Fundera kring huvudsakliga funktioner som borde kunna delas. Granulärt återanvändbara funktioner, funktioner i funktioner.

### Sprint 3

-  Anpassningsbar layout?
-  Spara användarens layout av Widgets i DB.

### Sprint 4

-  Skriva rapport och samla in data.
-  Fundera på förbättringspotential.

[[Top]](#top)
<br />
<br />

## <a name="Kund och användarbehov"></a>Kund och användarbehov

<figure class="abstract-image">
      <img src="/assets/figma2.png" alt="Sketch" width="330">
      <figcaption>
        Bild 1. En färdig idéskiss
      </figcaption>
    </figure>

Tillgången till marknads- eller användarundersökning var begränsad och har jobbat med företagets grundare och dennes kännedom om byggbranschen och dess branschfolk. Eftersom inget marknadsmaterial finns så görs väldigt enkla UserStories (finns som Bilaga). Jag tar fram en grundskiss som godkänns.
<br />
<br />
Jag diskuterar fram några uppslag till Widgets med företagets ena grundare. Dessa är dock mer riktlinjer då fokus har främst lagts på att bygga en modulär och återanvändbar mall och alla Widgets fungerande har fått lite sekundär prio.

| Widget             | Requester | Reseller | Carrier | Info                      |
| :----------------- | :-------- | :------: | ------: | :------------------------ |
| Status Numbers     | Yes       |   Yes    |     Yes | Overall status figures    |
| Monthly Rapport    | Yes       |   Yes    |     Yes | Graph of customer benefit |
| Project            | Yes       |          |         | Project page              |
| Best Seller        |           |   Yes    |         | Seller top list           |
| Current Deliveries |           |          |     Yes | Shows current deliveries  |
| More?              |           |          |         | TBD                       |

<figcaption>
    Tabell 1. Möjliga uppslag för Widgets
</figcaption>
<br />

<figure class="abstract-image">
      <img src="/assets/delar.png" alt="Sketch" width="330">
      <figcaption>
        Bild 2. Komponentuppbyggnad av Widget
      </figcaption>
    </figure>

Jag tänker att en enkel väg att gå är att varje widget som mest ska bestå av 5 komponenter:

-  `<WidgetItem />` Ett "kort" för alla widgets.
-  `<WidgetTitle />` En beskrivande titel
-  `<WidgetButton />` En eventuell knapp som kan se olika ut
-  `<WidgetDropdown />` En eventuell dropdown om knappen är av typen
-  `<WidgetContent />` En sektion för att ladda en valfri Widget

<br />
<br />

[[Top]](#top)
<br  />
<br  />

## <a name="Dataflow"></a>Dataflöde och struktur

Jag tänkte mig nedan övergripande dataflöde. En fil med metadata-objekt per användarroll där metadatan skapar en datadriven skalbarhet. Finns metadata till en widget, finns en widget. Tänker mig behöva en övergripande kontext som kan tillgodose med funktioner, till exempel knappens funktion om widgeten ska ha en knapp.
Denna metadata returneras till huvudkomponenten där de mappas sedan ut till olika widgets beroende på användarroll.
<br />
<br />

<figure class="abstract-image">
      <img src="/assets/dataflow.svg" alt="Sketch" width="650">
      <figcaption>
        Bild 3. Flödesschema för datan, kan ses som ett grovt ER-diagram
      </figcaption>
    </figure>

Senare skapas en ny Array (selectedWidget) med de widgets som användaren lägger till och tar bort med de widgets som finns i useWidgetInfo som grund.

De widget layout användaren vill ha på sin dashboard sparas i databasen samt widgets med CRUD-behov, tex Projekt-widgeten.
<br />
<br />
<br />
<br />
<br />
<br />

## <a name="Filstruktur"></a>Filstruktur för komponenter

-  **Dashboard.jsx** = Huvudkomponent, ligger i “pages” i Next och inte bland dessa andra komponenter.

<figure class="files-image">
      <img src="/assets/files.png" alt="Sketch" width="200">
      <figcaption>
        Bild 4. Visar upplägg av komponenternas filstruktur. 
      </figcaption>
    </figure>

-  **useWidgetInfo** = Den metadata och värden för användarroller och deras respektive Widgets.
-  **WidgetComponents** = Komponenter som fungerar som återanvändbara platshållare för den inkommande datan.
-  **Widgets** är till största del unikt innehåll med specifik metadata och funktionalitet per användarroll kan fortfarande skickas in till dessa, vilket gör att man kan återanvända även dessa med olika data beroende på specifika fall. Tex en widget som ser liknande ut för flera användarroller men som använder annan data. Detta har jag dock inte nått hela vägen med.

[[Top]](#top)
<br />
<br />
<br />
<br />

## useWidgetInfo (custom hook)

Filen var först en ren datafil med objekt för varje widgets. Men då jag vill använda Kontext för att ta emot funktioner tex för widgets knappens funktion görs den om till en hook.

Olika generiska, återanvändbara stilar på knappar och “Cards” ligger med som konstanter.

```js
const PRIMARY_BUTTON_STYLE = 'inline-block text-gray-800 dark:text-gray-400 hover:bg-gray-100 … rounded-lg text-sm
p-1.5';

const SECONDARY_BUTTON_STYLE = 'flex border border-gray-300 h-12 bg-gray-100 font-semibold … hover:transition
ease-in-out';

const CARDS_FORM_STYLE = [ 'bg-white px-4 py-6 rounded-xl h-full', 'bg-white px-4 py-5 rounded-xl h-full',
'bg-gradient-to-b from-white to-teal-200 px-4 py-3 rounded-xl h-full', ];
```

Objekten byts ut mot ett interface(enligt “Interface segregation principle”, läs “i” i SOLID) Jag definierar vartefter de variabler jag tänker mig behöva för olika sorters metadata i funktionen makeWidget, som efter testande vuxit till 11 i antalet.
<br />

```js
const makeWidget = (
   id,
   title,
   role,
   cardForm,
   size,
   buttonStyle,
   buttonType,
   buttonDesc,
   dropdownOptions,
   action,
   content
) => {
   return {
      id,
      title,
      role,
      card: cardForm,
      size,
      buttonStyle,
      buttonType,
      buttonDesc,
      dropdownOptions,
      action,
      content,
   };
};
```

<figcaption>
Kodexempel 2: Visar i kompakthet det interface som bestämmer innehållet i en Widget. 
</figcaption>

Därefter listar jag sen metadata för widgets i array:er för varje användarroll. Och kan skapa arrayer uppbyggda efter detta tex för rollen “inköpare” och en widget:

```js
const requestor = [
   makeWidget(
      1,
      "Kvartalsrapport",
      "requestor",
      CARDS_FORM_STYLE[1],
      "w-1/2",
      PRIMARY_BUTTON_STYLE,
      "dropdown",
      undefined,
      ["Kvartalsrapport", "Månadsrapport", "Översikt"],
      () => dropdownHandler(2),
      <Monthly
         stapleValues={[
            { title: "Rabatt", color: "bg-teal-200" },
            { title: "Månadsbudget", color: "bg-teal-500" },
         ]}
      />
   ),
   makeWidget(
      2
      /* … */
   ),
]; /* … */

return { requestor, reseller, carrier };
```

<figcaption>
Kodexempel 3: Visar ett exempel på en statisk Widget i filen useWidgetInfo.
</figcaption>

[[Top]](#top)

<br />
<br />

## <a name="Composition"></a>Studie av komponent komposition

<br />

### Component composition

Fastnade tidigt för ett koncept kallat “Component composition” efter diskussion med min handledare. Detta möjliggör skapandet av större komponenter genom att kombinera mindre, återanvändbara komponenter. Komponenter kan skickas som props till andra komponenter, som sedan kan återge dem på ett flexibelt sätt, detta blir flexibelt eftersom den kan ha olika header, footer och children beroende på vilka props som skickas till den. Vanligt vid layout-”komposition” vilket kändes passande.
<br />  
Där huvudkomponenten propsar komponenter till en underliggande struktur.

```html
<Layout
header = {<Header />}
footer = {<Footer />}>
<MainContent />
</Layout>
```

Vilket ger en väldigt flexibel lösning där man i huvudkomponenten kan “komponera” sitt upplägg av komponenter från den övre strukturen.

```html
const Layout = ({ header, footer, children }) => { return (
<div>{header} {children} {footer}</div>
);};
```

Jag försökte strukturera enligt mönstret “Components composing” vilket gav ett fungerande resultat. Jag skickade många värden som props från huvudkomponenten vilket gav dålig läsbarhet och komponenterna blir hårt definierade av alla props för att kännas fullt flexibelt.

<br />

#### Huvudkomponent

```html
selectedWidgets.map((widget, index) => {
                return (
                  <WidgetItem
                    key={widget.id}
                    widget={widget}
                    size={widget.size}
                    isPrelAdmin={isPrelAdmin}
                    title={<WidgetTitle title={widget.title} />}
                    button={
                      <WidgetButton
                        index={index}
                        button={widget.button}
                        buttonDesc={widget.buttonDesc}
                        buttonStyle={widget.buttonStyle}
                        buttonFunc={widget.buttonFunc}
                        buttonType={widget.buttonType}
                        showDropdown={widget.showDropdown}
                      />
                    }
                    dropdown={
                      <WidgetDropdown
                        widgetId={widget.id}
                        selectedWidgets={selectedWidgets}
                        setSelectedWidgets={setSelectedWidgets}
                        selectedMonthlyWidget={selectedMonthlyW...
                        setSelectedMonthlyWidget={setSelectedM...
                        dropdownOptions={widget.dropdownOptions}
                        showDropdown={widget.showDropdown}
                      />
                    }
                    content={
                      <WidgetContent
                        loading={loading}
```

#### Underliggande kopmponent struktur

```html
const WidgetItem = ({ widget, title, button, content, dropdown }) => { return (
<div className="{`p-2" transition-all duration-500 w-full mobile:${widget.size}`}>
   <div className="{`${widget.card}`}">
      <section
         className="flex justify-between
      items-center"
      >
         {title} {button}
      </section>
      <section>{dropdown}</section>
      <section>{content}</section>
   </div>
</div>
); }; WidgetItem.Title = WidgetTitle; export default WidgetItem;
```

<br />

### Compound components

Detta mönster gjorde att jag fick bort propsen idén att du har en huvudkomponent (WidgetItem i det här fallet), som delar någon form av gemensam logik eller värde
(i mitt fall den mappade “widget”-variabeln) med sina barn (via Context API) med dess barnkomponenter (WidgetItem.Title, WidgetItem.Button, WidgetItem.Dropdown och WidgetItem.Content). Dessa barnkomponenter kan återanvändas och ordnas om efter behov.

Denna version var jag ganska nöjd med men jag hittade dock ett sätt senare att kombinera Compound components med Component composition vilket jag kände gav det mest flexibla resultatet. Detta redovisar jag under resultat delen.

<br />

#### Huvudkomponent

```html
selectedWidgets.map((widget, index) => { return (
<WidgetItem key="{widget.id}" index="{index}" widget="{widget}" loading="{loading}">
   <WidgetItem.Title />
   <WidgetItem.Button />
   <WidgetItem.Dropdown />
   <WidgetItem.Content />
</WidgetItem>
);
```

#### Underliggande kopmponent struktur

```html
const WidgetItem = ({ widget, loading, index }) => {

return (
<WidgetInfoContext.Provider value={{ widget }}>
<section
className={`p-2 transition-all duration-500 ...
   <article className={`card ${widget.card}`}>
      <header className="w-full flex justify-between ...
         <WidgetItem.Title />
         <WidgetItem.Button index={index} />
      </header>
      <div className="w-full p-2">
         <WidgetItem.Dropdown />
      </div>
      <div className="w-full p-2">
         <WidgetItem.Content loading={loading} />
      </div>
     </article>
</section>
</WidgetInfoContext.Provider>
);
};

WidgetItem.Title = WidgetTitle;
WidgetItem.Button = WidgetButton;
WidgetItem.Dropdown = WidgetDropdown;
WidgetItem.Content = WidgetContent;

export default WidgetItem;
```

<style>
  .start {
    margin-top: 1em;
  }
  .files-image {
    float: right;
    margin: -1em 1em 2em 2em;
    max-width: 200px;
  }

  .files-image img {
    border-radius: 8px;
    margin-bottom: 1.5em;
  }

  @media (max-width: 1020px) {
    .files-image {
      float: none;
      margin: 0 auto 2em;
    }
  }
</style>
