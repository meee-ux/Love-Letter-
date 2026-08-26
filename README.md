<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <link href="https://googleapis.com" rel="stylesheet">
    <!-- Memuat library confetti dari CDN -->
    <script src="https://jsdelivr.net"></script>
    <style>
        body {
            /* Perpaduan warna gradasi Lilac dan Mint Pastel yang super lucu */
            background-color: #e8dbfc;
            background-image: linear-gradient(135deg, #e8dbfc 0%, #f1fcf1 50%, #dbf5fc 100%);
            font-family: 'Quicksand', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        .container {
            position: relative;
            width: 320px;
            height: 380px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .card-initial {
            background: #ffffff;
            padding: 35px 25px;
            border-radius: 24px;
            box-shadow: 0 10px 30px rgba(162, 155, 254, 0.3);
            text-align: center;
            width: 100%;
            position: absolute;
            transition: all 0.6s ease-in-out;
            animation: float 3s ease-in-out infinite;
            border: 2px solid #f1f0fe;
        }

        .card-initial.hidden {
            opacity: 0;
            transform: scale(0.8) translateY(-50px);
            pointer-events: none;
        }

        .card-letter {
            background: #fffdf9;
            padding: 30px 22px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(162, 155, 254, 0.25);
            text-align: left;
            width: 100%;
            position: absolute;
            opacity: 0;
            transform: scale(0.8) translateY(50px);
            pointer-events: none;
            transition: all 0.6s ease-in-out;
            /* Garis putus-putus berwarna ungu lilac lembut */
            border: 2px dashed #b2bec3;
        }

        .card-letter.show {
            opacity: 1;
            transform: scale(1) translateY(0);
            pointer-events: auto;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }

        .emoji {
            font-size: 50px;
            margin-bottom: 12px;
            text-align: center;
        }

        h1 {
            color: #6c5ce7; /* Warna teks utama ungu lilac tua agar kontras */
            font-size: 20px;
            margin-bottom: 10px;
            text-align: center;
        }

        p {
            color: #636e72;
            font-size: 13.5px;
            line-height: 1.6;
            margin-bottom: 20px;
            text-align: center;
        }

        .letter-text {
            color: #2d3436;
            font-size: 13px;
            line-height: 1.7;
            margin-bottom: 20px;
            max-height: 180px;
            overflow-y: auto;
        }

        .btn {
            background-color: #a29bfe; /* Tombol warna lilac pastel */
            color: white;
            border: none;
            padding: 10px 22px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 600;
            font-family: 'Quicksand', sans-serif;
            transition: 0.2s;
            display: block;
            margin: 0 auto;
            box-shadow: 0 4px 10px rgba(162, 155, 254, 0.4);
        }

        .btn:hover {
            background-color: #6c5ce7;
            transform: scale(1.05);
        }

        .btn-back {
            background-color: #ffeaa7; /* Tombol kembali kuning pastel */
            color: #636e72;
            box-shadow: 0 4px 10px rgba(255, 234, 167, 0.4);
        }
        .btn-back:hover {
            background-color: #fdcb6e;
            color: #fff;
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Tampilan Kartu Pertama -->
        <div class="card-initial" id="cardInitial">
            <div class="emoji">🧸🎂</div>
            <h1>Happy Birthday, Bestie!</h1>
            <p>Semoga hari ini penuh tawa, makanan enak, dan semua impianmu jadi kenyataan. Ada surat spesial buat kamu nih! ✨</p>
            <button class="btn" onclick="bukaSurat()">Buka Surat 💌</button>
        </div>

        <!-- Tampilan Kartu Surat -->
        <div class="card-letter" id="cardLetter">
            <h1>Untuk Temanku Tersayang </h1>
            <div class="letter-text">
                Hai! Gak nyangka kamu udah nambah umur lagi tahun ini. Makasih ya udah jadi teman yang selalu ada pas senang maupun susah (terutama pas lagi gabut bareng).<br><br>
                Semoga di usia yang baru ini, kamu makin bahagia, tercapai semua target-target kerenmu, dijauhin dari orang-orang nyebelin, dan jangan lupa traktirannya ya! Tetap jadi asik dan kocak terus. 🥳🥂
            </div>
            <button class="btn btn-back" onclick="tutupSurat()">Kembali ⬅️</button>
        </div>
    </div>

    <script>
        // Fungsi memutar melodi ceria dengan Web Audio API
        function mainkanMusik() {
            const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            const notes = [261.63, 293.66, 329.63, 349.23, 392.00, 440.00, 493.88, 523.25];
            let waktuMulai = audioCtx.currentTime;

            // Nada-nada ceria pendek
            const urutanNada =;
            urutanNada.forEach((noteIndex, i) => {
                const osc = audioCtx.createOscillator();
                const gainNode = audioCtx.createGain();
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(notes[noteIndex], waktuMulai + (i * 0.2));
                
                gainNode.gain.setValueAtTime(0.15, waktuMulai + (i * 0.2));
                gainNode.gain.exponentialRampToValueAtTime(0.001, waktuMulai + (i * 0.2) + 0.18);
                
                osc.connect(gainNode);
                gainNode.connect(audioCtx.destination);
                
                osc.start(waktuMulai + (i * 0.2));
                osc.stop(waktuMulai + (i * 0.2) + 0.2);
            });
        }

        // Fungsi efek confetti meledak dengan warna pastel yang senada
        function jalankanConfetti() {
            confetti({
                particleCount: 80,
                spread: 70,
                origin: { y: 0.6 },
                colors: ['#a29bfe', '#74b9ff', '#81ecec', '#fab1a0', '#ffeaa7']
            });
        }

        function bukaSurat() {
            document.getElementById('cardInitial').classList.add('hidden');
            document.getElementById('cardLetter').classList.add('show');
            jalankanConfetti();
            mainkanMusik();
        }

        function tutupSurat() {
            document.getElementById('cardInitial').classList.remove('hidden');
            document.getElementById('cardLetter').classList.remove('show');
        }
    </script>

</body>
</html>

        

