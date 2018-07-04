---
excerpt: Jókorát szólt az ügy, hogy az AirBnb mobil csapata elengedi a React Nativeot és visszaáll natívra.
title: AirBnb 💔 React Native
date: 2018-06-30
tags: [microsoft, windows, mobile, fun]
short_title: AirBnb 💔 React Native
---

![alt text](https://appcraft.hu/assets/img/airbnb-react.png)

Két hete jókorát szólt az ügy, hogy miután bitang sok energiát invesztált az AirBnb mobil csapata a React Nativeba, most ezt elvágják és inkább fallbackelnek natív kódra.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">After two years, 220 screens, and 120,000 lines of javascript, we&#39;re moving away from React Native at Airbnb. I tried to summarize our experience in a single blog post but that wouldn&#39;t do it justice so it turned into five! <a href="https://t.co/B8yDzcocAy">https://t.co/B8yDzcocAy</a></p>&mdash; Gabriel Peal (@gpeal8) <a href="https://twitter.com/gpeal8/status/1009113030339129345?ref_src=twsrc%5Etfw">June 19, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Ki akartam várni ennek a reakciónak a megírásával, kicsit csillapodjon ez a hangulat, valamint a gondolatok is összébb álljanak a fejemben.

## Elvárások és eredmények

Nem aprózták el, Gabriel Peal (@gpeal8) öt részes blogpost sorozattal foglalta össze az érveiket, amiből az ügy számos aspektusát ki lehet olvasni.

Szerintem segíti a megértést, ha előre veszem az elvárásaikat:
* Allow us to **move faster** as an organization.
* Maintain the **quality bar** set by native.
* Write product code *once* for mobile instead of twice.
* Improve upon the *developer experience*.

Komoly elvárásokat támasztottak, nehéz utat választottak, komolyan toltak bele erőforrást, az eredményt végülis látjuk. Végül nem sikerült ezeket megugrani.

Két kulcs momentumot szeretnék kiemelni a sztoriból, mindkettőn sok múlhatot szerintem.

## Amire tervezték a toolt és amire használták volna...

A fenti felsorolás hármas pontja szerintem nagyon lényeges. A csapat egy *“write once, run everywhere”* megoldást keresett, kódot akart újrafelhasználni iOS és Android között.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">The ability for RN product code to be shared across platforms at Airbnb *in my opinion* was an overwhelming success. Features in RN were often done with zero lines of platform-specific code. In this regard, it WORKED.</p>&mdash; Leland Richardson (@intelligibabble) <a href="https://twitter.com/intelligibabble/status/1010948686501691393?ref_src=twsrc%5Etfw">June 24, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Ez részben sikerült is, viszont a React Native-ot nem kifejezetten erre a use casere tervezték, ez explicit ki is van mondva. Ez egy *“learn once, write everywhere”* platform. Ha weben már használod a Reactot és ha az ott megtanultak minták alapján építkeznél a többi platformra is, akkor jó választásnak bizonyulhat. Persze ez számos körülményen múlhat..

Plusz használhatsz néhány egész varázslatos toolt:
- Mint az [Expo](http://bit.ly/expo-rn), amivel egészen elképesztően leegyszerűsödik a deplyoment.
- Vagy épp az AirBnb sajátja, a [Paint with Code](http://bit.ly/airbnb-paint-with-code), amivel Sketch.app és a React komponensek hozhatóak össze.

De persze nem szeretnék legyinteni a React Native problémáira, mert van neki bőven, de nekem nem stimmel ez a sztori.

Egész egyszerűen nincs szükség több ezer mérnök órára és két évre ezen problémák felderítéséhez. Két ügyes fejlesztő egy 2-3 hetes spike során tuti kiderítené az issuek jelentős részét. Ez alapján pedig már lehet döntéseket hozni.

*A VP of engineering helyében nem lennék boldog.* 😓

## Nem passzolt a fejlesztői kultúrába

Épp ezért gondolom azt, hogy nem tisztán a technikai problémákról van itt szó.

Erre világít rá egy [idézet](http://bit.ly/expo-airbnb-rn) Charlie Cheevertől ([@ccheever](https://twitter.com/ccheever)) az [Expo](http://bit.ly/expo-rn) egyik alapítójától:

> [...] organizations where there are people who identify themselves strongly as iOS programmers and Android programmers have a really hard time being happy with React Native. iOS programmers in particular are very unhappy with it and generally regard JS as an infestation of the company’s codebase, while Android programmers have more mixed feelings.

Emlékszem, natív mobil fejlesztők hada kritizálta az AirBnb csapat döntését, amikor belevágtak ebbe kísérletbe. Furcsa volt most látni a mostani rakciókat, sokan szabályosan ünnepelték a történéseket.

Nem is vitázok ezzel, évekig ércelődtem a JavaScriptet a tervezési döntései miatt, sőt még időnként manapság is, de nem is ez a lényeg. Megvan az a problem domain, ahol tök jól működik. Továbbá nem a személyes preferencia meghatározza meg a nyelvválasztást, az manapság inkább üzleti és HR kérdés.

Felteszem volt náluk egy elég nagy és kellően hangos csoport, akik nem tudtak megbarátkozni vele, és mostanra mentek át az érveik. Hiába minden effort, tanulás, miegymás, van ilyen a fejlesztési világban, amikor a csapatok kultúrájába nem fér bele egy technológiai csomag.

## A React Native csapat is látja a problémákat

Mindezek a problémák feltehetőleg korábban eljutottak a React Native cora csapatához is. Pár nappal az AirBnb bejelentés előtti blogpostjában Sophie Alpert ([@sophiebits](https://twitter.com/sophiebits))  összefoglalta a [nagy refactort](http://bit.ly/alpert-state-of-rn), amin a csapat épp nagy erőkkel dolgozik.

Kigyűjtöttem a lényeget:

>Changing the threading model. Instead of each UI update needing to perform work on three different threads, it will be possible to call synchronously into JavaScript on any thread for high-priority updates while still keeping low-priority work off the main thread to maintain responsiveness.

>️Incorporating async rendering capabilities into React Native to allow multiple rendering priorities and to simplify asynchronous data handling.

>Simplifying our bridge to make it faster and more lightweight; direct calls between native and JavaScript are more efficient and will make it easier to build debugging tools like cross-language stack traces.

>Why? Today, it's not possible to incorporate native navigation and gesture handling or native components like UICollectionView and RecyclerView without complex hacks. After our changes to the threading model, building features like this will be straightforward.

Érdemes még mellé elolvasni Nick Schrock ([@schrockn](http://bit.ly/schrock-airbnb-rn)) tweet-szálát a témában, tök jól egymás mellé teszi‏ Gabriel és Sophie írásait:
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">5/ From <a href="https://twitter.com/gpeal8?ref_src=twsrc%5Etfw">@gpeal8</a>: re &quot;Long Lists&quot; Many of the limitations are difficult to overcome because of the threading. Adapter data can’t be accessed synchronously so it is possible to see views flash in as they get asynchronously rendered while scrolling quickly.&quot;</p>&mdash; Nick Schrock (@schrockn) <a href="https://twitter.com/schrockn/status/1009460618259296256?ref_src=twsrc%5Etfw">June 20, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Nyilván ezek rövid távon nem segítettek volna rajtuk, idő amíg elkészülnek.

## Utolsó gondolatok

Rengeteg hibája van a React Nativenak, de vannak az AirBnb háza táján is furcsa dolgok rendesen.

Nem fekete-fehér a sztori. Nem tisztán technológiai problémákról van szó, akadnak kultúrális sajátosságok is rendesen.

Azok pedig ízes kérdések, hogy miért toltak bele ennyi időt és energiát, ha ennyire nem volt meg a fit.

*Ti mit gondoltok?*