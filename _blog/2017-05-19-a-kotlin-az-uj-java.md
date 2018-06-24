---
excerpt: Rövid összefoglaló a Kotlin előnyeiről a Java-val szemben, és hogy miért éri meg, ha váltunk.
title: A Kotlin az új Java
date: 2017-05-19
tags: [programming, kotlin, java]
---

> Ha már Java fejlesztőként dolgozol egy ideje, talán már elgondolkoztál azon, hogy melyik legyen a következő nyelv, amibe beleásod magad.
> Érdemes ránézni például a  [Clojure](https://clojure.org/), a [Rust](https://www.rust-lang.org/en-US/) vagy a [Haskell](https://www.haskell.org/) izgalmas megoldásaira, de ha olyan nyelvvel szeretnél foglalkozni, amivel pénzt is lehet keresni és emellett kellemes vele kódot írni, akkor válasszd a Kotlint.

## Szóval mi is a Kotlin?

- A [JetBrains](https://www.jetbrains.com/) saját fejlesztésű programozási nyelve, azé a cégé, akik az [IDEA](https://www.jetbrains.com/idea/) fejlesztői környezet mögött is állnak.
- Egy egyszerű, és sokoldalú Java alternatíva
- Ami kifogástalan együttműködésre képes a Java-val
- Java bájtkódra fordul
- A JVM-en fut
- Továbbá képes Javascript-re is fordulni

Ha elolvassuk a dokumentációt, akkor találhatunk még pár ígéretes dolgot:
- Többet elérhetünk kevesebb kód írásával
- Megoldást kínál sok, Java-ban fellelhető problémára
- Továbbra is használhatjuk a Java ökoszisztémát vele
- Frontend és backend kódot is tudunk írni ugyanazon a nyelven
- 100%-ban együttműködő a Java-val
- E tekintetben jobban teljesít, mint más alternatívák (Clojure, Scala)
- És csak egy vékony réteg komplexitást ad hozzá a Java-hoz

Jól hangzik, nem? Mielőtt rátenyerelünk a Letöltés gombra azért még tekintsük át, hogy mit is jelent ez a gyakorlatban.

## Érték- és adatosztályok
Amit itt láthatunk, az egy jó öreg POJO a szokásos boilerplate kóddal:

{% gist 0c86e6a2c6bb91f44983c5d9fd342117 %}

Az értékosztályok készítése elég nehézkes még akkor is, ha Lombok-ot használunk (a Lombok használatához telepíteni kell egy beépülő modult a fejlesztői környezetünkbe, ami nem minden esetben megoldható). Habár ehhez segítséget nyújt az IDEA (illetve az Eclipse), különböző kódgeneráló eszközökkel, ezek nem igazán megbízhatóak (gondoljunk csak arra, amikor hozzáadunk egy új mezőt az osztályhoz és elfelejtjük újragenerálni az `equals` metódust.

Nézzük meg, hogy néz ki ugyanez Kotlin-ban:

{% gist 306e9222179ef822fa7ce852ac2c4d9b %}

Hoppá! Ehhez lényegesen kevesebbet kellett gépelni a Java-verzióhoz képest! A Kotlin adatosztályok a következőket adják:
- `equals` + `hashCode`,
- `toString` és
- getterek + setterek
Ezeken kívül megkapjuk a `copy` metódust, amivel másolatokat tudunk készíteni már meglévő adatosztály példányokról. Erről [itt](https://kotlinlang.org/docs/reference/data-classes.html) lehet többet olvasni.

## String interpoláció
A `String`-ek manipulálása Java-ban nem éppen kényelmes művelet. Ezen segíthet a `String.format`, de nem túl sokat.

{% gist 12b7888d78ddda93144aebddac1d779e %}

A Kotlin ennek a problémának a megoldására a [String interpolációt](https://stackoverflow.com/questions/37442198/how-does-string-interpolation-work-in-kotlin) nyújtja, amivel kényelmesebben tudunk kezelni szövegeket:

{% gist eeb7dd12e75d1f4013f76b4dd00529f4 %}

## Kiegészítő funkciók

Dekorátorokat írni Java-ban trükkös feladat és nem mindig sikerül tökéletesen. Például, ha egy olyan dekorátort szeretnénk készíteni, ami a `List` interfész összes implementációjával képes működni, akkor nem szerencsés a `List`-et kiterjesztenünk, mert úgy elég sok metódust kellene implementálnunk, ehelyett érdemesebb az `AbstractList`-ből kiindulnunk:

{% gist 6e2b6932521ca83ae8e156ce016d9a3a %}

Ha viszont valami olyasmit akarunk dekorálni, ami nem ad az `AbstractList`-hez hasonló könnyítéseket, vagy akár az általunk dekorálandó osztály `final`, akkor gondban vagyunk. Ebben a problémában tudnak segítséget nyújtani a kiegészítő funkciók:

{% gist 96322e2c30883b24c3f46a53777ca568 %}

Ez a funkció dekorátorként viselkedik minden `List` példányon. A Java-s alternatívával összehasonlítva ez az egy soros lényegesen egyszerűbb és képes `final` osztályokon is működni. Természetesen [ez sem mindenre megoldás](https://www.philosophicalhacker.com/post/how-to-abuse-kotlin-extension-functions/).

## Null biztonság

A `null`-ok ellenőrzése általában sok logikai művelettel és boilerplate-tel jár. A Java 8 megjelenése óta ezen már tudunk segíteni az `Optional` használatával, de mi történik akkor, ha egy `Optional` referencia a `null`? Bizony, ilyenkor megkapjuk a szokásos `NullPointerException`-t, ami a Java 20 éves fennállása óta még mindig nem képes megmondani, hogy **mi** volt a `null`.
Nézzük meg a következő példát:

{% gist 074849246682406ac6faaac78461bae9 %}

A Kotlin használatával több opciónk is van. Ha együtt akarunk működni Java-projektekkel, vagy egy már meglévő Java-projekten használunk Kotlin-t is, akkor lehet a `null` biztonsági operátort (`?`) használni:

{% gist a4ffb5d187a893ac59af7b349ef399b3 %}

A `?` jobb oldalán lévő kód csak akkor fog futni, ha a bal oldalán lévő kifejezés nem `null`. A `let` funkció létrehoz egy lokális scope-ot azzal az objektummal, amin meg lett hívva, így itt az `it` változó az `it.city`-re fog mutatni a visszatéréskor. 

Ha viszont nem kell Java-kóddal együttműködni, akkor jobban járunk, ha egyáltalán nem használunk `null`-t a projektünkön:

{% gist 7c3530e7257e161d475755dd4bc0c504 %}

Ha nincs a kódbázisunkban `null` (nics `?` sehol), akkor lényegesen egyszerűbb lesz az egész.

## Típus kikövetkeztetés

A Kotlin támogatja a típusok kikövetkeztetését, ami azt jelenti, hogy sok esetben a kontextusból ki tudja deríteni a fordító a típusok megjelölése nélkül is azt, hogy egy-egy referencia milyen típussal rendelkezik. Ez kicsit olyan, mint a gyémántjelölés Java-ban, csak sokkal sokoldalúbb! Nézzük meg a következő példát:

{% gist 5416e0d1aa9134b7036ff2af09e207a1 %}

Ez Kotlin-ban alapból hasonlóan néz ki:

{% gist d81a7681415e4988c72fd23fd923efcd %}

Amíg rá nem hagyjuk a Kotlin-fordítóra, hogy kikövetkeztesse a változóink típusait:

{% gist 58c106ff475e9c261ac39cfd76b602ae %}

Vagy akár a funkciók visszatérési értékeit:

{% gist a83328555586f45efeb523c440fc17d3 %}

## Nincsenek ellenőrzött kivételek
Az alábbi kódot valószínűleg már milliószor láthattad:

{% gist d51b2eb08d5be1908e93c2daf69b78a4 %}

Régimódi Java IO. Ugyanez Kotlin-ban így néz ki:

{% gist ec2e31718bbe0343dd17ca3037ebe3b8 %}

Itt több dolog is történik egyszerre. Először is a Kotlin-ban nincsenek ellenőrzött kivételek, így itt az IO végrehajtása során nem kell elkapnunk az esetlegesen keletkező kivételeket. Másodszor a Kotlin az összes `Closeable` osztályhoz hozzáadja az `use` műveletet, ami a dokumentáció szerint az alábbiakat végzi el:

> Executes the given [block] function on this resource and then closes it down correctly whether an exception is thrown or not.
> (Kivonat a Kotlin dokumentációból)

Ezeken kívül a `File` osztályhoz hozzáadott `readLines` funkciót is láthatjuk működés közben. Ez a minta a Kotlin által adott függvény-könytárban sokszor előfordul. Ha használtál már Guava-t vagy esetleg Apache Commons-t, akkor az azokban található függvények sokszor visszaköszönnek mint Kotlin kiegészítő funkciók hozzáadva a JDK osztályokhoz. Ezeket használva sok kellemetlenségtől megkímélhetjük magunkat.

## Lambda támogatás
Nézzünk meg egy példát egy Java-s lambdára:

{% gist 9276ed18fec50fa4bdf030139e813572 %}

Mivel a Java-ban nincsen külön szintaxis, amivel metódusok szignatúráját írhatnánk le, általában egy interfészt kell létrehozni nekik. Az alábbi példában ugyan használhatnánk a `Function<String, Boolean>` típust, de ez csak olyan függvényekre működik, amiknek egy paraméterük van. Erre vannak részmegoldások a JDK-ban, de ha valaki ránéz a kódunkra, lehet, hogy nem lesz egyértelmű számára, hogy mire is való egy `BiFunction`. Ezen egy kicsit javít a Kotlin:

{% gist 392370158e68247cddf7585cee92575b %}

A Kotlin szintaxist ad funkciók leírására az alábbi módon: `(ParamType1, ...ParamTypeN) -> ReturnType`.
Mivel a Kotlin-ban vannak függvény- és mező referenciák is, ezért lehet hivatkozni egy már létező objektum egy függvényére is!
Az alábbi példában egy konkrét példány `filterBy` műveletére hivatkozunk így:

{% gist 08584eff41be9c03e84ebd1bc1532ea8 %}

## Funkcionális programozás
Mostanában sokat hallani a funkcionális programozásról és a Java 8 megjelenésével már használhatjuk az Oracle által megálmodott eszköztárat, a Stream API-tis erre a célra, ami így működik:

{% gist 71b953cf1610fcd80584d738e8025cd1 %}

Ennek a megfelelője a Kotlinba nagyon hasonló, de némileg mégis más:

{% gist 09491cc6059659f270b2820f1a817cd6 %}

A lényeges különbség az, hogy nincs explicit konverzió stream-ekre, mivel az összes Kotlin collection támogatja őket alapból.
Ennek egyenes következménye az is, hogy a fenti példában nem kell lambda-t átadnunk a `flatMap` függvénynek.
Az eredmények összegyűjtése is automatikus (nincs szükség a `Collectors.to*` metódusok használatára).
Ebben a példában csak azért kellett a `toSet` függvényt használnunk, mert `Set`-et akarunk visszaadni. Ha ez nem lenne elvárás, akkor elhagyhatnánk a `.toSet()` hívást.

## Együttműködés Kotlin és Java között
Ha az együttműködés a két nyelv között nem kielégítő az sokakat elrettenthet (és el is rettent más nyelvekben), de a JetBrains itt kiköszörülte a csorbát:

{% gist 085d8a371f87eaca5cf28cab1aef5ee5 %}

{% gist cf6b7c6eb5ff4c9e20476a8a3d7b112c %}

Az együttműködés akadály- és fájdalommentes a két kódbázis között. Java- és Kotlin-osztályok projekten belül is vegyíthetők és a Kotlin ad pár annotációt (például a `@JvmStatic` a fenti példában), amivel a Kotlin osztályokat lehet felokosítani úgy, hogy Java oldalról könnyű legyen a használatuk. Erről [itt](https://kotlinlang.org/docs/reference/java-interop.html) lehet többet olvasni.

Ha megnézzük a fenti példákat, akkor jól láthatóvá válik egy séma: a Kotlin megőrzi a Java jó ötleteit, azokat feljavítja, míg a hibáit próbálja kiküszöbölni. Az, hogy a Google az Android egyik hivatalos nyelvévé tette a Kotlin-t szintén ezt támasztja alá.

## Mit mondjak a főnökömnek?
Ha esetleg meggyőztek a fentiek és kipróbálnád a Kotlin-t a munkahelyeden, de nincs ötleted, hogy mit mondj a főnöködnek és a csapattársaidnak, akkor adok pár tippet, amik talán segítenek majd:

- A Kotlin az iparból érkezett, nem egy egyetem falai közül. Valós problémákat old meg, amikkel programozók nap mint nap találkoznak
- Ingyenes és nyílt forráskódú
- Van hozzá egy könnyen használható Java -> Kotlin konvertáló eszköz
- Gyakorlatilag __0__ energiabefektetéssel keverhető a Java- és a Kotlin-kód
- *Minden* már létező Java-eszközt és keretrendszert lehet használni Kotlin-ból is
- A Kotlin-hoz a piac legjobb integrált fejlesztői környezete ad támogatást (aminek van ingyenes verziója)
- Könnyen olvasható, még a nem-Kotlin fejlesztők is át tudják nézni a kódodat
- **Nem kell elköteleződni** a Kotlin mellett a projekteden: *elég az is, ha csak a teszteket írod az elején Kotlin-ban*
- A JetBrains nem valószínű, hogy abbahagyja a nyelv fejlesztését egyhamar, mivel bevallottan is az a céljuk, hogy a bevételeiket növeljék vele
- A Kotlin közösség meglehetősen aktív és a [KEEP](https://github.com/Kotlin/KEEP)-en akár te is tehetsz javaslatokat a nyelv fejlesztési irányát illetően

A kérdést, hogy több-e a Kotlin, mint egy egyszeri hype, viszont csak Te tudod eldönteni.
Ha ki akarod próbálni a nyelvet, akkor itt van pár tipp, hogy hol kezdd:

- [Kotlin Tutorial-ok](https://kotlinlang.org/docs/tutorials/)
- [A Kotlin Reddit](https://www.reddit.com/r/Kotlin/)
- [Kotlin Koan-ok](https://kotlinlang.org/docs/tutorials/koans.html)
- [Kotlin Blog](https://blog.jetbrains.com/kotlin/) <-- napi hírek
- [Awesome Kotlin](https://kotlin.link/) <-- Válogatott függvénykönyvtárak és források
- Ezen kívül [itt](https://github.com/AppCraft-Projects/java-to-kotlin-examples) megtekintheted a cikkben látható példákat
