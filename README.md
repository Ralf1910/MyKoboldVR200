# Vorwerk Kobold VR200 Modul
Das Modul fragt �ber die Wunderground API Wetterdaten ab.  
Daf�r ist eine Registrierung auf www.wunderground.com n�tig, um einen API-Key zu erhalten.  
Es k�nnen aktuelle Daten, Unwetterwarnungen, sowie st�ndliche als auch 12-st�ndliche Vorhersagen abgefragt werden.  

### Inhaltverzeichnis

1. [Funktionsumfang](#1-funktionsumfang)
2. [Voraussetzungen](#2-voraussetzungen)
3. [Software-Installation](#3-software-installation)
4. [Einrichten der Instanzen in IP-Symcon](#4-einrichten-der-instanzen-in-ip-symcon)
5. [Statusvariablen und Profile](#5-statusvariablen-und-profile)
6. [WebFront](#6-webfront)
7. [PHP-Befehlsreferenz](#7-php-befehlsreferenz)

### 1. Funktionsumfang

* De-/Aktivierbare Abfrage von gew�nschten Wetterdaten.
* Einstellbarkeit der Menge der Unwetter, st�ndlichen und 12-st�ndlichen Daten.
* Timer f�r automatische Aktualisierung der Daten.

### 2. Voraussetzungen

- IP-Symcon ab Version 4.x

### 3. Software-Installation

�ber das Modul-Control folgende URL hinzuf�gen.  
`git://github.com/paresy/SymconMisc.git`  

### 4. Einrichten der Instanzen in IP-Symcon

- Unter "Instanz hinzuf�gen" ist das 'WundergroundWeather'-Modul unter dem Hersteller '(Sonstige)' aufgef�hrt.  

__Konfigurationsseite__:

Name                              | Beschreibung
--------------------------------- | ---------------------------------
Standort                          | Standort, von dem die Daten entnommen werden sollen. Ob ein Standort verf�gbar ist, kann auf der www.wunderground.com Seite ausprobiert werden. Sollte ein Standort nicht vorhanden sein, sollte ein n�chstgelegener gr��erer Ort gew�hlt werden.
Land                              | Hier muss das Land eingetragen werden.
API Key                           | Wunderground API-Key. Kann auf der Wunderground Homepage nach Registrierung angefordert werden. "More"->"Weather API for Developers".
Aktuelle Daten abfragen           | Aktiviert die Abfrage der aktuellen Wetterdaten.
St�ndliche Vorhersage             | Aktiviert die Abfrage der st�ndlichen Vorhersage.
12st�ndliche Vorhersage           | Aktiviert die Abfrage der 12-st�ndlichen Vorhersage.
Unwetterwarnung abfragen          | Aktiviert die Abfrage der Unwetter Vorhersage.
Anzahl Vorhersagen (12-st�ndlich) | Die Anzahl der 12-st�ndlichen Vorhersagen. Maximalwert: 8
Anzahl Vorhersagen (std�ndlich)   | Die Anzahl der st�ndlichen Vorhersagen. Maximalwert: 24
Anzahl Unwetterwarnung            | Die Anzahl der Unwetter Vorhersagen. Maximalwert: 6
Update Wetterdaten                | Setzt den Timer in Minuten, wie oft die Wetterdaten aktualisiert werden sollen. (aktuell/st�ndlich/12-st�ndlich)
Update Unwetterwarnungen          | Setzt den Timer in Minuten, wie oft die Unwetterwarnungen aktualisiert werden sollen.
Button Update Wetter              | Aktualisiert die Wetterdaten (aktuell/st�ndlich/12-st�ndlich). Sofern alle drei Abfragen deaktiviert sind oder der Timer auf 0 gesetzt ist => Timer deaktiviert
Button Update Unwetterwarnungen   | Aktualisiert die Unwetterwarnungen. Sofern die Unwetterwarnungsabfrage deaktiviert oder der Timer auf 0 gesetzt ist => Timer deaktiviert


### 5. Statusvariablen und Profile

Die Statusvariablen/Kategorien werden automatisch angelegt. Das L�schen einzelner kann zu Fehlfunktionen f�hren.

##### Aktuelle Wetterdaten

Name                | Typ     | Beschreibung
------------------- | ------- | ----------------
Luftdruck           | Float   | Angabe in hPa
Luftfeuchtigkeit    | Float   | Angabe in %
Niederschlag/h      | Float   | Angabe in Liter/m�
Niederschlag Tag    | Float   | Angabe in Liter/m�
Sichtweite          | Float   | Angabe in km
Sonnenstrahlung     | Float   | Angabe in W/m�
Temperatur          | Float   | Angabe in �C
Temperatur gef�hlt  | Float   | Angabe in �C
Temperatur Taupunkt | Float   | Angabe in �C
UV Strahlung        | Integer | Informationen: [UVIndex Erkl�rung](https://www.wunderground.com/resources/health/uvindex.asp)
Windb�e             | Float   | Angabe in km/h
Windgeschwindigkeit | Float   | Angabe in km/h
Windrichtung        | Float   | Angabe in Himmelsrichtungen

##### St�ndliche Vorhersage
Die Variablen werden mit 1..24h gekennzeichnet. (1 = Vorhersage n�chste volle Stunde; 24 = Vorhersage der 24ten vollen Stunde)

Name                | Typ     | Beschreibung
------------------- | ------- | ----------------
Gegebenheit         | String  | Beschreibt das Wetter z.B. "Bedeckt", "Regen m�glich"
Luftfeuchtigkeit    | Float   | Angabe in %
Luftdruck           | Float   | Angabe in hPa
Regenmenge          | Float   | Angabe in Liter/m�
Temperatur          | Float   | Angabe in �C
Wolkendecke         | Integer | Angabe in %
Windgeschwindigkeit | Float   | Angabe in km/h

##### 12-st�ndliche Vorhersage
Die Variablen werden mit 12, 24..96h gekennzeichnet (12 = Vorhersage in 12 Stunden; 96 = Vorhersage in 96 Stunden)

Name             | Typ   | Beschreibung
---------------- | ----- | ----------------
H�chsttemperatur | Float | Angabe in �C
Tiefsttemperatur | Float | Angabe in �C

##### Unwetterwarnung

Name         | Typ     | Beschreibung
------------ | ------- | ----------------
Beschreibung | String  | Beschreibt die Warnung mit m�glichen weiteren Informationen wie z. B. Windgeschwindigkeiten oder Regenmengen.
Datum        | Integer | Angabe in UnixTimeStamp. Datum wann die Warnung ausgesprochen wurde.
Name         | String  | Ausgeschriebener Typ. z.B. Gewitter
Typ          | String  | 3-Buchstabenk�rzel f�r die Warnung ([�bersicht](https://www.wunderground.com/weather/api/d/docs?d=data/alerts))

##### Profile:

Name             | Typ
---------------- | -------
WGW.Rainfall     | Float
WGW.Sunray       | Float
WGW.Visibility   | Float
WGW.WindSpeedkmh | Float
WGW.UVIndex      | Integer

### 6. WebFront

�ber das WebFront werden die Variablen angezeigt. Es ist keine weitere Steuerung oder gesonderte Darstellung integriert.

### 7. PHP-Befehlsreferenz

`boolean WGW_UpdateWeatherData(integer $InstanzID);`  
Aktualisiert die Wetterdaten (aktuell/st�ndlich/12-st�ndlich) des Weathergroundmoduls mit der InstanzID $InstanzID.  
Die Funktion liefert keinerlei R�ckgabewert.  
Beispiel:  
`WGW_UpdateWeatherData(12345);`

`boolean WGW_UpdateStormWarningData(integer $InstanzID);`  
Aktualisiert die Unwetterwarnungen des Weathergroundmoduls mit der InstanzID $InstanzID.  
Die Funktion liefert keinerlei R�ckgabewert.  
Beispiel:  
`WGW_UpdateStormWarningData(12345);`
