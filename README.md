# 17-BE-Extra-03-Render

## Render.com hosting guide

1. Erstelle neuen Account auf [Render.com](https://render.com)

2. Klicke auf "New" und wähle "Web Service".

3. Wähle dein Repository und gewähre Render.com die Berechtigung, auf dein Repository zuzugreifen.

4. Wähle das entsprechende Repository aus der Liste aus, das du für das Hosting verwenden möchtest.

5. Name: Gib deinem Service einen Namen (z.B. "Mongoose Express Backend"). Wichtig: Der Name wird in der URL verwendet.

6. Branch: Wähle den Git-Branch, der deployed werden soll (normalerweise main oder master).

7. Build Command: Gib das Build-Kommando ein, das zur Installation der Abhängigkeiten und zum Starten des Projekts benötigt wird. Normalerweise: `npm install`.

8. Start Command: Definiere das Startkommando für deinen Server. Dies kann node oder npm start sein. Beispiel:`node server.js` oder `npm start`(schaue startskript in deinem package.json).

9. Environment: Wähle Node als Umgebung.

10. Region: Wähle die Region, die deiner Zielgruppe am nächsten liegt.

11. Environment Variables festlegen
    * Falls du Umgebungsvariablen (Environment Variables) wie die MongoDB-Verbindungszeichenkette, API-Schlüssel usw. benötigst, kannst du diese in Render.com einrichten.
    1. Klicke auf den Abschnitt Environment.
    2. Füge die benötigten Umgebungsvariablen hinzu. Zum Beispiel:
        * MONGODB_URI: Die MongoDB-URI, die deine Datenbankverbindung darstellt.
        * PORT: Der Port, auf dem dein Server läuft (z.B. 3000).

12. Deployment starten

13. Logs überprüfen

14. Deine App ist jetzt live! Du kannst auf die bereitgestellte URL mit Postman testen.

Note: deine Mongo Datenbank muss auf MongoDB Atlas gehostet werden, um eine Verbindung herzustellen.

## Mit Docker auf render.com hosten

1. Erstelle ein Dockerfile in deinem Projektordner.
   
3. Zuerst benötigst du eine Dockerfile im Stammverzeichnis deines Node.js-Projekts. Hier ist ein Beispiel für eine Dockerfile:
   
```Dockerfile
# 1: Wähle die Node.js-Umgebung
FROM node:18

# 2: Setze das Arbeitsverzeichnis
WORKDIR /app

# 3: Kopiere die package.json und package-lock.json
COPY package*.json ./

# 4: Installiere die Abhängigkeiten
RUN npm install --production

# 5: Kopiere den gesamten Code in das Arbeitsverzeichnis
COPY . .

# 6: Setze die Umgebungsvariable für den Port (Render verwendet automatisch PORT)
ENV PORT=3000

# 7: Exponiere den Port
EXPOSE 3000

# 8: Starte die Node.js-Anwendung
CMD ["npm", "start"]
```

3.(optional) Falls du eine docker-compose.yml verwenden möchtest (z.B. für eine MongoDB-Datenbank), könnte sie so aussehen:

```yml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - MONGODB_URI=mongodb://mongodb:27017/mydb
    depends_on:
      - mongodb
  mongodb:
    image: mongo:5
    ports:
      - "27017:27017"
```

4. neue webservice bei render erstellen
   
6. Wähle als Umgebung (Environment) Docker aus.
   
8. Wähle die Region, die deiner Zielgruppe am nächsten liegt.
   
10. Deployment starten
    
12. Logs überprüfen
