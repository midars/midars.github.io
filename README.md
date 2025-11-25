# midars.github.io
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestor de Ventas Web</title>
    <!-- Carga de Tailwind CSS para un diseño moderno y responsive -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Fuente y estilos base */
        body { font-family: 'Inter', sans-serif; background-color: #f7f7f7; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        /* Estilos específicos para la tabla */
        .tabla-ventas th { cursor: pointer; }
    </style>
</head>
<body class="p-4 sm:p-8">

<div class="max-w-4xl mx-auto bg-white shadow-xl rounded-xl overflow-hidden">
    <header class="bg-indigo-600 text-white p-6">
        <h1 class="text-3xl font-bold">🛒 Caja Diaria Web</h1>
        <p class="text-indigo-200 mt-1">Gestión de Productos, Ventas y Reportes (Día/Mes)</p>
    </header>

    <!-- Navegación por Pestañas -->
    <div class="flex border-b border-gray-200">
        <button onclick="changeTab('productos')" id="tab-productos" class="tab-button active flex-1 py-3 px-4 text-center text-sm font-medium border-r border-gray-200 bg-indigo-50 hover:bg-indigo-100 text-indigo-700 transition duration-150">
            1. Productos
        </button>
        <button onclick="changeTab('ventas')" id="tab-ventas" class="tab-button flex-1 py-3 px-4 text-center text-sm font-medium border-r border-gray-200 text-gray-700 hover:bg-gray-50 transition duration-150">
            2. Registrar Venta
        </button>
        <button onclick="changeTab('reportes')" id="tab-reportes" class="tab-button flex-1 py-3 px-4 text-center text-sm font-medium text-gray-700 hover:bg-gray-50 transition duration-150">
            3. Reportes
        </button>
    </div>

    <!-- Contenido de las Pestañas -->
    <main class="p-6">
        <!-- Pestaña 1: Gestión de Productos -->
        <div id="productos" class="tab-content active space-y-6">
            <h2 class="text-2xl font-semibold text-gray-800">Añadir Nuevo Producto</h2>

            <div id="message-productos" class="hidden p-3 rounded-lg text-white font-medium"></div>

            <div class="grid sm:grid-cols-3 gap-4">
                <input type="text" id="nombreProducto" placeholder="Nombre del Producto" class="p-3 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500 col-span-2">
                <input type="number" id="precioProducto" placeholder="Precio ($)" step="0.01" min="0.01" class="p-3 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500">
            </div>
            <button onclick="agregarProducto()" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-4 rounded-lg transition duration-150 shadow-md">
                + Agregar Producto
            </button>

            <h3 class="text-xl font-semibold mt-8 text-gray-800 border-t pt-4">Lista de Productos</h3>
            <div class="overflow-x-auto">
                <table class="min-w-full divide-y divide-gray-200 rounded-lg overflow-hidden shadow-lg">
                    <thead class="bg-gray-100">
                    <tr>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">ID</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider tabla-ventas" onclick="sortProducts('nombre')">Nombre</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider tabla-ventas" onclick="sortProducts('precio')">Precio</th>
                    </tr>
                    </thead>
                    <tbody id="productosTableBody" class="bg-white divide-y divide-gray-200">
                    <!-- Filas de productos se insertan aquí -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- Pestaña 2: Registro de Ventas -->
        <div id="ventas" class="tab-content space-y-6">
            <h2 class="text-2xl font-semibold text-gray-800">Registrar Nueva Venta</h2>

            <div id="message-ventas" class="hidden p-3 rounded-lg text-white font-medium"></div>

            <div class="grid sm:grid-cols-2 gap-4">
                <div>
                    <label for="selectProducto" class="block text-sm font-medium text-gray-700 mb-1">Producto:</label>
                    <select id="selectProducto" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500">
                        <!-- Opciones de productos se llenan aquí -->
                    </select>
                </div>
                <div>
                    <label for="cantidadVenta" class="block text-sm font-medium text-gray-700 mb-1">Cantidad:</label>
                    <input type="number" id="cantidadVenta" placeholder="Cantidad" value="1" min="1" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500">
                </div>
            </div>

            <p class="text-lg font-bold text-gray-800 mt-4">Total Estimado: <span id="totalVenta" class="text-indigo-600">$0.00</span></p>

            <button onclick="registrarVenta()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-lg transition duration-150 shadow-md">
                Registrar Venta
            </button>
        </div>

        <!-- Pestaña 3: Reportes -->
        <div id="reportes" class="tab-content space-y-6">
            <h2 class="text-2xl font-semibold text-gray-800">Historial y Reportes de Ventas</h2>

            <div class="flex space-x-2 mb-6">
                <button onclick="mostrarReporte('DIA')" class="flex-1 py-2 px-4 bg-purple-500 hover:bg-purple-600 text-white rounded-lg transition duration-150">Ventas del Día</button>
                <button onclick="mostrarReporte('MES')" class="flex-1 py-2 px-4 bg-purple-500 hover:bg-purple-600 text-white rounded-lg transition duration-150">Ventas del Mes</button>
                <button onclick="mostrarReporte('TOTAL')" class="flex-1 py-2 px-4 bg-purple-500 hover:bg-purple-600 text-white rounded-lg transition duration-150">Total Histórico</button>
            </div>

            <h3 id="reporteTitulo" class="text-xl font-semibold text-gray-800"></h3>
            <p class="text-3xl font-extrabold text-indigo-600 mt-2">Total: <span id="reporteTotal">$0.00</span></p>

            <div class="overflow-x-auto mt-6">
                <table class="min-w-full divide-y divide-gray-200 rounded-lg overflow-hidden shadow-lg">
                    <thead class="bg-gray-100">
                    <tr>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Fecha</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Producto</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Cantidad</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total</th>
                    </tr>
                    </thead>
                    <tbody id="reportesTableBody" class="bg-white divide-y divide-gray-200">
                    <!-- Filas de reportes se insertan aquí -->
                    </tbody>
                </table>
            </div>
        </div>
    </main>
</div>

<!-- JavaScript para la Lógica de la Aplicación -->
<script>
    // --- Variables Globales ---
    let productos = [];
    let ventas = [];

    // --- Almacenamiento (Simula Base de Datos .txt) ---
    const STORAGE_KEY_PRODUCTS = 'gestor_productos';
    const STORAGE_KEY_VENTAS = 'gestor_ventas';

    function loadData() {
        try {
            // Carga productos (Arreglo unidimensional de objetos)
            productos = JSON.parse(localStorage.getItem(STORAGE_KEY_PRODUCTS) || '[]');

            // Carga ventas (Arreglo bidimensional de objetos)
            ventas = JSON.parse(localStorage.getItem(STORAGE_KEY_VENTAS) || '[]');

            // Asegura que las fechas se mantengan como strings para comparación
            ventas = ventas.map(v => ({
                ...v,
                fecha: v.fecha.toString()
            }));
        } catch (e) {
            console.error("Error al cargar datos de localStorage:", e);
            productos = [];
            ventas = [];
        }
    }

    function saveData() {
        localStorage.setItem(STORAGE_KEY_PRODUCTS, JSON.stringify(productos));
        localStorage.setItem(STORAGE_KEY_VENTAS, JSON.stringify(ventas));
        renderAll();
    }

    // --- Funcionalidad General ---

    // Muestra mensajes de feedback al usuario
    function showMessage(type, message, targetId) {
        const el = document.getElementById(targetId);
        el.textContent = message;
        el.className = `p-3 rounded-lg text-white font-medium ${type === 'success' ? 'bg-green-500' : 'bg-red-500'} font-bold`;
        el.classList.remove('hidden');
        setTimeout(() => {
            el.classList.add('hidden');
        }, 3000);
    }

    // Cambia entre pestañas
    function changeTab(tabId) {
        document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');

        document.querySelectorAll('.tab-button').forEach(el => el.classList.remove('bg-indigo-50', 'text-indigo-700'));
        document.getElementById(`tab-${tabId}`).classList.add('bg-indigo-50', 'text-indigo-700');

        if (tabId === 'ventas') {
            populateVentaSelect();
        }
        if (tabId === 'reportes') {
            mostrarReporte('DIA'); // Carga el reporte del día por defecto
        }
    }

    // --- Pestaña de Productos ---

    // Función para agregar productos (Similar a la lógica de Java)
    function agregarProducto() {
        const nombre = document.getElementById('nombreProducto').value.trim();
        const precio = parseFloat(document.getElementById('precioProducto').value);

        if (!nombre || isNaN(precio) || precio <= 0) {
            showMessage('error', 'Por favor, ingrese un nombre y un precio válido (> 0).', 'message-productos');
            return;
        }

        // Búsqueda secuencial (lineal) para evitar duplicados
        if (productos.some(p => p.nombre.toLowerCase() === nombre.toLowerCase())) {
            showMessage('error', 'Error: Este producto ya existe.', 'message-productos');
            return;
        }

        const nuevoProducto = {
            id: productos.length + 1, // Simulación de ID
            nombre: nombre,
            precio: precio
        };

        productos.push(nuevoProducto);
        saveData();

        document.getElementById('nombreProducto').value = '';
        document.getElementById('precioProducto').value = '';
        showMessage('success', `Producto "${nombre}" agregado.`, 'message-productos');
    }

    // Ordenamiento (Bubble Sort para la tabla)
    let sortDirection = {};
    function sortProducts(key) {
        sortDirection[key] = sortDirection[key] === 'asc' ? 'desc' : 'asc';

        // Implementación de Bubble Sort simplificada
        let n = productos.length;
        let swapped;
        do {
            swapped = false;
            for (let i = 0; i < n - 1; i++) {
                let a = productos[i][key];
                let b = productos[i + 1][key];

                // Convertir a minúsculas si es cadena (para orden alfabético)
                if (typeof a === 'string') {
                    a = a.toLowerCase();
                    b = b.toLowerCase();
                }

                let shouldSwap = false;
                if (sortDirection[key] === 'asc') {
                    shouldSwap = a > b;
                } else { // desc
                    shouldSwap = a < b;
                }

                if (shouldSwap) {
                    [productos[i], productos[i + 1]] = [productos[i + 1], productos[i]];
                    swapped = true;
                }
            }
            n--;
        } while (swapped);

        renderProductsTable();
    }

    function renderProductsTable() {
        const tbody = document.getElementById('productosTableBody');
        tbody.innerHTML = ''; // Limpia la tabla

        if (productos.length === 0) {
            tbody.innerHTML = '<tr><td colspan="3" class="px-6 py-4 text-center text-gray-500">No hay productos registrados.</td></tr>';
            return;
        }

        productos.forEach((p, index) => {
            const row = `
                <tr>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${index + 1}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${p.nombre}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">$${p.precio.toFixed(2)}</td>
                </tr>
            `;
            tbody.innerHTML += row;
        });
        // Vuelve a llenar el select de ventas cada vez que se actualizan los productos
        populateVentaSelect();
    }

    // --- Pestaña de Ventas ---

    function populateVentaSelect() {
        const select = document.getElementById('selectProducto');
        select.innerHTML = ''; // Limpiar opciones

        if (productos.length === 0) {
            select.innerHTML = '<option value="">--- Agregue productos primero ---</option>';
            document.getElementById('totalVenta').textContent = '$0.00';
            return;
        }

        // Ordenar por nombre antes de mostrar en el select (Mejora de UX)
        productos.sort((a, b) => a.nombre.localeCompare(b.nombre));

        productos.forEach(p => {
            const option = document.createElement('option');
            option.value = p.id;
            option.setAttribute('data-precio', p.precio);
            option.textContent = `${p.nombre} ($${p.precio.toFixed(2)})`;
            select.appendChild(option);
        });

        // Event listener para actualizar el total al cambiar producto o cantidad
        select.onchange = updateVentaTotal;
        document.getElementById('cantidadVenta').oninput = updateVentaTotal;
        updateVentaTotal();
    }

    function updateVentaTotal() {
        const selectedId = parseInt(document.getElementById('selectProducto').value);
        const cantidad = parseInt(document.getElementById('cantidadVenta').value) || 0;
        const producto = productos.find(p => p.id === selectedId);

        let total = 0;
        if (producto && cantidad > 0) {
            total = producto.precio * cantidad;
        }
        document.getElementById('totalVenta').textContent = `$${total.toFixed(2)}`;
    }

    function registrarVenta() {
        const selectedId = parseInt(document.getElementById('selectProducto').value);
        const cantidad = parseInt(document.getElementById('cantidadVenta').value);
        const producto = productos.find(p => p.id === selectedId);

        if (!producto || isNaN(cantidad) || cantidad <= 0) {
            showMessage('error', 'Seleccione un producto y una cantidad válida.', 'message-ventas');
            return;
        }

        const total = producto.precio * cantidad;
        const fecha = new Date().toISOString().split('T')[0]; // Formato YYYY-MM-DD

        const nuevaVenta = {
            fecha: fecha,
            nombreProducto: producto.nombre,
            cantidad: cantidad,
            total: total
        };

        ventas.push(nuevaVenta);
        saveData();

        // Limpieza de campos
        document.getElementById('cantidadVenta').value = 1;
        updateVentaTotal();
        showMessage('success', `Venta registrada: $${total.toFixed(2)}`, 'message-ventas');
    }

    // --- Pestaña de Reportes ---

    function mostrarReporte(periodo) {
        let filteredVentas = [];
        const hoy = new Date().toISOString().split('T')[0];
        const hoyDate = new Date(hoy);
        let totalReporte = 0;

        document.getElementById('reporteTitulo').textContent = `Reporte de Ventas: ${periodo}`;

        // Lógica de filtrado (Similar a la lógica del GestorVentas.java)
        ventas.forEach(v => {
            const ventaDate = new Date(v.fecha);
            let shouldInclude = false;

            switch (periodo) {
                case 'DIA':
                    if (v.fecha === hoy) { // Compara strings YYYY-MM-DD
                        shouldInclude = true;
                    }
                    break;
                case 'MES':
                    if (v.fecha.substring(0, 7) === hoy.substring(0, 7)) { // Compara YYYY-MM
                        shouldInclude = true;
                    }
                    break;
                case 'TOTAL':
                    shouldInclude = true;
                    break;
            }

            if (shouldInclude) {
                filteredVentas.push(v);
                totalReporte += v.total;
            }
        });

        // Mostrar el Total
        document.getElementById('reporteTotal').textContent = `$${totalReporte.toFixed(2)}`;

        // Mostrar la Tabla
        const tbody = document.getElementById('reportesTableBody');
        tbody.innerHTML = '';

        if (filteredVentas.length === 0) {
            tbody.innerHTML = '<tr><td colspan="4" class="px-6 py-4 text-center text-gray-500">No hay ventas en este periodo.</td></tr>';
            return;
        }

        filteredVentas.forEach(v => {
            const row = `
                <tr>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${v.fecha}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${v.nombreProducto}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${v.cantidad}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-indigo-600">$${v.total.toFixed(2)}</td>
                </tr>
            `;
            tbody.innerHTML += row;
        });
    }

    // --- Inicialización ---
    function renderAll() {
        renderProductsTable();
        populateVentaSelect();
        mostrarReporte('DIA');
    }

    document.addEventListener('DOMContentLoaded', () => {
        loadData(); // Carga todos los datos del localStorage
        renderAll(); // Renderiza todas las tablas e interfaces

        // Inicializa la primera pestaña
        changeTab('productos');

        // Inicializa el cálculo del total de venta
        updateVentaTotal();
    });
</script>
</body>
</html>
