[index.html](https://github.com/user-attachments/files/24064726/index.html)
<!DOCTYPE html>
<html lang="lv">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Gleznu Galerija</title>
  <style>
    body { font-family: Inter, sans-serif; background:#f5f5f5; margin:0; padding:0; }
    header { background:#000; color:#fff; padding:20px; text-align:center; font-size:24px; }
    .container { max-width:1100px; margin:30px auto; padding:10px; }
    .upload-box, .card { background:#fff; border-radius:12px; padding:20px;
      box-shadow:0 6px 18px rgba(0,0,0,0.08); }
    .upload-box input, .upload-box button { width:100%; margin-top:10px; padding:12px; font-size:16px; }
    .upload-box button { background:#000; color:#fff; border:none; cursor:pointer; }
    .gallery { margin-top:30px; display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:20px; }
    .card img { width:100%; height:220px; object-fit:cover; border-radius:10px; }
    .price { margin-top:10px; font-size:18px; font-weight:600; }
    .buy-btn { margin-top:10px; background:#0a5; color:#fff; padding:10px; text-align:center;
      border-radius:8px; text-decoration:none; display:block; font-size:16px; }
  </style>
</head>
<body>

<header>Gleznu Galerija</header>

<div class="container">

  <div class="upload-box">
    <h2>Pievienot jaunu gleznu</h2>
    <input type="file" id="imageInput" accept="image/*" />
    <input type="text" id="priceInput" placeholder="Ievadi cenu (€)" />
    <input type="text" id="paypalInput" placeholder="Ievadi PayPal pirkuma linku" />
    <button onclick="addImage()">Pievienot galerijai</button>
  </div>

  <div class="gallery" id="gallery"></div>

</div>

<script>
function addImage() {
  const imgInput = document.getElementById("imageInput");
  const price = document.getElementById("priceInput").value;
  const paypal = document.getElementById("paypalInput").value;

  if (!imgInput.files[0]) { alert("Izvēlies bildi!"); return; }

  const reader = new FileReader();
  reader.onload = e => {
    const gallery = document.getElementById("gallery");

    const card = document.createElement("div");
    card.classList.add("card");

    const img = document.createElement("img");
    img.src = e.target.result;

    const priceTag = document.createElement("div");
    priceTag.classList.add("price");
    priceTag.textContent = price ? price + " €" : "Cena nav norādīta";

    const btn = document.createElement("a");
    btn.classList.add("buy-btn");
    btn.textContent = "Pirkt";
    btn.href = paypal || "#";
    btn.target = "_blank";

    card.appendChild(img);
    card.appendChild(priceTag);
    card.appendChild(btn);
    gallery.appendChild(card);
  };

  reader.readAsDataURL(imgInput.files[0]);
  imgInput.value = "";
  document.getElementById("priceInput").value = "";
  document.getElementById("paypalInput").value = "";
}
</script>

</body>
</html>
