# DER GRANSIER – Installierbare Android-APK erzeugen (ohne Android Studio)

Mit dem enthaltenen GitHub-Actions-Workflow kann GitHub eine signierte **Debug-APK** bauen.
Die Debug-APK ist zum privaten Testen und zur Installation auf einem Android-Handy geeignet.
Für eine öffentliche Veröffentlichung im Play Store wird später ein signierter Release-Build benötigt.

## Schritte

1. Falls noch nicht vorhanden, kostenlos auf https://github.com/ registrieren.
2. Auf GitHub ein neues **privates** Repository erstellen (z. B. `der-gransier-android`).
   Beim Erstellen **keine zusätzliche README** anlegen.
3. Die ZIP-Datei `DER_GRANSIER_Android_mit_APK_Build.zip` auf dem Computer **entpacken**.
4. Im erstellten GitHub-Repository **Add file → Upload files** wählen.
   Die **Inhalte** des Ordners `DER_GRANSIER_Android` hochladen, nicht die ZIP-Datei.
   Wichtig: Auch den versteckten Ordner `.github` mit der Datei
   `.github/workflows/android-apk.yml` hochladen.
   Im Mac-Finder blendet **Cmd + Shift + .** versteckte Dateien/Ordner ein.
5. **Commit changes** wählen. Wenn der Repository-Hauptbranch `main` oder `master`
   heißt, wird der APK-Build beim Hochladen automatisch gestartet.
6. GitHub-Reiter **Actions** öffnen → **DER GRANSIER - Android APK**.
   Falls er nicht automatisch gestartet ist, **Run workflow** ausführen.
7. Nach einem erfolgreichen Durchlauf die Workflow-Ausführung öffnen.
   Unten bei **Artifacts** auf `DER-GRANSIER-Android-APK` klicken.
8. Das heruntergeladene ZIP entpacken. Darin liegt die Datei **`app-debug.apk`**.
   Diese APK auf das Android-Handy übertragen und installieren. Ggf. muss auf dem
   Handy die Installation aus dieser Quelle ausdrücklich erlaubt werden.

**Bitte beachten:** Die APK wird erst auf GitHub gebaut; hier liegt noch keine
fertig kompilierte APK vor. Der Kotlin-Code ist bisher nicht auf einem Android-Gerät
getestet. Sollte GitHub einen Buildfehler anzeigen, das Protokoll der fehlgeschlagenen
Ausführung aufrufen. Der Fehler lässt sich dann gezielt korrigieren.

**Datenschutz/Hinweis:** Das Repository kann privat sein. Der Debug-Build wird mit
GitHubs temporärem Entwicklungszertifikat signiert. Für dauerhaft verteilte
Release-Versionen sollte ein eigener Signaturschlüssel verwendet und sicher
aufbewahrt werden.
