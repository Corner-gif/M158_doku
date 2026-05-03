# Testcases CRM Migration

## Testing

1. **Lokale DNS-Auflösung**  
   Befehl: `ping crmserver.sample.ch`  
    Erwartet: Antwort von 10.0.2.15  
    Ergebniss: Erfolgreich<br>
    ![help](../Screenshot/dnstest.png)
2. **Zweite Domain**  
   Befehl: `ping crm-soll.sample.ch`  
   Erwartet: Antwort von 10.0.2.15  
   Ergebniss: Erfolgreich<br>
   ![help](../Screenshot/dnstest2.png)

3. **DNS extern**  
   Befehl: `nslookup crmserver.sample.ch`  
   Erwartet: Domain wird auf 10.0.2.15 aufgelöst
   Ergebniss: Erfolgreich
   ![help](../Screenshot/nxtest.png)


4. **Webserver HTTP**  
   Befehl: `curl -I http://crmserver.sample.ch`  
   Erwartet: HTTP 200 / 301 / 302 
   Ergebniss: Erfolgreich
   ![help](../Screenshot/httptest.png)

5. **Webserver HTTPS**  
   Befehl: `curl -I https://crmserver.sample.ch`  
   Erwartet: Fehler, da kein HTTPS konfiguriert ist  
   Ergebniss: Fehlschlag
   ![help](../Screenshot/httpsfehlertest.png)

6. **Website erreichbar**  
   URL: http://127.0.0.1/vtigercrm/index.php 
   Erwartet: Erreichbar
   ![test](../Screenshot/webertest.png)

7. **PHP Version**  
   Befehl: `php -v`  
   Erwartet: version 8.3.6
   Ergebniss: Version 8.3.6
   ![help](../Screenshot/phpvertest.png)

8. **PHP Module**  
   Befehl: `php -m`  
   Erwartet: mysqli, curl vorhanden  
   Ergebniss: Vorhanden
   ![help](../Screenshot/msqlicurlvortest.png)

9. **DB läuft**  
   Befehl: `systemctl status mariadb`  
   Erwartet: active (running)  
   Ergebniss: Läuft
   ![help](../Screenshot/mariadbläuttest.png)

10. **DB Login**  
    Befehl: `mysql -u <user> -p`  
    Erwartet: Login erfolgreich  
    Ergebniss: Erfolgreich
    ![help](../Screenshot/dblogintest.png)
11. **Tabellenanzahl**  
    SQL: `SELECT COUNT(*) FROM information_schema.tables WHERE table_schema='<db>';`  
    Erwartet: gleiche Anzahl wie vorher  

    Ergebnis Datenvergleich

    Die wichtigsten migrierten Geschäftsdaten wurden verglichen.

    | Tabelle | Altsystem | Zielsystem |
    |---|---:|---:|
    | vtiger_account | 703 | 703 |
    | vtiger_contactdetails | 379 | 379 |
    | vtiger_potential | 600 | 600 |
    | vtiger_users | 3 | 1 |
    | vtiger_products | 40 | 0 |
    | vtiger_crmentity | 2414 | 2282 |

    Die Abweichungen entstehen, weil die Migration über den Vtiger-Import durchgeführt wurde und nicht über einen vollständigen Datenbank-Dump. Dabei wurden primär die ausgewählten CRM-Module importiert.
  

13. **CRM Login**  
    Vorgehen: Login im Browser  
    Erwartet: Dashboard sichtbar  
    Ergebnis: Login geht
    ![help](../Screenshot/logintest.png)

14. **Daten anzeigen**  
    Vorgehen: Kontakt öffnen  
    Erwartet: Daten korrekt sichtbar  

15. **Datensatz erstellen**  
    Vorgehen: neuen Kontakt erstellen  
    Erwartet: gespeichert  

16. **Datensatz bearbeiten**  
    Vorgehen: Kontakt ändern  
    Erwartet: Änderung gespeichert  

17. **SFTP Zugriff**  
    Befehl: `sftp user@crmserver.sample.ch`  
    Erwartet: Login möglich  

18. **Backup erstellen**  
    Befehl: `mysqldump -u user -p db > backup.sql`  
    Erwartet: Datei erstellt  

19. **Backup Restore**  
    Befehl: `mysql -u user -p testdb < backup.sql`  
    Erwartet: Import erfolgreich  

20. **DB Zugriffsschutz**  
    Befehl: `mysql -u falscherUser -p`  
    Erwartet: Access denied  


## Auftrag #13 – Monitoring

21. **Webserver Monitoring**  
    Erwartet: Status OK im Monitoring  

22. **DB Monitoring**  
    Erwartet: Status OK  

23. **Fehler erkennen**  
    Befehl: `systemctl stop apache2`  
    Erwartet: Fehler erkannt  

24. **Alarm-Mail**  
    Aktion: Webserver stoppen  
    Erwartet: Mail wird gesendet  

25. **Auto-Restart**  
    Befehl: `systemctl stop apache2`  
    Erwartet: Service startet neu  