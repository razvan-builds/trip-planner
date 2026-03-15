# Prompt AI Trip

Ești un trip planner expert. Ajută-mă să planific o călătorie și generează un JSON importabil în aplicația mea de Trip Planner.

## Informații despre călătorie

**Destinație:** [ex: Roma, Italia]  
**Durate:** [ex: 3 zile, 15-17 Aprilie 2026]  
**Aeroport sosire:** [ex: Fiumicino FCO]  
**Ora aterizare:** [ex: 21 Martie, 08:00]  
**Aeroport plecare:** [ex: Fiumicino FCO] (sau același)  
**Ora zbor retur:** [ex: 23 Martie, 22:30]  
**Cazare:** [ex: Hotel Colosseum Roma, lângă Colosseum]  
**Adresa cazare (sau link Maps):** [ex: Via dei Fori Imperiali 12]  
**Buget mâncare/zi:** [ex: €30-50]  
**Stil de călătorie:** [ex: îmi place să mă plimb mult, nu mă interesează muzee, prefer street food]

## Obiective deja stabilite (opțional)

[Listează aici locurile pe care deja le-ai decis. Poți pune linkuri Google Maps, nume, sau chiar text copiat din research-ul tău. Exemple:]  
- Colosseum (am bilet pe 16 Apr la 10:00)  
- Trastevere seara pentru mâncare  
- https://maps.app.goo.gl/xxxxx (link copiat din Maps)  
- Vatican — dar nu vreau să intru, doar să văd din exterior

## Linkuri Google Maps cu locații salvate (opțional)

[Dacă ai o listă Google Maps sau locații salvate, pune linkurile aici. Pot fi:]  
- Linkuri individuale: https://maps.app.goo.gl/xxxxx  
- Sau descrie: "Am o listă pe Google Maps cu 12 locuri salvate în Roma"  
- Sau pune screenshot-uri cu locațiile

## Ce vreau de la tine:

1. **Organizează** obiectivele mele + adaugă sugestii proprii într-un itinerariu pe zile, eficient geografic
2. **Găsește coordonatele GPS** (lat/lng) pentru fiecare locație
3. **Sugerează** viewpoints gratuite, hidden gems, restaurante locale bune
4. **Marchează** ce necesită rezervare
5. **Include** stațiile de transport relevante (aeroport ↔ hotel, stații de metrou cheie)
6. **Generează JSON-ul** în formatul de mai jos

## FORMAT JSON OBLIGATORIU:

```json
{
  "tripName": "Roma",
  "dates": "15 — 17 Aprilie 2026",
  "hotel": {
    "name": "Hotel Colosseum Roma",
    "lat": 41.8902,
    "lng": 12.4922
  },
  "transport": [
    {
      "name": "Fiumicino Airport (FCO)",
      "lat": 41.8003,
      "lng": 12.2389,
      "note": "Zbor sosire: 15 Apr 08:00 / Zbor retur: 17 Apr 22:30"
    },
    {
      "name": "Roma Termini",
      "lat": 41.9013,
      "lng": 12.5022,
      "note": "Gară centrală + metrou"
    }
  ],
  "days": [
    {
      "id": "d1",
      "title": "Ziua 1",
      "date": "Miercuri, 15 Aprilie",
      "subtitle": "Zona X → Zona Y → Zona Z",
      "collapsed": false,
      "spots": [
        {
          "id": "s1",
          "name": "Numele locației",
          "time": "10:00",
          "desc": "Descriere scurtă 1-2 propoziții.",
          "type": "sight",
          "lat": 41.8902,
          "lng": 12.4922,
          "visited": false,
          "appointment": "",
          "ticketUrl": "",
          "attachments": [],
          "tags": ["Iconic", "Gratis"],
          "mapsUrl": "https://maps.google.com/?q=41.8902,12.4922"
        }
      ]
    }
  ]
}
```

## Reguli pentru type:

- "sight" = obiectiv turistic, plimbare, clădire, monument
- "food" = restaurant, piață de mâncare, cafenea (prânz sau cină)
- "viewpoint" = punct panoramic, rooftop, terasă cu vedere
- "transport" = stație de tren/metrou/bus importantă

## Reguli pentru itinerariu:

- Organizează pe zone geografice (nu sări dintr-o parte în alta a orașului)
- 2 mese pe zi (prânz + cină), fără mic dejun
- Include ora aproximativă pentru fiecare oprire
- Adaugă "appointment" doar dacă e specificat explicit (ex: bilet la oră fixă)
- Adaugă "ticketUrl" cu link de cumpărare bilete unde e relevant
- "mapsUrl" = link Google Maps pentru fiecare locație (format: https://maps.google.com/?q=LAT,LNG)
- Include viewpoints gratuite (rooftop bars gratuite, dealuri, terase)
- Marchează cu tag "Rezervare!" ce necesită booking anticipat
- Fiecare id trebuie să fie unic (d1, d2... pentru zile, s1, s2... pentru spots)

## IMPORTANT:

- Returnează DOAR JSON-ul valid, fără explicații suplimentare
- JSON-ul trebuie să fie complet și gata de import (copy-paste într-un .json file)
- Nu pune comentarii în JSON (// nu e valid în JSON!)
- Asigură-te că coordonatele GPS sunt corecte
- Generează linkuri Google Maps funcționale
