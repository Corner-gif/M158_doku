# Planung
## Projektplan
Im Rahmen dieses Projekts wird das bestehende Vtiger CRM-System, das aktuell auf einem CentOS 6.6 Server mit MySQL-Datenbank betrieben wird, auf eine moderne und unterstützte Systemumgebung migriert.

**Ist**
* System: Vtiger CRM
* Betriebssystem: CentOS 6.6
```
[root@crmserver ~]# cat /etc/redhat-release
CentOS release 6.6 (Final)
```
* Datenbank: MySQL 14.14 Distrib 5.1.73
```
[root@crmserver ~]# sudo mysql --version
mysql  Ver 14.14 Distrib 5.1.73, for redhat-linux-gnu (x86_64) using readline 5.1
```
* Webserver: Apache/2.2.15 (Unix)
```
[root@crmserver ~]# sudo httpd -v
Server version: Apache/2.2.15 (Unix)
Server built:   Oct 16 2014 14:48:21
```
* Server: crmserver.sample.ch
* System läuft on-prem als VM
* CentOS 6.6 ist veraltet / nicht mehr unterstützt


**Soll**

* System: Vtiger CRM V9  
Aktuelle Version mit besserer Sicherheit und Unterstützung moderner Systeme.

* Betriebssystem: Ubuntu Server 24.04 LTS  
Wird bis 2029 unterstützt und ist sicherer und aktueller als CentOS 6.6.

* Datenbank: MariaDB 10.6  
Stabile Version und kompatibel mit MySQL, daher gut für Vtiger geeignet.

* Webserver: Apache 2.4  
Aktuell, sicher und gut mit PHP und Vtiger kompatibel.

* PHP: PHP 8.3.6  
Neue Version mit besserer Performance und Sicherheit.
**Diagramm**
![help](../Screenshot/planungdiagramm.png)

| Komponente | IST | SOLL |
|-----------|-----|------|
| OS | CentOS 6.6 | Ubuntu 24.04 |
| DB | MySQL 5.1 | MariaDB 10.6 |
| Webserver | Apache 2.2 | Apache 2.4 |
| PHP | alt | PHP 8.3 |


### Risiken

- Datenverlust bei Migration
- Inkompatibilität zwischen alter und neuer Vtiger-Version
- Ausfallzeit während Migration
- Fehler beim Import der Daten

### Schutz

- Vollständiges Backup vor Migration
- Testmigration in separater VM
- Vergleich der Daten nach Migration
- Durchführung ausserhalb der Geschäftszeiten

**MySQL**:
Bestehende Datenbanken:<br>
* mysql
* test
* vtigercrm
* information_schema
```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| test               |
| vtigercrm          |
+--------------------+
```

Bestehende User:
vtigercrm: 
```
mysql> SELECT user_name, user_password, email1 FROM vtiger_users;

+-----------+------------------------------------+--------------------+
| user_name | user_password                      | email1             |
+-----------+------------------------------------+--------------------+
| admin     | $1$ad000000$r3hzdtsdvtvXX9nD2w4yb0 | hans@sample.com    |
| sepp      | $1$se000000$KRn9kiYxE/S641n24kfbA/ | sepp@sample.com    |
| chantal   | $1$ch000000$9NT/kT3TKqF3tDE0w.YTz1 | chantal@sample.com |
+-----------+------------------------------------+--------------------+
```

### Zeitplan
![help](../Screenshot/Zeitplan.png)

## Vtiger
![help](../Screenshot/vtigerweb.png)


### Migrationsstrategie

Die Migration erfolgt über den Vtiger-Import.

Vorgehen:
1. Installation des neuen Systems
2. Einrichtung der Datenbank
3. Import der CRM-Daten über Vtiger
4. Überprüfung der Datenintegrität

Begründung:
Der Import über Vtiger ist kompatibler bei Versionswechseln als ein direkter Datenbank-Dump.

## Kostenvoranschlag

| Position               | Aufwand | Preis/h | Total |
|-----------------------|--------:|--------:|------:|
| Analyse IST-System    | 4h      | 120 CHF | 480 CHF |
| Planung               | 4h      | 120 CHF | 480 CHF |
| Aufbau Zielsystem     | 8h      | 120 CHF | 720 CHF |
| Migration Daten       | 6h      | 120 CHF | 720 CHF |
| Testing               | 4h      | 120 CHF | 480 CHF |
| Dokumentation         | 5h      | 120 CHF | 600 CHF |
| **Total**             | **31h** |         | **3480 CHF** |