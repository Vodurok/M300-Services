# M300-Services

# Dokumentation

GitHub Toolumgebung: https://github.com/mc-b/M300/tree/master/10-Toolumgebung
	Ich habe eine VM normal erstellt und dannach eine mit Vagrant.
    Von denn Anleitungen hab ich einfach die Links kopiert da mir das reicht.

Mehr Dokumente: https://github.com/mc-b/M300/tree/master/20-Infrastruktur
	Ich habe jetzt noch eine VM von der Vagrant Cloud gedownloadet und dannach in VirtualBox eingefügt.
	
  | Befehl                         | Beschreibung																										|
  |--------------------------------|--------------------------------------------------------------------------------------------------------------------|
  |vagrant init				   	   |Initialisiert im aktuellen Verzeichnis eine Vagrant-Umgebung und erstellt, falls nicht vorhanden, ein Vagrantfile   |
  |vagrant up					   |Erzeugt und Konfiguriert eine neue Virtuelle Maschine, basierend auf dem Vagrantfile                                |
  |vagrant ssh					   |Baut eine SSH-Verbindung zur gewünschten VM auf                                                                     |
  |vagrant status				   |Zeigt den aktuellen Status der VM an                                                                                |
  |vagrant port					   |Zeigt die Weitergeleiteten Ports der VM an                                                                          |
  |vagrant halt					   |Stoppt die laufende Virtuelle Maschine                                                                              |
  |vagrant destroy				   |Stoppt die Virtuelle Maschine und zerstört sie.                                                                     |
  |vagrant cloud                   |Cloud Speicher von Vagrant mit verschiedenen VMs																	|
  |vagrant cloud search "begriff"  |Damit sucht man in der Cloud z.b nach einem Betriebssystem															|
  |vagrant box add "box name"	   |Damit kann man in der Vagrant Cloud eine Box runterladen und zwar in dem Verzeichnis wo man drin ist				|
  |Git add "file"/ -A			   |Damit werden Datein ausgewählt die hoch geladen werden sollen.                                                      |
  |Git status                      |Zeigt die Datein an von dem Ordner der mit GitHub geteilt worden ist.                                               |
  |Git commit -m "comment"		   |Bestätigung welche datein hochgeladen werden sollen und man kann einen Kommentar abgeben was sich geändert hat      |
  |Git push                        |Läd die Datein dann auf GitHub hoch                                                                                 |
  |Git pull "url"                  |Damit wird das GitHub Reposetory in denn Ordner runtergeladen                                                       |
  |docker run 					   |Das ist der befehl zum starten von einem Container																	|
  |docker ps					   |Überblick über alle aktuellen Container																				|
  |docker ps -a					   |Aktive und beendete Container anzeigen																				|
  |docker images/docker images ls  |Gibt eine liste von allen Lokalen Images aus 																		|
  |docker rm					   |Entfernt einen oder mehrere Container																				|
  |docker rmi					   |löscht ein oder mehrere Images																						|
  |docker start					   |Kann zum neustarten oder zum erstmalligen starten benutzt werden													|
  |docker stop					   |Kann einen oder mehrere Container stopen																			|
  |docker kill 					   |Beendet sofort einen Container																						|
  |docker logs					   |Gibt logs über einen bestimten Container aus																		|
  |docker inspect				   |Gibt alle Wichtigen informationen eines Containers aus wie Netzwerk einstellung und wie er Konfiguriert wurde		|
  |docker diff					   |Gibt an was es alles für änderungen an diesem Container gibt im gegensatz vom ursprungs Image						|
  |docker top					   |Gibt informationen aus zu allen laufenden Prozessen inerhalb eines Containers										|
  |docker build -t (name) .		   |Startet Docker von einem Dockerfile																					|
  |kubectl create				   |Erzeugt einen pod mit dem image was ausgewählt worden ist															|
  |kubectl expose				   |(folgt)																												|
  |kubectl run "image"			   |startet ein bestimmtes image in einem Container und legt es in einen pod											|
  |kubectl set 					   |Dient zum updaten und bearbeiten von vorhandenen images etc.														|
  |kubectl explain 				   |Beschreibung und Details von .yaml files																			|
  |kubectl get                     |Macht eine Liste mit denn wichtigsten informationen einer resource welche dann mit --selector definieren kann		|
  |kubectl edit 				   |Mann kann direkt eine resource in der command zeile bearbeiten													    |
  |kubectl delete				   |Damit werden vorhandene Pots gelöscht mit denn Daten																|
  |kubectl						   |Zeigt alle Befehle an die es bei Kubectl gibt																		|
  
