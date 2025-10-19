# Rapport de révision de la documentation atoum
## Version cible : atoum 4.4.1 (depuis 3.2.0)

**Date du rapport** : 19 octobre 2025  
**Dernier commit de la documentation** : 30 juillet 2023  
**État** : Documentation obsolète nécessitant des mises à jour

---

## 📊 Résumé exécutif

La documentation d'atoum est actuellement figée à la version **3.2.0** (2017) alors que la version actuelle d'atoum est **4.4.1** (2025). Cette différence représente **8 ans d'évolution** et des changements majeurs incluant :
- Changement de namespace (`\mageekguy\atoum` → `\atoum\atoum`)
- Support PHP 8.0+ uniquement (abandon PHP 5.x et 7.x)
- Corrections de compatibilité PHP 8.1 à 8.5
- Nouvelles fonctionnalités et corrections de bugs

---

## ✅ Modifications déjà effectuées

### 1. Mise à jour des fichiers de configuration
- ✅ `source/en/conf.py` : version 3.2.0 → 4.4.1
- ✅ `source/fr/conf.py` : version 3.2.0 → 4.4.1
- ✅ Copyright mis à jour : 2014-2017 → 2014-2025

---

## ⚠️ Changements majeurs entre v3.2.0 et v4.4.1

### Version 4.0.0 (21 novembre 2020) - **BREAKING CHANGES**

#### 1. Changement de namespace (CRITIQUE)
- **Ancien** : `\mageekguy\atoum`
- **Nouveau** : `\atoum\atoum`
- **Impact** : Tous les exemples de code dans la documentation doivent être mis à jour

#### 2. Compatibilité PHP
- **Ancien** : PHP 5.6+ supporté
- **Nouveau** : PHP 8.0+ uniquement (depuis v4.2.0, PHP 7.4 abandonné)
- **Impact** : Requis mise à jour des prérequis système

#### 3. Suppression de l'extension IDE
- L'extension IDE a été retirée du core d'atoum
- **Impact** : Documentation sur l'IDE potentiellement obsolète

#### 4. Suppression de l'implémentation des hooks de test
- Les hooks de tests ont été supprimés
- **Impact** : Documentation sur les hooks à vérifier/supprimer

### Versions 4.1.0 à 4.4.1 (2022-2025)

#### Support des nouvelles fonctionnalités PHP
- ✅ Type de retour `static` dans le générateur de mocks (v4.1.0)
- ✅ PHP 8.2 support (v4.1.0)
- ✅ PHP 8.3 support (v4.2.0)
- ✅ Support des types `null`, `true`, `false` (v4.2.0)
- ✅ PHP 8.4 support (v4.3.0, v4.4.0)
- ✅ PHP 8.5 support (v4.4.0)
- ✅ Correction des types de retour `self`, `parent`, `static` (v4.4.1)

---

## 🔍 Sections de la documentation nécessitant des mises à jour

### 1. **Installation** (PRIORITÉ HAUTE)

#### Fichiers concernés :
- `source/en/installation.rst`
- `source/fr/installation.rst`

#### Problèmes identifiés :

##### a) Archive PHAR cassée
```rst
.. warning::
	For the moment the phar build is broken, so this is not available....
```
**Action** : Vérifier si le PHAR est à nouveau disponible. Si oui, retirer l'avertissement et mettre à jour les liens.

##### b) Prérequis PHP obsolètes
**Actuel** : Documentation mentionne PHP 5.6+  
**Requis** : PHP 8.0+ (depuis atoum 4.2.0)

**Tableau de compatibilité à ajouter** :
```markdown
| Version PHP | Version atoum      |
|-------------|--------------------|
| 5.3 → 5.6   | 1.x → 3.x          |
| 7.2 → 8.1   | 4.0 → 4.1          |
| 8.0+        | 4.1+ (actuelle)    |
```

##### c) Liens vers les PHAR obsolètes
Les liens pointent vers des versions 3.2.0 inexistantes.

**À mettre à jour dans** :
- README.md du dépôt atoum
- Pages d'installation

