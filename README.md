<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Menú del Restaurante</title>
  <style>
    body { font-family: Arial; padding: 20px; background-color: #f2f2f2; }
    h1 { font-size: 28px; text-align: center; }
    .menu-item {
      background: white; padding: 15px; margin: 15px 0;
      border-radius: 10px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    img {
      width: 250px; height: 180px; object-fit: cover;
      border-radius: 10px; margin-bottom: 10px;
    }
    .descripcion { font-size: 14px; margin-top: 5px; }
    .precio { font-weight: bold; margin-top: 5px; }
    .total { margin-top: 30px; font-size: 20px; font-weight: bold; }
    button { margin: 5px 5px 0 0; padding: 5px 10px; }
  </style>
</head>
<body>
  <h1>Menú del Restaurante</h1>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Hamburguesa+Sencilla">
    <div>Hamburguesa Sencilla</div>
    <div class="descripcion">Carne artesanal, queso doble crema, verduras, salsas, pan artesanal.</div>
    <div class="precio">Precio: $10.000</div>
    <button onclick="agregarProducto('Hamburguesa Sencilla', 10000)">Agregar</button>
    <button onclick="quitarProducto('Hamburguesa Sencilla')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Hamburguesa+Especial">
    <div>Hamburguesa Especial</div>
    <div class="descripcion">Carne, tocineta, huevo, queso doble crema, codorniz, verduras y salsas.</div>
    <div class="precio">Precio: $15.000</div>
    <button onclick="agregarProducto('Hamburguesa Especial', 15000)">Agregar</button>
    <button onclick="quitarProducto('Hamburguesa Especial')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Hamburguesa+Tetakeo">
    <div>Hamburguesa Tetakeo</div>
    <div class="descripcion">Carne, pechuga, tocineta, huevo, queso, codorniz, verduras y salsas.</div>
    <div class="precio">Precio: $22.000</div>
    <button onclick="agregarProducto('Hamburguesa Tetakeo', 22000)">Agregar</button>
    <button onclick="quitarProducto('Hamburguesa Tetakeo')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Perro+Caliente">
    <div>Perro Caliente</div>
    <div class="descripcion">Salchipapa americana, cebolla, papas, queso campesino, salsas y pan artesanal.</div>
    <div class="precio">Precio: $8.000</div>
    <button onclick="agregarProducto('Perro Caliente', 8000)">Agregar</button>
    <button onclick="quitarProducto('Perro Caliente')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Mechiperro">
    <div>Perro Especial Mechiperro</div>
    <div class="descripcion">Salchipapa, carne desmechada, lechuga, queso, papas y salsas.</div>
    <div class="precio">Precio: $15.000</div>
    <button onclick="agregarProducto('Mechiperro', 15000)">Agregar</button>
    <button onclick="quitarProducto('Mechiperro')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Salchipapa+Sencilla">
    <div>Salchipapa Sencilla</div>
    <div class="descripcion">Salchipapa americana, papas a la francesa, queso campesino y salsas.</div>
    <div class="precio">Precio: $10.500</div>
    <button onclick="agregarProducto('Salchipapa Sencilla', 10500)">Agregar</button>
    <button onclick="quitarProducto('Salchipapa Sencilla')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Salchipapa+Especial">
    <div>Salchipapa Especial</div>
    <div class="descripcion">Carne desmechada, salchicha, papas, lechuga, codorniz, maíz, queso y salsas.</div>
    <div class="precio">Precio: $20.500</div>
    <button onclick="agregarProducto('Salchipapa Especial', 20500)">Agregar</button>
    <button onclick="quitarProducto('Salchipapa Especial')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Salchipapa+Pollo">
    <div>Salchipapa Especial de Pollo</div>
    <div class="descripcion">Pollo, salchicha, papas, lechuga, tomate, codorniz, queso y salsas.</div>
    <div class="precio">Precio: $23.500</div>
    <button onclick="agregarProducto('Salchipapa Pollo', 23500)">Agregar</button>
    <button onclick="quitarProducto('Salchipapa Pollo')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Picada">
    <div>Picada</div>
    <div class="descripcion">Res, cerdo, pechuga, salchicha, papas, verduras, codorniz, queso, aguacate y salsas.</div>
    <div class="precio">Precio: $35.500</div>
    <button onclick="agregarProducto('Picada', 35500)">Agregar</button>
    <button onclick="quitarProducto('Picada')">Quitar</button>
  </div>

  <div class="menu-item">
    <img src="https://via.placeholder.com/250x180?text=Mazorca">
    <div>Mazorca</div>
    <div class="descripcion">Res, cerdo, pechuga, papas, maíz tierno, queso campesino y salsas.</div>
    <div class="precio">Precio: $35.500</div>
    <button onclick="agregarProducto('Mazorca', 35500)">Agregar</button>
    <button onclick="quitarProducto('Mazorca')">Quitar</button>
  </div>

  <div class="total">Total: $<span id="total">0</span></div>
  <button onclick="reiniciar()">Reiniciar Orden</button>

  <script>
    let orden = [];

    function actualizarTotal() {
      let total = orden.reduce((acc, item) => acc + item.precio, 0);
      document.getElementById("total").innerText = total.toLocaleString('es-CO');
    }

    function agregarProducto(nombre, precio) {
      orden.push({ nombre, precio });
      actualizarTotal();
    }

    function quitarProducto(nombre) {
      const index = orden.findIndex(item => item.nombre === nombre);
      if (index !== -1) {
        orden.splice(index, 1);
        actualizarTotal();
      } else {
        alert("Este producto no está en la orden.");
      }
    }

    function reiniciar() {
      orden = [];
      actualizarTotal();
    }
  </script>
</body>
</html>
<html>
  <head>
    <!-- Aquí va el título, estilos y todo eso -->
  </head>
  <body>

    <!-- Aquí va todo tu menú (hamburguesas, perros, salchipapas, etc.) -->

    <!-- Luego aparece la sección del total -->
    <div class="total">Total: $<span id="total">0</span></div>
    <button onclick="reiniciar()">Reiniciar Orden</button>

    <!-- AQUÍ INSERTAS la sección de FORMAS DE PAGO -->
    <h2>Formas de pago</h2>
    <div>
      <!-- Código de formas de pago -->
    </div>

    <!-- Aquí va el script -->
    <script>
      // Tu script JS
    </script>

  </body>
</html>
