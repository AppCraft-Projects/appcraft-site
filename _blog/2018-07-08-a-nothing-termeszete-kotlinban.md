---
title:  A Nothing természete a Kotlinban
short_title: A Nothing természete a Kotlinban
excerpt: Aki a Java világból jön, annak a Nothing koncepciója szokatlan lehet. Ebben a cikkben kitisztázzuk ezt pár életszerű példával.
date: 2018-07-08
tags: [programming, kotlin, data-types]
---

## Mi az a `Nothing`?

Egyszerüen elmagyarázva a `Nothing` egy olyan típus, ami minden egyéb típusnak a leszármazottja.

> In type theory, a theory within mathematical logic, the bottom type is the type that has no values.
> A function whose return type is bottom cannot return any value.
> 
> Forrás: Wikipedia

Szóval akkor ez azt jelenti, hogy a `Nothing` az valami olyasmi, mint a `Void` a Java-ban és az ellentetje az `Any`-nek?
Az a helyzet, hogy nem teljesen. A Java-ban ha egy metódusnak nincs visszatérési értéke, akkor azt `void`-dal deklaráljuk:

{% gist 06706a4e4b6aa1c3fffa0092482f09a6 %}

Kotlinban ezzel szemben, van már egy típusunk, amit olyan függvényekből adunk vissza, melyek nem deklarálnak visszatérési
értéket, ez az  [`Unit`](https://kotlinlang.org/docs/reference/functions.html#unit-returning-functions).

{% gist 3f5a995d91b52182c281424757dfa97e %}

Habár a dokumentáció szerint az `Unit` olyan, mint a `void`, a valóságban van közöttük egy fontos különbség.
Az `Unit`-nak van egy példánya, ezért tudjuk az értékét változóba is elmenteni:

{% gist 154558b50fa85cadd7b85d91a2c17b9c %}

Akkor tulajdonképpen mire is jó a `Nothing`? Nézzük meg mi történik, ha egy függvény sosem tér vissza:

{% gist e212a555b4da323cac665f69155f885a %}

Ha ez a függvény nem dobott volna egy kivételt, akkor `Unit`-tal tért volna vissza. Ha most azt tippeled, hogy
ez egy olyan eset, amikor `Nothing`-gal térünk vissza, akkor jól gondolod. Nézzük meg a `Nothing` implementációját:

{% gist ea790c881e10b9fa0911f5bb9248794a %}

Az osztálynak privát konstruktora van, ami nincs meghívva onnan. Ez azt is jelenti, hogy a `Nothing`-ból egyetlen
példány sem létezhet. Emellett a `Nothing` rendelkezik azzal a tulajdonsággal is, hogy minden egyéb típus leszármazottja
(az `Unit`-tal együtt).

## Kivétel kezelés `Nothing`-gal:

Mostanra már elgondolkozhattál, hogy vajon ez az egész mire is jó? Nézzük meg az alábbi példát, amiben egy függvényünk van,
ami Java kóddal dolgozik együtt, ami `null` értékkel is visszatérhet:

{% gist d9c336a408127bf2134c63ec3f4732d6 %}

Ha meghívjuk ezt a kódunkban, akkor kezdenünk kell valamit a nullozhatósággal, ha olyan kódot szeretnénk, amiben nem
nullozható `String` van:

{% gist ea25f2d93fdf18ccbdddb9d2ef5f73b3 %}

Várjunk csak...ez le se fordul, mert a `throwException` `Unit`-tal tér vissza, de mi `String`-et szeretnénk.
Próbáljuk meg egy kicsit átírni az implementációt:

{% gist a65c6fedd849874609d14e77718d3204 %}

Most már lefordul a kódunk. Miért is van ez? A válasz nagyon egyszerű: **mivel a `Nothing` minden más típusnak a
leszármazottja, ezért a fordító elfogadja a kódunkat és mivel a `throwException` soha nem fog eredménnyel visszatérni,
ezért az értékadás sosem fog megtörténni.** Még ennél is jobb, hogy innentől kezdve el is kezdhetjük a `Nothing`-ot arra
használni, hogy egy olyan függvényt jelöljünk vele, ami mindig kivételt fog dobni.

A `Nothing` működésének a megértése egy kicsit nehéz lehet, de segíthet, ha úgy gondolunk rá, mint valamire, ami az `Any`
ellentetje. Az `Any` mindennek az őse (mint az `Object` a Java-ban), a `Nothing` pedig mindennek a gyermeke, ezért
bármilyen függvénynek megadhatjuk, mint visszatérési érték.

## A `null` reprezentálása

Most, hogy már tudod hogy működik a `Nothing`, akár fel is lélegezhetsz...amíg nem írsz egy ilyen függvényt:

{% gist 884a0ba4b5242b97135c0544fc38d86f %}

Ha ezt kipróbálod az előző példával, akkor már nem fordul többé. Miért van ez? Nézzük meg, hogy van-e olyan érték,
amivel vissza lehet térni egy olyan függvényből, aminek `Nothing?` a visszatérési értéke:

{% gist 6f367272c8a5cc06613fa77b67789932 %}

Igen. Az egyetlen érték, amivel vissza lehet térni ebből a függvényből az a `null`. Ez azt is jelenti, hogy a `null`
típusa `Nothing?`. Habár ez nem túl hasznos a napi munkában, azért jó, ha megértjük.

## Algebrai adattípusok

Az [Algebrai adattípusok](https://en.wikipedia.org/wiki/Algebraic_data_type) néha elég hasznosak, sőt valószínüleg
már használod is őket valahol úgy, hogy nem is tudsz róluk (linkelt listák például). A Kotlinban a `Nothing`-ot fel
tudjuk használni arra, hogy implementáljunk őket. Nézzünk meg egy jó példát, az `Either`-t:

{% gist af19dc65f93577a77038b981045bd685 %}

Az `Either` egy olyan objektumot reprezentál, ami felvehet `Left`, vagy `Right` értéket. A `Left` hagyományosan valamilyen
kivételt jelent, a `Right` pedig általában csak egy sima érték. A fontos az, hogy az `Either` a kettő közül csak az egyik
értékét veheti fel egy adott pillanatban. Ezt a koncepciót a `Nothing`-gal reprezentáljuk. A `Left` jobb oldali
és a `Right` bal oldali típusparamétere `Nothing` lesz. Ezt a konstrukciót fel tudjuk utána hasznáni arra, hogy visszatérjünk
a kivétellel, ahelyett, hogy kivételt dobnánk:

{% gist 0abe7bcf1245004e547eb0cce1fd196c %}

Fontos itt megjegyezni, hogy ha itt a `Nothing` helyett `Unit`-ot használnánk, akkor a kódunk nem fordulna le, mert az
`Unit` nem mindennek a leszármazottja. Itt, tehát a `Nothing` pont azt reprezentálja, amire kitalálták: semmit.

Egy másik jó példa a `Nothing` bemutatására egy fa struktúra:

{% gist 06d8075e5f721418a1f90101d8e44be4 %}

Itt a `Nothing` hiányzó gyermeket jelöl a fában.

## Összefoglalás

Habár a `Nothing` nem tűnik könnyen érthető koncepciónak elsőre, ha megtanuljuk hogy működik, akkor gyorsan egy hasznos
eszközzé válik a kezünkben. Használhatjuk arra, hogy nem létezést jelöljünk vele adatstruktúrákban, vagy akár arra is,
hogy olyan függvényeket készítsünk, amelyeknek mindenképpen kivételt kell dobniuk.

Most, hogy mindezt tudjuk, nyomás **kódolni**!