## Kubernetes

Da Kubernetes mitler weiler das aktuellste auf dem Markt ist und somit Docker ziemlich ersetzt hat habe ich mich in LB02 nur eigentlich auf Kubernetes
konzentriert. Meine erfahrungen waren sehr positiv und es viel mir auf jeden fall einfacher als mit docker zu arbeiten.
Kubernetes ist ein Open-Source programm und dient zu bereitstellung und verwaltung von Container-Anwendungen. Bei Kubernetes werden verschiedene Container-Lösungen
unterstützt wie z.b Docker. Da es oft darum geht das zwei Container miteinander arbeiten müssen werdene diese unter Kubernetes in sogennanten Pods erstellt wodurch sie
miteinander komunizieren können. Mit Services kann man dann von auserhalb auf die Container zugreifen um so mit diesen zu arbeiten.


## Massnahmen zur Container-Sicherheit
- Least Privilege
- Ressourcen begrenzung
- Container absichern

## Mögliche Angriffe
- Kernel Exploit
- Container Breakouts
- manipulierte Images

----------------------------------------------------------------LB01-----------------------------------------------------------------------------------------  
  
## Dokumentation VM per vagrant Cloud downloaden


Als erstes geht man am besten in das verzeichnis in dem dann auch später die VM erstellt werden soll.
Bei mir wäre das in Vagrant\VagrantCloud

Wenn man dann im Verzeichnis ist gibt man "vagrant cloud" ein und sobald man dann drin ist kann man
mit "vagrant cloud search "begriff"" z.b nach einem Betriebssystem suchen.

Sobald man eine Box in der Cloud gefunden kann man mit dem befehl "vagrant box add "name der box" diese herunterladen
in das Verzeinis in dem man sich befindet. Mann muss dann noch schauen das man das richtige file runterläd da es welche für Hyper-V oder Virtualbox.

Nach dem ich ich dann eine Windows VM gedownloadet habe ich die VM mit "vagrant up" gestartet.



## Sicherheit

### Die Befehle für die Firewall, SSH-Key, Proxy

```config.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get apache2 -y
sudo apt-get install ufw -y
sudo ufw --force enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
cat <<%EOF% >> sudo ~/.ssh/authorized_keys
dein SSH-Key
%EOF%
sudo service apache2 stop #Stop Apache2 um Port freizugeben für nginx
sudo apt-get install nginx -y #nginx installation
sudo unlink /etc/nginx/sites-enabled/default #virtueller host deaktivieren
cd etc/nginx/sites-available/ #In das Verzeichnis wechseln
sudo cat >> reverse-proxy.conf << EOF #Reverse-proxy config file beschreiben
server {
listen 80;
location / {
proxy_pass http:// apache2 ip adresse
}
}
EOF

%EOF%
sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf #Verknüpfung zur Datei erstellen
%EOF%
```
### User und Gruppen hinzufügen

```sudo groupadd SMP
sudo useradd steve -G SMP -m
sudo chpasswd <<<steve:----

sudo groupadd manberg
sudo useradd phil -G manberg -m
sudo chpasswd <<<phil:----

sudo groupadd eggpire
sudo useradd bad -G eggpire -m
sudo chpasswd <<<bad:----

sudo touch smp.txt
sudo touch manberg.txt
sudo touch eggpire.txt

sudo chgrp SMP smp.txt
sudo chgrp manberg manberg.txt
sudo chgrp eggpire eggpire.txt

sudo chown steve smp.txt
sudo chown phil manberg.txt
sudo chown bad eggpire.txt
```