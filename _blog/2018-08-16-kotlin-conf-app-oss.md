---
excerpt: Pár nap különbséggel két nyílt forrású konferencia app is kapott némi felhajtást twitteren, úgy gondoltam érdekes lehet pár mondatot ezekről kicsit beszélni.
title: 🕵️‍♀️ Kotlinos csemege - Betekintés két konferencia app forrásába
date: 2018-08-16
tags: [kotlin, android, reference, conference, app, architecture, component]
short_title: 🕵️‍♀️ Kotlinos csemege - Betekintés két konferencia app forrásába
---

Pár nap különbséggel két nyílt forrású konferencia app is kapott némi felhajtást twitteren, úgy gondoltam érdekes lehet pár mondatot ezekről kicsit beszélni.

# Google I/O 2018 app

![alt text](https://appcraft.hu/assets/img/oss-conf-app-01.png)

Már szinte hagyomány, hogy minden évben megnyitja a Google a saját nagy konferenciájának alkalmazását, habár most sem kapkodták el, de itt van.

Az elmúlt években többször morogtam a kód minőségén és az itt használt mintákon. Nem gondoltam, hogy ténylegesen egy példás referencia kódbázist adtak ki a lányaik a kezükből. Márpedig azt várnám, hogy valami ilyen alakul belőle.

Most viszont újraírták és sokkal inkább próbálták tartani magukat a saját ajánlásaikhoz és egy jó kis modern csomag állt össze:
- Követik az [App Architecture Guide-ot].(http://bit.ly/droid-app-archi-guide)
- Mozgatták a logikát, Activity és Fragment helyett a [ViewModel](http://bit.ly/aaa-viewmodel) fogja össze.
- [LiveData](http://bit.ly/aaa-livedata) observálja az adatokat és [Data Binding Libraryval](http://bit.ly/aaa-data-bind-lib) kötnek a UI komponensekhez.
- Repository réteg fogja össze az adat operációkat, ami több forrással is jól működhetne, ezúttal a felhasználói adatok a [Firestoreban](http://bit.ly/cloud-firestore) vannak.
- [Dagger2](http://bit.ly/oss-dagger2) adja a DI-t, plusz a [dagger-android](http://bit.ly/oss-dagger-android) kímél meg sok boilerplate kódtól.
- Teszteléshez [Espressot](http://bit.ly/android-espresso) és [Mockitot](http://bit.ly/oss-mockito) használnak.
- ... ezen túl még van egy csomó Firebase motyó, persze Kotlin az egész és [Android KTX](http://bit.ly/android-kotlin-ktx) kiegészítéseket használnak, illetve naná, hogy [Material Theming](http://bit.ly/android-material-theming).

Később szeretnénk több Jetpack komponenst is behúzni, ahogy érettebbé válnak, de ezt majd meglátjuk.

🔖 [Itten](http://bit.ly/oss-google-io-app-2018-source) lehet belebújni a forrásba:

# DroidCon NYC 2018 app

![alt text](https://appcraft.hu/assets/img/oss-conf-app-02.png)

A DroidCon NYC mögötti csapat a 4. évükben még ambíciózusabbak voltak. Használnak sokat az előző appnál használt a komponesekből, de az egyedi fűszer itt a a Koltin Multiplatform projekt..

Igen, így Android mellett iOS-en is menni fog a buli,  de érdemes arra készülni, hogy az egész feeling sokkal... khmm... kísérletezősebb. Nem biztos, hogy production appban ma erre mennék, de POC-olni és a jövőbe tekinteni frankó.

A videó összefoglalja hogyan buildelhető az app és ad egy korrekt architektúrális áttekintést is...
<iframe width="560" height="315" src="https://www.youtube.com/embed/YAeDK3Ei0Lk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Sőt, még live kódoltak is...
<iframe width="560" height="315" src="https://www.youtube.com/embed/4BwmYYOQDGY" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

🔖 Na [itt](http://bit.ly/oss-droidcon-nyc-app-source) a forrás.

Jó kódböngészést és tanulást! Have fun! 😉