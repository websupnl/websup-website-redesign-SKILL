# WebsUp Website Redesign

Een herbruikbare instructieskill voor een zelfstandige website-redesignfilm: van een klantbericht naar de oude website, via een zichtbare verbouwing naar het eindresultaat, en terug naar het gesprek.

**Status:** de skill en productiespecificatie zijn uitgewerkt. Dit is nog geen gebouwde filmgenerator of gerenderde video. De animatie-engine, concrete website-assets en audio zijn niet meegeleverd.

## Inhoud

```text
AGENTS.md
skills/
  websup-website-redesign/
    SKILL.md
    README.nl.md
    references/
      CASE-WEBSITE-REDESIGN.md
      ENGINE-ADAPTATION.md
      QA-CHECKLIST.md
```

- [De skill](skills/websup-website-redesign/SKILL.md): workflow, visuele continuiteit, uitvoering en oplevering.
- [De 35-secondenfilm](skills/websup-website-redesign/references/CASE-WEBSITE-REDESIGN.md): 13 shots, teksten, timing en geluidrichting.
- [Engine-aanpassing](skills/websup-website-redesign/references/ENGINE-ADAPTATION.md): hergebruik van motion-broll en wat nog gebouwd moet worden.
- [Kwaliteitscontrole](skills/websup-website-redesign/references/QA-CHECKLIST.md): beeld, beweging, mobiel, rendering en audio.
- [Oorspronkelijke pakket-uitleg](skills/websup-website-redesign/README.nl.md).

## Beginnen

Open deze repository in je code-agent. Gebruik bijvoorbeeld:

```text
Lees AGENTS.md, skills/websup-website-redesign/SKILL.md en alle referenties.
Gebruik deze skill voor een zelfstandige Website Redesign Animation.

Voor: [oude website-URL of referentiebestanden]
Na: [nieuwe website-URL, lokale broncode of goedgekeurd ontwerp]
Formaat: [staand of liggend]
Branding en audio: [beschikbare assets]

Inspecteer eerst de echte voor- en na-versie. Behoud de visuele identiteit
van de klant en laat herkenbare onderdelen doorlopend transformeren.
Volg de 35-secondenplanning en controleer ook de tussenframes.

Gebruik de bestaande motion-broll-engine wanneer beschikbaar. Zoek die
op in de werkomgeving; rapporteer ontbrekende afhankelijkheden eerlijk.
Geen talking-headvideo, transcript of voiceover nodig.
Lever een preview, bewerkbare bron en alleen daadwerkelijk gerenderde,
gecontroleerde videobestanden. Publiceer geen klantmateriaal zonder toestemming.
```

De concrete oude en nieuwe website, het uitvoerformaat en de definitieve assets moeten voor productie nog worden gekozen. De chatteksten in de case zijn scripttekst, geen bewijs van een echt klantgesprek.

## Technische basis

Deze skill is uitgewerkt als aanvulling op [Barty-Bart/motion-graphics](https://github.com/Barty-Bart/motion-graphics), met als onderzochte upstream commit `e8d610adcf946367430c8b43a97aad8059befaad`.

De vijf bestanden uit het oorspronkelijke skillpakket staan ongewijzigd onder `skills/websup-website-redesign/`. De upstream engine en lettertypebestanden zijn niet gekopieerd. Raadpleeg de bronrepository voor de engine en de daarbij behorende licenties.

## Bestanden en toegang

Deze repository bevat alleen de skill en documentatie. Houd klantcaptures, niet-vrijgegeven ontwerpen, audioassets, credentials en renders buiten een openbare repository. De meegeleverde `.gitignore` negeert enkele gebruikelijke lokale werkmappen en exports; controleer altijd zelf welke bestanden je commit.
