<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Historia Nicków Minecraft z NameMC</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 50px;
        }
        input {
            padding: 10px;
            font-size: 16px;
            margin-bottom: 10px;
            width: 300px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            margin-bottom: 20px;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background-color: #f0f0f0;
            margin: 5px 0;
            padding: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>Historia Nicków Minecraft z NameMC</h1>
    <input type="text" id="nickname" placeholder="Wpisz nick gracza">
    <button onclick="getNickHistory()">Pokaż historię</button>

    <h2>Historia:</h2>
    <ul id="history-list"></ul>

    <script>
        async function getNickHistory() {
            const nickname = document.getElementById('nickname').value.trim();
            const historyList = document.getElementById('history-list');
            historyList.innerHTML = ''; // Czyszczenie listy przed nowym wyszukaniem

            if (!nickname) {
                alert("Proszę wpisać nick!");
                return;
            }

            try {
                // Użycie proxy do ominięcia problemu CORS
                const proxyUrl = "https://cors-anywhere.herokuapp.com/";
                const url = `${proxyUrl}https://pl.namemc.com/profile/${nickname}`;

                const response = await fetch(url);
                if (!response.ok) {
                    throw new Error("Nie znaleziono gracza lub błąd serwera.");
                }
                
                const html = await response.text();
                const parser = new DOMParser();
                const doc = parser.parseFromString(html, 'text/html');
                
                // Pobieranie historii nicków ze strony
                const nicknameElements = doc.querySelectorAll('.card-body .row .col-12 a');
                
                if (nicknameElements.length === 0) {
                    historyList.innerHTML = '<li>Brak historii nicków dla tego gracza.</li>';
                    return;
                }

                nicknameElements.forEach(element => {
                    const li = document.createElement('li');
                    li.textContent = element.textContent.trim();
                    historyList.appendChild(li);
                });
                
            } catch (error) {
                console.error(error);
                alert("Wystąpił błąd podczas pobierania danych.");
            }
        }
    </script>

</body>
</html>
