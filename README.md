# Guide d'Utilisation FactuGlass

**Version 0.5.0** • Guide complet pour l'utilisateur final

---

## 📖 Table des matières

1. [Introduction](#introduction)
2. [Premier démarrage](#premier-démarrage)
3. [Tableau de bord](#tableau-de-bord)
4. [Gestion des collaborateurs](#gestion-des-collaborateurs)
5. [Import des activités](#import-des-activités)
6. [Génération de factures](#génération-de-factures)
7. [Cycle de vie des factures](#cycle-de-vie-des-factures)
8. [Analyse et anomalies](#analyse-et-anomalies)
9. [Paramètres](#paramètres)
10. [Mises à jour automatiques](#mises-à-jour-automatiques)

---

## Introduction

FactuGlass est un outil de facturation interne qui automatise le calcul de facturation à partir des temps déclarés par les collaborateurs.

### Fonctionnalités principales

✅ **Gestion des collaborateurs** : Création, modification, coûts journaliers avec historique
✅ **Import XML** : Import des fichiers d'activités WINDEV
✅ **Facturation intelligente** : Calcul automatique avec calendrier français
✅ **Cycle de vie** : Gestion complète du workflow de facturation (brouillon → émise → validée)
✅ **Alertes automatiques** : Rappels des échéances de facturation
✅ **Détection d'anomalies** : Identification automatique des incohérences
✅ **Exports** : Génération de rapports CSV et Excel

---

## Premier démarrage

### Installation

1. Téléchargez le fichier d'installation depuis les releases GitHub
2. Exécutez l'installeur Windows (.msi ou .exe)
3. Suivez les instructions d'installation
4. Lancez FactuGlass depuis le menu Démarrer

### Configuration initiale

Au premier lancement :

1. **Paramètres de base** :
   - Allez dans **Paramètres** (icône ⚙️ en haut à droite)
   - Configurez la **période de facturation** (par défaut : 21 → 20)
   - Définissez les **heures par jour** (7h ou 8h)

2. **Ajout de collaborateurs** :
   - Allez dans **Collaborateurs**
   - Cliquez sur **+ Nouveau collaborateur**
   - Renseignez : nom, prénom, email, coût journalier

---

## Tableau de bord

Le tableau de bord affiche une vue d'ensemble de la période de facturation en cours.

### Sections principales

#### 1. Alertes de facturation 🚨
Bandeau coloré en haut affichant les échéances :
- **Bleu (Info)** : Rappel informatif
- **Orange (Warning)** : Attention, échéance proche
- **Rouge (Critical)** : Urgent, action requise

**Calendrier des alertes** :
- **J14-15** : Préparez la facturation
- **J16** : Créer la facture brouillon
- **J18** : Émettre la facture
- **J28** : Valider la facture

#### 2. Timeline de la période
Barre de progression visuelle montrant :
- Période actuelle (dates de début et fin)
- Jours écoulés / restants / total
- Pourcentage d'avancement

#### 3. Activités enregistrées
- Couverture des jours ouvrés (%)
- Heures totales vs heures facturables
- Anomalies détectées par type

#### 4. Facturation et revenus
- Nombre de factures par statut (brouillon, émise, validée)
- Projets livrés en attente de facturation
- Chiffre d'affaires de la période
- CA validé

#### 5. Actions rapides
Boutons d'accès direct aux fonctions principales :
- Importer XML
- Nouveau collaborateur
- Générer rapport
- Gérer factures

---

## Gestion des collaborateurs

### Créer un collaborateur

1. Allez dans **Collaborateurs**
2. Cliquez sur **+ Nouveau collaborateur**
3. Remplissez les champs :
   - **Nom et Prénom** : Obligatoires
   - **Email** : Optionnel
   - **Coût journalier** : Tarif facturé par jour
   - **Équipe** : Si applicable (voir Équipes)
   - **Date d'entrée/sortie** : Pour gérer les périodes d'activité
   - **Jours assignés** : Jours de la semaine travaillés (par défaut Lun-Ven)

4. Cliquez sur **Créer**

### Modifier un collaborateur

1. Dans la liste des collaborateurs, cliquez sur **Modifier**
2. Modifiez les informations nécessaires
3. **Important** : Si vous changez le coût journalier, l'historique est automatiquement conservé

### Historique des coûts

L'application conserve automatiquement l'historique des coûts :
- Chaque modification de coût crée une entrée d'historique
- Les facturations utilisent le coût en vigueur à la date de l'activité
- Consultez l'historique depuis la fiche collaborateur

### Équipes et modes de facturation

Les collaborateurs peuvent être organisés en équipes avec deux modes :

**Facturation par période (mensuelle)** :
- Facturation classique chaque mois
- Basée sur les activités de la période

**Facturation par livraison de projet** :
- Facturation déclenchée lors de la livraison
- Nécessite de marquer les projets comme "livrés"

---

## Import des activités

### Format supporté

FactuGlass importe les fichiers XML au format WINDEV_TABLE.

Structure attendue :
```xml
<Activité>
  <Date>24/07/2025</Date>
  <Durée>03:00</Durée>
  <Activité>Intervention</Activité>
  <Code>PRJ-001</Code>
  <Projet>Nom du projet</Projet>
  <Statut>En cours</Statut>
</Activité>
```

### Procédure d'import

1. Allez dans **Import**
2. Deux options :
   - **Glisser-déposer** le fichier XML dans la zone
   - **Cliquer** pour sélectionner le fichier

3. **Associer le collaborateur** :
   - Sélectionnez le collaborateur correspondant dans la liste
   - Le système mémorise l'association pour les prochains imports

4. Vérification :
   - Le système affiche un aperçu des activités à importer
   - Vérifie la présence de doublons
   - Détecte les erreurs de format

5. Cliquez sur **Importer**

### Types d'activités

Les activités sont automatiquement classées :

**Facturables** :
- Intervention
- Développement
- Support
- Réunion
- Formation
- Etc.

**Non facturables** :
- Congés
- RTT
- Récupération
- Maladie
- Absence

---

## Génération de factures

### Workflow de facturation

FactuGlass distingue deux modes selon les équipes :

#### Mode 1 : Facturation mensuelle (par défaut)

1. Allez dans **Facturation**
2. Sélectionnez la **période** (dates de début et fin)
3. Cliquez sur **Calculer**
4. Consultez le résumé :
   - Total heures / jours facturables
   - Coût par collaborateur
   - Total général
5. Cliquez sur **Créer facture brouillon**

#### Mode 2 : Facturation par livraison

1. Allez dans **Facturation** → onglet **Livraisons**
2. Créez une livraison :
   - Code projet
   - Équipe concernée
   - Date de livraison
   - Période d'activités à facturer
3. Le système génère automatiquement la facture pour ce projet

### Exports disponibles

**CSV (Excel)** :
- Tableau complet avec détails par collaborateur
- Import direct dans Excel

**Excel formaté** :
- Rapport professionnel avec mise en forme
- Graphiques et totaux
- Prêt à envoyer

---

## Cycle de vie des factures

Les factures suivent un workflow à 3 états + 1 état d'annulation.

### États de facture

#### 1. 📝 Brouillon (Draft)
- Facture créée mais non finalisée
- **Vous pouvez** : modifier, ajouter des ajustements, supprimer
- **Action suivante** : Émettre la facture

#### 2. 📄 Émise (Issued)
- Facture envoyée au client
- **Vous pouvez** : ajouter des ajustements, annuler
- **Vous ne pouvez plus** : supprimer
- **Action suivante** : Valider après accord client

#### 3. ✅ Validée (Validated)
- Facture approuvée par le client
- **Vous pouvez** : consulter uniquement, annuler avec justification
- **Vous ne pouvez plus** : modifier
- **Action suivante** : Aucune (état final)

#### 4. ❌ Annulée (Cancelled)
- Facture annulée avec raison documentée
- **Conservée** pour historique
- **Ne compte plus** dans les statistiques

### Transitions

```
Brouillon → Émettre → Émise → Valider → Validée
    ↓                   ↓              ↓
  Suppr.            Annuler        Annuler
```

### Ajustements de facture

Vous pouvez appliquer des ajustements à tout moment (sauf état Validée) :

**Types d'ajustements** :
- **Remise** : Réduction tarifaire (montant négatif)
- **Supplément** : Ajout (montant positif)
- **Correction** : Correction d'erreur
- **Avoir** : Note de crédit

**Procédure** :
1. Ouvrez les détails de la facture
2. Cliquez sur **Ajouter un ajustement**
3. Sélectionnez le type
4. Indiquez le montant et la raison
5. Validez

Le montant final est recalculé automatiquement.

### Numérotation automatique

Les factures sont numérotées automatiquement :
- Format : `FAC-YYYY-NNN` (ex: FAC-2025-001)
- Séquentiel par année
- Unique et non modifiable

---

## Analyse et anomalies

### Page Analyse (KPI)

Accès : Menu **Analyse**

Visualisez vos métriques de facturation avec filtres personnalisables :

**Filtres disponibles** :
- Période (dates de début/fin)
- Collaborateur spécifique
- Équipe
- Type d'activité

**Onglets** :

#### 1. Vue Collaborateurs
- Heures et jours facturables par personne
- Coût journalier appliqué
- Total par collaborateur

#### 2. Vue Projets (Codes)
- Répartition par code projet
- Heures par projet
- Collaborateurs affectés

#### 3. Vue Détaillée
- Croisement collaborateur × projet
- Ventilation complète des activités

### Détection d'anomalies

Accès : Menu **Anomalies** ou depuis le Dashboard

#### Types d'anomalies détectées

**⚠️ Heures manquantes** :
- Pas d'activité sur un jour ouvré
- Jour incomplet (< heures requises)
- Heures insuffisantes

**⚡ Heures excessives** :
- Dépassement du seuil journalier sans congé/RTT

**📅 Travail week-end** :
- Activités enregistrées samedi ou dimanche

**🎉 Travail jours fériés** :
- Activités sur jours fériés français

#### Consultation des anomalies

1. Allez dans **Anomalies**
2. Filtrez par :
   - Période
   - Type d'anomalie
   - Collaborateur
3. Consultez les détails de chaque anomalie
4. Actions possibles :
   - Corriger les activités
   - Ajouter les temps manquants
   - Documenter les exceptions

**Note** : Le tableau de bord n'affiche que les anomalies sur les **jours écoulés** pour éviter les fausses alertes sur les jours futurs.

---

## Paramètres

Accès : Icône ⚙️ en haut à droite

### Période de facturation

**Jour de début** : Jour du mois de début de période (1-31)
**Jour de fin** : Jour du mois de fin de période (1-31)

**Exemple** :
- Début : 21, Fin : 20 → Période du 21 octobre au 20 novembre
- Début : 1, Fin : 31 → Période du 1er au 31 du mois (mensuel classique)

Cette configuration s'applique automatiquement :
- Calculs de facturation
- Tableau de bord
- Détection d'anomalies
- Alertes

### Heures par jour

Définit la base de conversion heures → jours facturables :
- **7 heures** : 1 jour = 7h (35h/semaine)
- **8 heures** : 1 jour = 8h (40h/semaine)

**Impact** :
- Calcul des jours facturables
- Détection des jours incomplets
- Totaux de facturation

### Sauvegarde

Tous les paramètres sont sauvegardés automatiquement en base de données.

---

## Mises à jour automatiques

FactuGlass intègre un système de mise à jour automatique via GitHub Releases.

### Comment ça fonctionne

1. **Vérification au démarrage** :
   - L'application vérifie automatiquement les nouvelles versions
   - Une notification apparaît si une mise à jour est disponible

2. **Installation** :
   - Cliquez sur **Installer la mise à jour**
   - L'application télécharge et installe la nouvelle version
   - Redémarrage automatique

3. **Notes de version** :
   - Consultez les nouveautés avant de mettre à jour
   - Lien direct vers les notes de version complètes

### Versions

FactuGlass suit le versionnement sémantique :
- **Majeure** (X.0.0) : Changements importants
- **Mineure** (0.X.0) : Nouvelles fonctionnalités
- **Patch** (0.0.X) : Corrections de bugs

**Version actuelle** : 0.5.0

---

## Conseils d'utilisation

### Workflow recommandé

**Mensuel** :

1. **Jour 1-10** : Import des activités des collaborateurs
2. **Jour 14** : Vérification des anomalies et correction
3. **Jour 16** : Création de la facture brouillon
4. **Jour 18** : Émission de la facture
5. **Jour 28** : Validation après accord client

### Bonnes pratiques

✅ **Importez régulièrement** les activités (hebdomadaire recommandé)
✅ **Vérifiez les anomalies** avant de générer les factures
✅ **Documentez les ajustements** avec des raisons claires
✅ **Sauvegardez** la base de données régulièrement (voir section suivante)
✅ **Suivez le workflow** de facturation (brouillon → émise → validée)

### Sauvegarde des données

**Emplacement de la base de données** :
- Windows : `%APPDATA%/com.factuglass.app/factuglass.db`

**Recommandations** :
- Sauvegardez ce fichier régulièrement
- Conservez des copies avant les mises à jour majeures
- Testez la restauration de vos sauvegardes

---

## Support et ressources

### En cas de problème

1. **Vérifiez** que vous utilisez la dernière version
2. **Consultez** les messages d'erreur dans l'interface
3. **Recherchez** dans la documentation technique (pour développeurs)
4. **Contactez** l'équipe de support

### Ressources techniques

Pour les développeurs et administrateurs, consultez :
- `CLAUDE.md` : Instructions pour le développement
- `docs/DEV.md` : Guide développeur
- `docs/AUTO_UPDATE_GUIDE.md` : Configuration des mises à jour

---

## Glossaire

**Activité** : Enregistrement de temps saisi par un collaborateur
**Anomalie** : Incohérence détectée dans les activités
**Brouillon** : Premier état d'une facture (modifiable)
**Code projet** : Identifiant d'un projet (ex: PRJ-001)
**Coût journalier** : Tarif facturé par jour pour un collaborateur
**Émise** : Facture envoyée au client (semi-verrouillée)
**Facturable** : Activité comptabilisée dans la facturation
**Jour ouvré** : Jour travaillé (Lun-Ven hors jours fériés)
**Livraison** : Marquage d'un projet comme terminé (pour facturation)
**Période** : Intervalle de dates pour la facturation
**Validée** : Facture approuvée par le client (verrouillée)

---

**FactuGlass v0.5.0** • Octobre 2025 • Made with ❤️
