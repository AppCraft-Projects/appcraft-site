---
excerpt: Rendesen vakarhatja a fejét, aki animációkat az Android app kapcsán animációkban gondolkodik, de az új MotionLayout sokat javíthat a helyzeten.
title: Pofásodik az Android layoutos és animációs része 👀
date: 2018-06-29
tags: [android, layout, animation, video, development]
short_title: Android layout és animáció fejlesztések
---

Rendesen vakarhatja a fejét, aki animációkat az Android app kapcsán animációkban gondolkodik, a keretrendszer kínál néhány lehetőséget, amelyeket lehet kombinálgatni:
- [Animated Vector Drawable](http://bit.ly/android-adg)
- [Property Animation framework](http://bit.ly/android-prop-anim)
- [LayoutTransition animations](http://bit.ly/android-layout-trans)
- [Layout transitions with TransitionManager](http://bit.ly/android-anim-layout-trans)
- [CoordinatorLayout](http://bit.ly/android-coord-layout)

És ha ez nem elég, pár napja [alfa verzióba](http://bit.ly/android-cs2-alpha) érkezett Constraint Layout 2.0-val megérkezett a MotionLayoutot komponens is. Az I/O 2018 során jelentették be, ha nem emlékeznétek alább nézhető a videó releváns része.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ytZteMo4ETk?start=1751" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Mi is ez?

tl;DR, csak a lényeg:
- Tud mindent, amit a CoordinatorLayout, gazdag a pozicionálási eszközkészlet.
- Megörökölte a TransitionManager layout tranzíciós képességeit.
- És hozzátettek egy property animációs keretrendszert, amivel komplex mozgások kezelhetőek.
- Mindezt deklaratívan.
- Rendesen megtámogatva [Android Studio](http://bit.ly/as-3-2-beta2) oldalról. Nem egy Flash vagy Blend, de némi előrelépés.

![alt text](https://appcraft.hu/assets/img/android-studio-prop-anim.gif)

Egy mondatban tehát, a legfontosabb képességeket egy csomagba gyúrták össze.

## Hasznos anyagok gyűjtése

Mindenképp izgi a cucc, összeszedtem magamnak néhány anyagot az átnézéshez, és úgy gondoltam nektek is hasznos lehet.

Nicolas Roard írt erről egy frankó cikksorozatot:
- [Part 1](http://bit.ly/android-motion-layout-p1)
- [Part 2](http://bit.ly/android-motion-layout-p2)
- [Part 3](http://bit.ly/android-motion-layout-p3)

Valamint frissítették a ConstraintLayout példáit, a MotionLayout is kapott néhányat.

## Ti mit gondoltok?
Próbáltátok már? Van róla bármi benyomás? Mennyire sikerült javítani?
