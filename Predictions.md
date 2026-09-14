# MiniTP4 — Prédictions

## Étape 1

| Prédiction | Votre nombre | Pourquoi (une phrase) |
|---|---|---|
| P1 — Au premier affichage de l'écran, combien de lignes RECOMP au Logcat ? | 1 | ProduitCard n'est appelée qu'une seule fois depuis onCreate. |
| P2 — Une fois le TODO A fait : combien de NOUVELLES lignes RECOMP après 3 clics sur « Ajouter 1 kg » ? | 3 | Le composable se rafraîchit (recomposition) à chaque changement d'état déclenché par le clic. |

## Étape 2 — Observation au Logcat (TODO A)

| Prédiction | Observé                               | Écart + explication                                                                                                                                                                                                                                                                                                              |
|---|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| P1 | 1 ligne RECOMP                        | Aucun écart                                                                                                                                                                                                                                                                                                                      | |
| P2 | 0 nouvelle ligne RECOMP après 3 clics | Au clic, Compose ne recompose que la portée interne et pas la fonction `ProduitCard` donc le log ne se redéclenche jamais.| |

**Question de contrôle :** sans `remember`, `mutableStateOf(0)` serait ré-exécuté à chaque recomposition, recréant un état neuf initialisé à 0 — l'incrément serait donc immédiatement perdu et le compteur resterait bloqué à 0 malgré les clics.
