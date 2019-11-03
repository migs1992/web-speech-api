# Web speech API
---

Web speech API avulla ääntä voidaan siirtää web-applikation ja käyttäjän välillä. API voidaan jakaa kahteen eri osioon, jotka ovat Speech Synthesis eli teksti ääneksi ja Speech Recognition eli Asynkroninen puheentunnistus. On monia tapoja, joilla tämä API voi olla erittäin hyödyllinen tulevaisuudessa. Etenkin puheen muuttamisessa tekstiksi on paljon mahdollisuuksia, mutta Web Speech API on vasta kokeiluvaiheessa.

## Speech Recognition

Sanojen tunnistamiseen täytyy antaa sovellukselle luettelo (SpeechGrammarList) sanoista ja sanamuodoista, joita haluamme tunnisteen tunnistavan. SpeechGrammarList on käyttää tällä hetkellä JSpeech Grammar Formatia (JSGF) mutta tulevaisuudessa voi olla muitakin formaatteja.

Lisäksi tarvitaan myös SpeechRecognitionEvent-käyttöliittymä luomaan tapahtumaobjektin tuloksen ja nomatch-tapahtumille ja sisältämään kaikki tiedot, jotka liittyvät väliaikaiseen tai lopulliseen puheentunnistustulokseen. 

Alapuolella esimerkki yksinkertaisesta väriä vaihtavasta applikaatiosta.

```js
var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
var SpeechGrammarList = SpeechGrammarList || webkitSpeechGrammarList;
var SpeechRecognitionEvent = SpeechRecognitionEvent || webkitSpeechRecognitionEvent

var colors = [ 'aqua' , 'azure' , 'beige', 'bisque', 'black', 'blue', 'brown', 'chocolate', 'coral' ... ];
var grammer = '#JSGF V1.0;'; grammar colors; public <color> = ' + colors.join(' | ') + ' ;'
```

Tärkeää tietoa

* Grammer - #JSGF V1.0; - ilmoittaa käytetyn formaatin ja version. Tämän on aina oltava ensin.
* Voit määritellä niin monta termiä kuin haluat erillisillä riveillä yllä olevan rakenteen mukaisesti ja niihin voi sisältyä melko monimutkaistakin kielioppia. 
* Käyttäjä tarvitsee luonnollisesti mikrofonin äänen lähettämiseen
* Toimii ainoastaan uudemmissa Google Chromen versiossa. 

## Speech Synthesis

Speech Synthesis-käyttöliittymä on puhepalvelimen ohjainrajapinta, jonka avulla teksti muuttuu puheeksi ja sen toistamista laitteen kaiutin- tai äänilähtöyhteydestä. Defaultina on luonnollisesti englanti, mutta voit käyttää muuta kieltä muuttamalla `lang` propertyä. Myös useamman eri äänen käyttäminen on mahdollista. Alla esimerkki suomen kielen käytöstä (fi-FI = suomi). Alla olevassa esimerkissä on käytetty `SpeechSynthesisUtterance`, joka sisätää puhepyynnön. 

```js
let utterance = new SpeechSynthesisUtterance('Moikka')
utterance.lang = 'fi-FI'
speechSynthesis.speak(utterance)
```

`lang` propertyn lisäksi voimme käyttää seuraavia attribuutteja, joilla modifioida `SpeechSynthesisUtterance`
* `utterance.text`: Tekstiä. 
* `utterance.voiceURI`:määrittelee käytettävän äänen ja synteesin.
* `utterance.volume`: Äänenvoimakkuus 0 ja 1 välillä.
* `utterance.rate`: Puhenopeus. 0-10 on mahdollinen, mutta on normaalia käyttää 1-2. 2 on kaksinkertainen nopeus, 3 kolminkertainen jne.
* `utterance.pitch`: Äänenkorkeus.

[Hyvä esimerkki Speech Synthesis toiminnasta](https://bradtraversy.github.io/type-n-speak/)

---
# Tehtävät

Tee toinen seuraavista tehtävistä

1. Luo yksinkertainen applikaatio, joka toteuttaa annetun tehtävän äänikomennolla. Applikaatio voi esimerkiksi etsiä halutun tiedon nettisivulta tai muuttaa väriä tai kuvaa.

2. Luo yksinkertainen Speech Synthesis käyttävä applikaatio, joka muuttaa kirjoitetun tekstin ääneksi. Sovelluksessa oltava mahdollisuus säätää äänen nopeutta ja äänenkorkeutta. 