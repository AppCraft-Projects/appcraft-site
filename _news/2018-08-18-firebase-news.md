---
excerpt: Az idei Google I/O során mintha idén elmaradt volna az elmúlt években megszokott Firebase tűzijáték, nem is rémlik semmi különösebb újdonság / bejelentés.
title: 🏖️ Véget érni látszik a nyári szünet a Firebase csapatnál
event_date: 2018-08-18
tags: [google, firebase, push notification, integration, jira, slack, cloud, firestore, functions, hosting]
author: Gabor Orosz
short_title: 🏖️ Véget érni látszik a nyári szünet a Firebase csapatnál
---

Az idei Google I/O során mintha idén elmaradt volna az elmúlt években megszokott Firebase tűzijáték, nem is rémlik semmi különösebb újdonság / bejelentés.

Ellenben az elmúlt hetekben rendesen felpörögtek a lányok, számos [új fejlesztéssel](http://bit.ly/firebase-whats-new) jelentkeztek, érdemes ezekből párat egy jó kis csokorba fűzni.

## In-app üzeneteket

Korrekt [csomagot](http://bit.ly/firebase-in-app-msg) raktak össze, a videó ad is egy gyors összefoglalást.

<iframe width="560" height="315" src="https://www.youtube.com/embed/5MRKpvKV2pg" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Röviden:

- Lehet egyszeri és visszatérő.
- User event is triggerelheti őket.
- Targetálhatsz különböző felhasználói szegmenseket.
- Normálisan témázható.
- A megszokott közös anilitika van mögötte.

Integrációs doksi [erre](http://bit.ly/firebase-iam-get-started).

## Crashlytics integrációk

Időnként szükség van arra, hogy mélyebben bele lehessen túrni a hibák okába, és ilyenkor nem volt nehéz elérni a reporting felület határait. Mostantól viszont lehetőség van BigQuery-be [exportálni](http://bit.ly/firebase-crashlytics-bigquery) az adatokat, innentől pedig egy lépés a normális vizualizálás Data Studioval.

A következő hetekben elindítanak egy Jira integrációt is, a hiba jelentésekből új issuekat hoz majd létre. Erről sajnos még nem találtam doksit.

Viszont tök jó párja lesz a nem is olyan régen bejelentett hasonló [Slack integrációnak](http://bit.ly/firebase-slack). Szerintem számos cégnél örülni fognak, ahol ezeket az eszközöket használja.

## És még sok más...

Innentől tényleg csak címszavakban:

- A konzol több felületén csiszolgattak.
- A Cloud Next 2018 során jó adat [FireStore](http://bit.ly/firebase-cloud-firestore) fejlesztést lehetett találni.
- A [Cloud Functions](http://bit.ly/firebase-cloud-functions-runtime) most már általánosan elérhető lesz európában és ázisában is.
- A Hosting lehetővé teszi [több site kiszolgálását egy projektből](http://bit.ly/firebase-hosting-multisite).
