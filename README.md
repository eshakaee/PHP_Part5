<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pemesanan Tiket Bioskop</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
            width: 350px;
            text-align: center;
        }
        h2 {
            color: #333;
        }
        input {
            width: 80%;
            padding: 10px;
            margin: 10px 0;
            border: 2px solid #ff758c;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background: #ff758c;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            transition: 0.3s;
        }
        button:hover {
            background: #ff5252;
        }
        #result, #history {
            margin-top: 15px;
            font-weight: bold;
            font-size: 18px;
            color: #333;
        }
        #history {
            text-align: left;
            font-size: 14px;
            color: #555;
            margin-top: 20px;
            max-height: 150px;
            overflow-y: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Sistem Pemesanan Tiket Bioskop</h2>
        <label for="usia">Masukkan Usia Anda:</label>
        <input type="number" id="usia" placeholder="Masukkan usia" min="1">
        <button onclick="cekHargaTiket()">Cek Harga Tiket</button>
        <p id="result"></p>
        <div id="history"><h3>Riwayat Pemesanan</h3><ul id="history-list"></ul></div>
    </div>

    <script>
        function cekHargaTiket() {
            let usia = document.getElementById("usia").value;
            let result = document.getElementById("result");
            let historyList = document.getElementById("history-list");
            
            if (usia === "" || usia <= 0) {
                result.innerText = "Masukkan usia yang valid!";
                result.style.color = "red";
                return;
            }

            let harga = "";
            let hargaAsli = 50000;
            let diskon = 0;
            let hargaDiskon = hargaAsli;

            if (usia < 5) {
                harga = "Gratis!";
            } else if (usia >= 5 && usia <= 12) {
                harga = "Rp20.000";
            } else if (usia >= 13 && usia <= 17) {
                harga = "Rp30.000";
            } else if (usia >= 18 && usia <= 59) {
                harga = "Rp50.000";
            } else {
                diskon = 50; // Diskon 50%
                hargaDiskon = hargaAsli - (hargaAsli * diskon / 100);
                harga = `Rp${hargaAsli.toLocaleString()} (Diskon ${diskon}%) → Rp${hargaDiskon.toLocaleString()}`;
            }
            
            result.innerText = "Harga tiket Anda: " + harga;
            result.style.color = "green";
            
            let newHistoryItem = document.createElement("li");
            newHistoryItem.innerText = `Usia: ${usia} - Harga: ${harga}`;
            historyList.appendChild(newHistoryItem);
        }
    </script>
</body>
</html>
