Ce projet est un lab pratique qui démontre les étapes fondamentales de la création d'un pipeline MLOps complet. Il couvre la structuration du projet, la gestion des dépendances, l'entraînement d'un modèle, l'évaluation, le déploiement en tant qu'API, et la surveillance rudimentaire de la dérive des données.

**Étape 1 : Initialiser la structure du projet**

**Objectif :** Créer une architecture de dossiers organisée pour le projet MLOps ,une structure bien organisée facilite la maintenance, le versionnement des modèles et la collaboration en équipe.

- Crée un dossier de travail mlops-lab-01

<img width="1919" height="792" alt="image" src="https://github.com/user-attachments/assets/8a9ad062-5da9-492a-8b66-c31488b9f372" />


- Crée les dossiers suivants :

`data` (Pour les données brutes et prétraitées)

`models` (Pour sauvegarder les modèles entraînés)

`registry` (Pour l'enregistrement et le suivi des modèles/métriques)

`logs` (Pour les journaux d'exécution et de prédiction)

<img width="1911" height="2044" alt="image" src="https://github.com/user-attachments/assets/2d3f4aa8-e062-4900-bffe-9b64245848d9" />


- Crée le fichier identifiant le modèle actif

 `src` (Pour le code source de l'application)

<img width="1884" height="376" alt="image" src="https://github.com/user-attachments/assets/b7000871-ec0f-4874-8d93-4a9843a8bf82" />


- Arborescence

<img width="1541" height="755" alt="image" src="https://github.com/user-attachments/assets/8f5e9d3d-1b97-4676-aec4-e45966eb82af" />


**Étape 2 : Préparer l'environnement Python**

**Objectif :** Isoler l'environnement de développement pour éviter les conflits de dépendances

 Les environnements virtuels garantissent que votre projet fonctionne de manière reproductible sur différentes machines.

- Création d'un environnement virtuel Python (avec PowerShell sur Windows)

<img width="1890" height="287" alt="image" src="https://github.com/user-attachments/assets/f5102e08-a2ca-4628-9734-531203a8ec9d" />


- Mise à jour de pip pour avoir les dernières fonctionnalités

<img width="1874" height="1413" alt="image" src="https://github.com/user-attachments/assets/f9f6460d-bc0d-4e65-ac37-3adebeb6632b" />


- Installation des bibliothèques nécessaires (scikit-learn, Flask, pandas, etc.)

<img width="1892" height="1842" alt="image" src="https://github.com/user-attachments/assets/daa113c0-14fe-49a5-b1da-4f131bde1132" />

**Étape 3 : Génération du dataset**

**Objectif:** Cette étape pour crée le script Python pour générer les données qui seront utilisées pour l'entraînement.

<img width="1892" height="551" alt="image" src="https://github.com/user-attachments/assets/1f8281c2-33bf-4379-9010-2739e6a4eeb7" />


<img width="1900" height="246" alt="image" src="https://github.com/user-attachments/assets/b02af19a-fd1d-4d95-bc75-751b993dc791" />

**Étape 4 : Préparer les données + quality checks**

**Objectif :** Cette étape se concentre sur le prétraitement des données brutes

- Création du fichier `prepare_data.py`

<img width="1900" height="473" alt="image" src="https://github.com/user-attachments/assets/0d6e3b23-10fe-48ce-a091-80a4054c6188" />


- Le script génère le fichier prétraité `data\processed.csv` et les statistiques d'entraînement `registry\train_stats.json`

<img width="1876" height="352" alt="image" src="https://github.com/user-attachments/assets/9441876e-3c81-4979-8cfc-977b3a320a16" />


**Étape 5 : Entraîner, versionner et valider le modèle**

**Objectif:** L'étape d'entraînement du modèle de Machine Learning et sa mise en "production" initiale.

- Création du fichier `train.py`

<img width="1896" height="480" alt="image" src="https://github.com/user-attachments/assets/badf2b42-1d15-4b10-b2f4-378e705bf964" />

- Exécution du script d'entraînement

<img width="1873" height="561" alt="image" src="https://github.com/user-attachments/assets/11d24483-cbb7-4263-97c0-146a743897e2" />


- Les **métriques** du modèle (accuracy, precision, recall, f1) sont affichées.
- Le modèle est sauvegardé .
- Le modèle est **activé** (déployé) comme modèle courant.

**Étape 6 : Inspecter la registry et le modèle courant**

**Objectif :** Cette étape vise à évaluer et potentiellement mettre à jour le modèle actif.

- Création du fichier `evaluate.py`

<img width="1842" height="464" alt="image" src="https://github.com/user-attachments/assets/3cef1f0c-6461-4403-9c97-052a7ff76c06" />


- **Exécution du script d'évaluation :**

<img width="1916" height="695" alt="image" src="https://github.com/user-attachments/assets/34fb5516-58dc-49f9-b84c-13ae59f3c4a9" />

**Étape 7 : Créer une API /predict qui utilise le modèle courant**

**Objectif :** Mise en place d'un service web (API) pour interagir avec le modèle déployé.

- Création du fichier `api.py`
    
    <img width="1899" height="457" alt="image" src="https://github.com/user-attachments/assets/72c1c2e2-76f5-4e4e-9288-58b04b8952b7" />

    

- Lancement de l'API avec Uvicorn (FastAPI)

<img width="1918" height="569" alt="image" src="https://github.com/user-attachments/assets/1bbcb5f1-818a-4b13-8a39-d5b9f29117b2" />



- Consultation de l'API :

<img width="1918" height="569" alt="image" src="https://github.com/user-attachments/assets/bdabcd8e-4dac-40cd-87a8-5816402d48a8" />


<img width="1898" height="1521" alt="image" src="https://github.com/user-attachments/assets/fdc94952-c7ab-4d67-bf6c-7fdeae14a8c7" />


- Deux exemples de requêtes POST ont montrés, retournant une prédiction (`prediction: 1` et  `0`)
<img width="1733" height="999" alt="image" src="https://github.com/user-attachments/assets/ca33d2c5-b650-43fb-9be0-08b57b7aaa5b" />

<img width="1724" height="1174" alt="image" src="https://github.com/user-attachments/assets/4a06b3f0-399b-4423-b99d-79a53ea91b26" />


<img width="1754" height="1248" alt="image" src="https://github.com/user-attachments/assets/89271fb7-7e2d-49fe-bcb2-1cd5ef28a0c6" />


<img width="1736" height="1152" alt="image" src="https://github.com/user-attachments/assets/e2f28449-f3bf-41a5-a813-c3368ee138a6" />


- le fichier des logs

<img width="3065" height="1106" alt="image" src="https://github.com/user-attachments/assets/2f01b184-b379-4dc6-a56d-431c3c26af86" />


**Étape 8 : Détecter une dérive des données via les logs**

**Objectif :** Cette étape simule la surveillance de la dérive (drift) des données de production par rapport aux données d'entraînement.

- Création du fichier `monitor_drift.py`

<img width="1878" height="490" alt="image" src="https://github.com/user-attachments/assets/e6fe09c0-72d1-41a0-b695-13fcca0a4c10" />


- Exécution du script de surveillance

<img width="1905" height="528" alt="image" src="https://github.com/user-attachments/assets/185ee21a-6447-4af2-aef3-49ca84348ec8" />

**Étape 9 : Gérer les versions du modèle et revenir en arrière**

**Objectif:** Réentraînement du modèle après détection de drift et démonstration de la gestion des versions.

- Réentraînement du modèle avec une nouvelle version (`v2`)

<img width="1877" height="511" alt="image" src="https://github.com/user-attachments/assets/19b99d4a-a988-4811-aef1-ec1ba673d205" />

<img width="1875" height="482" alt="image" src="https://github.com/user-attachments/assets/95b45805-e2d2-49cd-82a8-46b726611a62" />

<img width="1857" height="235" alt="image" src="https://github.com/user-attachments/assets/4e12bbc2-730e-4d0d-adad-c05887df80b1" />

