# Jasper Witt – privates Portfolio

Fertiges Paket für GitHub Pages. Kein Build, keine Installation, keine API und keine zusätzlichen Bilder erforderlich. Bilder und Logos sind im verschlüsselten Portfolio enthalten.

## Inhalt des Pakets

- `docs/index.html`: passwortverschlüsselte Website mit integrierten Bildern, Styles und JavaScript.
- `docs/.nojekyll`: deaktiviert Jekyll für die statische Seite.
- `README.md`: diese Anleitung; liegt außerhalb der Veröffentlichungsquelle.

## Veröffentlichung aus einem privaten Repo

GitHub Pages aus einem privaten persönlichen Repository setzt GitHub Pro voraus. Für Organisationen sind unter anderem GitHub Team oder Enterprise verfügbar. Ein privates Repo macht die veröffentlichte Pages-URL nicht automatisch privat.

1. Auf GitHub ein neues **privates** Repository erstellen, zum Beispiel `jasper-portfolio`.
2. Das ZIP lokal entpacken. Den Ordner `docs` und diese `README.md` direkt in die oberste Ebene des Repositorys hochladen und auf `main` committen. Das ZIP selbst wird nicht hochgeladen. `docs/index.html` muss genau so heißen und darf nicht in einem zusätzlichen Paket-Unterordner liegen.
3. Im Repo **Settings → Pages → Build and deployment** öffnen.
4. Als **Source** die Option **Deploy from a branch** wählen. Als Branch **main** und als Ordner **/docs** auswählen, dann **Save**.
5. Die Veröffentlichung abwarten. Die tatsächliche URL erscheint auf derselben Pages-Einstellungsseite. Diese öffnen und das separat mitgeteilte Passwort eingeben. **Enforce HTTPS** aktivieren, falls die Option nicht bereits aktiv ist.

Die Projekt-URL hat normalerweise die Form `https://BENUTZERNAME.github.io/REPOSITORY/`. Maßgeblich ist die tatsächlich von GitHub angezeigte URL.

## Passwortzugang

Der Portfolio-Inhalt ist mit AES-256-GCM verschlüsselt. Der Schlüssel wird lokal im Browser aus dem Passwort über PBKDF2/SHA-256 mit 310.000 Iterationen abgeleitet. Das Passwort ist weder im Paket noch in dieser Anleitung enthalten und wird nicht an einen Server gesendet oder im Browser gespeichert.

Die Seite benötigt einen aktuellen Browser mit JavaScript und Web Crypto. GitHub Pages liefert sie über HTTPS. Ein lokaler HTTP-Vorschau-Server außerhalb von `localhost` kann Web Crypto blockieren; das ist kein Hinweis auf ein falsches Passwort.

Dies ist die fertige Veröffentlichungsdatei. Text- oder Designänderungen werden am bearbeitbaren Original vorgenommen und anschließend erneut verschlüsselt. Zum Aktualisieren die neue `docs/index.html` ersetzen und committen; das bestehende Passwort bleibt erhalten, sofern nicht ausdrücklich geändert.

## Google und Suchmaschinen

Sowohl die sichtbare Passwortseite als auch der entschlüsselte Portfolio-Inhalt enthalten statische Meta-Angaben für `robots` und `googlebot`: `noindex, nofollow, nosnippet, noimageindex`.

Google soll die URL abrufen dürfen, um `noindex` lesen zu können. Deshalb enthält dieses Paket bewusst keine `robots.txt` mit Crawl-Sperre. Eine solche Sperre könnte verhindern, dass Google die `noindex`-Angabe erkennt. Bei einer Projekt-URL würde eine Datei unter `/REPOSITORY/robots.txt` ohnehin nicht als Robots-Datei der Domain gelten.

Nur `docs` wird veröffentlicht. Anleitung, offene Portfolio-Quelldateien, Lebenslauf-PDF und Passwort gehören nicht in diesen Ordner. Das Paket enthält dort ausschließlich die verschlüsselte Website und `.nojekyll`.

`noindex` ist eine Anweisung an kooperierende Suchmaschinen, keine Zugangskontrolle. GitHub Pages bietet in diesem Aufbau keinen serverseitigen Passwortschutz. Der Inhalt bleibt bis zur lokalen Entschlüsselung unlesbar; eine absolute Garantie, dass kein Dienst die URL erfasst, gibt es bei einem öffentlich erreichbaren Endpunkt nicht. Für eine strikt nicht öffentlich erreichbare Seite ist Hosting mit vorgeschalteter Authentifizierung nötig.

Falls eine eigene Domain bereits eine `robots.txt` besitzt, darf diese die Portfolio-Seite nicht blockieren, wenn Google deren `noindex` lesen soll. Für eine schon früher indexierte URL kann zusätzlich eine Entfernung über Google Search Console nötig sein.

## Referenzen

- GitHub Pages erstellen: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- Veröffentlichungsquelle konfigurieren: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- Google: Indexierung mit noindex blockieren: https://developers.google.com/search/docs/crawling-indexing/block-indexing?hl=de
