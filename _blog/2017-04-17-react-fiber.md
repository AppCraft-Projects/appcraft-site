---
excerpt: Az utóbbi időkben a React fórumok és konferenciák egyik legfelkapottabb témája lett a Fiber. Rengeteg az infó, de még több a nyitott kérdés a témával kapcsolatban.
title: React Fiber összefoglaló
date: 2017-04-17
tags: [react, fiber, algorithm]
author: Orosz Gábor
short_title: React Fiber összefoglaló
---

Az utóbbi időkben a React fórumok és konferenciák egyik legfelkapottabb témája lett a Fiber. Rengeteg az infó, de még több a nyitott kérdés a témával kapcsolatban.

Engem is sokat foglalkoztatott, az elmúlt másfél-két hónapban rengeteget olvastam róla, valamint számos videót pörgettem végig. Mindeközben vadul jegyzeteltem, ez a cikk lényegében ezeknek a jegyzeteknek egy tömörebb (sic!) összegzése.

Mindenek előtt fontos felhívnom a figyelmetek arra, hogy a Fiber még nincs kész. Folyamatos fejlesztés alatt van, kisebb mértékben még mindig alakul. Adott állapotban nem számítok nagyobb változásra, de biztos tudjátok, hogy működnek az ilyen projektek, nem lehet kizárni.

## Mi a React Fiber?

