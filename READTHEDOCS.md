# Configuration ReadTheDocs pour atoum-documentation

## Structure multi-langue

La documentation atoum est disponible en plusieurs langues :
- **English** (`/en/`) - Documentation principale
- **Français** (`/fr/`) - Documentation française

## Configuration locale

Pour générer la documentation localement :

### Prérequis

```bash
pip install -r requirements.txt
```

### Build English

```bash
sphinx-build -b html source/en build/en/html
```

### Build French

```bash
sphinx-build -b html source/fr build/fr/html
```

## Configuration ReadTheDocs

### Fichiers de configuration

- `.readthedocs.yaml` - Configuration principale ReadTheDocs
- `requirements.txt` - Dépendances Python/Sphinx
- `source/en/conf.py` - Configuration Sphinx EN
- `source/fr/conf.py` - Configuration Sphinx FR

### Multi-version

ReadTheDocs générera automatiquement :
- Dernière version stable (depuis master)
- Versions tagguées (si tags git présents)

## Liens

- **Documentation principale** : http://docs.atoum.org/
- **ReadTheDocs dashboard** : https://readthedocs.org/projects/atoum/

