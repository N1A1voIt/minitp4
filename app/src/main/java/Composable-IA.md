
@Composable
fun ProduitCard(produit: Produit) {
var quantite by remember { mutableStateOf(0) }
var selectionnee by remember { mutableStateOf(false) }

    Log.i(
        "RECOMP",
        "ProduitCard se (re)compose $quantite ${
            if (selectionnee) "couleur true" else "couleur false"
        }"
    )

    Card(
        modifier = Modifier
            .clickable { selectionnee = !selectionnee }
            .fillMaxWidth()
            .padding(16.dp),
        colors = CardDefaults.cardColors(
            containerColor = if (selectionnee)
                MaterialTheme.colorScheme.primaryContainer
            else
                MaterialTheme.colorScheme.surfaceVariant
        ),
    ) {
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .padding(16.dp),
            horizontalArrangement = Arrangement.SpaceBetween,
            verticalAlignment = Alignment.CenterVertically
        ) {
            Column(
                modifier = Modifier.weight(1f)
            ) {
                Text(
                    produit.nom,
                    style = MaterialTheme.typography.titleLarge
                )

                Text(
                    "Origine : ${produit.origine}",
                    style = MaterialTheme.typography.bodyMedium
                )

                Text(
                    produit.prixKg?.let {
                        "${formatAriary(it)} / kg"
                    } ?: "prix non fixé",
                    style = MaterialTheme.typography.bodyLarge
                )
            }

            Column(
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                Text("Quantité : $quantite kg")

                Button(
                    onClick = { quantite++ }
                ) {
                    Text("Ajouter 1 kg")
                }
            }
        }
    }
}