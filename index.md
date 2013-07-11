---
layout: default
title: API DocPlanner
---

API DocPlanner
==============

DocPlanner udostępnia prywantne API, dające dostęp do danych lekarzy, wyszukiwarki, a także umożliwiające zarządzanie całym procesem umawiania wizyt. 

API dostępne jest wyłącznie po HTTPS pod adresem:

    https://www.znanylekarz.pl/api/

Autoryzacja 
===========

API nie jest publiczne i wymaga podania pary `consumer_key` oraz `consumer_secret` do autoryzacji. Autoryzacja odbywa się protokołem *OAuth 1.0a* — więcej informacji na ten temat można przeczytać na [OAuth Bible](http://oauthbible.com/).

Dla testów, można używać danych aplikacji demo, która za każdym razem jedynie wyświetla parametry zapytania:

 * `consumer_key`: demo
 * `consumer_secret`: 26e25689f09b44092c5b4485e5761aedf9d7e732

Aby otrzymać produkcyjne dane dostępowe należy [skontaktować się z nami](#kontakt).


Format odpowiedzi
=================

Każdy komunikat zwracany przez API jest w formacie JSON i zawiera się w następującej strukturze:

```json
{
   "status": "ok",
   "message": null,
   "items": { … }
}
```

Lub, w przypadku błędu:

```json
{ 
  "status": "err",
  "message": "error description"
}
```

Gdyby komuś przyszło coś innego do głowy: komunikujemy się wyłącznie w UTF-8.

Metody dostępu
==============

Udostępniamy dwa sposoby dostępu do API:

 * Endpoint REST-owy, działa poprzez doklejenie parametru `method` w query, np. `https://www.znanylekarz.pl/api/?method=doctor.categories`
    
   Wszelkie parametry do metody powinny być przekazywane w query lub poprzez POST (`application/x-www-form-urlencoded`).
   
 * SOAP, pod tym samym adresem, a do którego WSDL znajduje się tu: `https://www.znanylekarz.pl/api/?wsdl`
   
   W przypadku SOAP `consumer_key` oraz `consumer_secret` należy uznać za dane do autoryzacji, a `access_token` użytkownika trzeba  podać jako pierwszy parametr wywoływanej metody.


Narzędzia
=========

Aby ułatwić pracę zostały przygotowane następujące narzędzia:

 * [SDK dla języka PHP]({{ site.baseurl }}/sdk)
 * [Rozszerzenie OAuth do PHP](http://php.net/oauth)
 * [Interaktywna konsola dostępu][mashape] — wymaga konta w serwisie Mashape

Przykłady
=========

Wywołanie używając aplikacji:
-----------------------------

![sample request](http://note.io/1atrZQv)

Przykładowy kod PHP:
--------------------

<script src="https://gist.github.com/mlebkowski/5047385.js"></script>

Kontakt
=======

 * [Maciej Łebkowski](mailto:maciej.lebkowski@docplanner.com)
 * [Piotr Ziewiec](mailto:piotr.ziewiec@docplanner.com)

[mashape]: https://www.mashape.com/mlebkowski/docplanner