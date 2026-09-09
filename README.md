# Hamdy Tabsissi

**Systems & Workplace Administrator** chez Action contre la Faim · Master Cybersécurité (SUP DE VINCI)
Microsoft 365 · Azure · Cloud & Identity · auto-hébergement

J'administre une infrastructure personnelle en production et je documente ce qui casse.
Tout ce qui suit tourne réellement, pas en local.

**→ [hamdy-tabsissi.com](https://hamdy-tabsissi.com)**

---

## Ce qui tourne en production

Une VM Oracle ARM (4 OCPU / 24 Go), Ubuntu, derrière Cloudflare.

| Domaine | Ce qui est en place |
|---|---|
| **Exposition** | Cloudflare Tunnel — aucun port entrant ouvert, pare-feu limité aux plages Cloudflare. Accès administrateur derrière Cloudflare Access (SSO) |
| **Durcissement** | nginx noté A+ sur les en-têtes de sécurité, fail2ban, mises à jour automatiques, services systemd contraints, Node en écoute loopback uniquement |
| **Déploiement** | CI/CD pull-based : GitHub Actions valide et pose un tag, la VM tire — aucun identifiant d'accès à la machine stocké chez GitHub. Healthcheck après déploiement, rollback automatique et mise en quarantaine du commit fautif |
| **Sauvegardes** | Litestream (réplication SQLite continue) + restic, vers Cloudflare R2 hors-site, chiffrées. Restaurations vérifiées par comparaison d'empreintes SHA-256 |
| **Supervision** | Uptime Kuma, moniteur externe indépendant, dead man's switch Healthchecks auto-hébergé |
| **Automatisation** | n8n auto-hébergé : veille de disponibilité, digests, alertes Telegram routées par thème |
| **Conformité** | Matomo auto-hébergé (anonymisation IP, rétention 25 mois), registre RGPD, SMSI ISO 27001 avec analyse EBIOS RM et Déclaration d'Applicabilité |

---

## Projets

| Projet | Ce que c'est | Stack |
|---|---|---|
| [Portfolio](https://hamdy-tabsissi.com) | Site personnel — accès par lien nominatif, consultations tracées | Node · Express · node:sqlite · CSS moderne |
| EventMap | Agrégateur d'événements Paris ↔ Nanterre ↔ Montreuil, filtré et daté | Python · FastAPI · Leaflet · SQLite |
| Observatory | Tableau de bord d'état des services, authentifié par JWT Cloudflare Access vérifié contre le JWKS | Python · FastAPI |
| Mindmap | Carte mentale fractale à navigation spatiale, canvas 2D sans librairie | JavaScript vanilla |
| [Projet SOC](https://github.com/flemops/Projet-SOC) | SOC externalisé — Wazuh, Suricata, pfSense, ELK, TheHive/Cortex, conformité ISO 27001 / RGPD / NIS | Master SUP DE VINCI |
| [Projet SIEM](https://github.com/flemops/Projet-SIEM) | Centralisation et corrélation de journaux | Master SUP DE VINCI |
| [Cloud Hybride](https://github.com/flemops/Projet-CLoud-Hybrid) | Architecture hybride on-premise / cloud | Master SUP DE VINCI |
| [Root-Me](https://github.com/flemops/Projet-Root-Me) | Analyse et exploitation en environnement contrôlé | Master SUP DE VINCI |

---

## Ce que je retiens de cette infrastructure

- Une sauvegarde non restaurée est une hypothèse. L'intégrité vérifiée par empreinte ne prouve rien tant qu'on n'a pas reconstruit la machine.
- - Un système d'alerte hébergé sur la machine qu'il surveille ne prévient jamais de sa propre panne. Il faut au moins un observateur extérieur.
  - - Un healthcheck qui répond 200 ne dit pas que la page s'affiche. D'où les tests de bout en bout avant toute mise en ligne.
    - - Un tableau de bord qui affiche des données de secours sans le signaler est pire que pas de tableau de bord.
     
      - ---

      [hamdy-tabsissi.com](https://hamdy-tabsissi.com) · [LinkedIn](https://www.linkedin.com/in/hamdy-tabsissi/) · [TryHackMe](https://tryhackme.com/r/p/4y4n0k0j1)
      
