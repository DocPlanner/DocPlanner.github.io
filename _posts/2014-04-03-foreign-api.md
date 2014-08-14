---
layout: default
title: "Jak przygotować API?"
published: true
---

Jak przygotować API dla ZnanegoLekarza?
=======================================

Słowem wstępu
-------------

Poniższa instrukcja ma na celu nakreślić ogóle wymagania dotyczące API służącego do wymiany informacji na temat lekarzy, harmonogramów i umawianych wizyt. Powinna być traktowana bardziej jako wskazówki, niż jako sztywne wytyczne. Rozumiemy, że procesy umawiania, model danych, etc, mogą znacząco się różnić w Państwa implementacji. W takiej sytuacji oczywiście ZnanyLekarz dostosowuje się do istniejącego systemu.

Jakie dane powinno udostępniać API?
-----------------------------------

W integracji ZnanegoLekarza z zewnętrznymi systemami obsługującymi rezerwację wizyt konieczny jest system wymiany danych na temat:

 * Placówek i poradni zdefiniowanych w systemie, wraz z ogólnymi danymi pomagającymi je dokładniej zidentyfikować, jak np. specjalizacje medyczne lub nazwa z adresem.
 * Lekarzy przyjmujących w ramach danej placówki/poradni.
 * Harmonogramów przyjęć lekarzy w ramach placówki/poradni
 * Oraz rezerwowania i zwalniania terminów wizyt

Architektura API
----------------

Technologia, o którą oparte będzie API jest dowolna, ze wskazaniem na WebService SOAP-owy.

Przykładowe interfejsy metod
----------------------------

Poniżej dokładniejszy opis tego, jakie metody mógłby udostępniać `WebService`:

### `getWorkplaces()`

Lista placówek / adresów / poradni, etc. Przykładowo:

    {
       "id": "00C55657-F0F8-4C8F-991E-C2FDF197D65D",
       "name": "POL LEK MED",
       "address": "ul. Solidarności 15a, Warsazwa",
       "specializations": ["ortopedia", "…"]
    }

### `getPersonnel(uuid workplaceId)`

Lekarze przyjmujący w danej jednostce:

    [
      {
        "id": "44BE83FB-6374-48AD-B420-C1A39E627A8B",
        "name": "Jan Kowalski",
        "specializations": ["ortopeda", "…"]
      }
    ]

### `getPersonnelSchedule(uuid personnel)`

Harmonogramy wizyt lekarza. Może być to w formie przedziałów czasowych, albo konkretnych dostępnych slotów. Z punktu widzenia ZnanegoLekarza istotne są jedynie godziny dostępne.

    [
      {
        "start": "2014-02-21 12:50",
        "end": "2014-02-21 17:00",
        "services_ids": ["…", "…"]
      }
    ]

### `getVisitDetails(uuid visitId)`

Szczegóły na temat wizyty (interesuje nas czas, miejsce i lekarz):

    {
      "id": "…",
      "personnel": "…",
      "workplace": "…",
      "services_ids": ["…", "…"],
      "start": "2014-02-25 12:20",
      "end": "2014-02-25 12:50"
    }

ZnanyLekarz będzie używał tej metody po otrzymaniu informacji z zewnętrznego systemu, że wizyta o danym ID zmieniła status. Nie są tu potrzebne jakiekolwiek dane pacjenta, jedynie informacja identyfikująca wizytę w czasie / miejscu.

### `bookVisit(uuid personnel, uuid workplace, datetime …)`

Rezerwuje wizytę, podając dane pacjenta. ZnanyLekarz dostarcza następujące dane identyfikujące pacjenta:

 * Imię oraz Nazwisko
 * Adres e-mail
 * Zweryfikowany (kodem SMS-owym) numer telefonu
 * PESEL (OPCJONALNIE

Oraz dodatkowo wszelkie dane dotyczące placówki / lekarza / daty w formacie wymaganym przez zewnętrzny system. 

Metoda powinna zwracać dane umożliwiające odwołanie się do danej wizyty później.

### `cancelVisit(uuid visitId)`

Anulowanie wizyty wcześniej umówionej przez ZnanegoLekarza.

### `getServices()`
Pobiera listę usług

    {
      "id": "…",
      "name": "…",
      "price": {
      		"min": …,
            "max": …
       },
       "duration": "…"
    }