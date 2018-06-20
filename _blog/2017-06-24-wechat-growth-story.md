---
excerpt: A conversation UI egy kiváló példa erre. Meglehetősen felkapott trend lett belőle, és felénk is teret kezdett hódítani magának.
title: A WeChat növekedési sztori
date: 2017-06-18
tags: [react, licensing, bsd, patents, facebook]
---

A [AppCraft csoportban](http://bit.ly/bpm-fb) már számos alkalommal elővettem a WeChat-et ([itt](http://bit.ly/sm-china-wechat), [itt](http://bit.ly/fb-f8-2015-ov), [itt](http://bit.ly/mobile-web-direction), [itt](http://bit.ly/meanwhile-in-asia), és [itt](http://bit.ly/mobile-ui-china)). Rendkívül érdekesnek tartom követni, egyfelelől a kulturális különbségek miatt, másrészt érdekes látni, ahogy ott kitalál dolgok felénk is átszivárognak.

A *conversation UI* egy kiváló példa erre. Meglehetősen felkapott trend lett belőle, és felénk is teret kezdett hódítani magának. Persze még jókora előnyben vannak. Náluk a *WeChat univerzális UI*, egy tényleges **kapu az internetre**, de nevezhetjük *meta-platformnak* is. Szinte mindent összekötnek vele, üzletek, infók, foglalás, rendelés, fizetés, amit akarsz. Gyakran automatizálva működnek, emberek nélkül.

![alt text](https://appcraft.hu/assets/img/wechat-story-01.png)

Egyébként ez a hozzáállás nekem kifejezetten furcsa. Még a nyugaton inkább darabolnák az appokat, addig Kínában egybe lapátolják a látszólag nem passzoló funkciókat. Hangsúlyozom látszólag, meg kell érteni őket.

Ezért is örülük az olyan [postoknak](http://bit.ly/wechat-growth-product), mint amit Anu Hariharantól olvashattam néhány napja, ami végig veszi a *WeChat* kevesebb mint 6 éves fejlődését. Hogyan pivotált a *Tencent* kifejezetten desktop irányból, nem félve attól, hogy önmagukat disztuptálják.

Pedig mennyire nem volt sikeres az elején, de később mégis befutott. **0-ról kis híján 900M MAU-ra növekedett***. Product döntések, új funkciók, miértek és persze azok hatásai, mert így teljes a dolog.

![alt text](https://appcraft.hu/assets/img/wechat-story-02.png)

## Csoportra terveznek

Talán ezt érdemes már a legelején kiemelni, teljes egészében a csoportok összehozása áll a termék stratégiájuk központjában. Erre optimalizálják a méréseiket, mindig a csoportos viselkedést vizsgálják.

Nyilván itt a szokásos nehézséggel kezdtek, hiába építenek a csoportra, ha nincsenek ismerőseid benne. Ezért az egyik elő feature volt a *People Nearby*. Ami arról szól, hogy láthatod a közeledben lévőket, és tudtok beszélgetni.

Ma már ez kevéséb fontos, de akkoriban 100k+ új felhasználót hozott.

Érdekes döntés, hogy eleinte különálló megoldásként működött, és **csak ezután kötötték össze a QQ-val**. Ez arról szólt, hogy importálhatták az ottani közösségi hálód. Okosak voltak, azokat húzták össze, akik mindkettőt használták, nem próbálták ráerőltetni magukat a másikra.

Erős ellenpélda erre a *Google+*, amit a cég minden szolgáltatásával össze akartak fűzni, de ott a felhasználók finoman szólva sem szimpatizálzak az ötlettel.

2011 novemberére már 50M felhasználót értek el így.

Azonban az újonnan csatlakozók még gyakran érezhették magukat egyedül. Ez indokolta a **Shake** funkció bevezetését, amivel random embereket kötött össze.

Csak az első hónapban 100M alkalommal hasznátlák ezt a funkciót. Nagyon népszerű volt a növekedési fázisban, most viszont már nem az. Akkoriban egyébként már napi 200k csatlakozott.

## Belső késztetések

Ezt követően rámentek azokra a belső késztetésekre, olyan dolgokra, amelyek nem olvashatóak ki az adatokból, illetve nem fogják az emberek felmérés / interjú alatt elmondani.

Ilyen volt a **Moments** funkció is. Privát módon, csak barát egy körével lehet megosztani képeket. Nem ők találták ki, a Path nevű tök jó, de nem túl sikeres fotó megosztó inpirálta egyébként. A *Snapchat, Facebook, Instagram* és még néhányan azonban már innen lesték el.

A nagy különbséget az implementáció adta. A 10 fős csapatuk 4 hónap alatt nem kevesebb mint 30 verziót tesztelt meg. Náluk, az igazi erősség az volt, hogy nem egy széles közösség felé szórták ki ezeket a képeket, hanem épp ellenkezőleg. A kis összetartó közösségek adták az egész bázisát, ráépülve a **kínai “kör kultúrára”**.

2012-ben járunk már. Ekkor indították útra a **WeChat Official Accounts (OA)**, amikor Twitter szerűen egyoldalúan lehet követni másokat, avagy fel lehetett iratkozni hírességekre. A hírességek szöveges, hangos vagy videó üzenetekkel kommunikálhattak a rajongóikkal.

Egyébként ennek a sikerén felbuzdulva **nyitottak a nagy márkák és az üzletek irányába**. Ezáltal a kiadók is szélesebb közönség rétegeket érhettek. Ez a Facebook és a többi chat rendszer esetében is elég komoly fókuszt kapott.

Ezt követően indult **Sticker Store**, amivel még jobban kifejezhették magukat a felhasználók. Frankó kis piactér épült erre. A felhasználók maguk dönthetik el mennyit adnak ezekért. Ez már évek óta hódít nálunk is. Ezen a ponton már bőven 300M MAU-nál járunk.

## Saját problémák

Hittek abban, hogy a nagy ötletek a saját problémák megoldásából jön.

Ennek első példája volt a **Red Packets**. Ez egy olyan szokásból származtatható, hogy a kínai újév utáni első napon a helyi managerek kis piros borítékokban adnak ajándékot a saját embereiknek. A *Tencent* azonban annyira nagyra nőtt, hogy ez már nagyon hosszadalmassá vált. A *WeChat*-el azonban ezt szépen lehetett “automatizálni”. Az eredeti verziót 20 mérnök 3 hét alatt építette.

2014 újévkor 5m felhasználó használta a *Red Packets* funckiót. Nagyon sokan a cégen belül is. Náluk mindig erősen élt a *dogfooding kultúrája*, avagy aktívan használják a saját terméküket. Érdekességképpen 1 évvel később már 1 milliárdot küldtek el így.

Különösképp figyeltek arra, hogy a különböző csoportok és családok hogyan használják ezt a funkciót. *Ennek következtében ma már számos verziója van:*

- random pénz összeggel,
- fix összeggel,
- többek közt osztja szét véletlenszerűen az adott összeget. Olyan ez mint a lottó és szerencse süti kombinációja.

**Ez a funkció nagyon ráerősített a csoport hatásra.**

Ezekre az alapokra építve alakult ki a **Pay** funkció is. Előbb szűk kis csoportok használták egymás között, aztán fokozatosan növekedett. Később fokozatosan nyitottak az üzletek fele. Online kereskedők és offline üzletek egyaránt előszeretettel használták.

A *Didi-vel (kínai Uber)* kötött partneri megállapodás is még tovább boostolta ezt az egészet. A *WeChat* ügyfelek ezzel tudtak fizetni a fuvarért. 2 év alatt a legjelentősebb fizetési szolgáltatássa vált Kínában. 600 millióan használják minden hónapban, és napi 600M tranzakciót bonyolítanak.

Nem ismerem a *PayPal* hasonló számait, de úgy érzem ezzel nem tudnak versenyezni.

## Monteizálj finoman

Nem akartak mindenből azonnal pénzt préselni.

A **Game Center** elsőre annyinak tűnik, hogy játszol a messenger appban, de a csoport hatás hatalmasat dob az egészen, és rengeteg embert bevonzanak ezáltal.

A **Moments Native Ads** 2015 januárjában indult. Azonban itt nagyon figyeltek arra, hogy ez ne legyen zavaró, és ne akadályozza a szolgáltatás növekedését. **Napi 1-et jelenítenek meg, ezzel szemben a *Facebook News Feed* 10 postonként mutat egyet.** Ebből a kevésből kell minnél jobban beletalálniuk.

Nagy figyelmet fordítottak arra, hogy a natív Moment élmény megmaradjon. Vizuálisan is korrekten kell kinéznie, csak a közös barátok látják, és nem kürtöli szét a nagyvilágba. Ennek ellenére nagyon jól teljesített többeknek.

A hagyományos **kupon** modellbe is vittek egy csavart, amivel ezt is közösségivé tették. Példaképp kapsz egy kupont az offline store-ban és azt megoszthatod a barátokkal. Nagyon okos húzás.

## Teremts értéket, nem csak user számban növekedj

Azzal mérik magukat, hogy mennyi feladatot lehet velük jól megoldani.

A **QR kód** nyugaton nem terjed el, náluk annál jobban, egyfajta link lett az offline világgal. Habár most már az Apple is beépítette alapból, ez sokat dobhat itthon is.

A **mikro programok** az *OA* kiegészítései. Olyan apró appok, amikkel különböző szolgáltatásokhoz lehet hozzáférni, egyszerűen és gyorsan. Nem kell saját appot készíteni, ott van, könnnyen, gyorsan, mindenkinek elérhetően.

Ahogy mondtam, kapu az internethez, ezzel szépen be is zárják magukhoz a felhasználókat.

## Nem emelnek ki 1–1 featuret

Kifejezetten tartanak attól, ha egy feature túl népszerű lesz. Inkább egy toolbeltet akarnak létrehozni, pici utility “appokból”. **Egyszerűen tartják az appot, mindössze 4 tab van és annyi.**

**Az egyes részek cégen belül versenyeznek**, ami itt jól működik. Fontos látni, hogy sokaknak ez nem csak egy app, hanem ez az internet

**Tesznek azért, hogy ne terelődjön el a figyelem valami olyan felé, ami hosszú távon csökkenti a valós értéket.**  Ezért is fogják vissza a marketing tartalmakat, egyszer lát olyat a user naponta. A subscription accountok napi 1x köldhetnek broadcast üzeneteket.

## Utolsó gondolat…

Hát így alakult a *WeChat* sztori eddig, számos érdekes és hasznos következtetést le lehet vonni, kíváncsi vagyok Ti miképp látjátok.