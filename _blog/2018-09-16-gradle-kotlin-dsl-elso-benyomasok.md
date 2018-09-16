---
excerpt: A Gradle Kotlin DSL már létezik egy ideje. Ebben a cikkben áttekintjük, hogy mennyire hasznos eszköz.
title: Gradle Kotlin DSL első benyomások
date: 2018-09-16
tags: [kotlin, gradle]
author: edem
short_title: Gradle Kotlin DSL első benyomások
---

> A Gradle Kotlin DSL már létezik egy ideje. Ebben a cikkben áttekintjük, hogy mennyire hasznos eszköz.

> Az írás megszületése óta [megjelent egy cikk](https://guides.gradle.org/migrating-build-logic-from-groovy-to-kotlin/)
 a témában a Gradle blogján. Érdemes elolvasni, nagyon hasznos dolgok vannak benne leírva, de ennek a cikknek a lényegén
 nem változtat.

## Szóval miért is kell ez?

Az első dolog, ami eszünkbe juthat, amikor valaki egy új nyelvet kezd el támogatni az eszközében az, hogy
miért is van erre szükség? Szerintem ez ebben az esetben is egy jó kérdés, szóval nézzük is át, hogy mik a
[Groovy](http://groovy-lang.org/) hátulütői.

Ha Java fejlesztő vagy és dolgoztál már [Maven](https://maven.apache.org/)-nel korábban, akkor a Gradle elég
furának tűnhet elsőre. Az első probléma az, hogy nem `xml`-t kell írni hozzá,
hanem programkódot. Ez önmagában is probléma lehet valakinek, aki a *Maven*-es deklaratív konfigurációhoz van szokva.

Ezen kívül a nyelv, amit a *Gradle* konfigurálásához használhatunk, az a *Groovy*, ami pedig egy dinamikus nyelv.
Szóval a Gradle nem csak az xml-t veszi el tőlünk, de a statikusságot is.

Emellett további problémát okoz az, hogy a Groovy fájlok szerkesztéséhez nyújtott IDE támogatás nem éppen ideális.
Nem tudunk refaktorálni sem, illetve a fordítási hibák sem egyértelműek.

A Groovy soha nem terjedt el igazán, ezért olyanokat találni, akik otthon vannak benne elég nehéz. Ebből következik,
hogy a legtobb fejlesztő, aki Gradle-el dolgozik, az csak félig-meddig ismeri a Groovy-t és sokszor, ha nyelvi problémákba
ütközik, akkor azok nagyon fájdalmasak.

Ezt a problémát szeretnék orvosolni a [kotlin-dsl](https://github.com/gradle/kotlin-dsl)-el, amivel Kotlinból script-elhetjük
a Gradle-t. Az alapötlet az, hogy kombinálják a már amúgy is elég jó IDE támogatást a szigorúan típusos nyelvvel,
és így megkapunk mindent, amit már megszokhattunk amikor Kotlinnal dolgozunk: refaktorálás, kód kiegészítést, enum-okat
és az összes többi Kotlin feature-t, amit szeretünk. Tekintsük át, hogy működik.


## Betekintés

Ha megnézzük a [példákat](https://github.com/gradle/kotlin-dsl/tree/master/samples) a *kotlin-dsl* repóban,
akkor találunk elég jól megírt kódokat:

{% gist b6269825d3a0151ba69d6b09f0ebd820 %}

Ismerős? A felszínen a *kotlin-dsl* nagyon hasonlít a régi Groovy konfighoz, de vannak kisebb különbségek.
Nézzünk meg párat.

### A beépített pluginek alkalmazása

Minden, ami megtalálható a hivatalos Gradle plugin repóban, az alkalmazható a `plugins` blokkból:

{% gist 63831edea1297fbaf67e84eeb2229c3b %}

Ugyanez *kotlin-dsl*-ben így néz ki:

{% gist 70e9fceb5bec8d96057d157339ccfe62 %}

Tulajdonképpen mi is történik it? Honnan jön a `java` és az `application`? Ha megnézzük a forrást, akkor rögtön
világossá válik:

{% gist 312889137af584446bf89ede080984ee %}

Ez az elmés trükk lehetővé teszi számunkra, hogy egyszerűen konfigurálhassuk a beépített plugin-eket, és emellett
a szigorú típusosságnak köszönhetően a fordítási hibák is kijönnek, ha vannak. Nincs többé félregépelésből eredő
probléma.

Mi történik akkor, ha viszont nem beépített plugin-t akarunk használni? Ebben az esetben van a szokásos módszer:

{% gist 11e44e37d1c4111606fdd6dc3acac881 %}

ami Kotlin-ban így néz ki:

{% gist c92805acf88c28ed5fa715b72753e007 %}

### Függőségek

A függőségek deklarálása egy elég fontos része minden Gradle script-nek, szóval nézzük át milyen különbségek
vannak:

Groovy:
{% gist 33a6e2e217b74dca9fc5cdd707d54a76 %}

és Kotlin:
{% gist dfa5433bcf51e6b2ec21c4c1edcdf1ed %}

Elég hasonló, de a Kotlin változat talán kicsit olvashatóbb.

### Task-ok

A plugin-ek és a függőségek után a következő legsűrűbben használt feature az talán a task-ok. Ez Groovy-ban kellőképpen
egyszerű:

{% gist b024695e21e0d3f9a12afc6db7fa9a2e %}

de Kotlinban egy kicsit több mágiát kell alkalmazni:

{% gist be3bf8dade6e5370c8290369b76fdf1f %}

Itt az történik, hogy a *kotlin-dsl* ad nekünk delegáltakat:

{% gist 260230b7cafe7ce7e845e28142bc6ad2 %}

> Ha több példát szeretnél látni erre, akkor klikk [ide](https://github.com/jnizet/gradle-kotlin-dsl-migration-guide).

Szóval úgy néz ki, hogy a *kotlin-dsl* lesz a megoldás minden problémánkra, ugye? Kapunk végre IDE feature-ket, mint
a refaktorálás, kód kiegészítés és végre kidobhatjuk a Groovy-t? A valóság ennél egy kicsit árnyaltabb.

## A hátulütők

Habár a kódpéldák a *kotlin-dsl* projektben elég jók és a neten olvasható cikkek többsége nagyon dícséri a projektet,
a valóságban jópár hátulütője is van a dolgonak.

### Lassú IDE támogatás

Az első amibe belebotlottam, amikor elkezdtem használni a *kotlin-dsl*-t az az elég lassú IDE támogatás volt.
Amit először próbáltam az a `buildSrc` hozzáadása egy multiplatform projektemhez. Készítettem pár osztályt, amibe
el tudom tárolni a projektem által használt verziókat, de ez valamiért az IDEA-nak egy 3 perces gondolkozás után
vált csak érthetővé. Ezt kipróbáltam több gépen és platformon is, de a tapasztalat mindenhol hasonló volt.

A plugin-ek konfigurációja hasonlóan lassú. Ha hozzáadunk egyet a `plugins` blokkhoz, akkor az adott plugin beállításai
elérhetővé válnak a lokális scope-ban, ugyanúgy, mint korábban Groovy-ban:

{% gist d15f5283e5582820c1af46ce7dc3d1cd %}

A gyakorlatban az IDE támogatás egy kicsit nehézkes. Többszöri újraindítás után tér csak észhez és teszi számunkra
elérhetővé a konfigurációs lehetőségeket, ami több percet is igénybe vehet.


### Kód példák hiánya

A Gradle-hez rengeteg Groovy példa áll rendelkezésre, amiket csak ki tudunk másolni ahhoz, hogy megoldjuk a problémáinkat.
A *kotlin-dsl* esetében ez sajnos nincs így, és ez nem beépített plugin-eknél még jobban érezhető. A legtöbb projekt
dokumentációjában Groovy kód található, de a Kotlin változatok egyelőre még hiányoznak. Ez alapvetően nem is lenne
probléma, ha 1:1 megfeleltethetőség lenne a két verzió között, de sajnos ez nincs így:


### Egyéni task-ok konfigurációja

Néha, amikor olyan plugin-t szeretnénk használni, ami egyedi task-okat hoz magával, akkor bele kell néznünk a
forrásba, hogy rájöjjünk, hogy milyen típusokat is használnak valójában. Például, hogy ezt a Groovy kódot
Kotlin-ra alakítsuk:

{% gist 54ac59ffdf40e88515c2b24252733fb2 %}

meg kell határoznunk a task osztályát:

{% gist 4c95f0fb15f096f3bf16a3677760e8df %}

és ez azt jelenti, hogy egy kicsit bele kell túrni a kódba.

Ez nem tűnik akkora problémának, de a valóságban sok időt el fogunk tölteni vele.

> Erre született áthidaló megoldás (bővebben [itt](https://guides.gradle.org/migrating-build-logic-from-groovy-to-kotlin/#configuring-plugins))
  de ez még mindig nem annyira egyszerű, mint a régi Groovy megoldás.

## Szóval megéri váltani?

Láthattuk, hogy a *kotlin-dsl* sok nagyszerű dolgot ad nekünk, amikről Groovy-val csak álmodhatunk, de ezeknek a
többsége a Kotlin használatából adódik. Igazából a Groovy-hoz is lehetne nagyszerű IDE átmogatást írni, de sajnos
ez nem történt meg eddig.

Ezzel szemben van pár hátulütő, ami sok időnket el fogja venni, és okozhat álmatlan éjszakákat is,
főleg, ha nem beépített plugin-eket használunk, amiket nem triviális konfigurálni.

Összességében a *kotlin-dsl* nagyon hasznos eszköz, de szerintem még nem érett meg igazán. Akkor javasolnám a használatát,
ha már a teljes Groovy doksiba is belerakják a Kotlin példákat és a főbb projektekhez (mint pl a Spring Boot) is lesznek
Kotlin kódok. Ezzel elég jól haladnak, már most is jelen van a dokumentációban [mindkét verzió](https://guides.gradle.org/creating-build-scans/)
sok helyen. Ha az IDE támogatást is kikupálják, akkor biztosan át fogok állni Kotlinra!

Ha esetleg utálod a Groovy-t, vagy pionír típus vagy, akkor természetesen most is neki lehet látni, de mint minden
friss projektnél, itt is tudni kell, hogy lesznek még bökkenők.
