<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Menú Restaurante</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background-color: #f2f2f2; }
    h1, h2 { text-align: center; }
    .menu-item { background: #fff; padding: 15px; margin-bottom: 10px; border-radius: 8px; box-shadow: 0 0 5px rgba(0,0,0,0.1); }
    .precio { font-weight: bold; color: green; }
    .boton { display: inline-block; margin: 10px auto; padding: 10px 20px; background: #28a745; color: white; border: none; border-radius: 5px; cursor: pointer; text-align: center; }
    .contador { margin-top: 10px; font-weight: bold; }
    .link-pago { display: block; margin: 10px auto; padding: 10px; background: #007bff; color: white; text-decoration: none; border-radius: 5px; max-width: 300px; }
    #mediosPago, #numeros, #total { display: none; text-align: center; margin-top: 30px; font-weight: bold; }
    .categoria { background-color: #ddd; padding: 10px; border-radius: 5px; margin-top: 20px; font-weight: bold; }
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
      <p>3152553101</p>
    </div>
  </div>

  <script>
    const menu = [
      { categoria: "Hamburguesas", nombre: "Hamburguesa Sencilla", descripcion: "Carne artesanal, queso doble crema, verduras (lechuga, tomate, cebolla caramelizada), salsas (tártara, ranchera, BBQ), pan artesanal.", precio: 10000 },
      { categoria: "Hamburguesas", nombre: "Hamburguesa Especial", descripcion: "Carne artesanal, tocineta ahumada, huevo, queso doble crema, huevo de codorniz, verduras, salsas, pan artesanal.", precio: 15000 },
      { categoria: "Hamburguesas", nombre: "Hamburguesa Tetakeo", descripcion: "Carne artesanal, pechuga a la plancha, tocineta, huevo, queso doble crema, huevo de codorniz, verduras, salsas, pan artesanal.", precio: 22000 },
      { categoria: "Perros Calientes", nombre: "Perro Caliente", descripcion: "Salchipapa americana, cebolla caramelizada, papas cabello de ángel, queso campesino, salsas, pan artesanal.", precio: 8000 },
      { categoria: "Perros Calientes", nombre: "Perro Especial Mechiperro", descripcion: "Salchipapa americana, carne esmechada, cebolla caramelizada, lechuga, papas cabello de ángel, queso campesino, salsas, pan artesanal.", precio: 15000 },
      { categoria: "Salchipapas", nombre: "Salchipapa Sencilla", descripcion: "Salchipapa americana, papas a la francesa, queso campesino, salsas.", precio: 10500 },
      { categoria: "Salchipapas", nombre: "Salchipapa Especial", descripcion: "Carne esmechada, salchicha americana, papas a la francesa, lechuga, tomate, queso campesino, huevos de codorniz, maíz tierno, salsas.", precio: 20500 },
      { categoria: "Salchipapas", nombre: "Salchipapa Especial de Pollo", descripcion: "Pollo, salchicha americana, papas a la francesa, lechuga, tomate, queso campesino, huevos de codorniz, salsas.", precio: 23500 },
      { categoria: "Otros", nombre: "Picada", descripcion: "Carne de res, cerdo, pechuga, salchicha americana, papas a la francesa, lechuga, tomate, cebolla caramelizada, queso campesino, aguacate, huevo de codorniz, salsas.", precio: 38500 },
      { categoria: "Otros", nombre: "Mazorca", descripcion: "Carne de res, cerdo, pechuga, papas cabello de ángel, maíz tierno, papas a la francesa, queso campesino, salsas.", precio: 38500 },
      { categoria: "Bebidas", nombre: "Bebida Coca-Cola", descripcion: "Bebida personal Coca-Cola", precio: 4000 },
      { categoria: "Bebidas", nombre: "Bebida Sprite", descripcion: "Bebida personal Sprite", precio: 4000 },
      { categoria: "Bebidas", nombre: "Bebida Cuatro", descripcion: "Bebida personal Cuatro", precio: 4000 },
      { categoria: "Bebidas", nombre: "Bebida Kola Román", descripcion: "Bebida personal Kola Román", precio: 4000 },
      { categoria: "Otros", nombre: "Papas a la Francesa (Porción)", descripcion: "Porción de papas a la francesa", precio: 6500 },
      { categoria: "Promociones", nombre: "Promo Martes: 2 Hamburguesas Sencillas", descripcion: "2 Hamburguesas por solo $18.000", precio: 18000 },
      { categoria: "Promociones", nombre: "Promo Martes: 2 Perros Calientes", descripcion: "2 Perros Calientes por $12.000", precio: 12000 },
      { categoria: "Promociones", nombre: "Promo Martes: Mazorcada Sencilla", descripcion: "Mazorcada sencilla por $22.500", precio: 22500 }
    ];

    let total = 0;
    function actualizarTotal() {
      document.getElementById("totalValor").textContent = total.toLocaleString();
    }

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

    const cantidades = new Array(menu.length).fill(0);

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
      window.scrollTo(0, document.body.scrollHeight);
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
    }
  </script>
</body>
</html>
