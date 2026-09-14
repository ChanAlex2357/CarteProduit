ITUniversity — Module M1 · Développement mobile Kotlin — Séance 4

**MINI-TP 4 — JETPACK COMPOSE**

« Faire vivre un écran »

*État, remember, recomposition — travail individuel, sur le projet fourni « CarteProduit »*

# 1. Objectifs

* Prédire puis observer la recomposition — la voir se produire, log à l'appui.
* Ajouter un état avec remember + mutableStateOf (le compteur de quantité).
* Rendre un composable réactif au clic (la carte sélectionnable).
* Porter un jugement de conception sur une variante proposée par l'IA.

# 2. Règles du mini-TP

1. Les prédictions se remplissent dans le modèle de l'étape 1 AVANT tout lancement de l'application : lire, prédire, puis seulement exécuter.
2. Pendant les étapes 1 à 3, aucune assistance IA — complétion IA de l’IDE désactivée.
3. Le log RECOMP est déjà en place dans le projet : ne le déplacez pas, il est votre instrument de mesure.

**ÉTAPE 1 — LIRE ET PRÉDIRE (SUR PAPIER, AVANT TOUT LANCEMENT)**

Téléchargez MiniTP4\_CarteProduit.zip depuis le dossier Drive de la séance, décompressez-le, ouvrez le projet dans Android Studio (File → Open) et LISEZ MainActivity.kt — la carte statique, le log RECOMP, les deux TODO en commentaire. Puis remplissez le modèle :

| **Prédiction** | **Votre nombre** | **Pourquoi (une phrase)** |
| --- | --- | --- |
| **P1 — Au premier affichage de l’écran, combien de lignes RECOMP au Logcat ?** |  |  |
| **P2 — Une fois le TODO A fait : combien de NOUVELLES lignes RECOMP après 3 clics sur « Ajouter 1 kg » ?** |  |  |

Ne lancez rien avant d'avoir rempli les deux lignes du modèle.

**ÉTAPE 2 — TODO A : LE COMPTEUR DE QUANTITÉ**

1. Suivez le commentaire TODO A du fichier : déclarez l'état (remember + mutableStateOf), puis branchez le Text et le Button. Le modèle exact est sur la diapositive « L'état » du cours.
2. Lancez l'application, filtrez le Logcat avec : tag:RECOMP
3. Vérifiez votre prédiction P1 (lignes au démarrage), puis cliquez 3 fois sur « Ajouter 1 kg » et vérifiez P2. Notez les écarts et leur explication au dos de la feuille.

**Question de contrôle (une phrase au dos de la feuille) :** retirez mentalement le remember (sans le faire) — que deviendrait le compteur à chaque clic, et pourquoi ?

**ÉTAPE 3 — TODO B : LA CARTE SÉLECTIONNABLE**

1. Suivez le commentaire TODO B : un second état booléen, Modifier.clickable, et la couleur de la carte qui change selon l'état.
2. Vérifiez : un clic sur la carte change sa couleur ET produit une ligne RECOMP. Capturez le Logcat montrant vos recompositions (démarrage + clics) : cette capture est un livrable.

**Observation bonus :** tournez l’écran. Que deviennent la quantité et la sélection — et quelle séance du module l’avait annoncé ?

**VOIE OUVERTE — UNE TÂCHE IA UNIQUE : JUGER UNE VARIANTE**

1. Demandez à l'IA de votre choix UNE variante de mise en page de votre carte. Prompt suggéré : « Voici un composable Kotlin. Propose UNE variante de mise en page (par exemple en Row), sans ajouter de fonctionnalité. » (collez votre ProduitCard).
2. Comparez les deux versions et rendez votre jugement en trois lignes : laquelle garder, et pourquoi — lisibilité du code, cohérence visuelle, simplicité. Vous recopierez ce jugement dans le champ « JOURNAL-IA » du formulaire de dépôt. Garder SA version avec de bonnes raisons est un résultat parfaitement valable.

# 3. Livrables (formulaire « S4 · Dépôt des livrables »)

Tout se dépose en fin de séance dans le formulaire unique « S4 · Dépôt des livrables » — le lien est affiché en séance et dans le dossier Drive de la séance :

* cette feuille remplie (modèle de prédictions, écarts, question de contrôle, observation bonus), en photo ou PDF ;
* la capture du Logcat filtré sur RECOMP (démarrage + clics) ;
* le projet avec les deux TODO aboutis, en URL Git
* votre jugement en trois lignes sur la variante, recopié dans le champ « JOURNAL-IA » du formulaire.

Ces dépôts servent au suivi de votre progression. Les modalités d'évaluation du module vous seront précisées ultérieurement.