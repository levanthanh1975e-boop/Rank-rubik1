<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <title>Bảng Xếp Hạng Rubik</title>
    <style>
        body {
            font-family: Arial;
            background: #111;
            color: white;
            text-align: center;
        }
        h1 {
            color: #00ffcc;
        }
        form {
            margin: 20px;
        }
        input {
            padding: 10px;
            margin: 5px;
            border-radius: 5px;
            border: none;
        }
        button {
            padding: 10px 20px;
            background: #00ffcc;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        table {
            margin: auto;
            border-collapse: collapse;
            width: 60%;
        }
        th, td {
            padding: 10px;
            border: 1px solid white;
        }
        th {
            background: #00ffcc;
            color: black;
        }
    </style>
</head>
<body>

<h1>🏆 Bảng Xếp Hạng Rubik Lớp</h1>

<form id="rubikForm">
    <input type="text" id="name" placeholder="Tên người chơi" required>
    <input type="number" id="time" placeholder="Thời gian (giây)" required>
    <button type="submit">Thêm</button>
</form>

<button onclick="resetData()">Reset</button>

<table>
    <thead>
        <tr>
            <th>Rank</th>
            <th>Tên</th>
            <th>Thời gian (s)</th>
        </tr>
    </thead>
    <tbody id="leaderboard"></tbody>
</table>

<script>
    let players = [];

    document.getElementById("rubikForm").addEventListener("submit", function(e) {
        e.preventDefault();

        let name = document.getElementById("name").value;
        let time = parseFloat(document.getElementById("time").value);

        players.push({ name, time });

        updateBoard();

        document.getElementById("rubikForm").reset();
    });

    function updateBoard() {
        players.sort((a, b) => a.time - b.time);

        let table = document.getElementById("leaderboard");
        table.innerHTML = "";

        players.forEach((p, index) => {
            let row = `<tr>
                <td>${index + 1}</td>
                <td>${p.name}</td>
                <td>${p.time}</td>
            </tr>`;
            table.innerHTML += row;
        });
    }

    function resetData() {
        players = [];
        updateBoard();
    }
</script>

</body>
</html>
