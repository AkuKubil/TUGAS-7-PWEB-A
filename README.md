# TUGAS-7-PWEB-A

## Description
Membuat Submit Form Without Page Refresh dengan mengimpelementasikan materi AJAX.
File : 
1. HTML
2. CSS
3. AJAX

## Code 

HTML 
```
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contact Form - AJAX Fetch</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <div class="header">
            <h2>✉️ Hubungi Kami</h2>
            <p>Kirim pesan tanpa reload halaman (AJAX).</p>
        </div>

        <form id="contactForm">
            <div class="form-group">
                <label>Nama Lengkap</label>
                <input type="text" id="nama" placeholder="Contoh: Fajar Baskoro" required>
            </div>

            <div class="form-group">
                <label>Email Address</label>
                <input type="email" id="email" placeholder="nama@email.com" required>
            </div>

            <div class="form-group">
                <label>Pesan</label>
                <textarea id="pesan" rows="4" placeholder="Tulis pesanmu di sini..." required></textarea>
            </div>

            <button type="submit" id="btnSubmit">
                <span id="btnText">Kirim Pesan</span>
                <span id="loader" class="loader hidden"></span>
            </button>
        </form>

        <div id="alertSuccess" class="alert hidden">
            ✅ <strong>Berhasil!</strong> Terima kasih telah menghubungi kami. Kami akan segera membalas.
        </div>

    </div>

    <script src="ajax.js"></script>
</body>
</html>
```

CSS
```
* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }

body {
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    display: flex; justify-content: center; align-items: center;
    min-height: 100vh; padding: 20px;
}

.container {
    background: #fff; padding: 2.5rem; border-radius: 15px;
    width: 100%; max-width: 450px;
    box-shadow: 0 15px 35px rgba(0,0,0,0.1);
}

.header { text-align: center; margin-bottom: 25px; }
.header h2 { color: #333; margin-bottom: 5px; }
.header p { color: #777; font-size: 0.9rem; }

.form-group { margin-bottom: 20px; }
label { display: block; margin-bottom: 8px; font-weight: 600; color: #555; }

input, textarea {
    width: 100%; padding: 12px; border-radius: 8px;
    border: 2px solid #ecf0f1; background: #fcfcfc;
    font-size: 1rem; outline: none; transition: 0.3s;
}

input:focus, textarea:focus { border-color: #3498db; background: #fff; }

button {
    width: 100%; padding: 14px;
    background: #3498db; color: white; border: none;
    border-radius: 8px; font-weight: bold; cursor: pointer;
    display: flex; justify-content: center; align-items: center; gap: 10px;
    transition: 0.3s;
}

button:hover { background: #2980b9; }
button:disabled { background: #95a5a6; cursor: not-allowed; }

.alert {
    margin-top: 20px; padding: 15px;
    background: #d4edda; color: #155724;
    border: 1px solid #c3e6cb; border-radius: 8px;
    text-align: center; font-size: 0.9rem;
    animation: fadeIn 0.5s;
}

.hidden { display: none; }

.loader {
    border: 3px solid #f3f3f3; border-top: 3px solid #3498db;
    border-radius: 50%; width: 20px; height: 20px;
    animation: spin 1s linear infinite;
}

@keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
```

AJAX
```
const form = document.getElementById('contactForm');
const btnSubmit = document.getElementById('btnSubmit');
const btnText = document.getElementById('btnText');
const loader = document.getElementById('loader');
const alertSuccess = document.getElementById('alertSuccess');

form.addEventListener('submit', function(e) {
    e.preventDefault();

    setLoading(true);
    alertSuccess.classList.add('hidden'); 

    const dataKirim = {
        nama: document.getElementById('nama').value,
        email: document.getElementById('email').value,
        pesan: document.getElementById('pesan').value
    };

    fetch('https://jsonplaceholder.typicode.com/posts', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(dataKirim)
    })
    .then(response => response.json()) 
    .then(result => {
        console.log('Success:', result); 

        alertSuccess.classList.remove('hidden');

        form.reset();
    })
    .catch(error => {
        console.error('Error:', error);
        alert('Terjadi kesalahan koneksi!');
    })
    .finally(() => {
        setLoading(false);
    });
});

function setLoading(isLoading) {
    if (isLoading) {
        btnText.textContent = "Mengirim...";
        loader.classList.remove('hidden');
        btnSubmit.disabled = true;
    } else {
        btnText.textContent = "Kirim Pesan";
        loader.classList.add('hidden');
        btnSubmit.disabled = false;
    }
}
```

## Web Result 
<img width="1221" height="1421" alt="image" src="https://github.com/user-attachments/assets/4bc6f524-40b0-484a-ad03-8fe971702341" />

LINK DEMO : https://sparkly-alfajores-e09f2a.netlify.app/


