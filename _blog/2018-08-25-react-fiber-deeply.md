---
excerpt: Hogyan működik és milyen koncepciókból áll össze a React Fiber? Ennek járt utána részletesen Brandon Dail.
title: Így működik a React Fiber!
date: 2018-08-25
tags: [react, fiber, algorithm]
short_title: Így működik a React Fiber!
---

Mikor egy bő éve a React Fiber sztorijával bővebben foglalkoztam, még bőven a kiadás előtt voltunk. De már kb egy éve kint van a stabil verzió, sokan észrevétlenül használják akár productionben is, illetve a csapat iterált jópárat az elképzelésen.

> *Ha nincs meg a téma*, röviden a core ún. reconciler algoritmus teljes újragondolásáról / újraírásáról van szó. De [itt](https://appcraft.hu/posts/blog/2017/04/17/react-fiber.html) bővebben is elolvashatod.

Hosszú összefoglaló volt, sok részlettel, de bőven voltak olyan területek, amelyekbe meg se próbáltam belemenni, túl mélyek voltak.

Nem így Brandon Dail, aki ebben a friss-ropogós React Rally konferenciás előadásában rendesen a mélyére nézett és adott erről egy frankó összefoglalót. Oda kell figyelni, de egyébként tök jól érthető.

<iframe width="560" height="315" src="https://www.youtube.com/embed/cWY1QzyFhfk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## tl;DR

*Tényleg csak néhány kiemelés:*
- Rávilágít párhuzamokra az async rendering koncepció és az operációs rendszerek szál és folyamat fogalmai között.
- A fancy kifejezés mögözz két kulcs fogalom van, a time slice és a suspense. Felosztja az időt kis szeletekre, minden kis munka csomag kap egy ilyen szeletet, és utána megállítja.
- Kell pár apróság, hogy ez a kettő jól működjön:
	- Ilyenkor jól jön egy call stack, amiben ez kezelve van.
	- Van még egy párhuzam a korutinokkal, kooperatív futtatási modellt írnak le.
	- Az algebraic effect fogalom valójában sokkal egyszerűbb mint, aminek elsőre tűnik. Kb mint az eventek, történik valami, és annak hatására lefut egy funkció, ami kezeli. Hibakezelésnél, adatbázis vagy hálózat hívásnál, illetve mondjuk logolásnál is jól jön.

Bizonyos szempontból olyan benyomást kelt bennem mintha egy mini-OS épülne a böngészőn belül, és ezt nem negatívan mondom. Látom a problémákat, amikre választ ad, tutire lesznek (sőt vannak) olyan komplex és reaktív webappok, ahol erre szükség van.

Have fun! 😀
