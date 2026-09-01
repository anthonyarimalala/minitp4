Verdict : garder la version Column (originale)

Lisibilité du code : la version Row ajoute un Row avec Arrangement.SpaceBetween et Alignment.CenterVertically, deux paramètres supplémentaires à comprendre, pour un gain nul en clarté par rapport à deux Text/Button simplement empilés.

Cohérence visuelle : la Column garde un alignement vertical homogène avec le reste de la carte (nom, origine, prix), alors que la Row introduit une rupture de rythme (un seul bloc horizontal isolé au milieu d'éléments verticaux) sans réel bénéfice ergonomique — le bouton reste petit et proche du texte dans les deux cas.

Simplicité : la Column est la solution la plus directe pour ce contenu (peu d'éléments, pas de besoin réel d'alignement horizontal étudié), donc à complexité égale de résultat, mieux vaut le code le plus court et le plus prévisible.


@Composable
fun ProduitCard(produit: Produit) {
Log.i("RECOMP", "ProduitCard se (re)compose")

    var selectionnee by remember { mutableStateOf(false) }
    var quantite by remember { mutableStateOf(0) }
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
            .clickable { selectionnee = !selectionnee },
        colors = CardDefaults.cardColors(
            containerColor = if (selectionnee)
                MaterialTheme.colorScheme.primaryContainer
            else MaterialTheme.colorScheme.surfaceVariant
            ),
    ) {
        Column(Modifier.padding(16.dp)) {
            Text(produit.nom, style = MaterialTheme.typography.titleLarge)
            Text(
                "Origine : ${produit.origine}",
                style = MaterialTheme.typography.bodyMedium,
            )
            Text(
                produit.prixKg?.let { "${formatAriary(it)} / kg" } ?: "prix non fixé",
                style = MaterialTheme.typography.bodyLarge,
            )

            Spacer(Modifier.height(12.dp))

            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically,
            ) {
                Text("Quantité : $quantite kg")
                Button(onClick = { quantite++ }) { Text("Ajouter 1 kg") }
            }
        }
    }
}