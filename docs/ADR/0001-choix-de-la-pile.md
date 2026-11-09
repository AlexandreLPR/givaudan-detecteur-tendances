# ADR 0001 — Choix de la pile technique

- **Statut :** Accepté
- **Date :** 2026-11-09
- **Décideurs :** Équipe (tech lead : ...)

## Contexte

Nous devons livrer, dans le temps du challenge, un prototype crédible d'outil de détection de tendances alimentaires et olfactives pour Givaudan, plus une vidéo de 2 minutes. Le prototype n'a pas besoin d'être entièrement fonctionnel, mais il doit montrer comment la solution détecte, analyse et priorise les tendances, et distinguer un buzz d'une tendance durable.

Contraintes : délai très court, équipe réduite, données fiables et diversifiées, respect du RGPD, limitation des biais.

## Décision

**Prototype**
- Front : React + Tailwind, généré et itéré avec Lovable (ou Base44)
- Graphiques : Recharts ; carte : Mapbox ou deck.gl
- Données : jeux simulés réalistes en JSON (cas de référence : Dubai Chocolate)
- IA : API Claude pour l'extraction, le scoring expliqué et la justification « suivre / attendre »
- Hébergement : celui de l'outil de génération (lien public pour la slide 05)

**Architecture cible (présentée en slide 08, non construite)**
- Ingestion : API sociales / agrégateurs, Google Trends, GDELT, brevets (EPO, Lens.org), données de consommation ; orchestration Airflow
- Stockage : entrepôt BigQuery ou Snowflake, PostgreSQL + pgvector
- ML : embeddings multilingues + clustering (BERTopic), prévision de séries temporelles, score d'innovation explicable
- Application : FastAPI + Next.js, SSO, cloud en région UE

## Alternatives écartées

- **Développement complet from scratch (FastAPI + Next.js) dès le prototype** : trop long pour le délai.
- **Maquette Figma seule** : moins crédible, aucune IA réelle à montrer.
- **Scraping direct des réseaux sociaux** : contraire aux CGU et risqué au regard du RGPD.

## Conséquences

- (+) Prototype rapide à produire, IA réelle sur des données simulées.
- (+) Architecture cible claire pour les slides Technologies et Faisabilité.
- (−) Les données du prototype sont simulées : à dire clairement pendant la démo.
- (−) Dépendance à un outil no-code pour le front du prototype.
