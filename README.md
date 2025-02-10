# Welcome to GitHub Desktop!
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pemesanan Tiket Bioskop</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        input, button {
            margin: 10px;
            padding: 10px;
            font-size: 16px;
        }
        #result {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h2>Sistem Pemesanan Tiket Bioskop</h2>
    <label for="usia">Masukkan Usia Anda:</label>
    <input type="number" id="usia" placeholder="Masukkan usia">
    <button onclick="cekHargaTiket()">Cek Harga Tiket</button>
    <p id="result"></p>

    <script>
        function cekHargaTiket() {
            let usia = document.getElementById("usia").value;
            let harga = "";

            if (usia < 5) {
                harga = "Gratis!";
            } else if (usia >= 5 && usia <= 12) {
                harga = "Rp20.000";
            } else if (usia >= 13 && usia <= 17) {
                harga = "Rp30.000";
            } else if (usia >= 18 && usia <= 59) {
                harga = "Rp50.000";
            } else if (usia >= 60) {
                harga = "Rp25.000 (Diskon 50%)";
            } else {
                harga = "Masukkan usia yang valid!";
            }

            document.getElementById("result").innerText = "Harga tiket Anda: " + harga;
        }
    </script>
</body>
</html>
