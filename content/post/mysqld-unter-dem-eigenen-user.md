+++
date = "2009-08-01T01:18:44+02:00"
title = "Mysqld unter dem eigenen user"
lang = "de"
description = "Einer der wenigen Dinge die mich am Mac nerven ist die Tatsache, dass viele Programme mit Gewalt am Anfang als Administrator installiert und betrieben werden wollen. Dabei ist dies in vielen Fällen gar nicht nötig. Wer auf dem Mac seine Programme nicht für alle Benutzer installieren will, leg sich einfach einen Applications-Ordner im Benutzerordner an und speichert seine Programme dort. Gleiches gilt für Mysql."
+++

Einer der wenigen Dinge die mich am Mac nerven ist die Tatsache, dass viele Programme mit Gewalt am Anfang als Administrator installiert und betrieben werden wollen. Dabei ist dies in vielen Fällen gar nicht nötig. Wer auf dem Mac seine Programme nicht für alle Benutzer installieren will, leg sich einfach einen Applications-Ordner im Benutzerordner an und speichert seine Programme dort. Der Vorteil liegt darin, dass man sich dann nur um das Sichern des Benutzerordners kümmern muss; die Programme die man nutzt werden mitgesichert. Bei einer Neuinstallation muss ich nur den Benutzerordner wiederherstellen und ich kann weiterarbeiten.

Aber zum eigentlichen Thema: Als Entwickler nutze ich auch MySQL und das Standardverhalten die Daten unter /var/ abzulegen finde ich ein wenig störend, da ich zum Nutzen von MySql Administrationsprivilegien brauche und die Daten aus oben genannten Gründen nicht in meinem Benutzerordner liegen. Man kann MySql allerdings auch recht einfach unter dem eigenen Benutzer starten.


Neben der offensichtlichen Lösung Mysql für den eigenen Benutzerordner zu kompilieren & zu installieren, reicht es auch aus, dem Mysql Programm den Pfad für die Datenbankdateien, die PID File und den Socket als Parameter bzw in der Konfiguration mitzugeben. Vorher muss aber noch im späteren Datenordner die Systemtabellen von Mysql angelegt werden:

```
/usr/local/mysql/scripts/mysql_install_db --datadir=$HOME/Library/MyApp/data --basedir=/usr/local/mysql
```

**Achtung**: Hier wird eine leere Datenbank mit frischen Benutzer installiert, d.h. der root-Benutzer besitzt kein Passwort und ist dementsprechend ungesichert!

Danach kann die Datenbank gestartet werden:

```
/usr/local/mysql/bin/mysqld --socket=/tmp/zeisss-mysql.sock --basedir=/usr/local/mysql --datadir=$HOME/Library/MyApp/data/ --port=3306
```

Wem das ganze zuviel Schreibarbeit ist, kann das das ganze auch einfach eine Konfigurationsdatei anlegen. Welche Dateien von Mysql hierfür ausgelesen werden, findet ihr mit `mysqld –help –verbose` heraus. Aber Achtung: Der mysql-Client liest nicht 100% die selben Dateien aus. Prüft dies also gegebenenfalls, welche für euch die richtige ist. Für mich hat folgendes als `.my.cnf` im Benutzerordner getan:

```
[mysqld]
port=3306
socket=/tmp/zeisss-mysql.sock
basedir=/usr/local/mysql
datadir=/Users/zeisss/Library/MyApp/data
[client]
port=3306
socket=/tmp/zeisss-mysql.sock
```

Zu beachten ist, dass ich auch einen `[client]` Bereich angegeben habe, der vom mysql-Befehl genutzt wird. Beenden kann man die Datenbank nun übrigens wie gehabt z.B. mit `mysqladmin` oder dem MySql Administrator herunterfahren.

Da mir aber auch das zu lästig ist, und die Datenbank ja auch nicht alleine sondern zumeist in Zusammenarbeit mit anderen Diensten wie Apache läuft, sei hier noch kurz auf [Supervisord](http://www.supervisord.org/) verwiesen, mit der man ganze Umgebungen definieren und starten/stoppen kann. Stürzt einer der Dienste mal ab, wird er je nach Konfiguration auch automatisch neu gestartet (aus diesem Grund nutze ich oben auch kein `mysqld_safe`).