### 2. **Exemples de code** (PRIORITÉ HAUTE)

#### Problème : Namespace obsolète
Tous les exemples de code utilisent l'ancien namespace `\mageekguy\atoum`.

#### Exemples à corriger :

**Ancien** :
```php
<?php
namespace vendor\project\tests\units;

use mageekguy\atoum;

class helloWorld extends atoum\test
{
    // ...
}
```

**Nouveau** :
```php
<?php
namespace vendor\project\tests\units;

use atoum\atoum;

class helloWorld extends atoum\test
{
    // ...
}
```

#### Fichiers à vérifier :
- Tous les fichiers `.rst` contenant des exemples de code
- Particulièrement :
  - `first_test.rst`
  - `how_to_write_test_cases.rst`
  - `mocking_systems.rst`
  - Tous les fichiers dans `asserters/`
  - `configuration_bootstraping.rst`

### 3. **Système de mocking** (PRIORITÉ MOYENNE)

#### Fichiers concernés :
- `source/*/mocking_systems.rst`
- `source/*/mocking_systems/*.inc.rst`

#### Nouvelles fonctionnalités à documenter :

##### a) Support des types de retour modernes PHP
- Type de retour `static` (depuis v4.1.0)
- Types `null`, `true`, `false` (depuis v4.2.0)
- Union types
- Intersection types (PHP 8.1+)

##### b) Comportements mis à jour
- Gestion correcte de `self`, `parent`, `static` dans les types de retour (v4.4.1)
- Tentative de types de retour dans les méthodes mockées (v4.0.2)

### 4. **Configuration et Bootstrap** (PRIORITÉ MOYENNE)

#### Fichiers concernés :
- `source/*/configuration_bootstraping.rst`
- `source/*/configuration_bootstraping/*.inc.rst`

#### Points à vérifier :
- Exemples de fichiers de configuration avec l'ancien namespace
- Autoloader Composer (intégration automatique depuis v2.8.0)
- Fichiers `.autoloader.atoum.php` (depuis v2.8.0)
- Argument CLI `--autoloader-file`/`-af` (depuis v2.8.0)

### 5. **Asserters** (PRIORITÉ BASSE)

#### Fichiers concernés :
- `source/*/asserters.rst`
- Tous les fichiers dans `source/*/asserters/*.inc.rst`

#### Points à vérifier :
- Asserter `generator` (ajouté en v3.0.0)
- Nouvelles méthodes sur les asserters existants
- Exemples de code avec namespace obsolète

### 6. **Extensions et IDE** (PRIORITÉ MOYENNE)

#### Fichier concerné :
- `source/*/ide.rst`

