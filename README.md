<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Historia Nicków Minecraft</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f5f5f5;
        }
        input {
            padding: 10px;
            font-size: 16px;
            margin-bottom: 20px;
            width: 300px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

    <h1>Historia Nicków Minecraft</h1>
    <input type="text" id="nickname" placeholder="Wpisz nick gracza">
    <button onclick="redirectToNameMC()">Pokaż historię</button>

    <script>
        function redirectToNameMC() {
            const nickname = document.getElementById('nickname').value.trim();
            if (nickname) {
                const url = `https://pl.namemc.com/profile/${nickname}`;
                window.open(url, '_blank');
            } else {
                alert("Proszę wpisać nick!");
            }
        }
    </script>

</body>
</html>
