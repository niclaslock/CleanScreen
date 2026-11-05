# CleanScreen – Projektkontext

Eigener Startbildschirm für einen Samsung The Frame (Tizen-Web-App).
Sprache mit dem Nutzer: Deutsch.

## Ziel

Samsung erlaubt es nicht, den Tizen-Home-Screen wirklich zu ersetzen. Stattdessen:

1. Eigene **Tizen-Web-App** (HTML/CSS/JS), per Entwicklermodus installiert.
2. **Home-Assistant-Automation**, die die App beim Einschalten des TVs startet.
3. Aus der App heraus andere Apps starten, per Fernbedienung bedienbar.

## Funktionsumfang v1

- Kacheln: **Netflix**, **Prime Video**, **Disney+**, **HD+**
  - Ob HD+ über die HD+ App oder über ein CI+-Modul läuft, ist noch offen. Danach richtet sich, ob die Kachel eine App startet oder auf den TV-Tuner umschaltet.
- Button: HA-Szene **Fernsehabend** starten (`scene.fernsehabend`)
- Kachel: **Art Mode** aktivieren
- Navigation komplett per Fernbedienung (Pfeiltasten, OK, Zurück)

## Gerät

| | |
|---|---|
| Modell | GQ55LS03TAUXZG (The Frame, Baujahr 2020, Tizen 5.5) |
| IP Fernseher | 192.168.178.130 |
| MAC | 68:72:c3:0b:ed:c2 |
| Entwicklermodus | wird vom Nutzer aktiviert; Host-PC-IP = IP des lokalen Rechners |

## Home Assistant

| | |
|---|---|
| URL im LAN | http://192.168.178.152:8123 |
| TV-Entity | `media_player.the_frame_tv_2` (+ `remote.the_frame_tv_2`) |
| Integration | SamsungTV Smart (HACS, `samsungtv_smart` 0.14.5), kann Apps starten |
| Szene | `scene.fernsehabend` |

Den HA Long-Lived Access Token nie ins Repo committen, sondern in eine lokale,
per `.gitignore` ausgeschlossene Config-Datei legen.

## Offene Punkte

- Betriebssystem des lokalen Rechners (Windows/Mac) → Installation der Tizen Studio CLI
- HD+: App oder CI+-Modul?
- Samsung-Zertifikat (Samsung-Konto) für das Signieren erstellen
- Tizen-App-IDs für Netflix, Prime Video, Disney+, HD+ ermitteln
  (z. B. per `sdb shell` / `apps` oder über die REST-API des TVs auf Port 8001)

## Nächste Schritte

1. App-Grundgerüst (`config.xml`, `index.html`, `app.js`, `style.css`)
2. Tizen-CLI lokal installieren, Zertifikat erstellen, App bauen und per `sdb` installieren
3. HA-Automation: TV an → CleanScreen starten
