# Logboek Responsive Typography #
## Research ##

- **Fluid layouts:** De layout continu veranderen aan de hand van de viewport breedte.
- **Adaptive layouts:** De layout stapsgewijs een aantal keer veranderen aan de hand van de viewport breedte.

**Adaptive layouts** met zo weinig mogelijk breakpoints is the way to go want readability is belangrijker dan content die altijd de viewport width matched.

- **Graded fonts** zijn typefaces waar voor verschillende weights bepaalde strokes wat extra weight krijgen. (Voor bijvoorbeeld wit-op-zwart tekst heel handig).
[Voorbeeld graded font](BureauRoman_graded.png)

> The serifed typeface is a priest, the sans is a hacker!


###  EM's and REM's ###
> An em is a unit in the field of typograpy, equal to the currently specified point size.

#### EM versus REM ####
Jeremy Church:
> While em is relative to the font-size of its direct or nearest parent, rem is only relative to the html (root) font-size.

REM is dus handiger om typografie schaalbaar te maken over een hele webpagina maar geeft minder controle in specifieke delen van een pagina.

#### Demo ####
Begin met default value voor 1rem te kiezen.

```css
html {
    font-size: 16px // dus 1rem = 16px
}
```
Vervolgens de relatieve grootte van andere elementen bepalen
```css
h1 {
    font-size: 2rem;
}
h2 {
    font-size: 1.5rem;
}
p {
    font-size: 1rem;
}
```
Dan proportionele ruimte tussen de elementen creeëren met REM

```css
h1 {
    font-size: 2rem;
    margin: 0 0 1rem;
}
h2 {
    font-size: 1.5rem;
    margin: 1rem 0 2rem;
}
p {
    font-size: 1rem;
    margin: 1rem 0;
}
```
Als laatste stap je ontwerp schalen met media queries waar je de waarde van 1rem aanpast
```css
@media screen and (min-width: 500px){
  html{
    font-size: 14px;
  }
}
@media screen and (min-width: 570px){
  html{
    font-size: 15px;
  }
}
@media screen and (min-width: 620px){
  html{
    font-size: 16px;
  }
}
@media screen and (min-width: 680px){
  html{
    font-size: 17px;
  }
}
@media screen and (min-width: 720px){
  html{
    font-size: 18px;
  }
}
@media screen and (min-width: 800px){
  html{
    font-size: 19px;
  }
}
@media screen and (min-width: 860px){
  html{
    font-size: 20px;
  }
}
@media screen and (min-width: 920px){
  html{
    font-size: 21px;
  }
}
@media screen and (min-width: 1000px){
  html{
    font-size: 22px;
  }
}
```
[Resultaat](demos/rems/rems.css)

Zeer gemakkelijk in gebruik!
### Flowtype.js ###
Javascript plugin met jQuery dependency.
FlowType zorgt ervoor dat er altijd 45-75 karakters per lijn zijn op je pagina, dit is algemeen aangenomen de meest leesbare standaard. Dit is moeilijk te bereiken met enkel CSS media-queries.
Met FlowType los je dit op een gemakkelijke en elegante manier op.

Je hebt enkel een typography base nodig.

```css
body {
 font-size: 18px;
}
h1,h2,h3,h4,h5,h6,p {
 line-height: 1.45;
}
h1 { font-size: 4em; }
h2 { font-size: 3em; }
h3 { etc... }
```

Hierna moet je enkel flowType aanroepen in je Javascript bestand.

```js
$('body').flowtype();
```
Hierin kan je alle beschikbare parameters van flowType veranderen.
(minimum, maximum, minFont, maxFont, fontRatio)

### Modular Scale ###
Modular Scale is een open-source typography tool voor Sass.
Het maakt gebruik van de gulden ratio om de scaling van je copy te doen.
Je kan deze increments natuurlijk ook kleiner of groter maken afhankelijk van wat je nodig hebt.

Als alle font-sizes geset zijn met REM's kan het moeilijk zijn om het aantal REM's te bepalen voor andere elementen. 
Hoeveel REM's moet een H1 of H2 zijn?
De meeste mensen doen dit op gevoel en stellen deze groottes af met het oog.
Sommige proporties zijn aangenamer voor het oog en komen veel voor in onder andere natuur, muziek en architectuur.

> [...] these proportions not only seem to please human beings in many different centuries and countries, they are also 
> prominent in nature far beyond the human realm.
> Robert Bringhurst — The Elements of Typographic Style

Modular Scale gebruikt de Modulor schaal van Le Corbusier, deze is gebaseerd op de gulden ratio en proporties van het menselijk lichaam.

Modular Scale is heel gemakkelijk in gebruik, het voorziet een aantal klassieke ratios om te gebruiken.
Je moet eerst een baseline instellen en vervolgens en ratio.

