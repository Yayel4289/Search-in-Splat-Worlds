<!-- markdownlint-disable MD033 -->
<div align="center">

# **ScanDDM**

## Requirements

Avoir un Google Drive avec les images dans un dossiers data.zip à l'intérieur d'un dossier data-zip

## Avancée sur la méthode

Les tests de ScanDDM sont assez concluants, bien que la fonction soit lente et assez peu précise.
On peut cependant modifier les paramètres pour lui donner un temps de recherche plus long ou un nuage de points plus élevé, mais le temps d'exécution augmente alors encore.

## Explication du code

Information par rapport au GPU utilisé ainsi qu'à la version de PyTorch

```python
!nvidia-smi

import sys, torch
print("Python :", sys.version)
print("PyTorch :", torch.__version__, "| CUDA dispo :", torch.cuda.is_available())
if torch.cuda.is_available():
    print("GPU :", torch.cuda.get_device_name(0))
```

Importation de `os` afin de pouvoir gérer la création des dossiers au premier lancement.
Et clone du git de scanDDM (phuselab) qui comprend un code de base utilisé dans l'implémentation.

```python
import os

REPO_DIR = "/content/scanDDM"
if not os.path.exists(REPO_DIR):
    !git clone https://github.com/phuselab/scanDDM.git {REPO_DIR}
else:
    print("Le dépôt est déjà cloné :", REPO_DIR)

%cd {REPO_DIR}
```

Il y a ensuite deux blocs de fichiers d'installation de l'environnement

Ici la connection au drive afin de pouvoir accéder au zip contenant les données.

```python
from google.colab import drive
drive.mount('/content/drive')
!ls "/content/drive/MyDrive"
```

Décompression des fichiers de data.zip vers ./scanDDM/data

```python
!unzip -q "/content/drive/MyDrive/data-zip/data.zip" -d /content/scanDDM/data
```

</div>
