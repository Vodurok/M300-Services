# M300-Services
Dokumentation

GitHub Toolumgebung: https://github.com/mc-b/M300/tree/master/10-Toolumgebung
	#Ich habe eine VM normal erstellt und dannach eine mit Vagrant.
    #Von denn Anleitungen hab ich einfach die Links kopiert da mir das reicht.

Mehr Dokumente: https://github.com/mc-b/M300/tree/master/20-Infrastruktur
	#Ich habe jetzt noch eine VM von der Vagrant Cloud gedownloadet und dannach in VirtualBox eingefügt.
	
#	Befehl							Beschreibung
	vagrant init					Initialisiert im aktuellen Verzeichnis eine Vagrant-Umgebung und erstellt, falls nicht vorhanden, ein Vagrantfile
	vagrant up						Erzeugt und Konfiguriert eine neue Virtuelle Maschine, basierend auf dem Vagrantfile
	vagrant ssh						Baut eine SSH-Verbindung zur gewünschten VM auf
	vagrant status					Zeigt den aktuellen Status der VM an
	vagrant port					Zeigt die Weitergeleiteten Ports der VM an
	vagrant halt					Stoppt die laufende Virtuelle Maschine
	vagrant destroy					Stoppt die Virtuelle Maschine und zerstört sie.