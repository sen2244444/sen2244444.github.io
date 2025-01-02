<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Masukkan Nama</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #f4f4f4;
            padding: 20px;
        }

        h1 {
            color: #333;
        }

        .pembuka {
            font-size: 20px;
            color: #555;
            margin-bottom: 30px;
        }

        .pilihan-container {
            margin-top: 20px;
            font-size: 18px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
            margin: 10px;
        }

        button:hover {
            background-color: #45a049;
        }

        .hasil {
            font-size: 24px;
            margin-top: 20px;
            font-weight: bold;
        }

        input {
            padding: 10px;
            font-size: 16px;
            margin: 10px;
            width: 200px;
            border-radius: 5px;
            border: 2px solid #ccc;
        }

        .container {
            display: none; /* Default hidden, will show when "ya" is clicked */
        }

        .quotes {
            font-size: 18px;
            margin-top: 20px;
            color: #333;
        }
    </style>
</head>
<body>

    <!-- Menambahkan tulisan di awal halaman -->
    <div class="pembuka">
        <h2>Apakah kamu penasaran pesan yang ingin aku sampaikan?</h2>
    </div>

    <!-- Pilihan Ya atau Tidak -->
    <div class="pilihan-container">
        <button onclick="pilihYa()">Ya</button>
        <button onclick="pilihTidak()">Tidak</button>
    </div>

    <!-- Formulir Input Nama (Disembunyikan sampai "Ya" dipilih) -->
    <div class="container">
        <h1>Masukkan Nama Anda</h1>
        <input type="text" id="namaInput" placeholder="Masukkan nama">
        <button onclick="cekNama()">Kirim</button>

        <div class="hasil" id="hasil"></div>
    </div>

    <!-- Gambar Bunga (Ditampilkan jika "Tidak" dipilih) -->
    <div id="gambarBunga" style="display:none;">
        <img src="https://www.example.com/flower-image.jpg" alt="Bunga" class="gambar-bunga">
    </div>

    <script>
        function pilihYa() {
            // Menyembunyikan pilihan dan menampilkan form input nama
            document.querySelector('.pilihan-container').style.display = 'none';
            document.querySelector('.container').style.display = 'block';
        }

        function pilihTidak() {
            // Menyembunyikan pilihan dan menampilkan gambar bunga
            document.querySelector('.pilihan-container').style.display = 'none';
            document.getElementById('gambarBunga').style.display = 'block';
        }

        function cekNama() {
            // Ambil nilai nama dari input
            const nama = document.getElementById('namaInput').value.trim().toLowerCase();
            const hasilDiv = document.getElementById('hasil');

            // Cek apakah nama yang dimasukkan "hardi"
            if (nama === 'hardi') {
                hasilDiv.textContent = 'hi mbul,hehehe uda lama ya aku ga manggil kamu dengan sebutan ini jujur aku kangen sifat kamu awal kita kenal gapernah nyuekin aku yaa mungkin ini semua jg salah ku tidak pernah ngertiin perasaan mu ,maafin aku selama ini yaa ,,aku bingung gatau mau bilang gmna tpi setiap aku coba hubungan baru aku selalu pengen gtu klo itu kamu hehehe,tpi aku malu bilang ke kamu klo ka u baca pesan inii ..';
                hasilDiv.style.color = 'green'; // Tulisan warna hijau untuk "Kangennnn"
            } else {
                // Jika nama selain "Hardi", tampilkan quotes acak
                const quotes = [
                    "Jangan pernah menyerah, karena kegagalan adalah langkah menuju kesuksesan.",
                    "Hidup ini seperti sepeda, untuk menjaga keseimbangan, kita harus terus bergerak.",
                    "Setiap hari adalah kesempatan baru untuk menjadi lebih baik.",
                    "Percayalah pada proses, karena usaha tidak pernah mengkhianati hasil.",
                    "Keberanian bukanlah ketiadaan rasa takut, tetapi kemampuan untuk melangkah meski merasa takut."
                ];

                // Ambil random quote
                const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
                hasilDiv.textContent = randomQuote;
                hasilDiv.style.color = 'blue'; // Tulisan warna biru untuk quotes
            }
        }
    </script>

</body>
</html>
