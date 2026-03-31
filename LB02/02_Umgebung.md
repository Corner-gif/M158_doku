# Umgebung

## Ubuntu VM installieren
![help](../Screenshot/umgebung2.png)
Musste die installation mehrfach neu starten. Fehler konnte ich nicht bestimmen.

## SSH Einrichten
Befehl: ssh admin@127.0.0.1 -p 2223

OpenSSH installieren:
```
sudo apt install openssh-server
sudo systemctl start ssh
sudo systemctl status ssh
```