#### Problème potentiel :
L'extension IDE a été retirée du core d'atoum en v4.0.0 (PR #707).

**Action requise** :
- Vérifier le contenu actuel de `ide.rst`
- Mettre à jour pour référencer l'extension externe si elle existe
- Ajouter un avertissement sur la séparation de l'extension

### 7. **FAQ et Troubleshooting** (PRIORITÉ BASSE)

#### Fichiers concernés :
- `source/*/faq.rst`

#### Points à vérifier :
- Problèmes liés aux anciennes versions de PHP
- Problèmes de compatibilité qui n'existent plus
- Ajout de nouvelles questions fréquentes

---

## 📝 Actions recommandées

### Phase 1 : Corrections critiques (Immédiat)

1. **Mettre à jour tous les exemples de code avec le nouveau namespace**
   - Script de recherche/remplacement global
   - Rechercher : `use mageekguy\\atoum` ou `mageekguy\\atoum`
   - Remplacer : `use atoum\\atoum` ou `atoum\\atoum`

2. **Mettre à jour les prérequis PHP**
   - Indiquer clairement : **PHP 8.0+ requis**
   - Ajouter le tableau de compatibilité versions PHP/atoum

3. **Corriger la page d'installation**
   - Vérifier l'état du PHAR
   - Mettre à jour les liens de téléchargement
   - Recommander Composer comme méthode principale

### Phase 2 : Améliorations (Court terme)

4. **Documenter les nouveautés de la v4.x**
   - Support des types de retour PHP 8.x
   - Changements dans le système de mocking
   - Nouvelles fonctionnalités

5. **Réviser la documentation sur l'IDE**
   - Clarifier la séparation de l'extension
   - Fournir des liens vers l'extension externe

6. **Ajouter des notes de migration**
   - Créer une section "Migrer de la v3 à la v4"
   - Documenter les breaking changes
   - Fournir des exemples de migration

### Phase 3 : Optimisations (Moyen terme)

7. **Réviser l'ensemble du contenu**
   - Vérifier la cohérence des exemples
   - Mettre à jour les captures d'écran si nécessaire
   - Améliorer la structure si besoin

8. **Ajouter des exemples PHP 8.x**
   - Propriétés typées
   - Named arguments
   - Match expressions
   - Attributs PHP 8

9. **Mettre à jour le cookbook**
   - Nouvelles recettes pour PHP 8.x
   - Meilleures pratiques actualisées

---

## 🛠️ Script de migration suggéré

### Recherche globale des namespaces obsolètes

```bash
# Rechercher toutes les occurrences de l'ancien namespace
grep -r "mageekguy\\\\atoum" source/

# Compter les fichiers affectés
grep -rl "mageekguy\\\\atoum" source/ | wc -l
```

### Remplacement automatique (à tester avec précaution)

```bash
# Sauvegarde avant remplacement
git add -A
git commit -m "Backup before namespace migration"

# Remplacement dans tous les fichiers .rst
find source/ -name "*.rst" -type f -exec sed -i 's/mageekguy\\atoum/atoum\\atoum/g' {} \;
find source/ -name "*.rst" -type f -exec sed -i 's/use mageekguy\\\\atoum/use atoum\\\\atoum/g' {} \;
```

---

## 📚 Ressources de référence

### Documentation officielle atoum v4.x
- Repository : https://github.com/atoum/atoum
- CHANGELOG : https://github.com/atoum/atoum/blob/master/CHANGELOG.md
- Releases : https://github.com/atoum/atoum/releases
- Extensions : http://extensions.atoum.org/

### Changements importants par version
- **v4.0.0** : Changement de namespace, compatibilité PHP 7+
- **v4.1.0** : Support PHP 8.2, type `static`
- **v4.2.0** : Abandon PHP 7.4, support types `null`/`true`/`false`
- **v4.3.0** : PHP 8.4 support
- **v4.4.0** : PHP 8.5 support
- **v4.4.1** : Corrections types de retour `self`/`parent`/`static`

---

## ✅ Checklist de vérification

### Avant publication
- [ ] Tous les exemples utilisent `atoum\atoum`
- [ ] Les prérequis PHP sont à jour (PHP 8.0+)
- [ ] Les liens de téléchargement sont valides
- [ ] L'avertissement PHAR est correct
- [ ] Le tableau de compatibilité est présent
- [ ] Les nouvelles fonctionnalités v4.x sont documentées
- [ ] La section IDE est mise à jour
- [ ] Une note de migration v3→v4 existe
- [ ] Le copyright est à jour (2014-2025)
- [ ] La version dans conf.py est correcte (4.4.1)

### Tests
- [ ] La documentation se compile sans erreur
- [ ] Les exemples de code sont syntaxiquement corrects
- [ ] Les liens internes fonctionnent
- [ ] Les liens externes sont valides

---

## 🎯 Conclusion

La documentation nécessite une **révision importante** pour refléter la version actuelle d'atoum (4.4.1). Les changements critiques concernent principalement :

1. **Le namespace** (impact sur tous les exemples)
2. **Les prérequis PHP** (PHP 8.0+ obligatoire)
3. **L'état du PHAR** (vérification nécessaire)
4. **Les nouvelles fonctionnalités** (PHP 8.x, types de retour)

**Estimation du travail** :
- Corrections critiques : 4-8 heures
- Améliorations : 8-16 heures
- Révision complète : 16-32 heures

**Priorité** : HAUTE - La documentation actuelle peut induire en erreur les nouveaux utilisateurs sur les namespaces et les prérequis.

