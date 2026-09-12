# Remise en route de ASKACC / K-Account / AS-Concept sur Windows moderne pour consultation d’archives comptables

Ce dépôt documente une procédure de diagnostic et de remise en route d’un ancien environnement **ASKACC / K-Account / AS-Concept** sur un poste Windows moderne.

Il s’adresse aux utilisateurs qui disposent déjà légalement de leur logiciel, de leurs données comptables et de leurs supports d’installation.

## Avertissement important

Ce dépôt ne contient :

- aucun fichier propriétaire ;
- aucun exécutable ;
- aucune DLL ;
- aucun OCX ;
- aucune licence ;
- aucune clé d’activation ;
- aucune donnée comptable.

Il ne fournit pas de lien direct de téléchargement vers un installateur AS-Suite / AS-Concept.

L’objectif est uniquement de documenter les problèmes rencontrés et les principes généraux de remise en route.

## Contexte

ASKACC / K-Account est un ancien logiciel comptable lié à l’environnement **AS-Concept / AS-Suite**.

Sur un Windows récent, le programme peut ne plus démarrer, même si le fichier principal `ASKACC.Exe` est encore présent.

Le problème vient souvent de l’environnement technique autour du logiciel :

- runtime Visual Basic 5 ;
- DLL de langue française ;
- composants ActiveX 32 bits ;
- bibliothèques AS-Concept ;
- chemin d’installation attendu ;
- fichiers de configuration historiques.

## Messages d’erreur possibles

Lors d’une remise en route, les erreurs peuvent apparaître dans cet ordre ou dans un ordre différent :

```
MSVBVM50.DLL est introuvable
```

```
The language DLL 'vb5fr.dll' or '409' could not be found
```

```
Erreur d’exécution '-2147221164 (80040154)' :
Classe non enregistrée
```

```text
Erreur d’exécution '50003' :
Erreur inattendue
```

```text
Version incorrecte de la DLL d’exécution
```

```text
Votre version du programme doit être installée correctement
```

Ces messages indiquent généralement que le programme ne retrouve pas son environnement d’origine.

## Chemin d’installation attendu

Dans le cas analysé, ASKACC ne fonctionnait correctement que lorsqu’il était placé dans le chemin historique suivant :

```text
C:\PVJL\ASKACC
```

Un lancement depuis un autre dossier ou un autre lecteur pouvait provoquer le message :

```text
Votre version du programme doit être installée correctement
```

Il est donc important de vérifier que le dossier du programme se trouve bien à cet emplacement.

## Composants techniques fréquents

ASKACC / K-Account est un ancien programme Windows 32 bits développé avec Visual Basic 5.

Il peut dépendre notamment des composants suivants :

```text
MSVBVM50.DLL
VB5FR.DLL
VBA5.DLL
DAO350.DLL
DAO2535.TLB
ASConcept.dll
ASConceptDep.dll
ASConcept320.dll
ChilkatZip2.dll
SSDATB32.OCX
OICFiscalPrinterLib.ocx
MSINET.OCX
MSCHART.OCX
MSFLXGRD.OCX
SYSINFO.OCX
COMDLG32.OCX
THREED32.OCX
TABCTL32.OCX
```

Certains de ces composants doivent être enregistrés dans Windows.

Sur un Windows 64 bits, les composants 32 bits se trouvent généralement dans :

```text
C:\Windows\SysWOW64
```

La version 32 bits de `regsvr32` se trouve également ici :

```text
C:\Windows\SysWOW64\regsvr32.exe
```

## Principe général de remise en route

La remise en route consiste généralement à :

1. sauvegarder intégralement le dossier d’origine ;
2. retrouver l’installateur ou le support d’installation AS-Suite / AS-Concept ;
3. installer ou restaurer les composants Visual Basic 5 et ActiveX 32 bits ;
4. vérifier que le dossier ASKACC est placé dans :

```
C:\PVJL\ASKACC
```

5. vérifier que les fichiers de données et de configuration sont présents ;
6. lancer le programme depuis son dossier réel, avec le bon répertoire courant.

## Exemple de lanceur local

Un simple fichier `.bat` peut aider à lancer le programme depuis le bon dossier :

```bat
@echo off
setlocal
cd /d "%~dp0"
start "" "%~dp0ASKACC.Exe"
```

Ce fichier doit être placé dans :

```text
C:\PVJL\ASKACC
```

## Données comptables

Les données comptables peuvent être présentes dans des fichiers tels que :

```text
.KAC
.DAT
.SYS
.PLA
.INI
```

Ces fichiers peuvent contenir des données sensibles : sociétés, clients, écritures comptables, paramètres internes ou informations liées à la licence.

Ils ne doivent jamais être publiés.

Avant toute intervention, il est recommandé de faire une copie complète du dossier d’origine sur un support séparé.

## Ce qu’il ne faut pas faire

Il est déconseillé de :

- télécharger des DLL ou OCX isolés depuis des sites inconnus ;
- remplacer des composants sans sauvegarde ;
- publier des fichiers propriétaires ;
- publier des fichiers comptables ;
- publier des clés ou licences ;
- publier un fichier `KACCWIN.INI` réel ;
- contourner un mécanisme de licence ou d’activation.

Une mauvaise version d’un composant peut provoquer de nouvelles erreurs, notamment :

```text
Version incorrecte de la DLL d’exécution
```

ou :

```text
Classe non enregistrée
```

## À propos de AS-Suite

Les utilisateurs doivent utiliser leurs propres supports d’installation, sauvegardes ou licences.

Dans le cas documenté, les composants AS-Concept nécessaires provenaient de l’environnement AS-Suite / AS-Concept.

Pour des raisons de licence, ce dépôt ne fournit pas l’installateur et ne donne pas de lien direct de téléchargement.

Les utilisateurs doivent utiliser leurs propres supports d’installation, sauvegardes ou licences.

## Objectif de ce dépôt

Ce dépôt a pour objectif d’aider les utilisateurs à comprendre les causes techniques possibles lorsqu’un ancien environnement ASKACC / K-Account ne démarre plus.

Il peut servir à :

- identifier les erreurs fréquentes ;
- préparer une restauration ;
- vérifier les composants nécessaires ;
- préserver l’accès à d’anciennes données comptables ;
- documenter une démarche de migration ou d’archivage.

## Limites

Cette documentation est fournie à titre informatif.

Elle ne constitue pas un support officiel AS-Concept, K-Account ou ASKACC.

Aucune garantie n’est donnée quant au fonctionnement sur tous les postes Windows.

Toute intervention doit être précédée d’une sauvegarde complète.
```
