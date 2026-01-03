# jurnal-pertanian
Jurnal Pertanian 
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Jurnal Harian Pertanian</title>
<style>
body{font-family:Arial,Helvetica,sans-serif;margin:0;background:#f4f7f4}
header{background:#2f7d32;color:#fff;padding:14px}
.card{background:#fff;margin:12px;padding:12px;border-radius:10px;box-shadow:0 2px 6px rgba(0,0,0,.08)}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
button{padding:12px;border:none;border-radius:10px;background:#4caf50;color:#fff;font-size:14px}
.small{font-size:12px;color:#555}
</style>
</head>
<body>
<header>
  <strong>🌾 Jurnal Harian Pertanian</strong>
  <div id="hst">HST: -</div>
</header>

<div class="card">
  <strong>Saldo Kebun</strong>
  <div id="saldo">Rp 0</div>
</div>

<div class="card grid">
  <button onclick="addPanen()">Tambah Panen</button>
  <button onclick="addBiaya()">Tambah Biaya</button>
</div>

<div class="card">
  <strong>Riwayat Panen</strong>
  <ul id="panenList" class="small"></ul>
</div>

<script>
if(!localStorage.getItem('tanam')){
  localStorage.setItem('tanam', new Date().toISOString());
}
const tanam = new Date(localStorage.getItem('tanam'));
const today = new Date();
const hst = Math.floor((today - tanam)/(1000*60*60*24))+1;
document.getElementById('hst').innerText = 'HST: '+hst;

let saldo = Number(localStorage.getItem('saldo')||0);
document.getElementById('saldo').innerText = 'Rp '+saldo.toLocaleString();

function addPanen(){
  const kg = Number(prompt('Berat panen (kg):'));
  const harga = Number(prompt('Harga per kg:'));
  if(!kg || !harga) return;
  const total = kg*harga;
  saldo += total;
  localStorage.setItem('saldo',saldo);
  const li = document.createElement('li');
  li.innerText = 'Panen '+kg+' kg x Rp '+harga+' = Rp '+total.toLocaleString();
  document.getElementById('panenList').appendChild(li);
  document.getElementById('saldo').innerText = 'Rp '+saldo.toLocaleString();
}

function addBiaya(){
  const biaya = Number(prompt('Biaya pengeluaran:'));
  if(!biaya) return;
  saldo -= biaya;
  localStorage.setItem('saldo',saldo);
  document.getElementById('saldo').innerText = 'Rp '+saldo.toLocaleString();
}
</script>
</body>
</html>
