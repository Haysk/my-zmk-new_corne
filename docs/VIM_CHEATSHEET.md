# Workflow PyCharm + IdeaVim — clavier Corne (Graphite / AZERTY)

Objectif : rester au clavier, naviguer en vim, **réduire la souris au minimum**.

---

## 1. Stratégie de navigation (le point clé)

Ton layout est **Graphite** : les touches `h j k l` sont éparpillées, donc le
rolling `hjkl` classique n'est **pas** la bonne approche ici.

➡️ **Navigation = cluster de flèches du layer NUMBER** (maintien pouce gauche
`SPACE`). Il marche *partout* (mode normal, insertion, dialogues PyCharm), ce
que `hjkl` ne fait pas.

| Geste clavier | Effet |
|---|---|
| `NUMBER` + home droite (`←↓↑→`) | déplacement caractère/ligne |
| `NUMBER` + rangée du bas (`Home / PgDn / PgUp / End`) | début/fin ligne, page |
| `NUMBER` + `Ctrl` (home gauche) + flèche | déplacement **par mot** |
| AceJump (`<leader>s`) | saut direct à un point visible à l'écran |

`hjkl` continuent de fonctionner (le clavier envoie les bons caractères), mais
sers-toi des flèches + AceJump pour le gros du déplacement.

---

## 2. Pré-requis PyCharm (à faire une fois)

Installe ces **plugins IDE** (Settings ▸ Plugins ▸ Marketplace), sinon certaines
lignes du `.ideavimrc` resteront inactives :

1. **IdeaVim** (si pas déjà là)
2. **AceJump** + **IdeaVim-EasyMotion** — requis par `easymotion`
   (`<leader>s` / `<leader>w` / `<leader>l`). Les deux sont nécessaires :
   EasyMotion s'appuie sur AceJump et permet `d`/`y`/`c` + saut.
3. **Which-Key** (éditeur *TheBlob42*) — popup d'aide des mappings `<leader>`.
   Cherche `Which-Key` dans le Marketplace. Si bloqué (proxy), télécharge le
   `.zip` depuis plugins.jetbrains.com/plugin/15976-which-key puis
   *Plugins ▸ ⚙️ ▸ Install Plugin from Disk…*

Puis : Settings ▸ Editor ▸ Vim → vérifier que `ideavimrc` est bien pris en
compte. Recharger la config : `:source ~/.ideavimrc` ou redémarrer.

> Astuce conflits : si un raccourci PyCharm capte une touche avant Vim, va dans
> Settings ▸ Editor ▸ Vim ▸ *Handlers* et choisis « IDE » ou « Vim » par touche.

---

## 3. Aide-mémoire des raccourcis (`<leader>` = Espace)

### Sauter à l'écran (remplace le clic)
| Touche | Action |
|---|---|
| `<leader>s` + 1 car. | easymotion : labels sur les occurrences visibles, tape la lettre du label pour sauter |
| `<leader>w` | saut par mot |
| `<leader>l` | saut par ligne |

### Fichiers / onglets / recherche
| Touche | Action |
|---|---|
| `<leader>o` | ouvrir un fichier par nom |
| `<leader>e` | fichiers récents (Switcher) |
| `<leader>E` | emplacements récents |
| `<leader>F` | rechercher dans tout le projet |
| `<leader>;` | Search Everywhere |
| `gt` / `gT` | onglet suivant / précédent |
| `<leader>q` | fermer l'onglet |
| `<C-o>` / `<C-i>` | reculer / avancer dans l'historique du curseur |

### Panneaux d'outils
| Touche | Action |
|---|---|
| `<leader>p` | panneau Projet |
| `<leader>P` | cibler le fichier courant dans l'arbre |
| `<leader>tt` | Terminal |
| `<leader>td` / `<leader>tr` | Debug / Run |
| `<leader>tg` | Git / Commit |
| `<leader>tp` / `<leader>tf` | Problèmes / Résultats de recherche |
| `<leader>z` | masquer tous les panneaux (focus code) |

### Code : navigation / refactor / quick-fix
| Touche | Action |
|---|---|
| `gd` / `gy` / `gi` | déclaration / type / implémentation |
| `gr` / `<leader>u` | usages (fenêtre / popup) |
| `gh` | doc rapide |
| `]e` / `[e` | erreur suivante / précédente |
| `]m` / `[m` | méthode suivante / précédente |
| `<leader>a` | quick-fix / intentions (ampoule) |
| `<leader>cr` | renommer |
| `<leader>cf` / `<leader>co` | reformater / ranger les imports |
| `<leader>cm` / `<leader>cg` | menu Refactor / Generate |
| `<leader>m` / `<leader>M` | poser un bookmark / liste |

### Run / Debug
| Touche | Action |
|---|---|
| `<leader>rr` / `<leader>rd` | Run / Debug |
| `<leader>rc` | Run la classe courante |
| `<leader>rb` | breakpoint sur la ligne |
| `<leader>rs` | Stop |

### Confort
| Touche | Action |
|---|---|
| `jk` / `kj` (insertion) | sortir en mode normal |
| `<leader>h` | enlever le surlignage de recherche |
| `J` / `K` (visuel) | déplacer les lignes sélectionnées |

---

## 4. Progresser : text objects & macros

### Text objects (combine `verbe` + `i/a` + `objet`)
- `ci(`, `ci"`, `cit` (balise), `cia` (argument — plugin argtextobj)
- `dap` paragraphe, `dae`/`yae` tout le fichier (textobj-entire)
- `vi{` sélectionne l'intérieur d'un bloc

### Macros (tu débutes — méthode simple)
1. `qa` : enregistre dans le registre `a`
2. fais ton édition (avec des motions **répétables**, pas avec la souris)
3. `q` : stop
4. `@a` : rejoue · `5@a` : rejoue 5× · `@@` : rejoue la dernière

Conseils macro : commence la ligne par `0` ou `^`, termine par `j` pour passer à
la ligne suivante → la macro devient rejouable en boucle. Préfère `*` / `n` pour
te repositionner plutôt que des déplacements à l'œil.

---

## 5. Proposition firmware (branche `vim-firmware-proposals`)

- **Caps Word** : les **deux pouces Shift ensemble** activent une frappe en
  majuscules continue (`MA_CONSTANTE`) qui se coupe au premier espace. Pratique
  pour les constantes en code, sans tenir Shift.

Idées firmware en réserve (à demander si tu veux les tester) :
- combo Échap sur la home row (compliqué ici car la home row porte les mods) ;
- **mouse keys** : un cluster déplacement souris + clics au clavier (le board
  supporte le pointing) pour les rares cas non atteignables au clavier.
