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
