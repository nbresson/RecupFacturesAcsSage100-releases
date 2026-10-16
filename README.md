# RecupFacturesAcsSage100

Rattache les factures PDF exportées de **Sage Automatisation Comptable (ACS)** aux écritures correspondantes d'une
base **Sage 100 Comptabilité** (SQL Server), pour que le PDF reste consultable depuis Sage sans dépendre du SaaS ACS.

Ce dépôt ne contient que les **versions publiées** de l'application (onglet *Releases*).

## Prérequis sur le poste

- Windows 10 ou 11.
- Sage 100 Comptabilité (SQL) avec les **Objets Métiers** installés (`objets100c.dll`, 32 bits) : testé en v12.25.
- Accès à l'instance SQL Server de la société en authentification Windows.
- Un utilisateur Sage autorisé à modifier les écritures.
- Pour le mode FileStream : FILESTREAM activé sur l'instance et la FileTable `DocumentFiles` présente dans la base.

Aucun runtime .NET à installer : l'application est autonome (x86).

## Installation

1. Télécharger `RecupFacturesAcsSage100-<version>-win-x86.zip` dans la dernière release.
2. Facultatif : vérifier l'empreinte avec `Get-FileHash <fichier>.zip` et la comparer au fichier `.sha256`.
3. Clic droit sur le ZIP > Propriétés > cocher **Débloquer**, puis extraire dans un dossier (par exemple
   `C:\Outils\RecupFacturesAcsSage100`).
4. Lancer `RecupFacturesAcsSage100.App.exe`.

Mise à jour : remplacer le contenu du dossier. Les paramètres sont conservés dans
`%APPDATA%\RecupFacturesAcsSage100\parametres.json` (mot de passe Sage chiffré pour l'utilisateur Windows, s'il a été
mémorisé).

## Utilisation

1. Choisir le fichier `.mae` de la société et saisir l'utilisateur Sage ; tester la connexion.
2. Choisir un export ACS (`export_aaaa_mm_jj.zip`), un export décompressé, ou un dossier contenant plusieurs ZIP.
3. Choisir le mode de stockage :
   - **Multimédia** : le PDF est copié dans le dossier `Multimedia` de la société et rattaché comme document ;
   - **FileStream** : le PDF est stocké dans la base et le n° de facture devient un lien dans Sage.
4. Analyser, contrôler la prévisualisation (trouvées, ambiguës, introuvables, déjà rattachées), puis rattacher.
5. Consulter le journal et l'exporter en CSV si besoin.

Le lien existant vers la visionneuse ACS est conservé. Une relance ne crée pas de doublon. En traitement d'un dossier
de ZIP, chaque export entièrement traité est déplacé dans un sous-dossier `Traites`.

**Conseil** : faire une sauvegarde de la base avant le premier traitement.

## Signaler un problème

Ouvrir une *issue* en indiquant la version, le mode de stockage et le message affiché. Ne jamais joindre d'export,
de PDF, de base ni de journal contenant des données de la société.
