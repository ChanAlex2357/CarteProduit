ITUNIVERSITY — MODULE M1 · SÉANCE 4
Jetpack Compose :
l’UI comme fonction de l’état
Composables, état, recomposition
Mini-TP « Faire vivre un écran »
Kit pédagogique —Séance 4 —version M1

XML vs Jetpack Compose : la même carte produit
XML + ACTIVITY — 2 langages, 2 fichiers JETPACK COMPOSE — 1 langage, 1 fonction
<!-- res/layout/produit_card.xml --> @Composable
<LinearLayout android:orientation="vertical"> fun ProduitCard(produit: Produit) {
<TextView android:id="@+id/tvNom" .../> Column(Modifier.padding(16.dp)) {
<TextView android:id="@+id/tvPrix" .../> Text(
</LinearLayout> produit.nom,
style = MaterialTheme
// ProduitActivity.kt .typography.titleMedium
val tvNom = )
findViewById<TextView>(R.id.tvNom) Text(produit.prixKg
val tvPrix = ?.let { "$it Ar/kg" }
findViewById<TextView>(R.id.tvPrix) ?: "prix non fixé")
tvNom.text = produit.nom }
tvPrix.text = formatPrix(produit.prixKg) }
// état modifié ? → recomposition AUTOMATIQUE
// donnée modifiée ? → resynchroniser
// chaque vue À LA MAIN
On ne décrit plus comment mettre l’écran à jour — on déclare ce que l’écran doit être : l’UI est une fonction de
l’état.

Le paradigme : décrire l’écran, pas les mises à jour
1 Un écran = une fonction 2 L’état change → recomposition 3 Un bug disparaît par construction
Annotée @Composable : elle reçoit des données Compose rappelle la fonction. Pas de L’« écran pas à jour », classe de bugs la plus
et décrit l’interface pour ces données-là. findViewById, pas de setText — pas d’oubli fréquente de l’Android historique, ne peut plus
possible. exister.
« L’interface est une photographie de l’état. L’état change ? On reprend la photo. »

Les briques : composables, conteneurs, Modifier
La carte produit — du Kotlin, rien d’autre Le Modifier — la chaîne de personnalisation
@Composable Modifier
fun ProduitCard(produit: Produit) { .padding(16.dp) // espace
Card(Modifier.padding(16.dp)) { .fillMaxWidth() // largeur
Column(Modifier.padding(16.dp)) { .clickable { ... } // réagir au clic
Text(
produit.nom, // L’ORDRE COMPTE :
style = MaterialTheme // padding puis clickable
.typography.titleLarge // ≠ clickable puis padding
) // (la zone cliquable change)
Text(produit.prixKg
?.let { "$it Ar/kg" }
?: "prix non fixé")
}
}
}
La null safety de la séance 1 traverse jusque dans l’interface : un prix null ne peut pas s’afficher par accident.

Le Modifier en action : une chaîne, un rendu
ProduitCard — la chaîne complète Ce que ça donne à l’écran
@Composable
fun ProduitCard(p: Produit, onClick: () -> Unit) {
2
Card( 5
modifier = Modifier Vanille Bourbon 18,5 kg
.fillMaxWidth() 1
250 000 Ar / kg
.padding(horizontal = 16.dp, 2
vertical = 8.dp)
.clickable { onClick() }, 3 4
) {
Column(Modifier.padding(16.dp)) { 4
Row(Modifier.fillMaxWidth()) {
Text(p.nom,
modifier = Modifier.weight(1f), 5
1
fillMaxWidth — la carte occupe toute la largeur
style = titleLarge)
Text("${p.stockKg} kg") 2 padding (extérieur) — l’espace entre la carte et le bord de
l’écran
}
Text(p.prixKg?.let { "$it Ar/kg" } 3
clickable — la carte réagit au toucher
?: "prix non fixé")
} 4 padding (intérieur) — l’espace entre le bord de la carte et le
texte
}
} 5 weight(1f) — le titre prend la place restante → le stock est poussé à
droite
L’ORDRE COMPTE : padding AVANT clickable → la marge n’est pas cliquable · padding APRÈS clickable → la marge le devient. Chaque maillon enveloppe le précédent.

L’état : remember + mutableStateOf
Le compteur du mini-TP
Les trois morceaux
@Composable
• mutableStateOf(0) : un état OBSERVABLE — Compose sait
fun ProduitCard(produit: Produit) {
qui en dépend
Log.i("RECOMP", "ProduitCard se (re)compose")
• remember : survit aux recompositions (sans lui : retour à 0
var quantite by remember { mutableStateOf(0) }
à chaque fois)
• by : délégation Kotlin — se lit et s’écrit comme une
Column {
Text("Quantité : $quantite kg") variable
Button(onClick = { quantite++ }) {
Text("Ajouter 1 kg")
}
}
}
remember survit aux recompositions —pas à la rotation (séance 3). La vraie survie a un nom : ViewModel, séance 6.

Les listes : LazyColumn
Mille produits, le prix de dix
À retenir
@Composable
• « Lazy » : seuls les éléments visibles sont composés
fun ListeProduits(produits: List<Produit>) {
LazyColumn {
• items(...) : un composable par élément
items(produits) { p ->
• ProduitCard réutilisée telle quelle — la composition, c’est
ProduitCard(p) // réutilisée !
aussi la réutilisation
}
}
• Séance 5 : cette liste devient cliquable → écran de détail
}

Lire un layout XML
activity_main.xml — à savoir LIRE
Table de correspondance mentale
<LinearLayout
| • LinearLayout vertical  |     | Column · horizontal  | Row |
| ------------------------ | --- | -------------------- | --- |
android:orientation="vertical"
android:layout_width="match_parent"
| • TextView  | Text · Button  | Button |     |
| ----------- | -------------- | ------ | --- |
android:layout_height="match_parent">
| • RecyclerView  | LazyColumn |     |     |
| --------------- | ---------- | --- | --- |
<TextView
| • android:id + findViewById  |     | (plus besoin : la fonction reçoit ses  |     |
| ---------------------------- | --- | -------------------------------------- | --- |
android:id="@+id/tvNom"
données)
android:layout_width="wrap_content"
| • match_parent  | fillMaxWidth / fillMaxSize |     |     |
| --------------- | -------------------------- | --- | --- |
android:layout_height="wrap_content"/>
<Button android:id="@+id/btnAjouter" .../>
</LinearLayout>
On ne l’écrit plus —on sait le lire. Et vous l’avez déjà lu : c’est le layout de CycleDeVie, séance 3.

Mini-TP 4 · « Faire vivre un écran »
1 Lire et prédire
Lire MainActivity.kt (carte statique, log RECOMP en place) ; prédire sur la feuille : lignes RECOMP au démarrage, puis après 3 clics.
2 TODO A — le compteur
remember + mutableStateOf + Button. Exécuter, cliquer 3 fois, compter les RECOMP au Logcat, expliquer l’écart.
3 TODO B — la carte sélectionnable
Second état booléen, Modifier.clickable, couleur qui change. La capture du Logcat prouve la recomposition.
4 Voie ouverte — juger une variante
UNE variante de mise en page demandée à l’IA ; en 3 lignes : laquelle garder, et pourquoi.
Dépôt en fin de séance : formulaire « S4 · Dépôt des livrables » —feuille, capture RECOMP, projet ZIP, jugement en 3 lignes.