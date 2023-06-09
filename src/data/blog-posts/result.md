---
title: 3.Resultat
publishDate: 7 Jun 2023
description: The result of the thesis
---

## Resultat

<br />

<div class="container">
   <figure class="abstract-image">
   <img src="/assets/dashboard.jpg" alt="Dashboard" width="330">
   <figcaption>
      Overview of the dashboard
   </figcaption>
   </figure>
   <p class="start">Jag har använt en kombination av kodmönstren "Composing Components" och "Compound Components" för min dashboard.</p>
<p>
Denna kombination kan vara den mest lämpliga för att bygga en flexibel och återanvändbar dashboard. "Composing Components" mönstret används när man bygger upp en komplex komponent genom att kombinera mindre delkomponenter.
Å andra sidan används "Compound Components" mönstret för att dela gemensam funktionalitet och data mellan flera komponenter.
</p>
<p>
Detta skapar en bra läsbarhet utan propsande då jag endast propsar mitt mappade objekt “widget”. Komponenten lätt återanvändas i olika situationer, antingen använda den som den är med de inbyggda komponenterna, eller du kan passa in egna komponenter via props för att ändra dess beteende.
</p>

<br />

#### Huvudkomponent

```html
selectedWidgets.map((widget, index) => {
   return (
      <WidgetItem
         key={widget.id}
         index={index}
         widget={widget}
         loading={loading}
         header={
            <WidgetItem.Header>
               <WidgetItem.Title />
               <WidgetItem.Button />
            </WidgetItem.Header>
         }
         dropdown={<WidgetItem.Dropdown />}
         content={<WidgetItem.Content />}
      />
   );
})}
```

#### Underliggande kopmponent struktur

```html
const WidgetItem = ({ widget, index, loading, header, dropdown, content }) => { return ( <WidgetInfoContext.Provider
   value="{{widget}}"
>
   <section className="{`p-2" transition-all duration-500 w-full mobile:${widget.size}`}>
      <article className="{`card" ${widget.card}`}>
         <header
            className="w-full flex justify-   
         between items-center p-2"
         >
            {header}
         </header>
         {dropdown}
         <div className="w-full p-2">{content}</div>
      </article>
   </section>
</WidgetInfoContext.Provider>
); }; WidgetItem.Title = WidgetTitle; WidgetItem.Button = WidgetButton; WidgetItem.Dropdown = WidgetDropdown;
WidgetItem.Content = WidgetContent; WidgetItem.Header = WidgetHeader; export default WidgetItem;
```

### Widget-komponenter

Widget-komponenterna fungerar som platshållare för den metadata som skickas in från useWidgetInfo hooken. Så här ser komponenten WidgetTitle ut tex:

```html
import { useWidgetInfoContext } from './widget-item-context'; const WidgetTitle = () => { const { widget } =
useWidgetInfoContext(); return (
<h5 className="text-xl font-semibold leading-none text-gray-800">{widget.title}</h5>
);}; export default WidgetTitle;
```

### Funktioner

Funktioner har flyttats ut till utils-specifika filer för varje widget. Beroende på om de kan göras mer allmänt återanvändbara även för andra ställen har jag flyttat dem till ”utils”.
<br />
<br />

<figure class="files-image">
    <img src="/assets/utils.png" alt="Dashboard" width="330">
    <figcaption>
    Utils funktioners struktur
    </figcaption>
</figure>

Jag har även velat undersöka återanvändbarheten i enskilda utils-funktioner som kan skrivas små och istället köras “i varandra”. Detta har jag bara i viss utsträckning hunnit med att göra.

```js
export const findItemsByIndex = (items, index) => items.find((item, i) => i === index);

export const findItemsById = (items, id) => items.find((item, i) => i === id);
```

En typ av funktion som nästan uppträtt som ett mönster i detta projekt har varit att uppdatera eller mutera state eller existerande metadata med ny data. Här nedan är en funktion som exempel på detta, som handlar om att uppdatera storleken på en widget. Objektet “widget” innehåller en värde(widget.size) i form av en string som byts ut.

```js
export function handleWidgetSize(widget, setSelectedWidgets) {
   setSelectedWidgets((prev) => {
      const newSelectedWidgets = [...prev];
      const index = newSelectedWidgets.findIndex((sel) => sel.id === widget.id);
      newSelectedWidgets[index].size = newSelectedWidgets[index].size === "w-full" ? "w-1/2" : "w-full";
      return newSelectedWidgets;
   });
}
```

## Fortsatt arbete

Vidare arbete ligger i att skapa widgets där utseende ser liknande ut för flera användarroller men som använder olika funktioner för att hämta specifika data för en specifik användarroll. Detta har jag dock inte hunnit gå hela vägen med.

</div>

<style>
  .start {
    margin-top: 1em;
  }
  .abstract-image {
    float: right;
    margin: -1em 1em 2em 2em;
    max-width: 400px;
  }

.abstract-image img {
border-radius: 8px;
margin-bottom: 1.5em;
}

@media (max-width: 1020px) {
.abstract-image {
float: none;
margin: 0 auto 2em;
}
}
</style>