```css
$ms-base: 1rem;      //Baseline van 1 rem
$ms-ratio: $golden;  // Gulden ratio van 1,618
```

Als dit gebeurd is, is het heel gemakkelijk om andere waardes van deze schaal aan te roepen met de ms() functie.
Op deze manier kan je die waardes aan alle verschillende elementen koppelen.

```css
body { font-size: ms(0); }   // 1rem - $ms-base
h5 { font-size: ms(1); }     // 1,68 rem
h4 { font-size: ms(2); }
h3 { font-size: ms(3); }
h2 { font-size: ms(4); }
h1 { font-size: ms(5); }
```

### Sass ###
Nu je een goede typografische fundering hebt gebouwd met Modular Scale, FlowType, of de manuele manier met EM's of REM's moet je deze nog responsive maken.
Door deze fundering is het zo gemakkelijk als de font-size property van het html element te veranderen, maar met enkel CSS kom je snel aan veel media queries voor alle screen sizes. In het voorbeeld met REM gebruik ik 9 media queries.

De responsive mixin van Sass laat je toe om dit met veel minder code en op een veel leesbaardere manier aan te pakken.

```css
html{
  @include responsive("font-size", 11px,
    (
       500px: 14px,
       570px: 15px,
      620px: 16px,
      680px: 17px,
      720px: 18px,
      800px: 19px,
      860px: 20px,
      920px: 21px,
      1000px: 22px
    )
  );
}
```
Op deze manier kan je zelf ook veel sneller lezen hoeveel 1rem bedraagt bij welke screen size.

Met deze mixin heb je ook gemakkelijker controle over welke screen sizes je wilt manipuleren.
Stel dat je de font-size wil aanpassen voor iPads in landscape mode.

```css
@include responsive("font-size", 11px,
  (
    (min-device-width 768px) 
    (max-device-width 1024px) 
    (orientation landscape) : 16px
  )
);
```

In css wordt dit:
```css
@media only screen 
and (min-device-width : 768px) 
and (max-device-width : 1024px) 
and (orientation : landscape) { font-size: 16px; }
```

Je kan in SASS ook gebruik maken van named-breakpoints waardoor het gemakkelijker is om deze te hergebruiken.
Sla je breakpoints (met naam) op in een globale variabele genaamd $named-breakpoints.

```css
$named-breakpoints: (
    "xs": 350px,
     "s": 600px,
     "m": 800px,
     "l": 1420px,
    "xl": 2100px,
  "ipad_landscape": (min-device-width 768px) (max-device-width 1024px) (orientation: landscape)
); 
```

Hierna kan je deze named-breakpoints aanroepen in je responsive mixins zoals je bij normale breakpoints zou doen.

```css
@include responsive("font-size", 11px,
  (   
    "xs" : 12px,
    "s" : 13px,
    "m" : 14px,
    "l" : 15px,
    "xl" : 16px,
    "ipad_landscape" : 16px
  )
);
```

Nu heb je een goede, leesbare en compacte responsieve typografische basis waarop je je website verder kan uitbouwen!

### Responsive Logos ###
Responsive logos vallen niet helemaal binnen 'responsive typography' maar goed gebruik ervan kan zeker en vast bijdragen aan een betere responsive layout en de leesbaarheid van zowel het logo als de hele pagina te verbeteren.
Wanneer we aan responsive denken bij afbeelding denken de meesten enkel aan het schalen van de afbeelding en niet zozeer aan de mogelijkheid om de afbeelding zelf te veranderen.

Het idee is om logos afhankelijk van hoe klein de viewport is te versimpelen.
Bijvoorbeeld het complexe Walt Disney logo zal op een klein scherm enkel de cursieve hoofdletter D behouden.
Dit zorgt ervoor dat het logo er niet te rommelig zal uitzien of niet meer 'werkt' in het geheel van de pagina.
Wat er ook gebeurt met te complexe logos op kleine schermen is dat de details niet meer goed zichtbaar zijn en het logo er gewoon raar uitziet.

Meer voorbeelden zijn te vinden op [responsive logos](http://responsivelogos.co.uk/) door Joe Harrison.

######  Sources:  ######
- http://css-tricks.com/confused-rem-em/
- http://www.awwwards.com/responsive-typography-a-roundup-of-the-best-articles-and-tutorials.html
- http://en.wikipedia.org/wiki/Em_(typography)
- http://www.webdesignerdepot.com/2012/10/a-simple-guide-to-responsive-typography/
- http://ia.net/blog/responsive-typography-the-basics/
- https://bugsnag.com/blog/responsive-typography-with-rems
- http://responsivelogos.co.uk/
- https://gist.github.com/maxluster/168e650267bac9faaafd
- http://www.fastcodesign.com/3033446/what-corporate-logos-would-look-like-if-you-shrank-them
- https://github.com/at-import/modular-scale
- http://simplefocus.com/flowtype
