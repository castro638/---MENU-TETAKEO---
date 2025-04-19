<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Menú de Taqueo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-image: url('https://i.imgur.com/jwwHzfY.jpg');
      background-size: cover;
      background-attachment: fixed;
      background-repeat: no-repeat;
      background-position: center;
      color: #000;
    }

    h1, h2 {
      text-align: center;
      color: black;
    }

    .menu-item {
      background: rgba(255, 255, 255, 0.95);
      padding: 15px;
      margin-bottom: 10px;
      border-radius: 8px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }

    .precio { font-weight: bold; color: green; }
    .boton {
      display: inline-block;
      margin: 10px auto;
      padding: 10px 20px;
      background: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      text-align: center;
    }

    .contador { margin-top: 10px; font-weight: bold; }
    .link-pago {
      display: block;
      margin: 10px auto;
      padding: 10px;
      background: #007bff;
      color: white;
      text-decoration: none;
      border-radius: 5px;
      max-width: 300px;
    }

    #mediosPago, #numeros, #total, #extras {
      display: none;
      text-align: center;
      margin-top: 30px;
      font-weight: bold;
    }

    .categoria {
      background-color: #ddd;
      padding: 10px;
      border-radius: 5px;
      margin-top: 20px;
      font-weight: bold;
    }

    input, textarea {
      padding: 10px;
      margin-top: 10px;
      width: 80%;
      max-width: 500px;
      border-radius: 5px;
      border: 1px solid #ccc;
      display: block;
      margin-left: auto;
      margin-right: auto;
    }

    #tarifas {
      background: white;
      padding: 10px;
      margin-top: 30px;
      border-radius: 5px;
      max-width: 400px;
      margin-left: auto;
      margin-right: auto;
    }

    #direccionMapa {
      margin-top: 10px;
      font-size: 14px;
      text-align: center;
    }
  </style>
