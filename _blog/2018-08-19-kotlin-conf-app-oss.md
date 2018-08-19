---
excerpt: A Jetpack csomagot a Google I/O legfontosabb bejelentésének éreztem. Azon belül pedig a Navigation Components  különösen felkeltette a figyelmem.
title: 🛣️ Hasznos Android Navigation Component anyagok
date: 2018-08-19
tags: [android, jetpack, navigation, component, kotlin]
short_title: 🕵🛣️ Hasznos Android Navigation Component anyagok
---

## Néhány kósza bevezető gondolat...

Amennyire [laposra sikerült](https://appcraft.hu/posts/news/2018/08/18/firebase-news.html) Firebase szempontból az idei Google I/O, annyire pörgős Android fejlesztői szemmel.

Nem győztem kapkodni a fejem az újdonságokat látva, számos más hasznosság mellett a Jetpack csomagot vitán felül nagyon fontos előrelépésnek gondolom. Azon belül az egyelőre még alpha verziós Navigation Components  különösen felkeltette a figyelmem.

<iframe width="560" height="315" src="https://www.youtube.com/embed/8GCXtCjtg40" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Szükség volt valami ilyenre mint egy falat kenyérre, tudja ezt szerintem a legtöbb Android fejlesztő. *Ahogy valaki egy kicsit mélyebbre ásott az Android navigáció témakörben, úgy kiderülhetett, hogy ...*

- meglehetősen komplexé tud válni (pl. argumentum átadás, fragment tranzakciók, up és back, deep linkek, tesztelés ... stb.),
- valamint jelentős mennyiségű boilerplate kód is kell hozzá,
- oda kell figyelni, másképp gonosz [bugokra](https://www.androiddesignpatterns.com/2013/08/fragment-transaction-commit-state-loss.html) lehet futni.

Mennyivel kényelmesebb élete van az iOS fejlesztőknek a Storyboardokkal. Nyilván az sem tökéletes, de nagyságrendekkel egyszerűbb sztori.

![alt text](https://appcraft.hu/assets/img/android-nav-comp-01.png)

> Nos, a jó hír az, hogy Androidon is hasonló irányba látszanak mozdulni a dolgok.

## Hasznos anyagok

A hosszúra nyúlt bevezető, nem is húzom tovább az időt, két tök jó írást szeretnék a figyelmetekbe ajánlani, amivel jobban beleáshatjátok magatokat ebbe az újdonságba.

Először is Dario Mungoi (Shopify és Android GDE) alaposan a mélyére nézett az új komponensnek és tök jól elmagyarázza az építő elvét. Vaskos olvasmány, rögtön három részben.

<blockquote class="embedly-card"><h4><a href="https://medium.com/google-developer-experts/android-navigation-components-part-1-236b2a479d44">Android Navigation Components - Part 1 - Google Developers Experts - Medium</a></h4><p>Last week I attended the Google I/O 2018 in Mountain View, California.It was a great event and a lot of things were announced. From all these things, the Navigation component was the one that captured most of my attention.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>

<blockquote class="embedly-card"><h4><a href="https://medium.com/google-developer-experts/android-navigation-components-part-2-ca643eb301e3">Android Navigation Components - Part 2 - Google Developers Experts - Medium</a></h4><p>Two weeks ago at the Google I/O, Google released a lot of great tools to help developers speed up their development process and build better apps. Some of these announcements were the Android Navigation Components. The Navigation Components is a library part of the Android Jetpack set of libraries.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>

<blockquote class="embedly-card"><h4><a href="https://medium.com/google-developer-experts/android-navigation-components-part-3-19554ec9ae83">Android Navigation Components - Part 3 - Google Developers Experts - Medium</a></h4><p>Two weeks ago, I started writing about the Android Navigation Components. The Android Navigation Components library is part of the Android JetPack set of libraries announced and released during Google I/O 2018. I started these series of posts talking about the importance of (re) understanding your app structure before using the library.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>

---

Másodszor pedig Sagar Viradiya mutatja be a használatot egy egyszerű példán keresztül.

<blockquote class="embedly-card"><h4><a href="https://proandroiddev.com/android-jetpack-navigationui-a7c9f17c510e">Android Jetpack - NavigationUI - ProAndroidDev</a></h4><p>With navigation component you can reduce boilerplate code for fragment transactions(and avoid possible bug if you don't do it properly) and starting activity.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>

## Zárásként

Szerintem nagyon izgalmas újdonság készülő, amivel egy kicsit biztosanakká válhatnak az Android fejlesztők.

Nem beszélve arról, hogy a fárasztó boilerplate helyett még inkább az üzleti problémák megoldására tudnak fókuszálni. Mert ugye azokból van is és lesz is bőséggel.

Happy coding! 😀