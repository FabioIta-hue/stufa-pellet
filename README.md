<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controllo Stufa</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: url('https://source.unsplash.com/1600x900/?fireplace') no-repeat center center fixed;
            background-size: cover;
            text-align: center;
            padding: 20px;
            color: white;
        }
        .container {
            max-width: 400px;
            margin: auto;
            background: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.5);
        }
        h1, label, p {
            font-size: 20px;
        }
        .button {
            display: block;
            width: 100%;
            padding: 15px;
            margin-top: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 20px;
        }
        .power-button {
            font-size: 24px;
            background-color: #ff4500;
            color: white;
            padding: 20px;
            border-radius: 50px;
            width: 80%;
            margin: auto;
        }
        .blue { background-color: #007BFF; color: white; }
        .gray { background-color: #6C757D; color: white; }
        .slider-container, .input-container {
            margin-top: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container" id="home">
        <h1>Controllo Stufa</h1>
        <button class="button blue" onclick="showScreen('controls')">Controlli Stufa</button>
        <button class="button blue" onclick="showScreen('schedule')">Programmazione</button>
        <button class="button gray" onclick="showScreen('maintenance')">Manutenzione</button>
    </div>
    
    <div class="container" id="controls" style="display: none;">
        <h1>Controlli Stufa</h1>
        <button class="button power-button" id="powerButton" onclick="togglePower()">&#128268; Accendi</button>
        <p>Orario attuale: <span id="currentTime"></span></p>
        <div class="slider-container">
            <label>Temperatura attuale: <span id="currentTemp">20</span>°C</label>
        </div>
        <div class="slider-container">
            <label>Accensione automatica sotto: <span id="autoTemp">10</span>°C</label>
            <input type="range" min="0" max="30" id="tempSlider" value="10" oninput="updateAutoTemp()">
            <input type="checkbox" id="autoToggle"> Attiva accensione automatica
        </div>
        <button class="button gray" onclick="showScreen('home')">Indietro</button>
    </div>
    
    <div class="container" id="schedule" style="display: none;">
        <h1>Programmazione Oraria</h1>
        <p>Aggiungi orari di accensione/spegnimento per ogni giorno della settimana.</p>
        <div id="scheduleList"></div>
        <button class="button blue" onclick="addSchedule()">Aggiungi Programmazione</button>
        <button class="button blue">Copia Programma</button>
        <button class="button blue">Incolla Programma</button>
        <button class="button gray" onclick="showScreen('home')">Indietro</button>
    </div>
    
    <div class="container" id="maintenance" style="display: none;">
        <h1>Manutenzione</h1>
        <p>Ore di funzionamento dall'ultima pulizia: <span id="hoursSinceClean">0</span></p>
        <button class="button blue" onclick="resetCleaningHours()">Eseguito Pulizia</button>
        <p>Ore totali di funzionamento: <span id="totalHours">100</span></p>
        <button class="button gray" onclick="showScreen('home')">Indietro</button>
    </div>

    <script>
        function showScreen(screen) {
            document.getElementById('home').style.display = 'none';
            document.getElementById('controls').style.display = 'none';
            document.getElementById('schedule').style.display = 'none';
            document.getElementById('maintenance').style.display = 'none';
            document.getElementById(screen).style.display = 'block';
        }

        function updateAutoTemp() {
            document.getElementById('autoTemp').innerText = document.getElementById('tempSlider').value;
        }

        function togglePower() {
            let powerButton = document.getElementById('powerButton');
            if (powerButton.innerText.includes('Accendi')) {
                powerButton.innerHTML = "&#128268; Spegni";
                powerButton.style.backgroundColor = "green";
            } else {
                powerButton.innerHTML = "&#128268; Accendi";
                powerButton.style.backgroundColor = "#ff4500";
            }
        }

        function resetCleaningHours() {
            document.getElementById('hoursSinceClean').innerText = "0";
            alert("Ore di funzionamento azzerate");
        }

        function updateClock() {
            let now = new Date();
            let timeString = now.toLocaleTimeString('it-IT');
            document.getElementById('currentTime').innerText = timeString;
        }
        setInterval(updateClock, 1000);
        updateClock();

        function addSchedule() {
            let scheduleList = document.getElementById('scheduleList');
            let newSchedule = document.createElement('div');
            newSchedule.innerHTML = `
                <input type="text" placeholder="Nome Programma" />
                <input type="time" /> - <input type="time" />
                <button onclick="this.parentElement.remove()">Elimina</button>
            `;
            scheduleList.appendChild(newSchedule);
        }
    </script>
</body>
</html>
