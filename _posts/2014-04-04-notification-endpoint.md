---
layout: default
title: WebService powiadomień
published: true
---

Powiadomienia o zmianie statusu wizyty
======================================

Baza danych wolnych terminów lekarzy w aplikacji synchronizowana jest okresowo z zewnętrznymi systemami. Aby uniknąć w maksymalnym stopniu różnic w harmonogramach i konfliktów przy umawianiu wizyt, zewnętrzny system powinien informować ZnanegoLekarza o zmianie statusu wizyte (bookowanie / anulowanie / zmiana terminu, etc).

W tym celu udostępniony został `WebService` obsługujący takie notyfikacje.

Adres WSDL: [https://www.znanylekarz.pl/soap/wsdl.xml](https://www.znanylekarz.pl/soap/wsdl.xml)

Opis
----

`WebService` udostępnia dwie metody. Obie przyjmują jednakowe parametry:

  * `token` — są to dane autoryzacyjne, udostępnione dla konkretnej placówki przez ZnanegoLekarza
  * `visitId` — identyfikator wizyty w zewnętrznym systemie. Nie musi być to wartość numeryczna, może być to ciąg znaków lub bardziej złożona struktura typu XML lub JSON. Na podstawie tych danych ZnanyLekarz zidentyfikuje odpowiednik lokalnej wizyty, albo pobierze dodatkowe dane z systemu zewnętrznego (np. w przypadku podania ID lekarza, placówki i daty wizyty).

Nie są tu przesyłane jakiekolwiek dane pacjentów, ZnanyLekarz nie potrzebuje tych informacji.

Sandbox
----
 - WSDL: http://www.sandbox.znanylekarz.pl/soap/wsdl.xml
 - Token: 78e32ad37a54.42a2d369d686246945ca6f427bf60d7d