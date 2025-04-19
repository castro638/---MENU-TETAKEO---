<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Menú Restaurante</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      margin: 0;
      background-color: #f8f9fa;
      color: #333;
      padding: 0 10px 50px;
    }

    h1, h2 {
      text-align: center;
      color: #343a40;
      margin-top: 30px;
    }

    .categoria {
      background-color: #ffc107;
      padding: 10px;
      border-radius: 8px;
      font-weight: bold;
      font-size: 20px;
      margin: 30px auto 10px;
      text-align: center;
      max-width: 600px;
    }

    .menu-item {
      background: #ffffff;
      padding: 20px;
      margin: 10px auto;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.05);
      max-width: 600px;
    }

    .menu-item h3 {
      margin: 0 0 10px;
      color: #212529;
    }

    .precio {
      color: #28a745;
      font-weight: bold;
      margin-top: 10px;
    }

    .contador {
      margin: 10px 0;
      font-weight: bold;
    }

    button {
      margin-right: 10px;
      margin-top: 10px;
      padding: 8px 15px;
      border: none;
      border-radius: 5px;
      background-color: #17a2b8;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background-color: #138496;
    }

    .boton {
      background: #007bff;
      margin: 15px auto;
      display: block;
    }

    .boton:hover {
      background: #0056b3;
    }

    .link-pago {
      display: block;
      margin: 10px auto;
      padding: 10px;
      background: #28a745;
      color: white;
      text-decoration: none;
      border-radius: 5px;
      max-width: 300px;
      text-align: center;
    }

    .link-pago:hover {
      background: #218838;
    }

    #total, #mediosPago, #numeros {
      text-align: center;
      font-size: 20px;
      margin-top: 30px;
      display: none;
    }

    #WHATSAPP {
      display: block;
      margin: 10px auto;
      padding: 10px;
      background-color: #25D366;
      color: white;
      text-align: center;
      border-radius: 5px;
      text-decoration: none;
      max-width: 300px;
    }

    #WHATSAPP:hover {
      background-color: #1ebe5d;
    }

    input, textarea {
      width: 80%;
      padding: 10px;
      margin: 10px auto;
      display: block;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <h1>Menú Restaurante</h1>
  <div id="menu"></div>
  <div id="total">Total a pagar: $<span id="totalValor">0</span></div>
  <button class="boton" onclick="finalizarCompra()">Finalizar Compra</button>
  <button class="boton" onclick="reiniciar()">Reiniciar</button>

  <div id="mediosPago">
    <h2>Medios de Pago</h2>
    <a href="intent://send?phone=+573152553101#Intent;scheme=nequi;package=com.nequi.mobile.app;end" class="link-pago">Pagar con Nequi</a>
    <a href="intent://send?phone=+573152553101#Intent;scheme=daviplata;package=com.davivienda.daviplata;end" class="link-pago">Pagar con Daviplata</a>
    <div id="numeros">
      <p><strong>Número:</strong> 3152553101</p>
    </div>

    <input id="direccion" type="text" placeholder="Dirección de entrega" />
    <textarea id="comentario" rows="3" placeholder="Comentarios adicionales..."></textarea>

    <a id="WHATSAPP" target="_blank">Enviar por WhatsApp</a>
  </div>

  <script>
    const menu = [
      { categoria: "Hamburguesas", nombre: "Hamburguesa Sencilla", descripcion: "Carne artesanal (100g), queso doble crema, verduras, salsas, pan artesanal.", precio: 10000 },
      { categoria: "Hamburguesas", nombre: "Hamburguesa De Patakon", descripcion: "Carne, queso, verduras, patacón maduro, salsas.", precio: 13000 },
      { categoria: "Hamburguesas", nombre: "Hamburguesa Especial", descripcion: "Carne, tocineta, huevo, verduras, queso, pan artesanal.", precio: 15000 },
      { categoria: "Hamburguesas", nombre: "Hamburguesa Tetakeo", descripcion: "Carne, pechuga, tocineta, huevo, queso, verduras, pan.", precio: 22000 },
      { categoria: "Perros Calientes", nombre: "Perro Caliente", descripcion: "Salchicha, papas, cebolla caramelizada, queso, salsas.", precio: 8000 },
      { categoria: "Perros Calientes", nombre: "Perro Especial Mechiperro", descripcion: "Carne esmechada, salchicha, queso, verduras, papas, salsas.", precio: 15000 },
      { categoria: "Salchipapas", nombre: "Salchipapa Sencilla", descripcion: "Salchicha, papas a la francesa, queso, salsas.", precio: 10500 },
      { categoria: "Salchipapas", nombre: "Salchipapa Especial", descripcion: "Carne, salchicha, papas, verduras, huevos, maíz, queso, salsas.", precio: 20500 },
      { categoria: "Otros", nombre: "Picada", descripcion: "Res, cerdo, pechuga, salchicha, papas, verduras, aguacate, salsas.", precio: 38500 },
      { categoria: "Otros", nombre: "Mazorca", descripcion: "Res, cerdo, pechuga, maíz, papas, queso, salsas.", precio: 38500 },
      { categoria: "Otros", nombre: "Papas a la Francesa", descripcion: "Porción de papas a la francesa", precio: 7000 },
      { categoria: "Bebidas", nombre: "Coca-Cola", descripcion: "500ml", precio: 4000 },
      { categoria: "Bebidas", nombre: "Sprite", descripcion: "400ml", precio: 4000 },
      { categoria: "Bebidas", nombre: "Kola Román", descripcion: "400ml", precio: 4000 },
      { categoria: "Combos", nombre: "Combo Sencillo", descripcion: "Hamburguesa sencilla + gaseosa + papa", precio: 20000 },
      { categoria: "Combos", nombre: "Combo Especial", descripcion: "Hamburguesa especial + gaseosa + papa", precio: 26000 },
      { categoria: "Promociones", nombre: "Martes 2 Hamburguesas", descripcion: "2 hamburguesas sencillas por $18.000", precio: 18000 }
    ];

    let total = 0;
    const cantidades = new Array(menu.length).fill(0);
    const contenedorMenu = document.getElementById("menu");

    function actualizarTotal() {
      document.getElementById("totalValor").textContent = total.toLocaleString();
    }

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

    function finalizarCompra() {
      document.getElementById("mediosPago").style.display = "block";
      document.getElementById("numeros").style.display = "block";
      document.getElementById("WHATSAPP").style.display = "block";
      enviarPorWhatsApp();
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

      if (direccion) mensaje += `%0A🏠 *Dirección:* ${direccion}`;
      if (comentario) mensaje += `%0A🗒️ *Comentario:* ${comentario}`;

      mensaje += `%0A%0A👉 Por favor confirmar disponibilidad.`;

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
      document.getElementById("numeros").style.display = "none";
      document.getElementById("WHATSAPP").style.display = "none";
      document.getElementById("direccion").value = "";
      document.getElementById("comentario").value = "";
    }
  </script>
</body>
</html>
