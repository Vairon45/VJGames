# VJGames 
<h1>❔apa itu VJGames</h1>
<p>VJGames adalah komunitas percodingan</p>
nama pengembang komunitas
<ol>
  <Li>Vero</Li>
  <li>Ojan</li>
</ol>

<!DOCTYPE html>
<html>
<head>
  <title>Game 1</title>
  <h1>Tambah sampai angkanya 1000</h1>
  <ol>
    <li>Setiap tambah, nambah 5</li>
    <li>Angka pertama adalah 0</li>
  </ol>
</head>
<body>
  <button onclick="tambah()">Tambah</button>
  <button onclick="hasil()">Hasil</button>
  <p id="hasil"></p>
  <h2>Leaderboard:</h2>
  <ol id="leaderboard"></ol>
  <button onclick="login()">Login</button>
  <button onclick="gantiNama()">Ganti Nama</button>
  <button onclick="bagikan()">Bagikan</button>
  <div id="waktu"></div>
</body>
</html>


<script>
let angka1 = 0;
let angka2 = 5;
let pemain = [];
let namaPemain = "";
let waktu = 60; 
let interval;
let sudahSubmit = false;

// Login
function login() {
  namaPemain = prompt("Masukkan nama Anda:");
  if (namaPemain && namaPemain.trim() !== "") {
    localStorage.setItem("namaPemain", namaPemain);
  } else {
    alert("Nama tidak boleh kosong!");
  }
}

// Ganti Nama
function gantiNama() {
  const namaBaru = prompt("Masukkan nama baru:");
  if (namaBaru && namaBaru.trim() !== "") {
    namaPemain = namaBaru;
    localStorage.setItem("namaPemain", namaPemain);
  } else {
    alert("Nama tidak boleh kosong!");
  }
}

// Tambah
function tambah() {
  angka1 += angka2;
}

// Hasil
function hasil() {
  document.getElementById("hasil").innerText = angka1;
  submitSkor();
}

// Submit Skor
function submitSkor() {
  if (!sudahSubmit) {
    pemain.push({ nama: namaPemain, skor: angka1 });
    pemain.sort((a, b) => b.skor - a.skor);
    updateLeaderboard();
    sudahSubmit = true;
  }
}

// Leaderboard
function updateLeaderboard() {
  const leaderboard = document.getElementById("leaderboard");
  leaderboard.innerHTML = "";
  const pemainAkhir = { nama: namaPemain, skor: angka1 };
  leaderboard.innerHTML += `<li>1. ${pemainAkhir.nama}: ${pemainAkhir.skor}</li>`;
}


function submitSkor() {
  updateLeaderboard();
}


// Waktu
function waktuMundur() {
  waktu--;
  document.getElementById("waktu").innerText = `Waktu: ${waktu} detik`;
  if (waktu <= 0) {
    clearInterval(interval);
    submitSkor();
    alert("Waktu habis!");
  }
}

// Bagikan
function bagikan() {
  const teks = `Saya mencapai skor ${angka1}!`;
  navigator.clipboard.writeText(teks);
  alert("Teks telah disalin!");
}

// Inisialisasi
namaPemain = localStorage.getItem("namaPemain");
pemain = JSON.parse(localStorage.getItem("pemain")) || [];
interval = setInterval(waktuMundur, 1000);
</script>
