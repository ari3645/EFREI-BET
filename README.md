# Projet : Application de paris sportifs
 
## Description. 
 
Application  de paris sportifs, construite comme un ensemble de services indépendants qui communiquent entre eux par des événements. Les utilisateurs peuvent consulter des matchs, parier avec un solde virtuel et recevoir leurs gains lorsque le match est terminé.
 
> Aucun argent réel n'est utilisé : les soldes et les mises sont purement fictifs.
 
## Services
 
| Service | Rôle |
|---|---|
| **Matchs** | Gère les matchs, les cotes et les résultats. Émet un événement lorsqu'un match est créé, qu'une cote change ou qu'un match se termine. |
| **Paris** | Permet de placer un pari (match, issue, mise) et suit son statut (en cours, gagné, perdu). Conserve une copie locale des matchs et des cotes pour valider un pari sans appeler le service Matchs. |
| **Utilisateurs / Portefeuille** | Gère les comptes et les soldes : débit de la mise lors d'un pari, crédit des gains lorsqu'il est gagné. |
 
## Interactions principales
 
- Le service **Matchs** informe le service **Paris** de la création et de la mise à jour des matchs et des cotes.
- Le service **Paris** demande au service **Utilisateurs / Portefeuille** de débiter la mise lors d'un pari.
- À la fin d'un match, le service **Paris** règle les paris concernés et demande le crédit des gains.

## Équipe
 
- Christophe CUI
- Serenic MOHANRAJU
- Albin RIVIERE
- Nabil SAIED
