<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pendaftaran & Rincian Biaya UTA'45</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; padding: 20px; background-color: #f4f4f4; display: flex; justify-content: center; }
        .container { max-width: 400px; width: 100%; background: white; padding: 30px; border-radius: 15px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        .header { text-align: center; margin-bottom: 20px; }
        .header h2 { color: #ce1212; margin: 0; }
        .header p { color: #666; font-size: 13px; }
        label { font-weight: bold; display: block; margin-top: 10px; color: #333; }
        input { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box; }
        button { width: 100%; padding: 15px; background-color: #ce1212; color: white; border: none; border-radius: 8px; cursor: pointer; font-size: 16px; font-weight: bold; margin-top: 20px; transition: 0.3s; }
        button:disabled { background-color: #ccc; cursor: not-allowed; }
        #loading { display: none; text-align: center; margin-top: 10px; color: #ce1212; font-weight: bold; }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <h2>UTA'45 JAKARTA</h2>
        <p>Isi data untuk melihat Rincian Biaya Kuliah 2025/2026</p>
    </div>

    <form id="studentForm">
        <label>Nama Lengkap</label>
        <input type="text" name="nama" id="nama" placeholder="Masukkan nama lengkap" required>

        <label>Tempat, Tanggal Lahir</label>
        <input type="text" name="ttl" id="ttl" placeholder="Contoh: Jakarta, 01-01-2007" required>

        <label>Nomor WhatsApp</label>
        <input type="tel" name="telepon" id="telepon" placeholder="08xxxxxxxxxx" required>

        <label>Asal Sekolah</label>
        <input type="text" name="sekolah" id="sekolah" placeholder="Nama SMA/SMK/MA" required>

        <button type="submit" id="submitBtn">KIRIM & LIHAT BIAYA</button>
        <div id="loading">Memproses data... Mohon tunggu.</div>
    </form>
</div>

<script>
    const scriptURL = 'https://script.google.com/macros/s/AKfycbzRyJwCjvjF9MbLowZvAlbggLDCApB-13Mjahr2BG6uLIKI3epjoOjan_GOd_8yNVx76Q/exec';
    const form = document.getElementById('studentForm');
    const btn = document.getElementById('submitBtn');
    const loading = document.getElementById('loading');

    form.addEventListener('submit', e => {
        e.preventDefault();
        
        btn.disabled = true;
        btn.style.display = 'none';
        loading.style.display = 'block';

        const formData = new URLSearchParams();
        formData.append('nama', document.getElementById('nama').value);
        formData.append('ttl', document.getElementById('ttl').value);
        formData.append('telepon', document.getElementById('telepon').value);
        formData.append('sekolah', document.getElementById('sekolah').value);

        fetch(scriptURL, { 
            method: 'POST', 
            body: formData,
            headers: { "Content-Type": "application/x-www-form-urlencoded" }
        })
        .then(response => {
            // Notifikasi sebelum pindah halaman
            alert("Data berhasil tersimpan! Anda akan diarahkan ke halaman rincian biaya kuliah.");
            
            // REDIRECT OTOMATIS KE LINK RINCIAN BIAYA
            window.location.href = 'https://www.uta45jakarta.ac.id/rincian-biaya-kuliah-s1-reguler-2025-2026/';
        })
        .catch(error => {
            console.error('Error!', error.message);
            alert("Maaf, terjadi kesalahan. Silakan coba lagi.");
            btn.disabled = false;
            btn.style.display = 'block';
            loading.style.display = 'none';
        });
    });
</script>

</body>
</html>
