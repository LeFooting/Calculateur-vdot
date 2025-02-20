<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculateur VDOT</title>
    <script>
        function calculateVDOT() {
            let distanceKm = parseFloat(document.getElementById("distanceKm").value);
            let timeSec = parseFloat(document.getElementById("timeSec").value);
            let targetDist = parseFloat(document.getElementById("targetDist").value);

            if (isNaN(distanceKm) || isNaN(timeSec) || isNaN(targetDist)) {
                document.getElementById("result").innerHTML = "Veuillez remplir tous les champs correctement.";
                return;
            }

            let velocity = distanceKm / (timeSec / 3600); // vitesse en km/h
            let vo2max = 0.182258 * velocity + 0.000104 * Math.pow(velocity, 2); // VO2 max
            let efficiency = 0.2989558 * velocity;
            let vdot = vo2max / efficiency;

            let predictedTime = targetDist / velocity * 3600; // temps estimé en secondes
            let hours = Math.floor(predictedTime / 3600);
            let minutes = Math.floor((predictedTime % 3600) / 60);
            let seconds = Math.round(predictedTime % 60);

            document.getElementById("result").innerHTML = 
                `Temps prédit pour ${targetDist} km : ${hours}h ${minutes}m ${seconds}s`;
        }
    </script>
</head>
<body>
    <h1>Calculateur VDOT</h1>
    <label>Distance de référence (km) :</label>
    <input type="number" id="distanceKm" step="0.01"><br><br>
    <label>Temps de référence (secondes) :</label>
    <input type="number" id="timeSec" step="1"><br><br>
    <label>Distance cible (km) :</label>
    <input type="number" id="targetDist" step="0.01"><br><br>
    <button onclick="calculateVDOT()">Calculer</button>
    <p id="result"></p>
</body>
</html>
