# stackwild-instagram

Ablage für Bilder und Videos des Instagram-Kanals **StackWild**. Das Repo ist
öffentlich, weil Instagram Medien nur von öffentlichen Adressen abholt. Hier
liegt nur, was ohnehin auf Instagram erscheint.

## Aufbau

```
posts/
  2026-11-20-claude-code-erste-schritte/
    01.jpg … 10.jpg   Karussell-Bilder in Reihenfolge (oder video.mp4)
    caption.md        Text und Hashtags, genau so wie er gepostet wird
    post.json         Typ, Status, Instagram-ID nach Veröffentlichung
```

## Ablauf pro Post

1. **Entwurf:** Claude legt den Ordner an, baut die Medien und schreibt `caption.md`.
   `post.json` → `"status": "entwurf"`.
2. **Freigabe:** Myriam sieht Bilder und Text durch und gibt im Chat frei.
   → `"status": "freigegeben"`.
3. **Push:** Medien sind dann unter
   `https://raw.githubusercontent.com/myriam72/stackwild-instagram/main/posts/<ordner>/<datei>` erreichbar.
4. **Veröffentlichen:** Claude postet über Windsor.ai und trägt die Instagram-ID ein.
   → `"status": "veröffentlicht"`.

## KI-Kennzeichnung

Jeder Post mit KI-Anteil (Grafiken, Text, Video, Stimme) wird gekennzeichnet:

- **Text:** Die letzte Zeile vor den Hashtags lautet
  `Erstellt mit KI-Unterstützung (Claude).` – bei rein KI-generierten Bildern/Videos
  `Bilder/Video KI-generiert.` Dazu der Hashtag `#KIgeneriert`.
- **Instagram:** Das KI-Label lässt sich über die Schnittstelle nicht setzen; im Text steht der Hinweis immer.
- **TikTok:** Schalter „KI-generierte Inhalte“ (`is_aigc`) immer an.
- **YouTube:** „Veränderte oder synthetische Inhalte“ auf Ja, wenn realistisch wirkende KI-Inhalte enthalten sind; Hinweis zusätzlich in der Beschreibung.

`post.json` hält fest, wie gekennzeichnet wurde (`ki_kennzeichnung`).

Ohne ausdrückliches Okay im Chat wird nichts veröffentlicht. Entwürfe bleiben
lokal und werden erst nach der Freigabe gepusht.

## Was hier nie hineinkommt

Das Repo ist öffentlich, jeder Commit bleibt sichtbar.

- keine Zugangsdaten, Tokens, API-Schlüssel, `.env`-Dateien
- keine privaten Mailadressen: Commits laufen über
  `187094183+myriam72@users.noreply.github.com` (lokal in `.git/config` gesetzt)
- keine Entwürfe, Notizen, Redaktionspläne, Statistiken
- keine Metadaten in Medien: Bilder werden vor dem Commit ohne EXIF/GPS neu gespeichert
- keine Screenshots, auf denen Mails, Kundendaten, Pfade mit Namen oder Tokens zu sehen sind

## Technische Vorgaben von Instagram

| Format | Vorgaben |
|---|---|
| Einzelbild / Karussell | JPEG, max. 8 MB, Seitenverhältnis 4:5 bis 1.91:1 (empfohlen 1080×1350), Karussell 2–10 Bilder |
| Reel | MP4/MOV, 3 s – 15 min, max. 1 GB, 9:16 (1080×1920) |
| Story | JPEG oder MP4/MOV (3–60 s), 9:16, kein Text |
| Text | max. 2.200 Zeichen |
