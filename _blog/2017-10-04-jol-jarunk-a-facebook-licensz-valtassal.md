---
excerpt: Néhány héttel ezelőtt az Apache alapítvány látványosan a Facebooknak feszült a React (és még egy tucatnyi technológia) licenszálási gyakorlata kapcsán.
title: Jól járunk a Facebook licensz váltással?
date: 2017-10-04
tags: [react, licensing, bsd, patents, facebook]
author: Gabor Orosz
short_title: Facebook licenszek
---

![alt text](https://appcraft.hu/assets/img/fb-license-02.png)

Néhány héttel ezelőtt az Apache alapítvány látványosan a Facebooknak feszült a React (és még egy tucatnyi technológia) licenszálási gyakorlata kapcsán.

Az ügy meglehetősen széles körben váltott ki felháborodást a web fejlesztő közösségből, szinte minden irányból cincálták a cég BSD+Patent license variánsát.

*Pár héttel ezelőtt én is írtam róla hideg fejjel átgondolva néhány gondolatot, [itt](https://appcraft.hu/posts/blog/2017-08-30-fb-licensing) olvashatjátok.*

## A Facebook pár hét alatt beadta a derekát
Hatalmas örömhullám söpört végig a közösségi hálókon, amikor is két hete a Facebook végül visszavonulót fújt, és a közösség akaratának engedve számos projektüknél MIT licenszre váltottak. Őszintén szólva azonban ezúttal nem osztoztam ebben az örömben velük.

Persze értem, a Facebook szempontjából menteni kellett a helyzetet, hosszútávú jó megoldás ennyi idő alatt nem ment volna át. Végeredményben pedig mindenki potenciálisan kicsit rosszabbul járt.

---

Azért mondom ezt, mert habár a MIT és sok más licensz sem tárgyalja a szabadalmak kérdését, azok ennek ellenére jelen lehetnek a háttérben. Nem tűntek el, és adott helyzetben előkerülhetnek egy per során.

## A nyílt forrás és a szabadalmak két külön dolog

Kifejtem bővebben, van mit körbejárni. Mindenek előtt az egész sztori abból indul ki, hogy az USA-ban folytatsz üzleti tevékenységet. Más országokban másképp kezelendő mindez, mi most fókuszáljunk erre a régióra.

Az bolondítja meg a helyzetet, hogy az amerikai jog szerint a nyílt forráskód és a szabadalmak elválnak egymástól, külön kezelendő fogalmak.

A Facebook féle BSD+Patents licensz előnye az volt, hogy részben szabályozta a szabadalmak kérdését is. Azt mondta ki, hogy a Facebook, ha be is perli a licensz használóját, vállalást tesz arra, hogy az érintett szabadalmak kapcsán ezt nem teszi.

Fordított helyzetben azonban, amikor a licensz használója perel, a tulajdonos terminálhatja azt. Avagy a gyakorlatban viszont perelheti a használóját.

Érdemes azzal tisztában lenni, hogy ez a lépés nem vonja magával, hogy azonnal és automatikusan fel kell függeszteni a kérdéses kódok használatát. Nem kell ennyire előre rohanni, arra majd csak a per végén, a döntés függvényében kerülhet sor.

A hasonló perek jellemzően hosszú évekig húzódhatnak, valamint jellemzően a döntés sem követel azonnali lépéseket. Ezeket mind összeadva és a technológiák fejlődési ütemét mellé téve, olyan idő jöhet ki, ami alatt technológiai generációk egész sora válthatja egymást.

## Mi a helyzet az MIT licensz kapcsán?

Megérkeztünk a rossz hírhez, szerintem visszalépés történt. Adott esetben az MIT, de még sok egyéb licensz esetében nem került szabályozásra a szabadalmak helyzete. Használhatod a forráskódot, de ez nem jelenti azt, hogy a szabadalak ne lehetnének ott a háttérben.
Avagy azok tulajdonosa akár perbe is foghat azok kapcsán. És ez a visszalépés a BSD+Patent licensszel összevetve, ahol azért volt az a védelem, hogy ezek kapcsán nem perelhettek be.

## Nagy játék megy a szabadalmak körül

Komoly szabadalmi portfólióval szinte kizárólag a nagyobb cégek rendelkeznek. Egyrészt kifejezetten költséges és hosszadalmas procedúra a szabadalmak bejegyzése.

Másrészt az ezzel kapcsolatos perek is elég nehézkesek. Egy komolyabb ügyvédi irodánál $2–3 milliónál kezdődnek, évekig tartanak, aminek végén a számlán ennek a 10x-ese is szerepelhet. Ezeket a költségeket pedig nagyon-nagyon kevés startup vállalhatja fel.

A multik esetében komoly kereszt-licensz megállapodásokkal szabályozzák ezket, amivel kicsit egyszerűsítenek ezen az aknamezőn. Ezeket afféle meg-nem-támadási szerződéseknek lehet tekinteni.

## Hova tovább innen?

Egy szó mint száz, nem tartom kifejezetten jó megoldásnak az MIT-t, az Apache 2.0 licensz szerintem jobb megoldás lett volna, de valami okból mégis emellett döntöttek.

Én szeretném hinni, hogy a Facebook részéről ez egy átmeneti megoldás, gyors kármentés. Remélem fél-1 év múlva előállnak egy jobb megoldással, amit ezúttal sokkal jobban kommunikálnak majd.

## Baromi kacifántos ez az egész

Egyrészt láthatóan baromi komplex témáról van szó, ami komoly elmélyülést igényel, hogy ténylegesen átlátható legyen. Érezhetően nagyon kevesen szánják rá az időt, és értik ténylegesen.

Ennek sajnálatos eredménye az is, hogy most szerintem nagyon sok a közösségi hálókon befolyásos szakember megvezette a saját követőit. Biztos vagyok benne, hogy számos félreértés volt, és sokan hamis biztonságérzetben vannak most.

Habár ahogy azt az előző cikk esetében is tettem, most is hangsúlyozom. Úgy gondolom, pláne a mostani felháborodás hullám után, hogy a Facebook csak rendkívül szorul helyzetben nyúlna ehhez az eszközhöz.
