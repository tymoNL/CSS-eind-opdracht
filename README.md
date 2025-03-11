# CSS-eind-opdracht

**Tymo smids**

*27-02-2025*

## De gekozen opdracht

Voor het eindopdracht heb ik gekozen om de control panel te maken.

## Het idee

De control panel is een afstandsbediener voor een tv.
De afstandsbediener heeft een aanknop, meerdere kanaal knoppen, volume knop.

De afstandsbediener is in 3D gedraaid zodat de afstandsbediener naar de tv gekantend is.

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

### Week 1

De afstandsbediener gemaakt met de tv.
De tv laten werken op de power knop.

#### Feedback

- Geheime knop ergens toevoegen;
- tv static toevoegen na wisselen van channel;
- channelknoppen ook active toggelen;

### Week 2

De label knoppen omgezet naar radiobuttons met appearance: none.
De animaties laten werken per channel wijziging.
De kleuren van de tv veranderen per channel.

### Week 3

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

Via [Giphy](https://giphy.com/) heb ik de gifjes kunnen zoeken en overnemen voor dit project.

## Link

[Link naar opdracht](https://tymonl.github.io/CSS-eind-opdracht/index.html)
