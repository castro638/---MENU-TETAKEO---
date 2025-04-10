<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Menú del Restaurante</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f9f9f9;
      color: #333;
      padding: 20px;
    }
    h1, h2 {
      color: #c0392b;
    }
    .menu, .cart, #promociones {
      margin-top: 30px;
    }
    .item {
      border: 1px solid #ddd;
      padding: 15px;
      margin-bottom: 20px;
      background-color: #fff;
      border-radius: 8px;
      display: flex;
      align-items: center;
      gap: 15px;
    }
    .item img {
      width: 100px;
      height: auto;
      border-radius: 8px;
    }
    .info {
      flex: 1;
    }
    button {
      margin-right: 10px;
      background-color: #27ae60;
      color: #fff;
      border: none;
      padding: 8px 12px;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #219150;
    }
  </style>
</head>
<body>
  <h1>Menú del Restaurante</h1>

  <div class="menu">
    <h2>Hamburguesas</h2>
    <div class="item">
      <div class="info">
        <h3>Hamburguesa Sencilla</h3>
        <p>Carne artesanal, queso doble crema, verduras, salsas, pan artesanal. Precio: $10.000</p>
        <button onclick="agregarProducto('Hamburguesa Sencilla', 10000)">Agregar</button>
        <button onclick="quitarProducto('Hamburguesa Sencilla')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Hamburguesa Especial</h3>
        <p>Con tocineta, huevo, queso doble crema, verduras, salsas, pan artesanal. Precio: $15.000</p>
        <button onclick="agregarProducto('Hamburguesa Especial', 15000)">Agregar</button>
        <button onclick="quitarProducto('Hamburguesa Especial')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Hamburguesa Tetakeo</h3>
        <p>Carne, pechuga, tocineta, huevo, queso doble crema, verduras, salsas. Precio: $22.000</p>
        <button onclick="agregarProducto('Hamburguesa Tetakeo', 22000)">Agregar</button>
        <button onclick="quitarProducto('Hamburguesa Tetakeo')">Quitar</button>
      </div>
    </div>

    <h2>Perros Calientes</h2>
    <div class="item">
      <div class="info">
        <h3>Perro Caliente</h3>
        <p>Salchipapa americana, cebolla, papas, queso, salsas. Precio: $8.000</p>
        <button onclick="agregarProducto('Perro Caliente', 8000)">Agregar</button>
        <button onclick="quitarProducto('Perro Caliente')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Mechiperro</h3>
        <p>Carne esmechada, lechuga, queso, papas, salsas. Precio: $15.000</p>
        <button onclick="agregarProducto('Mechiperro', 15000)">Agregar</button>
        <button onclick="quitarProducto('Mechiperro')">Quitar</button>
      </div>
    </div>

    <h2>Salchipapas</h2>
    <div class="item">
      <div class="info">
        <h3>Salchipapa Sencilla</h3>
        <p>Papas, salchicha, queso, salsa. Precio: $10.500</p>
        <button onclick="agregarProducto('Salchipapa Sencilla', 10500)">Agregar</button>
        <button onclick="quitarProducto('Salchipapa Sencilla')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Salchipapa Especial</h3>
        <p>Carne esmechada, huevo, maíz, queso, papas. Precio: $20.500</p>
        <button onclick="agregarProducto('Salchipapa Especial', 20500)">Agregar</button>
        <button onclick="quitarProducto('Salchipapa Especial')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Salchipapa Especial de Pollo</h3>
        <p>Pollo, queso, papas, lechuga, tomate. Precio: $23.500</p>
        <button onclick="agregarProducto('Salchipapa Especial de Pollo', 23500)">Agregar</button>
        <button onclick="quitarProducto('Salchipapa Especial de Pollo')">Quitar</button>
      </div>
    </div>

    <h2>Otros</h2>
    <div class="item">
      <div class="info">
        <h3>Picada</h3>
        <p>Mixta con carnes, queso, huevo, aguacate. Precio: $35.500</p>
        <button onclick="agregarProducto('Picada', 35500)">Agregar</button>
        <button onclick="quitarProducto('Picada')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Mazorcada</h3>
        <p>Mixta con carnes, papas, maíz, queso, salsas. Precio: $35.500</p>
        <button onclick="agregarProducto('Mazorcada', 35500)">Agregar</button>
        <button onclick="quitarProducto('Mazorcada')">Quitar</button>
      </div>
    </div>

    <h2>Bebidas Personales</h2>
    <div class="item">
      <div class="info">
        <h3>Coca-Cola</h3>
        <p>Refresco personal clásico. Precio: $4.000</p>
        <button onclick="agregarProducto('Coca-Cola', 4000)">Agregar</button>
        <button onclick="quitarProducto('Coca-Cola')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Sprite</h3>
        <p>Refresco personal sabor limón. Precio: $4.000</p>
        <button onclick="agregarProducto('Sprite', 4000)">Agregar</button>
        <button onclick="quitarProducto('Sprite')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Cuatro</h3>
        <p>Refresco personal sabor cítrico. Precio: $4.000</p>
        <button onclick="agregarProducto('Cuatro', 4000)">Agregar</button>
        <button onclick="quitarProducto('Cuatro')">Quitar</button>
      </div>
    </div>
    <div class="item">
      <div class="info">
        <h3>Kola Román</h3>
        <p>Refresco tradicional colombiano. Precio: $4.000</p>
        <button onclick="agregarProducto('Kola Román', 4000)">Agregar</button>
        <button onclick="quitarProducto('Kola Román')">Quitar</button>
      </div>
    </div>
  </div>

  <div id="promociones"></div>

  <div class="cart">
    <h2>Tu pedido</h2>
    <ul id="carrito"></ul>
    <p><strong>Total: $<span id="total">0</span></strong></p>
    <p>Formas de pago: Nequi, Daviplata</p>
  </div>

  <script>
    const carrito = {};

    function agregarProducto(nombre, precio) {
      if (!carrito[nombre]) carrito[nombre] = { cantidad: 0, precio: precio };
      carrito[nombre].cantidad++;
      actualizarCarrito();
    }

    function quitarProducto(nombre) {
      if (carrito[nombre]) {
        carrito[nombre].cantidad--;
        if (carrito[nombre].cantidad <= 0) delete carrito[nombre];
        actualizarCarrito();
      }
    }

    function actualizarCarrito() {
      const lista = document.getElementById("carrito");
      const totalElemento = document.getElementById("total");
      lista.innerHTML = "";
      let total = 0;
      for (let producto in carrito) {
        const item = carrito[producto];
        total += item.cantidad * item.precio;
        lista.innerHTML += `<li>${producto} x ${item.cantidad} - $${item.cantidad * item.precio}</li>`;
      }
      totalElemento.textContent = total.toLocaleString();
    }

    // Promociones del martes
    const hoy = new Date();
    const esMartes = hoy.getDay() === 2;
    if (esMartes) {
      const promociones = document.getElementById("promociones");
      promociones.innerHTML = `
        <h2>Promociones del Martes</h2>
        <div class="item">
          <div class="info">
            <h3>2 Hamburguesas Sencillas</h3>
            <p>Promoción del martes: $18.000</p>
            <button onclick="agregarProducto('2 Hamburguesas Sencillas', 18000)">Agregar</button>
            <button onclick="quitarProducto('2 Hamburguesas Sencillas')">Quitar</button>
          </div>
        </div>
        <div class="item">
          <div class="info">
            <h3>2 Perros Calientes</h3>
            <p>Promoción del martes: $12.000</p>
            <button onclick="agregarProducto('2 Perros Calientes', 12000)">Agregar</button>
            <button onclick="quitarProducto('2 Perros Calientes')">Quitar</button>
          </div>
        </div>
        <div class="item">
          <div class="info">
            <h3>Mazorcada Sencilla Promo</h3>
            <p>Promoción del martes: $22.500</p>
            <button onclick="agregarProducto('Mazorcada Sencilla Promo', 22500)">Agregar</button>
            <button onclick="quitarProducto('Mazorcada Sencilla Promo')">Quitar</button>
          </div>
        </div>
      `;
    }
  </script>
</body>
</html>
