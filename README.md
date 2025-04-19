<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Menú de Taqueo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: url('https://images.unsplash.com/photo-1606756795732-76ad9c2b1c86') no-repeat center center fixed;
      background-size: cover;
      color: #000;
    }
    h1, h2 {
      text-align: center;
      color: #000;
      background-color: rgba(255, 255, 255, 0.8);
      padding: 10px;
      border-radius: 10px;
    }
    .menu-item {
      background: rgba(255, 255, 255, 0.95);
      padding: 15px;
      margin-bottom: 10px;
      border-radius: 8px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }
    .precio {
      font-weight: bold;
      color: green;
    }
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
    .contador, #direccionMostrada, #descripcionMostrada {
      margin-top: 10px;
      font-weight: bold;
      background-color: rgba(255,255,255,0.8);
      padding: 10px;
      border-radius: 8px;
    }
    #total, #mediosPago, #extras, #WHATSAPP {
      display: none;
      text-align: center;
      margin-top: 30px;
    }
    .categoria {
      background-color: #ffdd57;
      padding: 10px;
      border-radius: 5px;
      margin-top: 20px;
      font-weight: bold;
    }
    input, textarea {
      padding: 10px;
      width: 80%;
      margin: 10px auto;
      display: block;
      border-radius: 8px;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <h1>Menú de Taqueo</h1>

  <div id="menu"></div>
  <div id="total">Total a pagar: $<span id="totalValor">0</span></div>

  <button class="boton" onclick="finalizarCompra()">Finalizar Compra</button>
  <button class="boton" onclick="reiniciar()">Reiniciar</button>

  <div id="extras">
    <input type="text" id="direccion" placeholder="Escribe tu dirección aquí" oninput="mostrarDireccion()" />
    <textarea id="comentario" placeholder="Descripción o comentarios (ej: domicilio, cerca, etc.)" oninput="mostrarDescripcion()"></textarea>
    <div id="direccionMostrada"></div>
    <div id="descripcionMostrada"></div>
  </div>

  <div id="mediosPago">
    <h2>Medios de Pago</h2>
    <a id="nequiPago" href="#" class="link-pago">Pagar con Nequi</a>
    <a href="intent://send?phone=+573152553101#Intent;scheme=daviplata;package=com.davivienda.daviplata;end" class="link-pago">Pagar con Daviplata</a>
    <p>📞 Número: 3152553101</p>
    <p>🚚 Domicilio cerca: $4.000, lejos: $5.000, fuera de Funza: $6.000–$7.000</p>
    <a id="WHATSAPP" class="link-pago" target="_blank">Enviar por WhatsApp</a>
  </div>

  <script>
    const menu = [
      { categoria: "Hamburguesas", nombre: "Hamburguesa Sencilla", descripcion: "Carne artesanal(100g)...", precio: 10000 },
      { categoria: "Perros Calientes", nombre: "Perro Especial", descripcion: "Salchicha americana...", precio: 15000 },
      { categoria: "Bebidas", nombre: "Bebida Coca-Cola", descripcion: "Bebida 500ml", precio: 4000 },
      // Agrega todos los demás ítems de tu menú aquí
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

    function actualizarTotal() {
      document.getElementById("totalValor").textContent = total.toLocaleString();
    }

    function mostrarDireccion() {
      const direccion = document.getElementById("direccion").value.trim();
      document.getElementById("direccionMostrada").innerHTML = direccion
        ? `📍 Dirección: <a href="https://www.google.com/maps/search/${encodeURIComponent(direccion)}" target="_blank">${direccion}</a>`
        : '';
    }

    function mostrarDescripcion() {
      const comentario = document.getElementById("comentario").value.trim();
      document.getElementById("descripcionMostrada").textContent = comentario ? `🗒️ Descripción: ${comentario}` : '';
    }

    function finalizarCompra() {
      document.getElementById("mediosPago").style.display = "block";
      document.getElementById("extras").style.display = "block";
      document.getElementById("WHATSAPP").style.display = "inline-block";
      enviarPorWhatsApp();
      document.getElementById("nequiPago").href = `intent://send?phone=+573152553101&text=Total%20a%20pagar:%20$${total}#Intent;scheme=nequi;package=com.nequi.mobile.app;end`;
      window.scrollTo(0, document.body.scrollHeight);
    }

    function enviarPorWhatsApp() {
      let mensaje = "*Pedido desde el Menú:*%0A%0A";
      for (let i = 0; i < menu.length; i++) {
        if (cantidades[i] > 0) {
          mensaje += `🧾 ${menu[i].nombre} x${cantidades[i]} - $${(menu[i].precio * cantidades[i]).toLocaleString()}%0A`;
        }
      }
      mensaje += `%0A*Total a pagar:* $${total.toLocaleString()}%0A`;

      const direccion = document.getElementById("direccion").value.trim();
      const comentario = document.getElementById("comentario").value.trim();

      if (direccion) {
        mensaje += `%0A📍 *Dirección de entrega:* ${direccion}`;
      }

      if (comentario) {
        mensaje += `%0A🗒️ *Comentario:* ${comentario}`;
      }

      mensaje += `%0A%0A👉 Por favor confirmar disponibilidad y tiempo estimado.`;
      const telefono = "3152553101";
      const url = `https://wa.me/${telefono}?text=${encodeURIComponent(mensaje)}`;
      document.getElementById("WHATSAPP").href = url;
    }

    function reiniciar() {
      total = 0;
      for (let i = 0; i < cantidades.length; i++) {
        cantidades[i] = 0;
        document.getElementById(`cantidad-${i}`).textContent = 0;
      }
      actualizarTotal();
      document.getElementById("total").style.display = "none";
      document.getElementById("mediosPago").style.display = "none";
      document.getElementById("extras").style.display = "none";
      document.getElementById("WHATSAPP").style.display = "none";
      document.getElementById("direccionMostrada").textContent = '';
      document.getElementById("descripcionMostrada").textContent = '';
      document.getElementById("direccion").value = '';
      document.getElementById("comentario").value = '';
    }
  </script>
</body>
</html>
