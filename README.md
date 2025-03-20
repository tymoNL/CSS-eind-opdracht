# CSS-eind-opdracht

**Tymo smids**

*27-02-2025*

## De gekozen opdracht

Voor het eindopdracht heb ik gekozen om **control panel** te maken.

## Het idee

De control panel is een afstandsbediening voor een tv.  
De afstandsbediening bevat de volgende functionaliteiten:

- Een **powerknop** om de tv aan of uit te zetten;
- Meerdere **kanaalknoppen** om van kanaal te wisselen;

De afstandsbediener is in 3D gedraaid zodat de afstandsbediener naar de tv gekantend is.

- Bij het inschakelen van de tv verschijnt een groen scherm om aan te geven dat de tv aanstaat;
- Bij het selecteren van een kanaal wordt een gif afgespeeld die bij dat kanaal hoort.

## De techniek

De powerknop op de afstandsbediening is een checkbox en de channels zijn radiobuttons met dezelfde naam zodat er maar een actief kan zijn. De tv checkt of de powerknop aanstaat. Als dit zo is krijg je eerst een groen scherm om te laten zien dat de tv aanstaat. Als er een channel gekozen is dat wordt er een gif afgespeeld.

```css
/* 1st channel */
main:has(section:nth-of-type(2) div:nth-of-type(1) input[type="checkbox"]:checked):has(section:nth-of-type(2) > div:nth-of-type(2) > div:nth-of-type(1) input[type="radio"]:checked) {
    --screen-color: #000;

    section:nth-of-type(1) {
        background-image: url("images/dog-working.gif");
        background-size: contain;
        background-position: center;
        background-repeat: no-repeat;
    }
}
```

## Ontwikkelingsproces

<details>
<summary>Week 1</summary>

- De basisstructuur van de afstandsbediening en tv gemaakt.
- De powerknop toegevoegd en werkend gemaakt.

#### Feedback

- Geheime knop ergens toevoegen;
- tv static toevoegen na wisselen van channel;
- channelknoppen ook active toggelen;

</details>

---

<details>
<summary>Week 2</summary>

- De label-knoppen omgezet naar radiobuttons met `appearance: none`.
- Animaties toegevoegd die werken bij kanaalwijzigingen.
- De kleuren van de tv aangepast per kanaal.

</details>

---

<details>
<summary>Week 3</summary>

Deze week heb ik de gifjes toegevoegd aan de channels zodat de tv ook iets laat zien. Ook heb ik besloten om de animatie eruit te halen omdat het niet veel toevoeging was en niet goed werkt. Dit komt omdat de channels dezelfde naam hebben als radiobutton dus kan ik de animatie niet wijzigen.

```css
/* https://forum.freecodecamp.org/t/creating-an-animated-tv-static-effect-using-just-a-gradient/487486 */
@keyframes tv-static {
    0% {
        background-size: 100% 100%;
    }

    90% {
        background-size: 200% 200%;
    }

    100% {
        background-image: none;
        background-size: 100% 100%;
        animation: none;
    }
}
```

In de css heb ik een aantal overbodige lijnen kunnen wegwerken door data attributes in de html te gebruiken.

**Voor**

```css
            &:nth-of-type(2) input::after {
                content: "2";
            }

            &:nth-of-type(3) input::after {
                content: "3";
            }

            &:nth-of-type(4) input::after {
                content: "4";
            }

            &:nth-of-type(5) input::after {
                content: "5";
            }

            &:nth-of-type(6) input::after {
                content: "6";
            }

            &:nth-of-type(7) input::after {
                content: "7";
            }

            &:nth-of-type(8) input::after {
                content: "8";
            }

            &:nth-of-type(9) input::after {
                content: "9";
            }
```

**Na**

```css
 input::after {
                content: attr(data-number);
            }
```

</details>

---

<details>
<summary>Week 4</summary>

De radiobuttons zijn 3D gemaakt door een ::before toe te voegen aan de radiobuttons en de checkbox zodat er diepte ontstaat. De knoppen hebben ook een transition zodat de knoppen een animatie hebben.

Het scherm heeft nu een svg filter zodat er een transitie is tussen de verschillende kanalen. Er is ook een channel nummer toegevoegd aan het scherm zodat je weet welk kanaal actief is.

#### Container queries

De channel nummer is via een @container query gemaakt die test welk kanaal actief is en daarvan het nummer teruggeeft.

```css
@container not style(--active-channel: 0) {
    main > section:nth-of-type(1)::after { 
        counter-reset: channel var(--active-channel);
        content: counter(channel);
        display: flex; 
    }
}
```

De static werkt doormiddel van 2 svg fiters die achter elkaar snel wisselen zodat er een static effect komt. Ook work er een animatie afgespeeld die de opacity van de svg filter op 0 zet zodat deze niet meer zichtbaar zijn.

```css
@keyframes noiseAnimationReset1 {
    0% { filter: url(#tvNoise1); }
    50% { filter: url(#tvNoise2); }
    100% { filter: url(#tvNoise1); }
}

@keyframes hideSvg {
    0% { opacity: 1; }
    100% { opacity: 0; }
}
```

</details>

---

### Feedback

Na het gesprek met Sanne zijn er nog een aantal punten die verbeterd konden worden. Deze punten heb ik verwerkt in mijn project.

De data attributen zijn uit de inputs gehaald. Ook wordt in de css nu gekeken naar de value om de ::after te vullen.

```css
    /* Channel number */
    /* Na feedback veranderd naar value ipv data attribute */
    input::after { content: attr(value); }
```

De :has selector was onnodig lang en specefiek. Deze is nu korter gemaakt zodat het beter leesbaar is.

```css
    main:has(input[type="checkbox"]:checked):has(input[value="1"]:checked) {}
```

De kanalen hebben nu een standaard state die een aantal standaard waardes hebben zodat deze niet in elke selector  opnieuw aangegeven moeten worden.

```css
/* Any channel */
main:has(input[type="checkbox"]:checked):has(input[value]:checked) {
    --screen-color: #000;

    section:nth-of-type(1) {
        div:nth-of-type(1) {
            filter: url(#tvNoise);
            animation-play-state: running;
        }
    }
}
```

Via [Giphy](https://giphy.com/) heb ik de gifjes kunnen zoeken en overnemen voor dit project.

## Link

[Link naar opdracht](https://tymonl.github.io/CSS-eind-opdracht/index.html)