</head>
<body>
  <h1>Menú de Taqueo</h1>
  <div id="menu"></div>

  <div id="total">Total a pagar: $<span id="totalValor">0</span></div>

  <input type="text" id="direccion" placeholder="Dirección de entrega">
  <div id="direccionMapa"></div>
  <textarea id="comentario" placeholder="Descripción o comentario adicional"></textarea>

  <button class="boton" onclick="finalizarCompra()">Finalizar Compra</button>
  <button class="boton" onclick="reiniciar()">Reiniciar</button>

  <div id="mediosPago">
    <h2>Medios de Pago</h2>
    <a id="nequiBtn" href="#" class="link-pago">Pagar con Nequi</a>
    <a href="intent://send?phone=+573152553101#Intent;scheme=daviplata;package=com.davivienda.daviplata;end" class="link-pago">Pagar con Daviplata</a>
    <div id="numeros">Teléfono: 3152553101</div>
  </div>

  <div id="extras">
    <div id="tarifas">
      <p>Domicilio cerca: $4.000</p>
      <p>Domicilio lejos: $5.000</p>
      <p>Más lejos de Funza: $6.000 - $7.000</p>
    </div>
    <a id="WHATSAPP" class="link-pago" target="_blank">Enviar pedido por WhatsApp</a>
  </div>

  <script>
    const menu = [
      { categoria: "Hamburguesas", nombre: "Hamburguesa Sencilla", descripcion: "Carne artesanal (100g)...", precio: 10000 },
      { categoria: "Perros Calientes", nombre: "Perro Caliente", descripcion: "Salchicha americana...", precio: 8000 },
      { categoria: "Bebidas", nombre: "Bebida Coca-Cola", descripcion: "Coca-Cola 500ml", precio: 4000 },
      { categoria: "Promociones", nombre: "Promo Martes: 2 Hamburguesas Sencillas", descripcion: "2 por $18.000", precio: 18000 }
    ];

    let total = 0;
    const cantidades = new Array(menu.length).fill(0);

    const contenedorMenu = document.getElementById("menu");
    let categoriaActual = "";

    menu.forEach((item, index) => {
      if (item.categoria !== categoriaActual) {
        const cat = document.createElement("div");
        cat.className = "categoria";
        cat.textContent = item.categoria;
        contenedorMenu.appendChild(cat);
        categoriaActual = item.categoria;
      }
      const div = document.createElement("div");
      div.className = "menu-item";
      div.innerHTML = `
        <h3>${item.nombre}</h3>
        <p>${item.descripcion}</p>
        <p class='precio'>$${item.precio.toLocaleString()}</p>
        <p class='contador'>Cantidad: <span id="cantidad-${index}">0</span></p>
        <button onclick="agregar(${item.precio}, ${index})">Agregar</button>
        <button onclick="quitar(${item.precio}, ${index})">Quitar</button>
      `;
      contenedorMenu.appendChild(div);
    });

    function actualizarTotal() {
      document.getElementById("totalValor").textContent = total.toLocaleString();
    }

    function agregar(precio, index) {
      total += precio;
      cantidades[index]++;
      document.getElementById(`cantidad-${index}`).textContent = cantidades[index];
      document.getElementById("total").style.display = "block";
      actualizarTotal();
    }

    function quitar(precio, index) {
      if (cantidades[index] > 0) {
        total -= precio;
        cantidades[index]--;
        document.getElementById(`cantidad-${index}`).textContent = cantidades[index];
        actualizarTotal();
      }
    }

    function finalizarCompra() {
      document.getElementById("mediosPago").style.display = "block";
      document.getElementById("extras").style.display = "block";
      document.getElementById("numeros").style.display = "block";
      enviarPorWhatsApp();
      abrirGoogleMaps();
      window.scrollTo(0, document.body.scrollHeight);
    }

    function enviarPorWhatsApp() {
      let mensaje = "*🧾 Pedido desde el Menú de Taqueo:*%0A%0A";
      for (let i = 0; i < menu.length; i++) {
        if (cantidades[i] > 0) {
          mensaje += `- ${menu[i].nombre} x${cantidades[i]} - $${(menu[i].precio * cantidades[i]).toLocaleString()}%0A`;
        }
      }

      mensaje += `%0A💰 *Total a pagar:* $${total.toLocaleString()}%0A`;

      const direccion = document.getElementById("direccion").value.trim();
      const comentario = document.getElementById("comentario").value.trim();

      if (direccion) mensaje += `%0A📍 *Dirección de entrega:* ${direccion}`;
      if (comentario) mensaje += `%0A📝 *Comentario:* ${comentario}`;

      mensaje += `%0A%0A✅ Por favor confirmar disponibilidad y tiempo estimado.`;

      const telefono = "573152553101";
      const url = `https://wa.me/${telefono}?text=${mensaje}`;
      document.getElementById("WHATSAPP").href = url;

      // Nequi con total
      document.getElementById("nequiBtn").href = `intent://send?phone=+${telefono}#Intent;scheme=nequi;package=com.nequi.mobile.app;S.amount=${total};end`;
    }

    function abrirGoogleMaps() {
      const direccion = document.getElementById("direccion").value.trim();
      const link = direccion ? `<a href="https://www.google.com/maps/search/${encodeURIComponent(direccion)}" target="_blank">📍 Ver ubicación en Google Maps</a>` : "";
      document.getElementById("direccionMapa").innerHTML = link;
    }

    function reiniciar() {
      total = 0;
      cantidades.fill(0);
      menu.forEach((_, i) => {
        document.getElementById(`cantidad-${i}`).textContent = 0;
      });
      actualizarTotal();
      document.getElementById("total").style.display = "none";
      document.getElementById("mediosPago").style.display = "none";
      document.getElementById("extras").style.display = "none";
      document.getElementById("numeros").style.display = "none";
      document.getElementById("direccion").value = "";
      document.getElementById("comentario").value = "";
      document.getElementById("direccionMapa").innerHTML = "";
    }
  </script>
</body>
</html>
