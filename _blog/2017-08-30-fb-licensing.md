---
excerpt: Tíz éve még hatalmas szám volt, ha egy IT óriás cég megnyitotta bármely technológiájának forrását, ma azonban ennek az ellentettjét nehéz elképzelni.
title: A Facebook license mizériáról érthetően
date: 2017-08-30
tags: [react, licensing, bsd, patents, facebook]
---

![alt text](https://appcraft-projects.github.io/appcraft-site/assets/img/fb-license-01.png)

Tíz éve még hatalmas szám volt, ha egy IT óriás cég megnyitotta bármely technológiájának forrását, ma azonban ennek az ellentettjét nehéz elképzelni. Oda jutott a helyzet, hogy gyakorlatilag egyik jelentős szereplő sem maradhat ki.

Ezen időszak során azonban jogi oldalról szemlélve is egyre cizelláltabbá vált a nyílt forráskódú projektek kezelése.

Ami pedig jellemzően nehezíti a megértést, a kellemetlen meglepetésekről nem is beszélve.

Ennek következtében is alakulhatnak ki időről-időre olyan kacifántos ügyek, mint amelyen pár hete a Facebook licensek esetében jött fel.

## Egészséges kétkedés

Az egész sztorit Raúl Kripalani (Apache Foundation) [írásával](http://bit.ly/raul-facebook-license) indult, szó szerint futótűzként járta be a közösségi csatornákat.

Röviden összefoglalva felhívta a startupok figyelmét Facebook licenselési gyakorlatára a React példájával, és ellenjavallotta annak használatát.

Bár a React kerül jellemzően szóba, de azon túl még nagyjából egy tucat Facebook projekt érintett, többek között a szintén felkapott GraphQL is. Most viszont fókuszáljunk kizárólag a Reactra, könnyebb lesz követni.

Nem tartom magam megmondó-embernek a témában, viszont dolgozunk Reactos projekten, így mindenképp szükség volt egy objektív kép kialakítására. Ennek tanulságait osztom most meg veletek.

Fontos hangsúlyozni, minden alaposság ellenére kimaradhattak lényeges részletek, meglehet az értelmezésem sem mindig teljes. *Ha egészen biztosra szeretnél menni, érdemes felkeresni egy a témára specializálódott ügyvédet.*

## Apache 2.0 vs Facebook BSP+Patent

Közel sem fekete-fehér helyzetről van szó, Raúl postjában vannak jó pontok, de úgyszintén féligazságok is. Nem annyira egyszerű a verdikt, ahogy azt elénk tárta.

Az alaposabb megértés érdekében érdemes több dolgot is tisztán látni. Egyrészt a nyílt forrású kód használata és a szabadalmak erősen elválnak egymástól, nem szabad összemosni azokat.

Másrészt egy jelentős különbség van az *ASF (Apache Software Foundation) Apache 2.0* és a *Facebook féle BSD+patent* licensek között. Máris kifejtem:
- **ASF**: X szabadalmuk használójaként, ha pereled őket X miatt, akkor visszaveszik a licenszet X-re.
- **FB**: X szabadalmuk használójaként, ha perled őket bármely szabadalmuk miatt, akkor visszaveszik a licenszet X-re.

Ezek alapján úgy látom, hogy az ASF-hez hasonlóan a Facebook a BSD-3 licenset olyan módon egészítette ki a Facebook, hogy egyúttal a szabadalmakról is rendelkezett.

A fő különbség tehát az, hogy az ASF esetében adott licensz kapcsán pereskedve veszted el a használat jogát. Viszont a Facebook esetében bármely szabadalmukat perelve elveszthetel minden licenszet, nem csak az érintetteket.

Az *elveszted a licenset* részt megéri alaposan kifejteni, sokszor félreértett fogalomról van szó, pedig a helyzet egyik kulcsát adja. Konkrétan azt jelenti, hogy amikor szabadalmi ügyben perled a

Facebook visszaperelhet az általad használt nyílt forrású projekteket érintő szabadalmak kapcsán. Tehát nem egy automatikus következményről van szó.

Alapvetően a nyílt forrású projekteiket egyfajta falként használják a szabadalmi portfóliójuk védelmében.

Ez eddig nem hangzik túl jól, SŐT, viszont jár néhány fontos előnnyel is:

- Egyfelől írásos ígéretet tesznek, hogy nem fognak perelni téged a szabadalmak miatt. Ha azonban Te teszed ugyanezt, az már más téma.
- Nem használnak copyleftet, ami a későbbi potenciális szabadalmi trollkodásnak megy elébe.
- A sima BSD esetében elvi lehetőség van arra, hogy a tulajdonos úgy döntsön, hogy a projekt felhasználóit license díj megfizetésére kötelezze. (A szabadalom licenszelését el kell választani a nyílt forrású kód felhasználásától, külön dolgokról van szó.)

## Mi van akkor ha?

Terjünk rá a nehezebb témákra, amit sokan mások felhoztak a napokban.

**Előbb** nézzük a parásabbat. Tegyük fel egy **startup épít egy terméket / szolgáltatás, amely Reactra épül, és amit a Facebook idővel részben vagy egészben lemásol**. Nem kell messzire menni, nem voltak különösebben szívbajosak a Snapchat esetében sem.

Ezen a ponton adódik egy lényeges kérdés, **tervez a cég szabadalmat benyújtani?** Nem szokás ilyet hirtelen felindulásból csinálni. Alapvetően bonyolult, hosszadalmas és drága eljárásról van szó. Komolyan vehető portfóliót építeni különösképp az. Amennyiben nincs ilyen tervben, akkor az ügy ezen a ponton már le is zárult.

A következő fontos kérdés: **tervez a cég az USA piacán üzleti tevékenységet folytatni?** Amennyiben nem, akkor ez az egész szabadalmi / license kérdés fel sem fog merülni.

Egyébként egy gondolatot még hozzá szeretnék tenni, aki tervezett már hasonlót magyarországról indulva bizonyosan tudja, hogy sokszor mennyire nem triviális kérdésről van szó még egy szoftver esetében sem.

Tegyük fel, hogy mindkettőt tervezi, illetve akár folyamatban van, sőt még a másolás esete is fennforog. Ebben az esetben sem az az első, hogy a szabadalom kapcsán perbe fogod a Facebookot, vannak ennél egyszerűbb és olcsóbb opciók is.

A Facebook perelhető a copyright megsértése, kereskedelmi titkok eltulajdonítása, és még sok más okból is. A React license használatát kizárólag akkor vonják meg, ha szabadalom kapcsán perli a startup a Facebookot. Ráadásul, ha a másik oldal perek, akkor ilyen megvonástól nem is kell tartani.

Szabadalom kapcsán egyébként sem triviális perelni. Végig olvastam pár írást ennek kapcsán, és szerintem kifejezetten beszédesek a nagyságrendek. Egy ilyen kaliberű ügy komoly ügyvédi irodánál 2-3 milliónál kezdődik, ezt az összeget le kell tenni. Azonban a verdiktig tartó pár év alatt akár $20–30 millió körüli végszámla is elérhető. Ez tutira nem a kis cégek vagy startupok területe!

Mindezzel azt szeretném érzékeltetni, hogy ez a probléma főképp érett és tehetős startupokat lehetnek ilyen ügyekben érintettek.

Ha azonban a startup mindenképp ilyen irányba menne, akkor egy ilyen esetben a frontend újraírás költségével érdemes számolni. Viszont mielőtt ilyen döntésre jutna a startup érdemes a további pontokat is alaposan mérlegelni.

---

**Másrészt** felmerülhet a fordított verzió is, amikor is a **startup egy Facebook konkurens terméket épít**. Ebből természetesen simán lehetnek különböző jogi viták.
Ilyenkor akár szabadalom, akár más úton is perelhet a Facebook, viszont ilyenkor a fentiek a startupot védik, a React licenszét nem vonják vissza.

---

**Harmadrészt** Raúl a startupok kapcsán azt az érvet említi még, hogy **sok potenciális vásárló bottal se piszkálná a startupot, ha ilyen licenset használ**. Jogos és fontos felvetésről van szó, DE érdemes még néhány szempontot átgondolni ennek kapcsán.

Akvizíció esetében a vásárló alaposan körbe fogja vizsgálni a megvásárolni kívánt startupot, amely során a technológiai és számos más terület egyaránt érintve lesz, így a különböző licensek is. Mindezek természetesen befolyásolhatják az alkudozási folyamatot.

**A.** A vásárló cég és a Facebook között már létezhet valami kereszt-licensz megállapodás, amely többek közt ezt is tartalmazza. Ez esetben nincs gond.

Ezt támasztja alá, hogy megannyi komoly cég épít manapság a Facebook nyílt forrású technológiáira, bizonyosan tisztában vannak a licenselés részleteivel.

Tényleg egészen tekintélyes a lista, [Apple](https://developer.apple.com/documentation/), [Microsoft](https://dev.office.com/fabric) és [Skype](https://microsoft.github.io/reactxp/blog/2017/04/06/introducing-reactxp.html), [Amazon](https://twitter.com/theopak/status/799072706331295744), [Uber](https://eng.uber.com/tag/react/), [Tesla](https://gist.github.com/timdorr/35c95d0037c5334d143b49c25db303c9), [Netflix](https://medium.com/netflix-techblog/netflix-likes-react-509675426db), [Salesforce](https://www.lightningdesignsystem.com/) és [Quip](https://medium.com/@btaylor/react-with-c-building-the-quip-mac-and-windows-apps-c63155c1531b), [AppDynamics és Cisco](https://www.cisco.com/c/en/us/about/corporate-strategy-office/acquisitions/appdynamics.html), [AirBnb](https://medium.com/airbnb-engineering/rearchitecting-airbnbs-frontend-5e213efc24d2), [Twitter](http://m.twitter.com/), [Pinterest](https://medium.com/@Pinterest_Engineering/how-we-switched-our-template-rendering-engine-to-react-a799a3d540b0), [PayPal](https://www.paypal-engineering.com/2015/04/27/isomorphic-react-apps-with-react-engine/), [Slack](https://slack.engineering/rebuilding-slacks-emoji-picker-in-react-bfbd8ce6fbfe), [Dropbox](https://www.dropbox.com/paper). Kisebb meglepetés, de a szabadalmi csörtéjük után a [Yahoo](https://yahooeng.tumblr.com/post/101682875656/evolving-yahoo-mail) (mamár Verizon) is a listán van. Sőt, a pletykák szerint még a Google is használja belsős projekteken.

Egyébként nemrégiben a Netflix ügyvédei ismételten körbejárták a React licenszeket, és továbbra sem találtak vele problémát. Felteszem változna a hozzáállásuk, ha a Facebook egy szép napon indítana egy hasonló streaming szolgáltatást, de egyelőre erről nincs szó.

**B.** Fontos tisztázni **mi jelenti a cég esetében a tényleges üzleti értéket**. Természetesen vannak cégek, ahol a kliens oldalon jelentős érték van, ráadásul ha még potenciálisan közel is áll a Facebook területeihez, akkor nem választanám a Reactot.

Ez azonban szerintem a szűkebb réteg, manapság jellemzően inkább a szerver oldali üzleti logika, algoritmusok, adatok, illetve a szép számú felhasználói / ügyfél bázis szokták a valódi értéket képviselni. Ha ez a helyzet, akkor lehet jó választás.

**C.** Számos alkalommal láttam olyat, hogy **felvásárlás után a terméket UI oldalról teljesen újra tervezték**, hogy jobban illeszkedjen az új tulajdonos arculatához, vagy épp más termékeihez.

**D.** Arról nem is beszélve, hogy az **új tulajdonos gyakran ragaszkodik a saját technológiai stackjéhez**, ami kapcsán a frontent át- vagy akár újraírása elkerülhetetlenné válik.

**E.** Láttam már olyat is, hogy a **megvásárolt alkalmazásokat az új tulajdonos több-kevesebb lépésben a saját termékekébe olvasztotta**. A publikus példák közül lásd az elmúlt két évből sokunk kedvenceit, a Sunrise Caledart vagy a Wunderlistet, amelyeket a Microsoft darál be az Outlookba.

## Milyen más opciók vannak?

Tegyük fel, hogy bármelyik okból kifolyólag mégsem szeretnél Reacttal dolgozni / folytatni. Ez is érthető, ez esetben is van számos lehetőséged, válasszuk azonban szét az eseteket.

**Nehezebb dolgod lesz, ha erre építetted a már működő szolgáltatásod.** Ez esetben léteznek olyan drop-in replacmentek, mint a Preact és az Inferno, mindkettőre elég könnyű átállni, mindkettő MIT licenssel dolgozik.

Viszont sajnos nem teljesen problémáktól mentesek ezek a megoldások sem. Nem könnyű átlátni, hogy ezeknél a szabadalmi kérdések mennyire rendezettek, felteszem nem azok, és egy perben ugyanúgy sértenék a szabadalmakat.

**UPDATE #1** Sőt, bizonyos szempontból még rosszabb is lehet a helyzet. Mivel ezek licensében nem szerepel a szabadalmi kitétel. Feltehetőleg a Facebook a React kapcsán a [Virtual DOM és a diffing-algoritmusokat](https://github.com/Matt-Esch/virtual-dom) védette le. Így adott esetben, ha a Facebook beperel, akkor potenciálisan ezeket is támadhatja, nincs olyan védelem, mint a React license-e esetében.

Valamint ott van még az az eset is, ha univerzális technológiai csomagban gondolkodtál, és a [React Native](https://facebook.github.io/react-native/) is használatban van. Nos, sajnos ez esetben szó nincs ilyen egyszerű csere-berés megoldásról.
Egyszerűbb dolgod lesz azonban, ha még nem használod, csak a lehetséges technológiákat vizsgálod. Ilyenkor számos jó megoldásból választhatsz.

Egyrészt a web komponensek kifejezetten platform közeli és jövőálló megoldásokat kínálnak. A modern böngészők szinte teljes lefedettséget kínálnak, de azért a [Polymer](https://www.polymer-project.org/) szuper-vékony polyfill rétegét érdemes használni. React Native szerű megoldást nem kínál, de a [PWA](https://developers.google.com/web/progressive-web-apps/)-k Androidon már most is tök jók.

Ha valami igazán React szerűt szeretnél, akkor a [Vue.js](https://github.com/vuejs) jó választás lehet. Kicsi, egyszerű, gyors, és az Apache által gondozott [Weex](https://weex.incubator.apache.org/) projekt egy egészen fejlett React Native variánst is kínál.

---

**UPDATE #2** Az előző updateben leírtak a Vue.js esetében is fennállhatnak, a Virtual DOM és a diffing-algoritmusok miatt ez is lehet adott esetben bajos.

---

**UPDATE #3 A Wordpress-ügy**
Egészen érdekes helyzet alakult ki múlt héten az [Automattic háza táján](https://ma.tt/2017/09/on-react-and-wordpress/). A Wordpress Calypso és a Guttenberg projektek kifejezetten nagyobb méretű Reactos projekteknek számítanak. Illetve már csak számítottak, múlt idő, mivel rövid távon migrálni terveznek erről a technológiai csomagról.

Érdemes kiemelni az idoklásnak egy részét:

> I think Facebook’s clause is actually clearer than many other approaches companies could take, and Facebook has been one of the better open source contributors out there. But we have a lot of problems to tackle, and convincing the world that Facebook’s patent clause is fine isn’t ours to take on. It’s their fight.

Magyarán nincs bajuk a Facebook licensének tartalmával, a cég nem is rendelkezik komoly szabadlmi portfólióval, nem ezen okból váltanak. Sokkal inkább azért tartanak attól, mert az ügy számos ügyfelüket eltántoríthatja a termékeik használatától.

Úgy érzik ez nem az Ő csatájuk, nem szeretnének részt venni benne, ezt a helyzetet a Facebooknak kell tisztáznia.

Ezt az ügyet egyébként már azért is érdekes lesz követni, mert ebből láthatóvá válik mennyi idő az átállás nagyobb projektek esetében. Egyébként ahogy látom a [Mithrilt](https://mithril.js.org/) fontolgatják [helyette](https://github.com/Automattic/wp-calypso/issues/650#issuecomment-235086367).

## Eddig nem volt példa ilyen ügyre

Persze nem jelenti azt, hogy a jövőben sem lesz. Abban egészen viszont biztos vagyok, hogy a Facebooknál rendkívül óvatosnak kezelik majd ezt az egész kérdéskört.

Láttátok mekkorát ment a sztori, amikor csupán a lehetőség merült fel, hát még ha el is sütik ezt a fegyvert, egyhamar igazi kapitális öntökönlövés és PR rémálom alakulhat.

Ami pedig feltehetőleg visszafordíthatatlan károkat okozna a Facebook nyílt forrású ökoszisztémájában, cégen belül és azon kívül egyaránt.

Pedig ennek az ökoszisztémának az építésére az elmúlt években rengeteget áldoztak mind pénzt, mind energiát. Konferenciák, workshopok, meetupok, százával kisebb és nagyobb események. Rengeteg tehetséget vonzottak be, de az eredmények ezen felül is magukért beszélnek, nagy dolgot épített a közösség.

Biztos vagyok abban, hogy egy ilyen lépés szerencsétlen folyamatokat indítana meg, amely után számos nagyszerű OSS szakember, legyen Facebook alkalmazott vagy épp külsős, elfordulna a cégtől. Ez pedig talent menedzsment és rekrutálás szempontjából hatalmas csapást jelentene nekik.

Úgy gondolom ezerszer megfontolnák, megéri-e nekik ehhez a fegyverhez nyúlni, és ennek következtében mindezeket kockára tenni.

## Utolsó gondolatok

Annyi biztos, hogy minden érintett cégnek alaposan meg kell vizsgálnia ezt az ügyet a saját kontextusában. Nem egyértelmű és rengeteg szempontot kell figyelembe venni.

Végletesen leegyszerűsítve a szummája így hangozhat:
- A szabadalmak költségesek és időigényesek, ez már a nagyobbak játéka, az ilyen perek különösen.
- Igazán komoly halnak kell lenned, hogy megérje nekik rombolni az OSS programjukat, amire piszok sokat költöttek.
- Ha bármilyen okból úgy érzed, hogy a Facebookkal szabadalmak kapcsán tengelyt fogtok akasztani **az USA piacon**, akkor jobb, ha nem használod a technológiai stackjüket, vagy idővel migrálsz arról. Mondjuk a fentiek egyikére.
- Ha felvásárlásra játszol, akkor vizsgáld alaposan körbe a potenciális vásárlók múltját a Facebook nyílt forrású technológiák kapcsán. Látni fogod volt-e ilyen, vagy sem, és lesz arról ötleted, hogy ez jelenthet-e a későbbiek során valami gondot.
- Ha ezek nem merülnek fel, akkor használd nyugodtan, elképesztően pörgős ökoszisztémáról van szó, a közösség naponta készít új és igazán produktív eszközöket.

**Köszönöm, hogy elolvastál!**
