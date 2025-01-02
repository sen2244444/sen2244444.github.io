<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Desain dari Gambar</title>
    <style>
        /* Reset margin dan padding untuk elemen umum */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* Pengaturan untuk body */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }

        /* Header yang konsisten di semua perangkat */
        header {
            background-color: #333;
            color: #fff;
            padding: 1rem;
            text-align: center;
        }

        /* Kontainer utama yang responsif */
        .container {
            max-width: 1200px;
            width: 100%;
            margin: 2rem auto;
            padding: 1rem;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        h1, p {
            margin: 0 0 1rem 0;
        }

        /* Tombol yang menarik */
        .button {
            display: inline-block;
            padding: 0.5rem 1rem;
            color: #fff;
            background: #007BFF;
            text-decoration: none;
            border-radius: 4px;
        }

        .button:hover {
            background: #0056b3;
        }

        /* Responsif untuk perangkat kecil */
        @media (max-width: 768px) {
            header h1 {
                font-size: 1.5rem; /* Ukuran teks lebih kecil untuk header */
            }

            .container {
                padding: 1rem; /* Lebih sedikit padding di perangkat kecil */
            }

            .button {
                padding: 0.5rem 1.2rem; /* Ukuran tombol menyesuaikan perangkat */
            }
        }
    </style>
</head>
<body>

<header>
    <h1>@KAITOSEN1412</h1>
</header>

<div class="container">
    <h1>uda ilang webnya</h1>
    <p>bye bye.</p>
    <a href="https://saweria.co/sen002" class="button" target="_blank">Klik Saya</a>
</div>

</body>
</html>
