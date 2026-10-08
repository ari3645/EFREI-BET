# Projet : Application de paris sportifs
 
## Description. 
 
Application  de paris sportifs, construite comme un ensemble de services indépendants qui communiquent entre eux par des événements. Les utilisateurs peuvent consulter des matchs, parier avec un solde virtuel et recevoir leurs gains lorsque le match est terminé.

> Aucun argent réel n'est utilisé : les soldes et les mises sont purement fictifs.

## Services

| Service | Rôle | Commandes |
|---|---|---|
| **Matchs** | Gère les matchs, les cotes et les résultats. Émet un événement à chaque étape de la vie d'un match (créé, cotes modifiées, démarré, terminé, annulé). | `CréerMatch`, `ModifierCotes`, `DémarrerMatch`, `TerminerMatch`, `AnnulerMatch` |
| **Paris** | Permet de placer un pari (match, issue, mise) et suit son statut (en attente, accepté, refusé, gagné, perdu, remboursé). Conserve une copie locale des matchs et des portefeuilles pour valider un pari sans appeler les autres services. | `PlacerPari`, `ConfirmerPari`, `RefuserPari`, `RéglerPari`, `AnnulerPari` |
| **Portefeuille** | Gère les comptes et les soldes : débit de la mise lors d'un pari, crédit des gains lorsqu'il est gagné, remboursement si le match est annulé. | `CréerPortefeuille`, `DébiterPortefeuille`, `CréditerPortefeuille`, `RembourserPari`, `RechargerPortefeuille` |

## Interactions principales

- Le service **Matchs** informe le service **Paris** de chaque changement d'un match : création, modification des cotes, démarrage, fin ou annulation.
- Le service **Paris** demande au service **Portefeuille** de débiter la mise lors d'un pari (`PariPlacé`). Portefeuille confirme le débit (`SoldeModifié`) ou le refuse si le solde est insuffisant (`DébitRefusé`).
- À la fin d'un match, le service **Paris** règle les paris concernés et demande le crédit des gains (`PariGagné`).
- Si un match est annulé, le service **Paris** rembourse les paris concernés (`PariRemboursé`) et le service **Portefeuille** rend les mises.
- Le service **Portefeuille** informe le service **Paris** de la création des portefeuilles et de l'évolution des soldes (`PortefeuilleCréé`, `SoldeModifié`).

## Événements

| Événement | Émetteur | Récepteur |
|---|---|---|
| `MatchCréé`, `CotesModifiées`, `MatchDémarré`, `MatchTerminé`, `MatchAnnulé` | Matchs | Paris |
| `PariPlacé`, `PariGagné`, `PariRemboursé`, `PariPerdu` | Paris | Portefeuille |
| `PortefeuilleCréé`, `SoldeModifié`, `DébitRefusé` | Portefeuille | Paris |

## Documentation JSON

- `services.json` : les services et leurs commandes.
- `commandes_*.json` : le détail des commandes de chaque service.
- `agregats_*.json` : les agrégats de chaque service, y compris les réplicas du service Paris.
- `evenement_*.json` : un fichier par événement échangé entre services.

## Équipe

- Christophe CUI
- Serenic MOHANRAJU
- Albin RIVIERE
- Nabil SAIED
