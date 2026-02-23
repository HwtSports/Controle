<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controle de Estoque</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        /* Container principal */
        .app-container {
            display: flex;
            min-height: 100vh;
        }

        /* Menu Lateral */
        .sidebar {
            width: 250px;
            background: white;
            box-shadow: 2px 0 10px rgba(0,0,0,0.1);
            padding: 30px 0;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
        }

        .logo {
            padding: 0 20px 30px 20px;
            border-bottom: 1px solid #f0f0f0;
            margin-bottom: 20px;
        }

        .logo h2 {
            color: #333;
            font-size: 20px;
            font-weight: 600;
        }

        .logo p {
            color: #667eea;
            font-size: 14px;
            margin-top: 5px;
        }

        .menu-item {
            display: flex;
            align-items: center;
            padding: 15px 25px;
            color: #666;
            text-decoration: none;
            transition: all 0.3s;
            cursor: pointer;
            border-left: 4px solid transparent;
        }

        .menu-item:hover {
            background: #f8f9fa;
            color: #667eea;
        }

        .menu-item.active {
            background: #f0f3ff;
            color: #667eea;
            border-left-color: #667eea;
        }

        .menu-item span {
            font-size: 20px;
            margin-right: 15px;
        }

        .menu-item .menu-text {
            font-size: 15px;
            font-weight: 500;
        }

        /* Conteúdo Principal */
        .main-content {
            flex: 1;
            margin-left: 250px;
            padding: 30px;
        }

        /* Header */
        .header {
            background: white;
            border-radius: 15px;
            padding: 20px 30px;
            margin-bottom: 30px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header h1 {
            color: #333;
            font-size: 24px;
            font-weight: 600;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .user-name {
            color: #666;
            font-weight: 500;
        }

        .logout-btn {
            background: #e74c3c;
            color: white;
            border: none;
            padding: 8px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            transition: background 0.3s;
        }

        .logout-btn:hover {
            background: #c0392b;
        }

        /* Cards de Estatísticas */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            transition: transform 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-icon {
            width: 60px;
            height: 60px;
            background: #f0f3ff;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 20px;
        }

        .stat-icon span {
            font-size: 30px;
        }

        .stat-info h3 {
            color: #666;
            font-size: 14px;
            font-weight: 500;
            margin-bottom: 5px;
        }

        .stat-info .number {
            color: #333;
            font-size: 28px;
            font-weight: 700;
        }

        .stat-info .label {
            color: #999;
            font-size: 12px;
            margin-top: 3px;
        }

        /* Seções */
        .section {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .section-header h2 {
            color: #333;
            font-size: 18px;
            font-weight: 600;
        }

        .section-header button {
            background: #667eea;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: background 0.3s;
        }

        .section-header button:hover {
            background: #5a67d8;
        }

        /* Listas */
        .list-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            border-bottom: 1px solid #f0f0f0;
            transition: background 0.3s;
        }

        .list-item:last-child {
            border-bottom: none;
        }

        .list-item:hover {
            background: #f8f9fa;
        }

        .item-info h4 {
            color: #333;
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .item-info p {
            color: #666;
            font-size: 13px;
        }

        .item-info small {
            color: #999;
            font-size: 12px;
        }

        .item-status {
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 500;
        }

        .status-low {
            background: #fee7e7;
            color: #e74c3c;
        }

        .status-ok {
            background: #e6f7e6;
            color: #27ae60;
        }

        .status-loan {
            background: #e1f5fe;
            color: #17a2b8;
        }

        .item-actions {
            display: flex;
            gap: 10px;
        }

        .item-actions button {
            padding: 5px 12px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 500;
            transition: opacity 0.3s;
        }

        .item-actions button:hover {
            opacity: 0.8;
        }

        .btn-edit {
            background: #3498db;
            color: white;
        }

        .btn-loan {
            background: #17a2b8;
            color: white;
        }

        .btn-delete {
            background: #e74c3c;
            color: white;
        }

        .btn-return {
            background: #28a745;
            color: white;
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: 40px;
            color: #999;
        }

        .empty-state span {
            font-size: 50px;
            display: block;
            margin-bottom: 15px;
            opacity: 0.5;
        }

        .empty-state p {
            font-size: 16px;
        }

        /* Filtros */
        .filters {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .search-box {
            flex: 1;
            min-width: 250px;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
        }

        .category-filter {
            display: flex;
            gap: 8px;
            overflow-x: auto;
            padding: 5px 0;
        }

        .category-filter button {
            padding: 8px 15px;
            border: none;
            border-radius: 20px;
            background: #f0f0f0;
            color: #666;
            font-weight: 500;
            font-size: 13px;
            cursor: pointer;
            white-space: nowrap;
        }

        .category-filter button.active {
            background: #667eea;
            color: white;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            border-radius: 15px;
            padding: 30px;
            max-width: 500px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-header h2 {
            color: #333;
            font-size: 20px;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #999;
        }

        .modal-form {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .modal-form input,
        .modal-form select,
        .modal-form textarea {
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
        }

        .modal-form button {
            background: #27ae60;
            color: white;
            border: none;
            padding: 15px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }

        /* Login */
        .login-container {
            max-width: 400px;
            margin: 100px auto;
            background: white;
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
        }

        .login-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .login-header h1 {
            color: #333;
            font-size: 28px;
            margin-bottom: 10px;
        }

        .login-header p {
            color: #666;
            font-size: 14px;
        }

        .login-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .login-form input {
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
        }

        .login-form button {
            background: #667eea;
            color: white;
            border: none;
            padding: 15px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <!-- Tela de Login -->
    <div id="loginScreen" class="login-container">
        <div class="login-header">
            <h1>Controle de Estoque</h1>
            <p>Faça login para acessar o sistema</p>
        </div>
        <div class="login-form">
            <input type="text" id="username" placeholder="Usuário" value="admin">
            <input type="password" id="password" placeholder="Senha" value="123456">
            <button onclick="login()">Entrar</button>
        </div>
    </div>

    <!-- Aplicativo Principal -->
    <div id="appScreen" class="app-container hidden">
        <!-- Menu Lateral -->
        <div class="sidebar">
            <div class="logo">
                <h2>Controle de Estoque</h2>
                <p>Menu Principal</p>
            </div>
            
            <div class="menu-item active" onclick="showSection('dashboard')">
                <span>📊</span>
                <span class="menu-text">Dashboard</span>
            </div>
            <div class="menu-item" onclick="showSection('products')">
                <span>📦</span>
                <span class="menu-text">Produtos</span>
            </div>
            <div class="menu-item" onclick="showSection('loans')">
                <span>🔧</span>
                <span class="menu-text">Empréstimos</span>
            </div>
        </div>

        <!-- Conteúdo Principal -->
        <div class="main-content">
            <!-- Header -->
            <div class="header">
                <h1 id="sectionTitle">Dashboard</h1>
                <div class="user-info">
                    <span class="user-name">admin</span>
                    <button class="logout-btn" onclick="logout()">Sair</button>
                </div>
            </div>

            <!-- Seção Dashboard -->
            <div id="dashboardSection">
                <!-- Cards de Estatísticas -->
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-icon">
                            <span>📦</span>
                        </div>
                        <div class="stat-info">
                            <h3>Total de Produtos</h3>
                            <div class="number" id="totalProducts">0</div>
                            <div class="label">itens cadastrados</div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">
                            <span>⚠️</span>
                        </div>
                        <div class="stat-info">
                            <h3>Estoque Baixo</h3>
                            <div class="number" id="lowStockCount">0</div>
                            <div class="label">produtos</div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">
                            <span>🔧</span>
                        </div>
                        <div class="stat-info">
                            <h3>Emprestados</h3>
                            <div class="number" id="loanedCount">0</div>
                            <div class="label">itens</div>
                        </div>
                    </div>
                </div>

                <!-- Estoque Baixo -->
                <div class="section">
                    <div class="section-header">
                        <h2>📦 Estoque Baixo</h2>
                    </div>
                    <div id="lowStockList" class="empty-state">
                        <span>✅</span>
                        <p>Nenhum produto com estoque baixo</p>
                    </div>
                </div>

                <!-- Empréstimos Ativos -->
                <div class="section">
                    <div class="section-header">
                        <h2>🔧 Empréstimos Ativos</h2>
                    </div>
                    <div id="activeLoansList" class="empty-state">
                        <span>📭</span>
                        <p>Nenhum empréstimo ativo</p>
                    </div>
                </div>
            </div>

            <!-- Seção Produtos -->
            <div id="productsSection" class="hidden">
                <div class="section">
                    <div class="section-header">
                        <h2>📦 Todos os Produtos</h2>
                        <button onclick="openProductModal()">
                            <span>+</span> Novo Produto
                        </button>
                    </div>

                    <div class="filters">
                        <input type="text" class="search-box" id="searchProduct" placeholder="Buscar por nome ou local..." onkeyup="filterProducts()">
                        <div class="category-filter" id="categoryFilter"></div>
                    </div>

                    <div id="productsList"></div>
                </div>
            </div>

            <!-- Seção Empréstimos -->
            <div id="loansSection" class="hidden">
                <div class="section">
                    <div class="section-header">
                        <h2>🔧 Gerenciar Empréstimos</h2>
                        <button onclick="openLoanModal()">
                            <span>+</span> Novo Empréstimo
                        </button>
                    </div>

                    <div id="allLoansList"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Produto -->
    <div id="productModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="modalTitle">Novo Produto</h2>
                <button class="close-btn" onclick="closeModal('productModal')">&times;</button>
            </div>
            <div class="modal-form">
                <input type="text" id="productName" placeholder="Nome do produto">
                <input type="text" id="productLocal" placeholder="Localização">
                <select id="productCategory">
                    <option value="">Selecione a categoria</option>
                    <option value="Jardim">Jardim</option>
                    <option value="Elétrica">Elétrica</option>
                    <option value="Ferramentas">Ferramentas</option>
                    <option value="EPI">EPI</option>
                    <option value="Hidráulica">Hidráulica</option>
                    <option value="Geral">Geral</option>
                </select>
                <input type="number" id="productQuantity" placeholder="Quantidade">
                <input type="number" id="productMinQuantity" placeholder="Quantidade mínima">
                <input type="hidden" id="editingProductId">
                <button onclick="saveProduct()">Salvar</button>
            </div>
        </div>
    </div>

    <!-- Modal de Empréstimo -->
    <div id="loanModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Novo Empréstimo</h2>
                <button class="close-btn" onclick="closeModal('loanModal')">&times;</button>
            </div>
            <div class="modal-form">
                <input type="text" id="loanUserName" placeholder="Nome de quem está pegando">
                <select id="loanProduct"></select>
                <input type="number" id="loanQuantity" placeholder="Quantidade" value="1">
                <input type="date" id="loanDate">
                <textarea id="loanObservation" placeholder="Observação"></textarea>
                <button onclick="saveLoan()">Registrar</button>
            </div>
        </div>
    </div>

    <!-- Modal de Devolução -->
    <div id="returnModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Registrar Devolução</h2>
                <button class="close-btn" onclick="closeModal('returnModal')">&times;</button>
            </div>
            <div class="modal-form">
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 15px;" id="returnInfo"></div>
                <input type="date" id="returnDate">
                <textarea id="returnObservation" placeholder="Observação"></textarea>
                <input type="hidden" id="returnLoanId">
                <button onclick="saveReturn()">Confirmar</button>
            </div>
        </div>
    </div>

    <script>
        // DADOS INICIAIS
        let products = JSON.parse(localStorage.getItem('products')) || [
            { id: 1, name: 'Tesoura de Poda', local: 'Prateleira A1', category: 'Jardim', quantity: 8, minQuantity: 3 },
            { id: 2, name: 'Alicate Universal', local: 'Gaveta 10', category: 'Elétrica', quantity: 5, minQuantity: 2 },
            { id: 3, name: 'Martelo', local: 'Prateleira B1', category: 'Ferramentas', quantity: 10, minQuantity: 4 },
            { id: 4, name: 'Luva de Raspa', local: 'Armário D1', category: 'EPI', quantity: 12, minQuantity: 5 },
            { id: 5, name: 'Fita Veda-rosca', local: 'Gaveta 16', category: 'Hidráulica', quantity: 15, minQuantity: 5 },
            { id: 6, name: 'Cadeado', local: 'Gaveta 17', category: 'Geral', quantity: 8, minQuantity: 3 }
        ];
        
        let loans = JSON.parse(localStorage.getItem('loans')) || [];
        let movements = JSON.parse(localStorage.getItem('movements')) || [];
        let currentUser = null;
        let currentCategory = 'todos';

        // LOGIN
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === 'admin' && password === '123456') {
                currentUser = { name: username };
                document.getElementById('loginScreen').classList.add('hidden');
                document.getElementById('appScreen').classList.remove('hidden');
                updateDashboard();
                loadProducts();
                loadCategoryFilter();
                loadLoanProductSelect();
            } else {
                alert('Usuário ou senha incorretos! Use admin / 123456');
            }
        }

        function logout() {
            currentUser = null;
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('appScreen').classList.add('hidden');
        }

        // NAVEGAÇÃO
        function showSection(section) {
            document.querySelectorAll('.menu-item').forEach(item => item.classList.remove('active'));
            event.currentTarget.classList.add('active');
            
            document.getElementById('dashboardSection').classList.add('hidden');
            document.getElementById('productsSection').classList.add('hidden');
            document.getElementById('loansSection').classList.add('hidden');
            
            document.getElementById(section + 'Section').classList.remove('hidden');
            
            const titles = {
                'dashboard': 'Dashboard',
                'products': 'Produtos',
                'loans': 'Empréstimos'
            };
            document.getElementById('sectionTitle').textContent = titles[section];
            
            if (section === 'products') {
                loadProducts();
                loadCategoryFilter();
            } else if (section === 'loans') {
                loadAllLoans();
            }
        }

        // DASHBOARD
        function updateDashboard() {
            document.getElementById('totalProducts').textContent = products.length;
            
            const lowStock = products.filter(p => p.quantity <= p.minQuantity);
            document.getElementById('lowStockCount').textContent = lowStock.length;
            
            const activeLoans = loans.filter(l => !l.returned);
            document.getElementById('loanedCount').textContent = activeLoans.length;
            
            // Lista de estoque baixo
            const lowStockList = document.getElementById('lowStockList');
            if (lowStock.length > 0) {
                lowStockList.innerHTML = lowStock.map(p => `
                    <div class="list-item">
                        <div class="item-info">
                            <h4>${p.name}</h4>
                            <p>📍 ${p.local}</p>
                            <small>Mínimo: ${p.minQuantity}</small>
                        </div>
                        <div class="item-status status-low">
                            ${p.quantity} unid.
                        </div>
                    </div>
                `).join('');
            } else {
                lowStockList.innerHTML = `
                    <div class="empty-state">
                        <span>✅</span>
                        <p>Nenhum produto com estoque baixo</p>
                    </div>
                `;
            }
            
            // Lista de empréstimos ativos
            const activeLoansList = document.getElementById('activeLoansList');
            if (activeLoans.length > 0) {
                activeLoansList.innerHTML = activeLoans.map(l => `
                    <div class="list-item">
                        <div class="item-info">
                            <h4>${l.productName}</h4>
                            <p>👤 ${l.userName}</p>
                            <p>📍 ${l.productLocal}</p>
                            <small>📅 ${l.date}</small>
                        </div>
                        <div class="item-status status-loan">
                            ${l.quantity} unid.
                        </div>
                        <div class="item-actions">
                            <button class="btn-return" onclick="openReturnModal(${l.id})">Devolver</button>
                        </div>
                    </div>
                `).join('');
            } else {
                activeLoansList.innerHTML = `
                    <div class="empty-state">
                        <span>📭</span>
                        <p>Nenhum empréstimo ativo</p>
                    </div>
                `;
            }
        }

        // PRODUTOS
        function loadCategoryFilter() {
            const cats = ['todos', ...new Set(products.map(p => p.category))];
            const filterDiv = document.getElementById('categoryFilter');
            
            filterDiv.innerHTML = cats.map(cat => 
                `<button class="${cat === 'todos' ? 'active' : ''}" onclick="filterByCategory('${cat}')">
                    ${cat === 'todos' ? 'Todos' : cat}
                </button>`
            ).join('');
        }

        function filterByCategory(cat) {
            currentCategory = cat;
            document.querySelectorAll('#categoryFilter button').forEach(btn => {
                btn.classList.remove('active');
                if (btn.textContent === (cat === 'todos' ? 'Todos' : cat)) {
                    btn.classList.add('active');
                }
            });
            filterProducts();
        }

        function filterProducts() {
            const search = document.getElementById('searchProduct').value.toLowerCase();
            const filtered = products.filter(p => 
                (currentCategory === 'todos' || p.category === currentCategory) &&
                (p.name.toLowerCase().includes(search) || p.local.toLowerCase().includes(search))
            );
            displayProducts(filtered);
        }

        function displayProducts(list) {
            const activeLoans = loans.filter(l => !l.returned);
            
            document.getElementById('productsList').innerHTML = list.map(p => {
                const loaned = activeLoans.filter(l => l.productId === p.id).reduce((s, l) => s + l.quantity, 0);
                const available = p.quantity - loaned;
                
                return `
                    <div class="list-item">
                        <div class="item-info">
                            <h4>${p.name}</h4>
                            <p>📍 ${p.local}</p>
                            <p>🏷️ ${p.category}</p>
                            ${loaned > 0 ? `<small>🔧 ${loaned} emprestado(s)</small>` : ''}
                        </div>
                        <div class="item-status ${p.quantity <= p.minQuantity ? 'status-low' : 'status-ok'}">
                            Disponível: ${available}
                        </div>
                        <div class="item-actions">
                            <button class="btn-edit" onclick="editProduct(${p.id})">Editar</button>
                            <button class="btn-loan" onclick="openLoanModal(${p.id})">Emprestar</button>
                            <button class="btn-delete" onclick="deleteProduct(${p.id})">Excluir</button>
                        </div>
                    </div>
                `;
            }).join('') || '<div class="empty-state"><span>🔍</span><p>Nenhum item encontrado</p></div>';
        }

        function loadProducts() {
            filterProducts();
        }

        function openProductModal() {
            document.getElementById('modalTitle').textContent = 'Novo Produto';
            document.getElementById('productName').value = '';
            document.getElementById('productLocal').value = '';
            document.getElementById('productCategory').value = '';
            document.getElementById('productQuantity').value = '';
            document.getElementById('productMinQuantity').value = '';
            document.getElementById('editingProductId').value = '';
            document.getElementById('productModal').classList.add('active');
        }

        function editProduct(id) {
            const p = products.find(p => p.id === id);
            if (p) {
                document.getElementById('modalTitle').textContent = 'Editar Produto';
                document.getElementById('productName').value = p.name;
                document.getElementById('productLocal').value = p.local;
                document.getElementById('productCategory').value = p.category;
                document.getElementById('productQuantity').value = p.quantity;
                document.getElementById('productMinQuantity').value = p.minQuantity;
                document.getElementById('editingProductId').value = id;
                document.getElementById('productModal').classList.add('active');
            }
        }

        function saveProduct() {
            const id = document.getElementById('editingProductId').value;
            const product = {
                name: document.getElementById('productName').value,
                local: document.getElementById('productLocal').value,
                category: document.getElementById('productCategory').value,
                quantity: parseInt(document.getElementById('productQuantity').value) || 0,
                minQuantity: parseInt(document.getElementById('productMinQuantity').value) || 0
            };
            
            if (!product.name || !product.local || !product.category) {
                alert('Preencha todos os campos!');
                return;
            }
            
            if (id) {
                const index = products.findIndex(p => p.id == id);
                products[index] = { ...products[index], ...product };
            } else {
                product.id = Date.now();
                products.push(product);
            }
            
            localStorage.setItem('products', JSON.stringify(products));
            closeModal('productModal');
            loadProducts();
            updateDashboard();
            loadCategoryFilter();
            loadLoanProductSelect();
        }

        function deleteProduct(id) {
            if (confirm('Excluir este item?')) {
                products = products.filter(p => p.id !== id);
                localStorage.setItem('products', JSON.stringify(products));
                loadProducts();
                updateDashboard();
                loadCategoryFilter();
            }
        }

        // EMPRÉSTIMOS
        function loadLoanProductSelect() {
            const select = document.getElementById('loanProduct');
            const activeLoans = loans.filter(l => !l.returned);
            
            select.innerHTML = '<option value="">Selecione um item</option>' +
                products.map(p => {
                    const loaned = activeLoans.filter(l => l.productId === p.id).reduce((s, l) => s + l.quantity, 0);
                    const available = p.quantity - loaned;
                    return `<option value="${p.id}" ${available <= 0 ? 'disabled' : ''}>
                        ${p.name} (Disponível: ${available})
                    </option>`;
                }).join('');
        }

        function openLoanModal(productId = null) {
            document.getElementById('loanUserName').value = '';
            document.getElementById('loanQuantity').value = '1';
            document.getElementById('loanDate').value = new Date().toISOString().split('T')[0];
            document.getElementById('loanObservation').value = '';
            if (productId) document.getElementById('loanProduct').value = productId;
            document.getElementById('loanModal').classList.add('active');
        }

        function saveLoan() {
            const user = document.getElementById('loanUserName').value;
            const pid = parseInt(document.getElementById('loanProduct').value);
            const qty = parseInt(document.getElementById('loanQuantity').value);
            const date = document.getElementById('loanDate').value;
            
            if (!user || !pid || !qty || !date) {
                alert('Preencha todos os campos!');
                return;
            }
            
            const product = products.find(p => p.id === pid);
            
            loans.push({
                id: Date.now(),
                userName: user,
                productId: pid,
                productName: product.name,
                productLocal: product.local,
                quantity: qty,
                date,
                returned: false
            });
            
            movements.push({
                id: Date.now() + 1,
                productId: pid,
                productName: product.name,
                quantity: qty,
                date,
                type: 'loan'
            });
            
            localStorage.setItem('loans', JSON.stringify(loans));
            localStorage.setItem('movements', JSON.stringify(movements));
            
            closeModal('loanModal');
            updateDashboard();
            loadProducts();
            loadLoanProductSelect();
            showSection('dashboard');
        }

        function loadAllLoans() {
            const list = document.getElementById('allLoansList');
            const active = loans.filter(l => !l.returned);
            const returned = loans.filter(l => l.returned);
            
            if (active.length === 0 && returned.length === 0) {
                list.innerHTML = '<div class="empty-state"><span>📭</span><p>Nenhum empréstimo registrado</p></div>';
                return;
            }
            
            let html = '<h3 style="margin-bottom: 15px;">🔧 Empréstimos Ativos</h3>';
            
            if (active.length > 0) {
                html += active.map(l => `
                    <div class="list-item">
                        <div class="item-info">
                            <h4>${l.productName}</h4>
                            <p>👤 ${l.userName}</p>
                            <p>📍 ${l.productLocal}</p>
                            <small>📅 ${l.date}</small>
                        </div>
                        <div class="item-status status-loan">
                            ${l.quantity} unid.
                        </div>
                        <div class="item-actions">
                            <button class="btn-return" onclick="openReturnModal(${l.id})">Devolver</button>
                        </div>
                    </div>
                `).join('');
            } else {
                html += '<p style="color: #999; padding: 15px;">Nenhum empréstimo ativo</p>';
            }
            
            if (returned.length > 0) {
                html += '<h3 style="margin: 30px 0 15px;">✅ Histórico de Devoluções</h3>';
                html += returned.slice(0, 5).map(l => `
                    <div class="list-item">
                        <div class="item-info">
                            <h4>${l.productName}</h4>
                            <p>👤 ${l.userName}</p>
                            <p>📅 Empréstimo: ${l.date}</p>
                            <p>✅ Devolução: ${l.returnDate || 'N/A'}</p>
                        </div>
                        <div class="item-status status-ok">
                            ${l.quantity} unid.
                        </div>
                    </div>
                `).join('');
            }
            
            list.innerHTML = html;
        }

        function openReturnModal(loanId) {
            const loan = loans.find(l => l.id === loanId);
            if (loan) {
                document.getElementById('returnInfo').innerHTML = `
                    <strong>Devolução:</strong><br>
                    👤 ${loan.userName}<br>
                    🔧 ${loan.productName}<br>
                    📦 Quantidade: ${loan.quantity}
                `;
                document.getElementById('returnDate').value = new Date().toISOString().split('T')[0];
                document.getElementById('returnLoanId').value = loanId;
                document.getElementById('returnModal').classList.add('active');
            }
        }

        function saveReturn() {
            const loanId = parseInt(document.getElementById('returnLoanId').value);
            const returnDate = document.getElementById('returnDate').value;
            
            const index = loans.findIndex(l => l.id === loanId);
            if (index === -1) return;
            
            loans[index].returned = true;
            loans[index].returnDate = returnDate;
            
            movements.push({
                id: Date.now(),
                productId: loans[index].productId,
                productName: loans[index].productName,
                quantity: loans[index].quantity,
                date: returnDate,
                type: 'return'
            });
            
            localStorage.setItem('loans', JSON.stringify(loans));
            localStorage.setItem('movements', JSON.stringify(movements));
            
            closeModal('returnModal');
            updateDashboard();
            loadProducts();
            loadLoanProductSelect();
            showSection('dashboard');
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
        }
    </script>
</body>
</html>
