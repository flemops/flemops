# Carte des 16 dépôts — rôle, visibilité, statut

Mise à jour : 07/10/2026. Chaque dépôt a un rôle unique ; les dépôts ne sont pas censés avoir tous le même niveau de preuve.

| Dépôt | Rôle | Visibilité | Statut | Licence | Justification |
|---|---|---|---|---|---|
| [eventmap](https://github.com/flemops/eventmap) | FLAGSHIP | public | actif, production | MIT (code) ; données : licences des sources | Application complète, CI/CD, tests, décisions documentées |
| [alimconfiance-archive](https://github.com/flemops/alimconfiance-archive) | FLAGSHIP | public | actif, production | MIT (code) ; données : Licence Ouverte | Preuve simple et vérifiable d'une chaîne d'archivage |
| [ci-templates](https://github.com/flemops/ci-templates) | SUPPORT/DEVOPS | public | actif | MIT | Mécanisme de déploiement réutilisé par 4 applications |
| [mindmap](https://github.com/flemops/mindmap) | LAB (démo en production) | public | actif | MIT | Réalisation visuelle Three.js, démo publique |
| [alpaca-lab](https://github.com/flemops/alpaca-lab) | LAB | public | lab | aucune (par défaut) | Outil d'apprentissage, aucune prétention financière |
| [Projet-Cloud-Hybrid](https://github.com/flemops/Projet-Cloud-Hybrid) | ACADEMIC | public | figé | aucune (documents de cursus) | AD / messagerie : contribution individuelle documentée |
| [Projet-SIEM](https://github.com/flemops/Projet-SIEM) | ACADEMIC | public | figé | aucune | Rapport en binôme, limites explicites |
| [Projet-SOC](https://github.com/flemops/Projet-SOC) | ACADEMIC | public | figé | aucune | Cas d'étude individuel, conçu vs déployé distingués |
| [Projet-Root-Me](https://github.com/flemops/Projet-Root-Me) | ACADEMIC | public | figé | aucune | Exercice contrôlé ; support retiré car il montrait les flags |
| [mission-control](https://github.com/flemops/mission-control) | THIRD-PARTY-FORK | public | utilisé tel quel | MIT (upstream) | 0 commit propre : pas un projet de Hamdy |
| [trier-mes-mails](https://github.com/flemops/trier-mes-mails) | ARCHIVE | public, archivé | abandonné | aucune | Remplacé par règles de messagerie et n8n |
| [flemops](https://github.com/flemops/flemops) | PROFIL | public | actif | — | README de profil |
| `portfolio.hamdy-tabsissi.com` | PRIVATE-OPS | **privé** | actif, production | — | Code du site live ; la valeur est portée par le site |
| `observatory` | PRIVATE-OPS | **privé** | actif, production | — | Contient des informations opérationnelles |
| `smsi-interne` | PRIVATE-OPS | **privé, jamais public** | actif | — | État détaillé des défenses : informations sensibles |
| `atelier-claude` | WORKSPACE | **privé** | actif | — | Espace de travail personnel |

Règle de publication : un dépôt privé ne devient public qu'après analyse de l'historique (secrets, données personnelles, informations d'infrastructure), des captures, des configurations et des licences.

## Contrôles de base selon le type de dépôt

| Type | Contrôles attendus | État au 07/10/2026 |
|---|---|---|
| Application avec code | installation propre, lint, tests, audit des dépendances, détection de secrets, permissions minimales, délai maximal, actions épinglées par SHA | eventmap : complet ; portfolio : tests, contraste, captures, gitleaks, audit npm ; mindmap : tests, gitleaks, audit npm ; observatory : tests, gitleaks, pip-audit ; alpaca-lab : tests, ruff, pip-audit |
| Dépôt de snapshots | téléchargement, validation (taille, en-tête), idempotence, provenance | alimconfiance-archive : garde-fous et idempotence dans le workflow |
| Gabarit CI | validation par exécution depuis un consommateur, actions épinglées | ci-templates |
| Documentaire / académique / fork | aucun pipeline inventé | aucun |

Dependabot : uniquement là où il y a de vraies dépendances (npm : portfolio, mindmap ; pip : eventmap, observatory), mises à jour groupées mensuelles. Actions GitHub : épinglées par SHA vérifié sur la release officielle, mises à jour à la main. Historique Git analysé avant toute publication ; aucun secret trouvé sur les 16 dépôts (un identifiant de messagerie personnel non secret a été retiré de l'historique de ci-templates avant publication).

Guide de rédaction des README : [GABARITS-README.md](GABARITS-README.md).
