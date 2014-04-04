---
layout: default
title: Integracje
date: 2013-07-10 10:03
---

Integracja systemu obsługi placówki
===================================

Integracja może przebiegać w jednym z dwóch trybów:

 * W przypadku, gdy Klient posiada własne API, ZnanyLekarz podłącza i dostosowuje się do niego
 * W przeciwnym razie, Klient musi skorzystać z API udostępnionego przez ZnanegoLekarza

W tym dokumencje opisana jest druga ścieżka. Więcej na temat pierwszej opcji można przeczytać w artykule [Jak przygotować API dla ZnanegoLekarza](/foreign-api)

Ogólny zarys
============

Integracja z API ZnanyLekarz ma na celu:

 * Zsynchronizować stan wolnych terminów dla danego lekarza
 * Otrzymać informacje w czasie rzeczywistym na temat nowo zabookowanych terminów oraz anulowanych wizyt

Aplikacja synchronizująca się z API ZnanyLekarz musi:

 * Autoryzować się przy pomocy OAuth 1.0a
 * Pobrać listę dostępnych w danej placówce lekarzy oraz ich kalendarzy wizyt (`user.related-doctors`, `doctor.calendars`)
 * Ustawić poprawne godziny przyjęć (`calendar.set-hours`)
 * Informować na bieżąco o terminach zabookowanych w placówce (`visit.book`) oraz zwolnionych (`visit.cancel`)

Aplikacja w podobny sposób wyśle informacje zwrotne w przypadku, gdy użytkownik zapisze się lub odwoła wizytę on-line przez www.znanylekarz.pl.

Autoryzacja
===========

Każda placówka otrzyma konto użytkownika, które będzie posiadać uprawnienia do zarządzania kalendarzem/wizytami każdego z lekarzy przypisanych do tej placówki. Z poziomu tego konta należy dokonać autoryzacji w OAuth.

WebHooks
========

ZnanyLekarz informuje w czasie rzeczywistym o zdarzeniach związanych z kalendarzem poprzez wysłanie zapytania na adres API podany przez Klienta. Format tego zapytania jest zgodny z API ZnanegoLekarza i występuje w postaci REST (parametry w query) lub SOAP.

