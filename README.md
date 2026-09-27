# Étude et déploiement d'une solution IDS : Snort et Suricata

Projet académique de 4A réalisé par **Taher Bazzi et Ahmed Chegueni**, encadré par **Prof. Nader Mbarek**. Le rapport étudie la surveillance d'un réseau de laboratoire et compare qualitativement deux IDS open source.

## Problème et objectif

Un IDS doit voir le trafic pertinent, disposer de règles adaptées et produire des alertes exploitables. Le projet met en place un environnement GNS3 pour observer comment **Snort** et **Suricata** réagissent à des pings, à un envoi intensif de paquets ICMP et à des scans Nmap.

## Architecture du laboratoire

- **GNS3** héberge une topologie comprenant Kali Linux (attaquant), une VM Ubuntu (détecteur), un PC cible, deux routeurs et un switch.
- Le switch utilise une configuration **SPAN** pour recopier le trafic vers le détecteur.
- La configuration Snort adapte `HOME_NET` à `192.168.1.0/24` et ajoute des règles personnalisées dans `local.rules`.
- Suricata est configuré avec `suricata.yaml` et un fichier de règles local.

Le schéma et les captures de configuration sont reproduits dans le [rapport compilé](rapport-IDS.pdf).

## Réalisation et tests documentés

| Étape | Réalisation visible dans le rapport |
| --- | --- |
| Déploiement | Installation et lancement de Snort et Suricata sur Ubuntu ; configuration des fichiers de règles. |
| Capture réseau | Topologie GNS3 et commande SPAN présentées en figures. |
| Scénarios | Ping ICMP, ICMP flood et scans Nmap depuis Kali dans le laboratoire. |
| Observation | Captures d'alertes Snort et Suricata et captures de commandes Nmap/ICMP. |
| Analyse | Comparaison qualitative de la simplicité de Snort et du détail des journaux Suricata. |

Les captures montrent des détections sur les scénarios étudiés. **Aucun taux de détection, débit, mesure CPU/RAM ou banc d'essai quantitatif n'est fourni** : les appréciations de performance du texte sont qualitatives. Le rapport mentionne une « alerte automatisée » dans son introduction, sans en documenter une implémentation distincte ; elle n'est donc pas revendiquée ici comme livrable.

## Limites de la source

La couverture indique **janvier 2024**, alors que des captures affichent **janvier 2026**. Certaines captures utilisent également des sous-réseaux différents des adresses décrites dans le corps du texte. La capture du scan Nmap de Suricata ne suffit pas à confirmer tous les ports énumérés par le texte. Ces écarts figurent dans le rapport original et doivent être clarifiés avec les auteurs avant de présenter les expériences comme une seule campagne reproductible. La bibliographie originale ne fournit que des titres, sans URL ni données bibliographiques complètes.

## Compiler le rapport

Sur **Overleaf** : importer le contenu du dossier, choisir `main.tex` comme document principal et **pdfLaTeX** comme compilateur. Compiler deux fois pour mettre à jour les références et la table des matières.

En local avec une distribution TeX Live :

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

Les chapitres se modifient dans `sections/`. Pour remplacer une capture, conserver son nom dans `images/` ou modifier l'argument correspondant de `\capture` dans la section concernée. Les légendes et renvois sont générés par LaTeX.

## Structure

```text
.
├── main.tex
├── sections/
│   ├── 01-introduction.tex
│   ├── 02-etat-art.tex
│   ├── 03-implementation.tex
│   ├── 04-analyse-conclusion.tex
│   ├── 05-annexes.tex
│   └── 06-bibliographie.tex
├── images/               # Captures extraites du PDF source
├── rapport-IDS.pdf        # Rendu final fourni avec cette archive
├── README.md
└── .gitignore
```

## Publication

Avant une mise en ligne publique, vérifier l'accord de l'autre auteur, les droits d'utilisation des logos et des captures, et les informations éventuellement sensibles visibles dans les terminaux. Une version publique peut omettre les captures concernées et le PDF d'origine, tout en conservant le code LaTeX et les figures autorisées. Aucune licence de réutilisation du contenu n'est présumée.
