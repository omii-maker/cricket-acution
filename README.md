# cricket-acution
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Auction App</title>
    <link rel="stylesheet" href="styles.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f9fa;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: #007bff;
            color: white;
            padding: 10px 0;
        }
        main {
            padding: 20px;
        }
        section {
            background: white;
            padding: 15px;
            margin: 10px auto;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 80%;
        }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            margin-top: 10px;
            border-radius: 5px;
        }
        button:hover {
            background-color: #0056b3;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            padding: 10px;
            border-bottom: 1px solid #ddd;
            cursor: pointer;
        }
        li:hover {
            background-color: #f1f1f1;
        }
    </style>
</head>
<body>
    <header>
        <h1>Cricket Auction</h1>
    </header>

    <main>
        <section id="dashboard">
            <h2>Players List</h2>
            <ul id="players-list"></ul>
            <input type="text" id="player-name-input" placeholder="Enter player name">
            <button id="add-player-btn">Add Player</button>
        </section>

        <section id="auction">
            <h2>Auction</h2>
            <div id="auction-player">
                <h3>Player Name: <span id="player-name">None</span></h3>
                <p>Current Bid: ₹<span id="current-bid">0</span></p>
                <button id="bid-button">Place Bid</button>
            </div>
        </section>

        <section id="captains">
            <h2>Captains</h2>
            <ul id="captains-list"></ul>
            <p>Captain's Budget: ₹<span id="captain-budget">10000</span></p>
        </section>
    </main>

    <footer>
        <p>&copy; 2025 Cricket Auction App</p>
    </footer>

    <script>
        let players = [];
        let currentBid = 0;
        let currentAuctionPlayer = null;
        let captainBudget = 10000;

        document.getElementById("add-player-btn").addEventListener("click", addPlayer);
        document.getElementById("bid-button").addEventListener("click", placeBid);

        function addPlayer() {
            const playerNameInput = document.getElementById("player-name-input");
            const playerName = playerNameInput.value.trim();
            if (playerName) {
                players.push({ name: playerName, price: 0, stats: { runs: 0, wickets: 0 } });
                updatePlayerList();
                playerNameInput.value = "";
            }
        }

        function updatePlayerList() {
            const playersList = document.getElementById("players-list");
            playersList.innerHTML = "";
            players.forEach((player, index) => {
                const li = document.createElement("li");
                li.textContent = `${player.name} - ₹${player.price} (Runs: ${player.stats.runs}, Wickets: ${player.stats.wickets})`;
                li.addEventListener("click", () => startAuction(index));
                playersList.appendChild(li);
            });
        }

        function startAuction(index) {
            currentAuctionPlayer = players[index];
            document.getElementById("player-name").textContent = currentAuctionPlayer.name;
            document.getElementById("current-bid").textContent = currentAuctionPlayer.price;
            currentBid = currentAuctionPlayer.price;
        }

        function placeBid() {
            if (currentAuctionPlayer && captainBudget >= currentBid + 100) {
                currentBid += 100;
                document.getElementById("current-bid").textContent = currentBid;
                currentAuctionPlayer.price = currentBid;
                captainBudget -= 100;
                document.getElementById("captain-budget").textContent = captainBudget;
                updatePlayerList();
            } else {
                alert("Insufficient budget!");
            }
        }
    </script>
</body>
</html>
