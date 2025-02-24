<?php
session_start();
if (!isset($_SESSION['history'])) {
    $_SESSION['history'] = [];
}

// Hapus riwayat jika tombol ditekan
if (isset($_POST['clear_history'])) {
    $_SESSION['history'] = [];
}
?>

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
        #result {
            margin-top: 15px;
            font-weight: bold;
            font-size: 18px;
            color: #333;
        }
        #history {
            margin-top: 20px;
            text-align: left;
            font-size: 14px;
            color: #555;
            max-height: 150px;
            overflow-y: auto;
            border-top: 1px solid #ccc;
            padding-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Sistem Pemesanan Tiket Bioskop</h2>
        <form method="POST" action="">
            <label for="usia">Masukkan Usia Anda:</label>
            <input type="number" name="usia" id="usia" placeholder="Masukkan usia" min="1" required>
            <button type="submit">Cek Harga Tiket</button>
        </form>
        
        <?php
            if ($_SERVER["REQUEST_METHOD"] == "POST" && !isset($_POST['clear_history'])) {
                $usia = isset($_POST["usia"]) ? (int)$_POST["usia"] : 0;
                $harga = "";
                $hargaAsli = 50000;
                $diskon = 0;
                $hargaDiskon = $hargaAsli;

                if ($usia <= 0) {
                    $harga = "Masukkan usia yang valid!";
                } elseif ($usia < 5) {
                    $harga = "Gratis!";
                } elseif ($usia >= 5 && $usia <= 12) {
                    $harga = "Rp20.000";
                } elseif ($usia >= 13 && $usia <= 17) {
                    $harga = "Rp30.000";
                } elseif ($usia >= 18 && $usia <= 59) {
                    $harga = "Rp50.000";
                } else {
                    $diskon = 50;
                    $hargaDiskon = $hargaAsli - ($hargaAsli * $diskon / 100);
                    $harga = "Rp" . number_format($hargaAsli, 0, ',', '.') . " (Diskon {$diskon}%) → Rp" . number_format($hargaDiskon, 0, ',', '.');
                }
                
                echo "<p id='result' style='color: " . ($usia <= 0 ? 'red' : 'green') . ";'>Harga tiket Anda: $harga</p>";
                
                if ($usia > 0) {
                    $_SESSION['history'][] = "Usia: $usia - Harga: $harga";
                }
            }
        ?>

        <div id="history">
            <h3>Riwayat Pemesanan</h3>
            <ul>
                <?php
                    if (!empty($_SESSION['history'])) {
                        foreach (array_reverse($_SESSION['history']) as $historyItem) {
                            echo "<li>$historyItem</li>";
                        }
                    } else {
                        echo "<li>Belum ada riwayat pemesanan</li>";
                    }
                ?>
            </ul>
            <form method="POST" action="">
                <button type="submit" name="clear_history">Hapus Riwayat</button>
            </form>
        </div>
    </div>
</body>
</html>
