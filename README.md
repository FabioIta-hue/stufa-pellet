<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controllo Stufa</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            text-align: center;
            padding: 20px;
        }
        .container {
            max-width: 400px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        .button {
            display: block;
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .blue { background-color: #007BFF; color: white; }
        .green { background-color: #28A745; color: white; }
        .gray { background-color: #6C757D; color: white; }
        .red { background-color: #DC3545; color: white; }
        .slider-container, .input-container {
            margin-top: 10px;
            text-align: left;
        }
    </style>
</head>
<body>
    <div class="container" id="home">
        <h1>Controllo Stufa</h1>
        <button class="button blue" onclick="showScreen('controls')">Controlli Stufa</button>
        <button class="button green" onclick="showScreen('settings')">Impostazioni</button>
        <button class="button red" onclick="showScreen('maintenance')">Manutenzione</button>
    </div>
    
    <div class="container" id="controls" style="display: none;">
        <h1>Controlli Stufa</h1>
        <p>Ora attuale: <span id="currentTime"></span></p>
        <p>Temperatura attuale: <span id="currentTemp">22</span>°C</p>
        <label>
            <input type="checkbox" id="powerToggle"> Accendi Stufa
        </label>
        <br>
        <label>
            <input type="checkbox" id="fanToggle"> Ventola
        </label>
        <div class="slider-container">
            <label>Temperatura desiderata: <span id="tempValue">20</span>°C</label>
            <input type="range" min="15" max="30" id="tempSlider" value="20" oninput="updateTemp()">
        </div>
        <div class="slider-container">
            <label>Accensione automatica sotto: <span id="autoTemp">18</span>°C</label>
            <input type="range" min="15" max="25" id="autoTempSlider" value="18" oninput="updateAutoTemp()">
        </div>
        <div class="input-container">
            <input type="number" id="timerInput" placeholder="Timer in minuti">
            <button class="button blue" onclick="setTimer()">Imposta Timer</button>
        </div>
        <div class="input-container">
            <label>Accensione programmata:</label>
            <input type="time" id="startTime">
            <label>Spegnimento programmato:</label>
            <input type="time" id="endTime">
            <button class="button blue" onclick="setSchedule()">Imposta Programmazione</button>
        </div>
        <button class="button gray" onclick="showScreen('home')">Indietro</button>
    </div>
    
    <div class="container" id="settings" style="display: none;">
        <h1>Impostazioni</h1>
        <p>Qui puoi aggiungere impostazioni future.</p>
        <button class="button gray" onclick="showScreen('home')">Indietro</button>
    </div>

    <div class="container" id="maintenance" style="display: none;">
        <h1>Manutenzione</h1>
        <p>Ore di funzionamento: <span id="workingHours">120</span></p>
        <p>Ultima pulizia: <span id="lastMaintenance">10 giorni fa</span></p>
        <p>Tempo di funzionamento medio giornaliero: <span id="avgUsage">5 ore</span></p>
        <button class="button gray" onclick="showScreen('home')">Indietro</button>
    </div>

    <script>
        function showScreen(screen) {
            document.getElementById('home').style.display = 'none';
            document.getElementById('controls').style.display = 'none';
            document.getElementById('settings').style.display = 'none';
            document.getElementById('maintenance').style.display = 'none';
            document.getElementById(screen).style.display = 'block';
        }

        function updateTemp() {
            document.getElementById('tempValue').innerText = document.getElementById('tempSlider').value;
        }

        function updateAutoTemp() {
            document.getElementById('autoTemp').innerText = document.getElementById('autoTempSlider').value;
        }

        function setTimer() {
            let timer = document.getElementById('timerInput').value;
            alert("Timer impostato per " + timer + " minuti");
        }

        function setSchedule() {
            let startTime = document.getElementById('startTime').value;
            let endTime = document.getElementById('endTime').value;
            alert("Programmazione impostata: Accensione alle " + startTime + ", Spegnimento alle " + endTime);
        }

        function updateTime() {
            let now = new Date();
            document.getElementById('currentTime').innerText = now.toLocaleTimeString();
        }

        setInterval(updateTime, 1000);
    </script>
</body>
</html>
