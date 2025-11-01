<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bulletin de notes</title>
</head>
<body>
    <h2>Entrer les informations de l'étudiant</h2>

    <form method="POST">
        <label>Nom de l'étudiant :</label><br>
        <input type="text" name="nom_etudiant" required><br><br>

        <label>Notes (sur 20) :</label><br>
        <input type="number" name="note1" min="0" max="20" step="0.1" required>
        <input type="number" name="note2" min="0" max="20" step="0.1" required>
        <input type="number" name="note3" min="0" max="20" step="0.1" required>
        <input type="number" name="note4" min="0" max="20" step="0.1" required>
        <input type="number" name="note5" min="0" max="20" step="0.1" required><br><br>

        <input type="submit" value="Afficher le bulletin">
    </form>

    <hr>

    <?php
        // Exécution seulement après soumission du formulaire
        if ($_SERVER["REQUEST_METHOD"] == "POST") {

            // Récupération du nom et des notes
            $nom_etudiant = htmlspecialchars($_POST["nom_etudiant"]);
            $notes = array(
                $_POST["note1"],
                $_POST["note2"],
                $_POST["note3"],
                $_POST["note4"],
                $_POST["note5"]
            );

            // Calcul de la moyenne
            $somme_notes = 0;
            $nombre_notes = count($notes);

            for($i = 0; $i < $nombre_notes; $i++) {
                $somme_notes += $notes[$i];
            }

            $moyenne = $somme_notes / $nombre_notes;

            // Affichage des résultats
            echo "<h2>Bulletin de $nom_etudiant</h2>";

            echo "<h3>Notes obtenues :</h3>";
            echo "<ul>";
            foreach($notes as $note) {
                echo "<li>$note / 20</li>";
            }
            echo "</ul>";

            // Condition pour déterminer si l'étudiant a réussi
            echo "<h3>Résultat :</h3>";
            echo "<p>Moyenne : " . number_format($moyenne, 2) . "/20</p>";

            if($moyenne >= 10) {
                echo "<p style='color: green;'>✅ Félicitations ! Vous êtes admis.</p>";
            } else {
                echo "<p style='color: red;'>❌ Malheureusement, vous devez repasser l'examen.</p>";
            }

            // Vérification de la mention
            if($moyenne >= 16) {
                echo "<p>🌟 Mention : Très Bien</p>";
            } elseif($moyenne >= 14) {
                echo "<p>⭐ Mention : Bien</p>";
            } elseif($moyenne >= 12) {
                echo "<p>👍 Mention : Assez Bien</p>";
            } elseif($moyenne >= 10) {
                echo "<p>🙄 Mention : Passable</p>";
            } elseif($moyenne >= 5) {
                echo "<p>😡 Mention : Néant</p>";
            }
        }
    ?>
</body>
</html>
