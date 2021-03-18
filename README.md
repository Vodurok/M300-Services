# M300-Services
Dokumentation

GitHub Toolumgebung: https://github.com/mc-b/M300/tree/master/10-Toolumgebung
	Ich habe eine VM normal erstellt und dannach eine mit Vagrant.
    Von denn Anleitungen hab ich einfach die Links kopiert da mir das reicht.

Mehr Dokumente: https://github.com/mc-b/M300/tree/master/20-Infrastruktur
	Ich habe jetzt noch eine VM von der Vagrant Cloud gedownloadet und dannach in VirtualBox eingefügt.
	
  | Befehl                         | Beschreibung																										|
  |--------------------------------|--------------------------------------------------------------------------------------------------------------------|
  |vagrant init				   	   | Initialisiert im aktuellen Verzeichnis eine Vagrant-Umgebung und erstellt, falls nicht vorhanden, ein Vagrantfile  |
  |vagrant up					   | Erzeugt und Konfiguriert eine neue Virtuelle Maschine, basierend auf dem Vagrantfile                               |
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
  
  
  
  
  
  
  
## Dokumentation VM per vagrant Cloud downloaden


Als erstes geht man am besten in das verzeichnis in dem dann auch später die VM erstellt werden soll.
Bei mir wäre das in Vagrant\VagrantCloud

Wenn man dann im Verzeichnis ist gibt man "vagrant cloud" ein und sobald man dann drin ist kann man
mit "vagrant cloud search "begriff"" z.b nach einem Betriebssystem suchen.

Sobald man eine Box in der Cloud gefunden kann man mit dem befehl "vagrant box add "name der box" diese herunterladen
in das Verzeinis in dem man sich befindet. Mann muss dann noch schauen das man das richtige file runterläd da es welche für Hyper-V oder Virtualbox.

Nach dem ich ich dann eine Windows VM gedownloadet habe ich die VM mit "vagrant up" gestartet.



## Sicherheit

`Vagrant.configure("2") do |config|
`config.vm.box = "ubuntu/xenial64"

`config.vm.provision "shell", inline: <<-SHELL
	`sudo apt-get update
	`sudo apt-get apache2 -y
	`sudo apt-get install ufw -y
	`sudo ufw --force enable
	`sudo ufw default deny incoming
	`sudo ufw default allow outgoing
	`sudo ufw allow ssh
	`cat <<%EOF% >> sudo ~/.ssh/authorized_keys	
`ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDN3aIoD9DN41boSgeF0B/9G/CaPIwMmusvbJNUVFXVGcOW14a65R6ZPABQ0XTOM7rItd5neHL871Hd4g8MZRD07FOVeiHS8i2toC3k+R/KMFrmWEM3wLD/GfZl6YVib42ZVBOS1ATmDlFOxXDYrlClpJ57Y3lRSTSz/cMP2UUAwiU+tSGCpka0Ckd7hEJrihQ6e9WnJ5/e8UYymTUx1YCfGROGNIsZ+uanJ4OPCm2JREGs921CcMsHNsz3ZmzVIrv0Tklw1gamJXrNpjyC24em2h8kubx27hoIqzkPJiC90K1jH5jCbF9HrS+/+QwSEzd0zJQCBd/JjBS3eQwY03eb julian@DESKTOP-8FJB16I
`%EOF%
  `sudo service apache2 stop #Stop Apache2 um Port freizugeben für nginx
  `sudo apt-get install nginx -y #nginx installation
  `sudo unlink /etc/nginx/sites-enabled/default #virtueller host deaktivieren
  `cd etc/nginx/sites-available/ #In das Verzeichnis wechseln
  `sudo cat >> reverse-proxy.conf << EOF #Reverse-proxy config file beschreiben
    `server {
    `listen 80;
    `location / {
        `proxy_pass http:Die IP von deinem apache server;
    `}
`}
`EOF
`
`%EOF%
` sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf #Verknüpfung zur Datei erstellen
`%EOF%
`
`sudo groupadd SMP
`sudo useradd steve -G SMP -m
`sudo chpasswd <<<steve:1234
`
`sudo groupadd manberg
`sudo useradd phil -G manberg -m
`sudo chpasswd <<<phil:1234
`
`sudo groupadd eggpire
`sudo useradd bad -G eggpire -m
`sudo chpasswd <<<bad:1234
`
`sudo touch smp.txt
`sudo touch manberg.txt
`sudo touch eggpire.txt
`
`sudo chgrp SMP smp.txt
`sudo chgrp manberg manberg.txt
`sudo chgrp eggpire eggpire.txt
`
`sudo chown steve smp.txt
`sudo chown phil manberg.txt
`sudo chown bad eggpire.txt
`
`SHELL
`end
  
 Das ist mein ganzes vagrant file was ich benutzt habe für diese aufgabe. 