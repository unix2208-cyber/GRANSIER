# DER GRANSIER – Musik-App für Android

Native Android-App (Kotlin / Jetpack Compose), Projektversion 1.0.

## Was die App bereits macht

- Dunkles Künstlerdesign mit goldenen Akzenten, ohne künstliches Porträt.
- Ruft veröffentlichte Songs und Releases über Apples öffentlichen iTunes-Lookup-Katalog ab.
- Ergänzt Songs durch Abfrage der Album-/EP-/Single-Inhalte (bis zu 40 Releases).
- Zeigt Albumcover, Song- und Albumnamen, Veröffentlichung sowie Song-/Release-Zahlen an.
- Suche, Sortierung (neueste/A–Z), Albenübersicht mit Songauswahl.
- Öffnet Songseiten auf Apple Music.
- Öffnet Spotify pro Song: direkt über eine bekannte Track-URL in `spotify_links.json`, sonst gezielte Spotify-Suche nach Künstler und Songname.
- Direkte Künstler-Buttons für Spotify und Apple Music.
- Bindet die Weihnachts-Playlist auf Spotify ein.
- Speichert die zuletzt abgerufene Songliste auf dem Gerät, falls der Katalog gerade offline ist.

## Einschränkungen / ehrlich wichtig

Dies ist ein **Android-Studio-Quellcodeprojekt**, keine bereits installierbare oder signierte APK. Es konnte in dieser Umgebung mangels Android SDK und Gradle nicht kompiliert oder auf einem Telefon getestet werden.

Die App verwendet Apples öffentliche **iTunes Search/Lookup API** für Katalogdaten. Die Rückgaben hängen vom Store-Land, vorhandenen Releases und API-Limits ab; **vollständige Erfassung aller Veröffentlichungen ist nicht garantiert**. Der zusätzliche Albumabruf ist auf 40 Releases pro Aktualisierung begrenzt. Bei mehr als 40 Releases oder API-Fehlern weist die App auf mögliche Unvollständigkeit hin.

Spotify erfordert für einen offiziellen automatischen vollständigen Datenabgleich OAuth, Entwicklerzugang und die Einhaltung von Spotifys API-Bedingungen. Diese Starter-App speichert keine Geheimschlüssel und ruft keine Spotify-API ab. Nicht hinterlegte Songs öffnen deswegen eine Spotify-Suche, nicht zwingend den exakten Track. Im Verzeichnis `app/src/main/assets/spotify_links.json` kann man nach und nach **exakte** Tracklinks pro Songtitel eintragen.

Die App streamt oder lädt Songs **nicht selbst herunter**. Streaming erfolgt direkt bei Spotify bzw. Apple Music mit den dort üblichen Berechtigungen / Abonnements.

## APK ohne Android Studio über GitHub erstellen (empfohlen)

Dieses Projekt enthält den GitHub-Actions-Workflow
`.github/workflows/android-apk.yml`. Sobald du den entpackten Projektinhalt in
ein GitHub-Repository hochlädst, kann GitHub automatisch eine installierbare,
signierte **Debug-APK** bauen und als Download bereitstellen.

**Die vollständige Schritt-für-Schritt-Anleitung steht in
`APK_ERSTELLEN_GITHUB.md`.**

Die APK muss erst durch GitHub Actions erzeugt werden; sie ist nicht
im Projekt-ZIP enthalten.

## Öffnen / Build in Android Studio

1. Android Studio auf dem Rechner installieren (mit Android SDK 35 / Platform Tools, Java 17).
2. Das ZIP entpacken und in Android Studio `File > Open` wählen. Ordner `DER_GRANSIER_Android` öffnen.
3. Gradle-Synchronisierung erlauben. Das Projekt ist für **Gradle 8.9**, **Android-Gradle-Plug-in 8.7.3**, Kotlin 2.0.21 und `compileSdk=35` vorgesehen.
4. Falls Android Studio über eine fehlende Gradle-Wrapper-JAR klagt, **Gradle 8.9 installieren** und im Projekt einmal `gradle wrapper --gradle-version 8.9` ausführen; anschließend erneut synchronisieren. (Die Wrapper-JAR konnte in der Erstellungsumgebung nicht bezogen werden.)
5. Mit angeschlossenem Android-Telefon oder Emulator `Run > Run app` ausführen.
6. Für eine eigene APK: `Build > Build Bundle(s) / APK(s) > Build APK(s)`.
7. Für den Play Store: zusätzlich App-Signatur, aktuelle Ziel-SDK-Vorgaben, Datenschutzangaben, finale Marken-/Assetprüfung und Tests erledigen.

Internet-Zugriff wird ausschließlich zum Laden des Katalogs, der Cover und beim Öffnen von Streaming-Plattformen verwendet. Der lokale Cache nutzt SharedPreferences; es gibt keinen eigenen Nutzerlogin oder Analytics in diesem Projekt.

## Künstleradressen

Spotify: https://open.spotify.com/artist/5MoxnUOEkWHFWvO2ZgPu2j

Apple Music: https://music.apple.com/at/artist/timm-gransier/1874597361

## Spotify-Titellinks pflegen

Datei `app/src/main/assets/spotify_links.json` öffnen; weitere Paare ergänzen:

```json
{
  "Songtitel exakt wie bei Apple": "https://open.spotify.com/track/DEINE_TRACK_ID"
}
```

Für einen neuen Song ist **kein** App-Update nötig, solange die Apple-Lookup-Daten ihn liefern. Eine Änderung dieser **lokal eingebauten Spotify-Titellink-Datei** erfordert in V1 dagegen einen App-Neubuild. Eine später zentral gepflegte Online-Datenbank würde diesen Schritt ersparen.

## Technische Quellen

- Apple Lookup API: https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/iTuneSearchAPI/LookupExamples.html
- Spotify API / Authorization: https://developer.spotify.com/documentation/web-api/concepts/authorization
- Gradle-AGP-Kompatibilität: https://developer.android.com/build/releases/about-agp
