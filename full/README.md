# Cascade arbre — HMPV Full (EN)

Viewer chronologique reply/quote sur la **cascade anglaise** (composante liée aux ancres du corpus EN).

| | |
| --- | --- |
| Source | `donnees/parquet/cascade_en.parquet` |
| Collecte brute | `parcours/04_cascade_en/posts.jsonl` (~941k lignes) |
| Forêt affichable | ~106k posts · ~35k arbres (après `assign_levels`) |
| Ouverture | servir ce dossier en HTTP (fetch des arbres) |

## Lancer

```bash
# 1) table cascade (si besoin)
py -3.13 code/finalize_cascade_en.py

# 2) index + trees/
py -3.13 code/build_cascade_arbre_full.py

# 3) viewer
cd donnees/cascade_arbre_full
py -3.13 -m http.server 8799 --bind 127.0.0.1
# → http://127.0.0.1:8799/
```

`file://` ne charge pas les `trees/*.json` : un serveur local est requis.

## UX (aligné sur `cascade_arbre/` FR)

- Filtre : originales **isolées (n=1) et RT&lt;10** masquées (~5,1k affichées sur 35k)
- Préchargement agressif des `trees/*.json` dès l’ouverture
- Dézoom jusqu’à ~0.0006 · barre temps fixe · arcs ∝ RT enfant
- **Tout déplier** / **+1 niveau** : tous les arbres filtrés

## Fichiers

| Fichier | Rôle |
| --- | --- |
| `index.html` | Viewer (lazy-load) |
| `index.js` | Métadonnées des racines |
| `trees/<id>.json` | Arbre complet d’une ancre |
| `meta.json` | Effectifs |

Le viewer FR (plus petit, tout en mémoire) reste dans `donnees/cascade_arbre/`.
