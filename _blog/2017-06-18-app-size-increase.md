---
excerpt: Néhány hete már morogtam, hogy mekkorára nőttek mostanában az iOS appok, de a napokban három olyan “meglepő” felfedezésem volt, hogy újra elő kell vennem a témát.
title: OMG, mitől nőttek meg ezek az appok?
date: 2017-06-18
tags: [react, licensing, bsd, patents, facebook]
---

Néhány hete már morogtam, hogy mekkorára nőttek mostanában az iOS appok, de a napokban három olyan “meglepő” felfedezésem volt, hogy újra elő kell vennem a témát.

![alt text](https://appcraft-projects.github.io/appcraft-site/assets/img/app-size-01.jpeg)

Csak néhány példa:

- Egyrészt a héten redesignolt Twitter frissítés meghízott meg rendesen. Konkrétan már 117MB, de még így is a legkisebb az adott mezőnyben. Nyilván sok a tracking kód és az A/B tesztelt UI komponens, illetve a képernyő, de a látható funkciókhoz képest ez azért jelentős.
- Az első nagy durranás jön. A Facebook frissítése mostanra nagyobb lett mint az Excelé. 399MB vs 310MB, ez már szerintem barokkos túlzás. Ebben tuti minden van, ami eszedbe jut… meg az is, ami nem.
- Facebook és a Messenger update-ek együttesen 665MB-ot nyomnak. Ettől már leoldott az agyam.

## Miért ekkorák?
A Facebook app esetében volt egy jó kis elemzés néhány hónapja, érdemes átfutni. *Néhány az okok közül*:

- Rengeteg külső/belső keretrendszer és lib. Saját igényekre módosított *WebView*, talán a *JaveScriptCore*-al is játszottak valamit… stb.
- Tömérdek *A/B tesztelős* komponens.
- Rengeteg asset és brutál sok lokalizáció.
- *Duplikált resourceok*.

Trükkös továbbá, hogy nagyon sok féle nyelv keveredik a kódbázisban. *Objective-C, Objective-C++, Swift, JavaScript*. Vannak jó nagy natív részek, *webview*-val megoldott részek, de a *React Native* részek sem hiányoznak.

## Miért nem tetszik ez nekem?

Mert trend lett belőle. Fokozatosan növekszik a legtöbb app mérete, azoké is, amelyeket menet közben, egy konkrét célra és csak ritkán használnék, azon túl nem tartanék szívesen a telón.

Már csak azért sem, mert a 32GB tárhely is tud szűkös lenni. Nem is tudom mit csinálnak, akiknek 16GB vagy ne adj isten csak 8GB adatott. (Na jó, tudom, de csúnya lenne leírni.)

## WiFi vagy adatkapcsolat?

Nyilván ezeket az appokat nehéz összevetni a webes társakkal, de még más appokkal is. Más a modell, nem útközben jut eszedbe, hogy használni szeretnék őket.

Feltehetőleg egyszer lehúztad *WiFi*-n és csak használod (ha nem borított ki eddig valami mással, és törölted). Aztán a frissítést is így húzod le. Ez a része nem eszi az adatkereted, de azért így is fejvakarós.

Az viszont már aljasabb, ha egy játéknál lehúzul 2–3–4 GB-ot, majd svájc felé az autóban a gyerek békésen kivárja, ahogy első indításnál, az még lehúz néhány gigát roamingon.

Sajnos a többségnek se itthon, se a modern nyugaton nem korlátlan a adatkerete, roamingben pláne nem.

## Zárásképpen…

Ha a webnél fel van emlegetve a nagy méret, akkor igenis itt is fel kellene. Nem csoda, hogy a ki kell adniuk Lite verziókat, mert ez azért sok helyen ez erősen túlzás lett.

**Fel kellene vésni a nagy cégeknek, hogy a nagy méret egyszerűen rossz felhasználói élményt hoz!**