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

##  ToDo:  ##
- FlowType.js
- Responsive Typography using Sass

######  Sources:  ######
- http://css-tricks.com/confused-rem-em/
- http://www.awwwards.com/responsive-typography-a-roundup-of-the-best-articles-and-tutorials.html
- http://en.wikipedia.org/wiki/Em_(typography)
- http://www.webdesignerdepot.com/2012/10/a-simple-guide-to-responsive-typography/
- http://ia.net/blog/responsive-typography-the-basics/
- https://bugsnag.com/blog/responsive-typography-with-rems
