![Hamdy Tabsissi — Sécurité du cloud & Zero Trust](banniere.svg)

# Hamdy Tabsissi

**Systems & Workplace Administrator** — Action contre la Faim
Master Cybersécurité, SUP DE VINCI · Microsoft 365 · Azure · Cloud & Identity

J'exploite une infrastructure personnelle en production depuis août 2026 : un site, trois applications, des sauvegardes chiffrées hors-site et un déploiement continu. Je documente surtout ce qui casse — c'est là qu'on apprend.

### **[→ hamdy-tabsissi.com](https://hamdy-tabsissi.com)**

---

## L'infrastructure

Une VM Oracle ARM (4 OCPU / 24 Go) sous Ubuntu, derrière Cloudflare.

| | |
|---|---|
| **Exposition** | Cloudflare Tunnel. **Aucun port entrant ouvert**, pare-feu restreint aux plages Cloudflare. Administration derrière Cloudflare Access (SSO + JWT vérifié contre le JWKS) |
| **Durcissement** | nginx noté **A+** sur les en-têtes de sécurité · fail2ban · mises à jour automatiques · services systemd contraints (`NoNewPrivileges`) · applications en écoute loopback uniquement |
| **Déploiement** | CI/CD **pull-based** : GitHub Actions valide et déplace un tag, la machine vient le chercher. **Aucun identifiant d'accès à la VM n'existe chez GitHub.** Healthcheck après chaque mise en ligne, rollback automatique et mise en quarantaine du commit fautif |
| **Sauvegardes** | Litestream (réplication SQLite continue) et restic vers Cloudflare R2, chiffrées, hors-site. Restaurations contrôlées par comparaison d'empreintes SHA-256 |
| **Supervision** | Uptime Kuma · moniteur externe indépendant · dead man's switch auto-hébergé |
| **Automatisation** | n8n auto-hébergé : veille de disponibilité, digests programmés, alertes Telegram routées par thème |
| **Conformité** | Matomo auto-hébergé (anonymisation IP, rétention 25 mois) · registre RGPD · SMSI ISO 27001 avec analyse de risques EBIOS RM et Déclaration d'Applicabilité |

---

## Projets

| Projet | Description | Stack |
|---|---|---|
| **[Portfolio](https://hamdy-tabsissi.com)** | Site personnel à accès nominatif : chaque recruteur reçoit un lien qui lui est propre, les consultations sont tracées | Node · Express · node:sqlite · CSS moderne (`@container`, `:has()`, `color-mix()`) |
| **EventMap** *(privé)* | Agrégateur d'événements Paris ↔ Nanterre ↔ Montreuil : une proposition, au bon moment, déjà filtrée | Python · FastAPI · Leaflet · SQLite |
| **Observatory** *(privé)* | Tableau de bord d'état des services, protégé par vérification cryptographique du jeton Cloudflare Access | Python · FastAPI |
| **Mindmap** *(privé)* | Carte mentale fractale à navigation spatiale, canvas 2D sans aucune librairie | JavaScript vanilla |

### Master Cybersécurité — SUP DE VINCI

| Projet | Contenu |
|---|---|
| **[SOC externalisé](https://github.com/flemops/Projet-SOC)** | Conception complète d'un centre opérationnel de sécurité pour un cas client : agents Wazuh, détection Suricata derrière pfSense, tunnel chiffré, chaîne Logstash vers Elasticsearch, alerting, TheHive et Cortex. Conformité ISO/IEC 27001, RGPD et NIS |
| **[SIEM](https://github.com/flemops/Projet-SIEM)** | Centralisation et corrélation de journaux |
| **[Cloud hybride](https://github.com/flemops/Projet-CLoud-Hybrid)** | Architecture mixte on-premise / cloud |
| **[Root-Me](https://github.com/flemops/Projet-Root-Me)** | Analyse et exploitation en environnement contrôlé |

---

## Quatre pannes, quatre leçons

Ce que l'exploitation réelle m'a appris, et que la théorie ne m'avait pas dit.

| L'incident | Ce que j'en ai tiré |
|---|---|
| Un bot Telegram ne recevait plus aucun message. Le service tournait, le réseau répondait, la configuration était juste. **Cloudflare Access renvoyait les serveurs de Telegram vers une page de connexion** : ils recevaient une redirection au lieu de mon application | Un composant qui protège tout protège aussi contre ce qu'on attendait. Il faut savoir **par où entre chaque appelant**, y compris les machines |
| Un script de déploiement écrasait la configuration nginx durcie. Le site répondait 200 après chaque mise en ligne — les en-têtes de sécurité, eux, avaient disparu | **Un healthcheck qui répond 200 ne dit pas que tout va bien.** Il faut vérifier ce qui compte, pas ce qui est facile à mesurer |
| Une collecte de données échouait en silence depuis des semaines. Aucune alerte : le script mourait proprement | L'absence d'erreur n'est pas un signe de bonne santé. **Il faut surveiller la fraîcheur des données**, pas seulement le code de sortie |
| Mes trois systèmes de surveillance tournaient sur la machine qu'ils surveillaient | Un surveillant hébergé sur ce qu'il surveille **ne préviendra jamais de sa propre panne**. Il faut au moins un observateur extérieur |

Et une règle que je m'applique partout : **une sauvegarde jamais restaurée n'est pas une sauvegarde, c'est une hypothèse.** Vérifier une empreinte ne prouve rien tant qu'on n'a pas reconstruit la machine à partir de zéro.

---

**[hamdy-tabsissi.com](https://hamdy-tabsissi.com)** · [LinkedIn](https://www.linkedin.com/in/hamdy-tabsissi/) · [TryHackMe](https://tryhackme.com/r/p/4y4n0k0j1)
