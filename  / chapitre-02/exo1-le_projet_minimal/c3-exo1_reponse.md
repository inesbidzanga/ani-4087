




# Importe toutes les fonctions du DSL Jenga (workspace, project, files...)
from Jenga import *

# L'espace de travail est obligatoire, même avec un seul projet.
# Sans lui : "No .jenga workspace file found".
with workspace("MaSalleWks", location="."):
    # Les deux configurations. Ne jamais mesurer les performances en Debug.
    configurations(["Debug", "Release"])

    # Le projet : la chose que Jenga construit
    with project("MaSalle"):
        windowedapp()        # exécutable à fenêtre, sans console derrière
        language("C++")
        cppdialect("C++17")
        location(".")        # le projet vit à la racine

        # "**" descend dans tous les sous-dossiers de src/ ("*" seul non)
        files(["src/**.cpp"])

        # Les variables %{cfg.buildcfg} et %{cfg.system} évitent que
        # Debug et Release écrivent au même endroit et se mélangent.
        targetdir("bin/%{cfg.buildcfg}-%{cfg.system}")  # exécutable final
        objdir("obj/%{cfg.buildcfg}-%{cfg.system}")     # fichiers objets

        # Pas de links() ni de dependson() ici : aucune bibliothèque
        # n'est nécessaire pour cet exercice.
        # (links = bibliothèque qui existe déjà, dependson = projet que
        # Jenga construit lui-même avant le mien.)