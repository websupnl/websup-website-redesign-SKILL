# WebsUp Website Redesign — aangepaste skill

Dit pakket vertaalt Daans 35-secondenbrief naar een herbruikbare werkwijze voor een code-agent. De bestaande `motion-broll`-engine blijft de mogelijke technische basis; de workflow verandert van B-roll bij een spreker naar één zelfstandige website-redesignfilm.

## Inhoud

- `SKILL.md`: de aangepaste skill.
- `references/CASE-WEBSITE-REDESIGN.md`: verhaal, exacte teksten en alle 13 tijdvakken.
- `references/ENGINE-ADAPTATION.md`: bestaande mogelijkheden versus benodigde uitbreidingen.
- `references/QA-CHECKLIST.md`: controle van authenticiteit, motion, mobile, rendering en geluid.

## Status

Dit is een uitgewerkte instructieskill, geen al gebouwde of geteste filmgenerator. De upstream engine is niet meegeleverd, niet gewijzigd en niet geïnstalleerd. Er is nog geen website vastgelegd en geen MP4 gerenderd. In het aangeleverde brief ontbreken de concrete oude en nieuwe website en de definitieve merk-/audioassets.

## Gebruiken

Open dit pakket naast de bestaande `Barty-Bart/motion-graphics`-repository in je code-agent. Laat de agent `SKILL.md` als opdracht lezen; laat hem de werkelijke enginepaden in jouw project opzoeken. Een projectlokale skill-installatie kan daarna via de skillmap die jouw agent ondersteunt.

Plak bijvoorbeeld:

```text
Lees websup-website-redesign/SKILL.md en de bijbehorende referenties.
Gebruik deze aangepaste skill voor de Website Redesign Animation.
Mijn aangeleverde 35-secondenbrief blijft leidend.

Gebruik de bestaande motion-broll-engine waar die past, maar niet de
workflow voor een talking-headvideo, transcript, losse B-rollclips of
source-video-compositing. Verander geen bestaande globale installatie.

Voor: [oude website-URL of pad naar referenties]
Na: [nieuwe website-URL, lokale broncode of goedgekeurd ontwerp]
Formaat: [bijvoorbeeld 1080 x 1920 of 1920 x 1080]
WebsUp-branding: [pad of goedgekeurde bron]
Audio: [beschikbare/licentiegeschikte assets, of nog niet beschikbaar]

Inspecteer eerst de echte oude en nieuwe website. Maak een mapping van
logo, navigatie, kop, foto en primaire knop. Bouw één doorlopende scène
waarin deze onderdelen herkenbaar veranderen. Houd de oude site eerlijk
en geef de afgewerkte site de voorgeschreven schermtijd.

Controleer tussenframes, de echte mobiele layout, terugspoelen/seek,
beeldvergelijking en de uiteindelijke audio/video-export. Lever alleen
bestanden en testresultaten die daadwerkelijk bestaan. Benoem ontbrekende
referenties en aannames; presenteer geen fictieve klantcase als echt.
```

De instructies zijn bewust expliciet over wat de bestaande engine niet automatisch doet: sites uitlezen, elementen koppelen, mobiele layouts laten overvloeien en audio mixen. De implementerende agent moet die onderdelen daadwerkelijk bouwen en controleren.

## Bronnen

Onderzocht: `Barty-Bart/motion-graphics`, commit `e8d610adcf946367430c8b43a97aad8059befaad`, in het bijzonder README, SKILL.md, engine-api.md, motion.js, render.js en build.py.

Repository: https://github.com/Barty-Bart/motion-graphics

Case: door Daan aangeleverde Website Redesign Animation-brief in deze chat.

Dit pakket bevat geen upstream enginecode of lettertypebestanden.
