# Tp-Cisco-Dhcp-Nat
Projet TSSR : automatisation réseau avec DHCP Relay et accès Internet via NAT (PAT) sur infrastructure Cisco.

# Automatisation réseau Cisco – VLAN, DHCP Relay & NAT

## Contexte
Dans le cadre de ma formation TSSR, j’ai réalisé un projet d’évolution d’une infrastructure réseau existante.  
Suite à une première mise en place de segmentation réseau (VLAN), l’objectif était d’automatiser la configuration des postes et de permettre un accès à un réseau externe simulé.

---

## Objectifs
- Maintenir une segmentation réseau avec VLAN
- Automatiser l’attribution des adresses IP (DHCP)
- Mettre en place un relais DHCP
- Permettre l’accès à un réseau externe via NAT (PAT)
- Appliquer des règles de sécurité réseau

---

## Plan d’adressage

| VLAN | Nom    | Réseau            |
|------|--------|------------------|
| 10   | ADMIN  | 192.168.10.0/24  |
| 20   | TECH   | 192.168.20.0/24  |
| 30   | GUEST  | 192.168.30.0/24  |

Réseau DHCP : 192.168.40.0/24  
Réseau externe : 200.0.0.0/24  

---

## Architecture réseau

![Visio](schema/Schema.png)
![Topologie](schema/topologie-v2.png)

---

## Réalisation

### 🔹 VLAN & Routage
- Création des VLAN
- Configuration du trunk 802.1Q
- Routage inter-VLAN

📸 **Preuve VLAN**
![VLAN](preuves/vlan.png)

📸 **Preuve Trunk**
![Trunk](preuves/trunk.png)

---

### 🔹 DHCP Relay

Un serveur DHCP centralisé (192.168.40.40) a été mis en place afin d’automatiser l’attribution des adresses IP pour les différents VLAN.

Le routeur assure le relais DHCP via `ip helper-address` sur :
- G0/0.10
- G0/0.20
- G0/0.30

L’interface G0/1 (192.168.40.1) permet la communication avec le serveur.

**Preuve configuration relay**
![DHCP Relay](preuves/dhcp-relay.png)

**Preuve attribution IP**
![DHCP](preuves/dhcp-pool.png)
![DHCP](preuves/dhcp-pc-admin.png)
![DHCP](preuves/dhcp-pc-tech.png)
![DHCP](preuves/dhcp-pc-invite.png)
---

### 🔹 NAT (PAT)

Le NAT (PAT) permet aux VLAN d’accéder au réseau externe.

- Interfaces internes : `ip nat inside`
- Interface externe : `ip nat outside`
- ACL : réseaux autorisés
- NAT overload configuré

**Preuve NAT**
![NAT](preuves/nat.png)

📸 **Preuve accès Internet**
![Ping Internet](preuves/ping-internet.png)

---

### 🔹 Sécurité

- ACL mise en place
- Blocage VLAN GUEST → ADMIN

**Preuve blocage**
![ACL](preuves/ping-bloque.png)

---

## Tests

Attribution IP automatique  
Communication inter-VLAN  
Accès réseau externe  
Blocage respecté  

---

## Résultats

- Réseau automatisé via DHCP 
- Accès externe via NAT 
- Sécurité fonctionnelle  

---

## Compétences

- VLAN
- Routage inter-VLAN
- DHCP Relay
- NAT (PAT)
- ACL Cisco
- Diagnostic réseau
