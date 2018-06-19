---
excerpt: Ha dolgoztál már valahol nagyobb projekten, akkor jó eséllyel eszedbe jutott, hogy az általad írt kódot talán megérné nyílt forráskódúvá tenni. Ebben a cikkben összefoglalom a folyamat előnyeit és a hátrányait, valamint ha még sosem foglalkoztál nyílt forráskódú szoftverrel, adok pár ötletet, hogy miért lehet hasznos, ha így döntesz.
title: Miért nyissuk meg a forrást?
date: 2017-04-16
tags: [oss, programming, licensing]
---

> Ha dolgoztál már valahol nagyobb projekten, akkor jó eséllyel eszedbe jutott, hogy az általad írt kódot talán megérné nyílt forráskódúvá tenni. Ebben a cikkben összefoglalom a folyamat előnyeit és a hátrányait, valamint ha még sosem foglalkoztál nyílt forráskódú szoftverrel, adok pár ötletet, hogy miért lehet hasznos, ha így döntesz.

Nyílt forráskódú (továbbiakban [OSS](https://en.wikipedia.org/wiki/Open-source_software)) szoftveren dolgozni kifejezetten szórakoztató. Te választhatod meg, hogy min dolgozz, mikor tedd azt és hogyan. Ha másoknak számára is hasznos kódokat írsz, akkor az emberek előbb-utóbb elkezdik használni azt - és ekkor kezdődnek az igazán érdekes dolgok.

## Pull request-ek (PR)
A felhasználóidnak az esetek nagy részében nem lesz idejük vagy kedvük hozzájárulni a projektedhez. Azonban van pár programozó, aki kifejezetten szeret javításokat küldeni, amiket átböngészve rájöhetsz, hogy mások hogyan használják a programodat. Ha magának a PR-nek a minősége jó (tehát javítás vagy új feature fejlesztés, ami tesztelve van) akkor jó pár dolgot tudsz tanulni belőle:
- Látni fogod __pontosan__, hogy mások hogyan használják a programodat.
- Azt is látni fogod, hogy __hogyan szeretnék__ használni.
- Illetve betekintést nyerhetsz a fejlesztő perspektívájába is, ami segíthet új szemszögből látni a projektedet.

## Hibajelentések
Azok a felhasználók, akik nem akarnak (vagy tudnak) hozzájárulni kóddal a projektedhez, de szeretnének rávilágítani egy hibára, hibajelentést fognak küldeni neked. A legtöbb platform, ahol OSS kódot lehet host-olni rendelkezik olyan funkcióval, amellyel ezt meg lehet tenni (például [GitHub](https://github.com/). Habár ezek nem annyira hasznosak, mint egy PR, tekinthetsz rájuk úgy, mint ingyenes funkcionális tesztelésre. Ahogyan a PR-ek, úgy a bug reportok is hasznosak abból a szempontból, hogy rávilágíthatnak olyan részletekre, amelyekre nem is gondoltál a tervezés során.

## Feature request-ek
Néha-néha érkezik pár ötlet a külvilágból, feature request-ek formájában. Ezek szintén elég értékesek, mert általában *valódi üzleti igényeket* oldalnak meg, illetve ha tanácstalan lennél, hogy merre haladj tovább, akkor segíthetnek kijelölni a projekted irányát.

## Hozzájárulók és társak
Előfordulhat, hogy valakit annyira érdekel a projekted, hogy többször is hozzájárul, vagy akár teljes értékű csapattaggá is válhat, ha kiderül, hogy jól tudtok együtt dolgozni. Mondanom sem kell, hogy ez talán a legjobb dolog, ami történhet veled - és annak is egy nyilvánvaló jele, hogy jó irányba haladsz a projekteddel.

## Hátulütők
Annak ellenére, hogy az OSS fejlesztés sok előnnyel jár, vannak hátulütői is, amikbe előbb-utóbb bele fogsz futni. Ezeknek a többségét ki lehet küszöbölni, de jó, ha előre felkészülsz rájuk, ha nem akarod, hogy a projekted túlságosan időrablóvá váljon.

## Alacsony színvonalú hozzájárulások

Csak idő kérdése, hogy mikor kapod meg az első PR-edet a pokolból. Az is lehet, hogy törni fogja a build-et, vagy csak simán nincsenek hozzá tesztek. Láttam olyan PR-t is, amiben a fél projektet refaktorálták, csak hogy egy generikus típus paramétert betehessenek, aminek nem volt valódi előnye sem. Ezeknek az elkerülésére az alábbi módokon tudsz felkészülni:

- Csapj hozzá egy COC ([Code of Conduct](https://en.wikipedia.org/wiki/Code_of_conduct))-ot a projektedhez. Egy jó példa [itt](http://contributor-covenant.org/version/1/1/0/) található. Ez azért fontos, hogy ne tűnj majd hálátlannak, amikor valaki a projektedre áldozza az idejét. Ha van egy doksi, amelyben összeírod, hogy miképpen tudnak mások hozzájárulni a projekthez, akkor ez elkerülhető.
- Tegyél fel egy CLA ([Contributor License Agreement](https://en.wikipedia.org/wiki/Contributor_License_Agreement))-t. Ez segít abban, hogy másoknak is egyértelmű legyen, kié a projekt szellemi tulajdona ([Intellectual Property](https://en.wikipedia.org/wiki/Intellectual_property)). Ha ezt nem teszed meg, akkor belefuthatsz kötekedő emberekbe, akikkel vitázhattok ítéletnapig. Egy jó példa található [itt](https://github.com/ReactiveX/RxJava/blob/2.x/CONTRIBUTING.md).
- Használj [Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration) rendszert. Ha jól csinálod, akkor a meló java részét delegálhatod egy programnak, amely automatikusan lefordítja a hozzájárulásokat, sőt egyes platformok (pl. GitHub) nagyon könnyen integrálhatók build eszközökkel, mint a [Travis](https://travis-ci.org/), vagy kód elemző szoftverekkel, mint a [CodeCov](https://codecov.io/), ami kommentelni is tud PR-ekre. Egy példát [itt](https://github.com/Hexworks/hexameter/pull/24) láthatsz.

### Túl sok hűhó a projekted körül
Lehet, hogy kicsiben kezded, de ha elég időt beleraksz, akkor bármelyik projekt a következő Halál Csillaggá válhat. Az sem segít, ha népszerű lesz a programod és elárasztanak a PR-ek és a hibajelentések. Habár ezek alapvetően jók a projekt szempontjából, előfordulhat, hogy azon kapod magad, hogy lett egy második főállásod.

Erre a megoldás az lehet, ha bevonsz másokat is társként a projektbe, illetve ha nekilátsz SCRUM-ot vagy Kanban-t használni a projekt menedzseléséhez.

### Licenszelési problémák

Előfordulhat, hogy egy túl megengedő licensz mellett döntöttél a projektedhez (mint pl. a MIT), vagy éppen fordítva: rájöttél, hogy a feltételek túl szigorúak (pl. AGPL). Ahhoz, hogy ezt elkerüld érdemes [itt](https://choosealicense.com/) körülnézni.

## Mit mondhatsz a főnöködnek?

Ha esetleg úgy gondolnád, hogy van olyan kódod, aminek érdemes megnyitni a forrását, vagy éppen a munkahelyeden vannak olyan projektek, amelyek erre alkalmasak, akkor egy elég nehéz feladat áll előtted: *meggyőzni a főnöködet*. Összegyűjtöttem pár tippet, ami segíthet ebben:

> - A forrás megnyitása *szinte semmilyen költséggel nem jár*.
> - Nem kell minden forrást megnyitni, elég csak azokat a részeket, amelyek mások számára is hasznosak lehetnek. Ez abban is segít, hogy elgondolkodjatok azon, hogy érdemes-e modularizálni a kódot.
> - *Ingyen* hibajelentéseket, PR-eket vagy hibajavításokat fogtok kapni.
> - A fejlesztők szeretnek olyan helyen dolgozni, ahol tudják, hogy a kód, amit írnak nyílt, mert így a hozzájárulásuk jobban láthatók a külvilág számára.
> - Nem csak te, de a cég is kap némi *pozitív karmát*.
> - Ha megnyitod a forrást, akkor kétszer is meggondolod, hogy hozzáadod-e azt a hekket, amit kitaláltál, mivel a saját megítélésedet is kockáztatod ezzel. Ettől a kód némileg jobb minőségű lesz.

Véleményem szerint a forrás megnyitása sokkal több előnnyel jár, mint hátránnyal, így érdemes próbát tenni vele. Ha esetleg van már tapasztalatod vagy más véleményen vagy, akkor kíváncsian várom a hozzászólásodat a komment szekcióban.



