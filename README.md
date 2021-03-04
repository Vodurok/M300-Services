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


  
  
  