A **rövid verzió** szerint a core ún. [reconciler algoritmus](https://facebook.github.io/react/docs/reconciliation.html) teljes újragondolása és újraírása.

A **közepesen hosszú** verzió megértéséhez azonban tekintsünk vissza, nézzük honnan jöttünk. A React esetében a killer feature a kezdetektől Virtual DOM volt. Egyszerűbbé tette a fejlesztők dolgát, a felületeket deklaratívan írhattad le, illetve megoldotta az egyik állapotból a másikba transzformálást.

A motorháztető alatt arról van szó, hogy a DOM műveleteket batchekbe gyűjti, egy komoly mértékben optimalizált diff algoritmuson futtatja át, amely csak ott változtat, ahol ténylegesen kell. Ennek következtében nincs se nagy rombolás, se nagy újraépítés. Ezen az úton kikerüli a böngésző DOM szempontjából költséges műveleteket jelentős részét, és futás időben sokkal optimálisabb eredményt nyújt.

![alt text](https://appcraft.hu/assets/img/react-fiber-01.png)

A *valóban hosszú verziót* meg sem próbálom elmagyarázni, ellenben az alábbi kép elég jól összefoglalja. Csak a valóban elszántaknak.

![alt text](https://appcraft.hu/assets/img/react-fiber-02.jpeg)

Tovább lépve egy rendkívül fontos fejlemény volt, amikor némi kísérletezés után rájöttek, hogy ez a koncepció DOM nélkül is egészen kiválóan működik. Ma már számos példa van erre React Native, VR, csak néhány példa ezek közül.

![alt text](https://appcraft.hu/assets/img/react-fiber-03.png)

Fel is darabolták az évek során a React csomagot, és a react-dom már úgymond csak egy a sok közül.
Ezen a ponton vált el a két fő algoritmus, a reconciler és a renderer. Az előbbi fix, a másik cserélhető (pluggable).

## Miért van szükség a Fiberre? Miért ez az újraírás?

Több oka is van ennek, de elsődleges cél a simább animációkra és magasabb felhasználói élmény. Mind több komplex esetben szeretnék elérni a 60 fps-t, amely az a natív appok jobbik részénél manapság már megszokottá kezd válni.

**A komplex eset alatt mit értek?** Nem kell túl nagy dologra gondolni. A mai mobil telefonok már szinte szuper számítógépek, elképesztő grafikát lehet kihajtani belőlük, Full HD, akár 4K felvontás is. Ezzel szemben hányszor látunk akadozó listákat? Pedig azt mennyivel egyszerűbbnek gondolnánk. És ugye ez nem is különösebben komplex.

Még mielőtt belevágnék szemléletetni szeretném a Fiber projekt nagyságát. A Twitter tanulsága szerint, [Jordan Walke](https://twitter.com/jordwalke) és csapata legalább 2014 augusztusa óta töri a fejét ezen, számos verziót a kísérleteztek és prototipizáltak. Legalábbis ekkor adott írt először ezekről. Fiber ezeknek a legutóbbi iterációja.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/RReverser?ref_src=twsrc%5Etfw">@RReverser</a> <a href="https://twitter.com/floydophone?ref_src=twsrc%5Etfw">@floydophone</a> <a href="https://twitter.com/gozala?ref_src=twsrc%5Etfw">@gozala</a> <a href="https://twitter.com/reactjs?ref_src=twsrc%5Etfw">@reactjs</a> <a href="https://twitter.com/sebmarkbage?ref_src=twsrc%5Etfw">@sebmarkbage</a> Many features are all related. Async render, return arrays, multi-threaded reconcile..</p>&mdash; jordwalke (@jordwalke) <a href="https://twitter.com/jordwalke/status/500587022890061824?ref_src=twsrc%5Etfw">August 16, 2014</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Ez az egész munka egyébként publikusan folyt, bárki követhette, akár be is kapcsolódhatott. Simán megtalálható GitHub-on, a Fiber [itt](http://bit.ly/github-react-fiber), és a Fiber DOM pedig [erre](http://bit.ly/github-react-fiber-dom).

Lássuk azonban hogyan érik ezt el ezt a kívánt eredményt.

## Hogy működik a Fiber?

Három fontos újításból áll össze:
- Ütemezés,
- Konkurencia kezelés,
- Reconciler algoritmus.

---

### Scheduling / Ütemezés

JSX-el vagy anélkül, a React UI deklaratívan van kifejezve. A React irányítja, hogyan és mikor frissíti a UI-t, nem a fejlesztő. Úgyanígy van ez az állapotok közötti váltások esetében is.

Pull jellegű paradigmát követ, maga dönti el, nem egy külső utasítás hatására. Ez alól az egyes feladatok priorizálása sem kivétel:
- Felhasználói események (klikk, szöveg bevitel)
- Külső adat feliratkozások (Redux, Relay)
- Animációk (tranzíciók, gesztusok)

A scheduling tehát elkülöníti a magas és az alacsony prioritású feladatokat.

**Vegyünk egy nem is túl egyszerű példát.** Az alábbi videóban két Redux tároló update, és egy UI frissítés történik. Az előbbi 1000ms, az utóbbi 16ms időközönként történik. Ezt láthatod az alábbi videón.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Qu_6ItnlDQg" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Tegyük fel, hogy a magas felhasználói élmény érdekében stabil 60 fps-re törekszel… melyiket vennéd előre?

**A válasz simán adja magát.** A UI frissítést egyszerűen nem sorolhatjuk , akkor a másik elrabolja a fókuszt, rendering sorban el fogja dobálni a frameket. A felhasználó persze rögtön észre fogja venni ezt, és máris csökkenne az élmény.

![alt text](https://appcraft.hu/assets/img/react-fiber-04.png)

Ezzel összevetve sokkal kevésbé fáj az, ha pár frame-el később frissül be Redux tároló.

Az új algoritmus tehát optimalizál, hogy a UI frissítések és az animációk minél simábbak legyenek.

*Csomó más kis optimalizációt, illetve priorizációs stratégiát is bevetettek, ezekből most csak kettőt emelnék ki:*
- Prioritást kapnak azok a komponensek, amelyek nem láthatóak aktuálisan. A láthatót veszi előre. (Ezt csinálja egyébként a react-virtualized lib is egy úgynevezett windowing módszerrel.) Erre jó példa egy 1000 elemű lista, ahol éppen csak 5–10 elemet látni.
- Ha nagy komponens fát kombinálunk azzal, hogy az egyes elemek költséges műveleteteket végeznek, akkor UI update kicsit sem lesz sima, és hamar csúnya dolgokat fog látni a felhasználó. Azonban, a scheduling átalakításával, és a fő animáció priorizálásával, ezen sokat lehet segíteni. Avagy UI update előre, költséges műveletek utána.

---

### Concurrency / Konkurencia kezelés

Figyelem, még mindig egy szálon gondolkodunk! De ez is az egész React lényeg, hogy lehet ezt az egy szálat a lehető legjobban kihasználni.

A React olyan tehát olyan mint egy manager, aki jó a feladatok felosztásában, és azok priorizálásában. Valamint eközben figyeli az időt, mire és mennyi ment el.

*Ismét a priorizálásból indulunk ki:*
- Éppen fut egy alacsonyabb prioritású munka, de közben megérkezik egy fontosabb.
- Megállítani az alacsonyabb prioritásút.
- Futtatni a fontosabbat.
- Folytatni a kevésbé fontosat, ahol abban maradt.

**De ez lehet trükkös, ha ez a munka éppen egy rendering, akkor miképp történik ez?** Az egyes kompomnensekre, és a render folyamatra is funkciókként és alfunkciók egész soraként kell gondolni. Amit csinálnak az egy funkció hívás megszakítása.

**De hogyan oldható ez meg JS-ben?** Erre logikus válasz lehetne generátorok, amelyek a konkurencia alap építőelemei, megszakíthatóak, elvben mindent tudnak, ami ide kell, azonban más úton mentek.

**Mégis milyen úton?** A legegyszerűbben talán a “debugger;” híváshoz hasonlíthatnám. De nagy vonalakban ugyanezt kapod, ha a Chrome Dev Toolsban megállítod a végrehajtást egy sima breakpointtal. Látod a call stacket, mindent, teljesen megszokott.

*Ehhez nagyon hasonlót csinálnak ők is:*
- Megállítják egy funkció végrehajtását.
- Ha bejön valami fontosabb, akkor megállítják, félreteszik a heapben (stashing) a call stacket.
- Betöltik a fontosabb saját stackjét, és azon futtatják azt.
- Majd, amikor végzett, akkor betöltik a stashről a megszakított call stacket, és folytatják a futtatást.

Mindezt tetszőleges szinten egymásba lehet ágyazni (nesting).

Innen nézve a Fiber a végrehajtási stack újraimplementálása is, persze a React komponensekre specializálva. Egy virtual stack frame, a stackeket a heapre memóriába mozgatva elég nagy játékteret kaptak. De innentől mindez már szinte sötét mágia szinten van.

---

### Reconciler algoritmus

Az előbbi kettő ennek a magasabb szintű koncepciónak ágyaz meg. A korábbi algoritmus úgy működött, és egyúttal ezzel veszített sok időt, hogy a a fa egyes ágait teljes mélységében bejárta.

![alt text](https://appcraft.hu/assets/img/react-fiber-05.png)

Az új algoritmus azonban abban különbözik, hogy a fának akár egy kis részét is feldolgozhatja, hogy utána máshol folytassa, teljesen más a working loop képe ezáltal. Megfigyelhető, hogy a korábbi képességekre épít, megszakítás és prioritások.

![alt text](https://appcraft.hu/assets/img/react-fiber-06.png)

De szükség volt még más változtatásra is, hogy mindez jól működjön. Gondold el, hogy elkezdi frissíteni az elemeket a UI-on, de csak részlegesen fejezi be a frissítés előtt. Ez rögtön inkonzisztens állapotot eredményezne, és rosszul is nézne ki.

![alt text](https://appcraft.hu/assets/img/react-fiber-07.png)

Hogy ezt kivédjék, a folyamatot két részre bontották:
Előbb reconceliation / render, felépíti a Fiber work-in-progress fát, kitalálja a változtatások listáját.
Majd utána commit, amikor a tényleg változtatásokat végrehajtja a DOM-ban.

És itt jön a csel, még az előbbi megszakítható, az utóbbi nem. Erre szükség is van, mert az ütemezőtől mindenkinek limitált ciklusidő jut. Innentől tényleg úgy működik szinte mint egy operációs rendszer ütemezője.

![alt text](https://appcraft.hu/assets/img/react-fiber-08.png)

A requestIdleCallback fukcióval igényelnek ciklusidőt, már amelyik böngésző támogatja, a többi esetben polyfillt használnak. A legmagasabb prioritású mindig dolgozik egy-egy szeletet, utána megszakítás.

A Fiber fa építése is nagy előlelépés a múltbélihez képest. Ugye már nem kell egyenesen bejárni az ágakat. Ahol lehet simán klónoznak elemeket.

![alt text](https://appcraft.hu/assets/img/react-fiber-09.png)

Valamint csak azokkal az ágakkal foglalkoznak, azokat járják be, ahol ténylegesen volt változás.

![alt text](https://appcraft.hu/assets/img/react-fiber-10.png)

A commit, avagy a tényleges DOM-ba írás csak a folyamat végén történik meg.

## Mire lesz képes?

Első körben nem céljuk semmi új feature, fejlesztői oldalról nem fog különbözni a mostanitól. A lényeg, a priorizáció, ütemezés és a konkurencia kezelés a háttérben fog működni.
Ez alól csak egyetlen kivétel van, mégpedig az, hogy a render már képes lesz több elemet visszadni. Ez már rég várt változás volt, viszont az API-kat nézve más nem lesz.
Egyelőre nem kínálnak majd olyan API-okat, amire pl olyan libek mint a react-motion tudnának építeni, hogy az animációk prioritásával játszanak. Talán később.
Minél kevesebb jelenleg működő appot szeretnének eltörni. Elvben nem kell hozzá előre dolgozni. Feltehetőleg simán működni fognak, ahogy ma is vannak. Persze, ha valami disznóságot csinált a fejlesztő, valami anti patternt, akkor fejre is állhat a világ.

(Itt kiegészítésként meg kell említeni, hogy a setState() hívás aszinkron lesz, ezeket idővel át kell alakítani aszinkronná, de egy ideih marad a korábbi verzió is.)

*Csak néhány dolog, ami a jövőben várható, tényleg csak felsorolásszerűen:*
- Integrált layout kezelés, mint ahogy az már React Native esetében most is történik. Komolyan tizedelhetné a webapp-okban most túlzottan burjánzó div-ek számát.
- Lehetőséget kap a csapat a kódbázisuk kipucolására, egyúttal egyszerűbbé tenni a kontribútálást.
- A különböző ágakat külön kis workerek renderelik majd.

## Hol tart most? Mikorra várható?

A Fiber első verziója már nagyon közel van, a *React 16-al* várható. De ebben a verzióban még kompatibilis módban fog futni, szinkron ütemezővel, ahogy a mostani React verziók is.

Ez a verzió már jelenleg is kész van, a Facebook és a Facebook Messenger már ezt használja. Viszont az SSR (Server Side Rendering) és a React Native még két olyan nagy téma, amik még hátra vannak. *Az első stabil verzió valamikor nyáron várható.*

A React 17 izgalmasabb lesz, ott kapcsolják be alapértelmezetten az aszinkron ütemezőt, ettől a ponttól fogjuk a valódi előnyeit élvezni, de addig még sok munka van hátra.

## Érdekes és hasznos linkek
*A jobb források egyszerűen felsorolva:*
- [Kész van már?](http://bit.ly/is-fiber-ready-yet)
- [Andrew Clark tavaly nyári React Fiber architektúra összefoglalója.](http://bit.ly/react-fiber-architecture)
- [Sebastian Markbåge a Fiber működéséről.](http://bit.ly/how-react-fiber-works)
- [Andrew Clark szuper Fiber összefoglaló előadása.](http://bit.ly/react-next)
- [Dan Abramov és Andrew Clark Fiberes webinára.](http://bit.ly/react-fiber-webcast)
- [Lin Clark szokásos képregényes bevezetője a Fiberbe.](http://bit.ly/lin-clark-react-fiber-intro)
- [Reactiflux Q&A kiemelések Andrew Clarktól.](http://bit.ly/fiber-qa)