📌 Description du Projet:
Ce projet vise à entraîner un agent autonome à naviguer dans un environnement 3D simulé sous Unity, dans le but d'atteindre un drapeau cible tout en évitant des obstacles. Le projet a été conçu pour illustrer l’application de l’apprentissage par renforcement profond dans un environnement interactif.

Réalisé par :
Hajar Abdessadek,
Amal Lastak et
Salima Khalil El Bouni

🎯 Objectif
L’objectif principal est d’implémenter et entraîner un agent pour qu’il apprenne à se déplacer intelligemment vers un objectif final en :
évitant les obstacles présents dans son environnement,
choisissant des trajectoires optimales via l’apprentissage automatique,
s’adaptant à des environnements variés.

⚙️Technologies et Outils Utilisés:
Unity ML-Agents : Utilisé comme environnement de simulation 3D et interface pour communiquer avec le modèle d’apprentissage Python.

Python : Langage de programmation utilisé pour coder l'algorithme PPO et gérer l'entraînement.

TensorFlow : Framework de deep learning permettant de construire et d’entraîner les réseaux de neurones de l’agent.

Visual Studio Code : Environnements de développement pour coder, tester et visualiser les performances de l’agent.

🧠 Algorithmes Utilisés
📌 PPO (Proximal Policy Optimization)

Nous avons choisi PPO, un algorithme robuste de policy gradient, pour entraîner notre agent. PPO améliore la stabilité de l’entraînement grâce à une régularisation de la mise à jour de la politique, ce qui permet :

des mises à jour efficaces de la politique,

d’éviter les mises à jour trop agressives (grâce à une fonction de perte "clippée"),

un bon compromis entre exploration et exploitation.

📌 Actor-Critic

Notre architecture repose sur le paradigme Actor-Critic :

Actor : génère les actions à effectuer (politique).

Critic : estime la valeur de l’état (fonction de valeur), permettant à l’Actor de mieux s’ajuster.

L’agent apprend ainsi à améliorer progressivement ses choix d’actions en fonction des retours du Critic.


🎮 Aperçu de l’Environnement de Simulation

L’environnement a été conçu dans Unity afin de simuler un agent qui doit atteindre un drapeau tout en évitant des obstacles.

Espace d'observation (ou état) :
L’agent reçoit des observations sous forme vectorisée (au lieu d’une image), ce qui permet une représentation plus légère et adaptée au traitement par réseau de neurones.

Espace d’action :
Continu, ce qui signifie que les actions ne sont pas limitées à un ensemble discret mais peuvent prendre des valeurs réelles. Cela permet un meilleur contrôle de la navigation.

Forme de l’action :(nombre d'agents, 2)
Dans notre cas, il y a un seul agent actif à chaque étape, donc la forme est (1, 2) (correspondant par exemple aux actions de mouvement selon deux axes).

Système de récompense :

+2 : L’agent atteint la cible (le drapeau).

(1.0 / MaxStep) : Récompense légère à chaque étape pour encourager la progression vers l’objectif.

(1.0 / MaxStep) également en cas de collision avec un mur (aucune pénalité spécifique, mais pas d’incitation à foncer sur les obstacles non plus).

MaxStep : Détermine la durée maximale d’un épisode. Si l’agent n’atteint pas l’objectif avant ce nombre d'étapes, l’environnement se réinitialise.

 
 🔁 Fonctionnement du Modèle


1_L’agent observe l’environnement (positions relatives du drapeau, obstacles…).

2_Il choisit une action (avancer, tourner…) via la politique (Actor).

3_Il reçoit une récompense selon l’impact de son action.

4_Le Critic estime la qualité de l’action.

5_Les poids du réseau sont mis à jour via PPO.

6_Le processus se répète sur plusieurs épisodes jusqu’à convergence.

🛠️ Comment l'exécuter
Créer et activer l'environnement virtuel Python : (version Python utilisée - 3.8.x):

$ python -m venv myvenv

$ myvenv\Scripts\activate

Installer les dépendances : (vérifiez les versions exactes des dépendances dans le fichier requirements.txt )

(myvenv) $ pip install -e ./ml-agents/ml-agents-envs

(myvenv) $ pip install tensorflow

(myvenv) $ pip install keras

(myvenv) $ pip install tensorboardX

Maintenant, pour démarrer le processus de formation, utilisez les commandes suivantes :

(myvenv) $ cd PPO-algo-with-custom-Unity-environment

(myvenv) $ python train.py

Vue de l’environnement simulé avec obstacles et objectif:

![Capture d'écran 2025-06-06 150644](https://github.com/user-attachments/assets/34317cad-3b2c-4855-98d0-cc04ed280dcc)


