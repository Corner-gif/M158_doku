# Testcases CRM Migration

## Testing

1. **Lokale DNS-Auflösung**  
   Befehl: `ping crmserver.sample.ch`  
    Erwartet: Antwort von 10.0.2.15  
    Ergebniss:<br>
    ![help](../Screenshot/dnstest.png)
2. **Zweite Domain**  
   Befehl: `ping crm-soll.sample.ch`  
   Erwartet: Antwort von 10.0.2.15  
   Ergebniss:<br>
   ![help](../Screenshot/dnstest2.png)

3. **DNS extern**  
   Befehl: `nslookup crmserver.sample.ch`  
   Erwartet: NXDOMAIN  

4. **Webserver HTTP**  
   Befehl: `curl -I http://crmserver.sample.ch`  
   Erwartet: HTTP 200 / 301 / 302  

5. **Webserver HTTPS**  
   Befehl: `curl -I https://crmserver.sample.ch`  
   Erwartet: HTTP 200 / 301 / 302  

6. **HTTP → HTTPS Redirect**  
   Befehl: `curl -I http://crmserver.sample.ch`  
   Erwartet: 301 / 302 Redirect  

7. **PHP Version**  
   Befehl: `php -v`  
   Erwartet: Version wird angezeigt  

8. **PHP Module**  
   Befehl: `php -m`  
   Erwartet: mysqli, curl vorhanden  

9. **DB läuft**  
   Befehl: `systemctl status mariadb`  
   Erwartet: active (running)  

10. **DB Login**  
    Befehl: `mysql -u <user> -p`  
    Erwartet: Login erfolgreich  

11. **Tabellenanzahl**  
    SQL: `SELECT COUNT(*) FROM information_schema.tables WHERE table_schema='<db>';`  
    Erwartet: gleiche Anzahl wie vorher  

12. **Benutzerdaten**  
    SQL: `SELECT COUNT(*) FROM vtiger_users;`  
    Erwartet: gleiche Anzahl  

13. **CRM Login**  
    Vorgehen: Login im Browser  
    Erwartet: Dashboard sichtbar  

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