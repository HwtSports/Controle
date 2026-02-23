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
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background: #0a0a0a;
            min-height: 100vh;
            color: #e0e0e0;
        }

        .app-container {
            display: flex;
            min-height: 100vh;
        }

        /* Menu Lateral */
        .sidebar {
            width: 260px;
            background: #1a1a1a;
            box-shadow: 2px 0 12px rgba(0,0,0,0.5);
            padding: 32px 0;
            border-right: 1px solid #333;
            height: auto;
            align-self: flex-start;
        }

        .logo {
            padding: 0 24px 32px 24px;
            border-bottom: 1px solid #333;
            margin-bottom: 24px;
        }

        .logo h2 {
            color: #f97316;
            font-size: 20px;
            font-weight: 700;
            letter-spacing: -0.02em;
        }

        .logo p {
            color: #aaa;
            font-size: 13px;
            margin-top: 4px;
        }

        .menu-item {
            display: flex;
            align-items: center;
            padding: 12px 24px;
            color: #ccc;
            text-decoration: none;
            transition: all 0.2s;
            cursor: pointer;
            border-left: 3px solid transparent;
            margin: 4px 0;
        }

        .menu-item:hover {
            background: #2a2a2a;
            color: #f97316;
        }

        .menu-item.active {
            background: #2a2a2a;
            color: #f97316;
            border-left-color: #f97316;
        }

        .menu-item span {
            font-size: 20px;
            margin-right: 14px;
        }

        .menu-item .menu-text {
            font-size: 14px;
            font-weight: 500;
        }

        /* Conteúdo Principal */
        .main-content {
            flex: 1;
            padding: 32px;
        }

        /* Header */
        .header {
            background: #1a1a1a;
            border-radius: 20px;
            padding: 24px 32px;
            margin-bottom: 32px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #333;
        }

        .header h1 {
            color: #f97316;
            font-size: 24px;
            font-weight: 700;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 24px;
        }

        .user-name {
            color: #ccc;
            font-weight: 500;
            font-size: 14px;
        }

        .logout-btn {
            background: #f97316;
            color: #0a0a0a;
            border: none;
            padding: 8px 20px;
            border-radius: 40px;
            cursor: pointer;
            font-weight: 500;
            font-size: 13px;
            transition: all 0.2s;
        }

        .logout-btn:hover {
            background: #fb923c;
        }

        /* Cards de Estatísticas (agora clicáveis) */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 24px;
            margin-bottom: 32px;
        }

        .stat-card {
            background: #1a1a1a;
            border-radius: 20px;
            padding: 24px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            display: flex;
            align-items: center;
            transition: transform 0.2s, box-shadow 0.2s;
            border: 1px solid #333;
            cursor: pointer;
        }

        .stat-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 24px rgba(0,0,0,0.5);
            border-color: #f97316;
        }

        .stat-icon {
            width: 56px;
            height: 56px;
            background: #2a2a2a;
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 20px;
        }

        .stat-icon span {
            font-size: 28px;
        }

        .stat-info h3 {
            color: #aaa;
            font-size: 13px;
            font-weight: 500;
            margin-bottom: 4px;
        }

        .stat-info .number {
            color: #f97316;
            font-size: 28px;
            font-weight: 700;
        }

        .stat-info .label {
            color: #888;
            font-size: 12px;
            margin-top: 2px;
        }

        /* Seções (agora usadas apenas nas abas) */
        .section {
            background: #1a1a1a;
            border-radius: 20px;
            padding: 28px;
            margin-bottom: 32px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            border: 1px solid #333;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .section-header h2 {
            color: #f97316;
            font-size: 18px;
            font-weight: 700;
        }

        .section-header button {
            background: #f97316;
            color: #0a0a0a;
            border: none;
            padding: 10px 20px;
            border-radius: 40px;
            cursor: pointer;
            font-weight: 500;
            font-size: 13px;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.2s;
        }

        .section-header button:hover {
            background: #fb923c;
            transform: scale(1.02);
        }

        .btn-secondary {
            background: #2a2a2a !important;
            color: #f97316 !important;
        }

        .btn-secondary:hover {
            background: #333 !important;
        }

        /* Listas */
        .list-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px;
            border-bottom: 1px solid #333;
            transition: background 0.2s;
        }

        .list-item:last-child {
            border-bottom: none;
        }

        .list-item:hover {
            background: #2a2a2a;
            border-radius: 12px;
        }

        .item-info h4 {
            color: #f97316;
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .item-info p {
            color: #ccc;
            font-size: 13px;
        }

        .item-info small {
            color: #888;
            font-size: 12px;
        }

        .item-status {
            padding: 4px 12px;
            border-radius: 40px;
            font-size: 12px;
            font-weight: 600;
        }

        .status-low {
            background: #442a2a;
            color: #f97316;
        }

        .status-ok {
            background: #1a3a1a;
            color: #4caf50;
        }

        .status-loan {
            background: #1a3a4a;
            color: #42a5f5;
        }

        .status-archived {
            background: #333;
            color: #aaa;
        }

        .item-actions {
            display: flex;
            gap: 8px;
        }

        .item-actions button {
            padding: 6px 12px;
            border: none;
            border-radius: 40px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 500;
            transition: all 0.2s;
        }

        .item-actions button:hover {
            transform: translateY(-2px);
            filter: brightness(0.9);
        }

        .btn-edit {
            background: #2a2a2a;
            color: #f97316;
        }

        .btn-loan {
            background: #42a5f5;
            color: #0a0a0a;
        }

        .btn-delete {
            background: #f44336;
            color: #0a0a0a;
        }

        .btn-return {
            background: #4caf50;
            color: #0a0a0a;
        }

        .btn-permanent {
            background: #f97316;
            color: #0a0a0a;
        }

        .btn-restore {
            background: #fbbf24;
            color: #0a0a0a;
        }

        .btn-view {
            background: #a855f7;
            color: #0a0a0a;
        }

        .empty-state {
            text-align: center;
            padding: 48px 20px;
            color: #888;
        }

        .empty-state span {
            font-size: 48px;
            display: block;
            margin-bottom: 16px;
            opacity: 0.6;
        }

        .empty-state p {
            font-size: 14px;
        }

        .filters {
            display: flex;
            gap: 16px;
            margin-bottom: 24px;
            flex-wrap: wrap;
        }

        .search-box {
            flex: 1;
            min-width: 250px;
            padding: 12px 16px;
            border: 2px solid #333;
            border-radius: 40px;
            font-size: 14px;
            background: #2a2a2a;
            color: #e0e0e0;
            transition: border-color 0.2s;
        }

        .search-box:focus {
            outline: none;
            border-color: #f97316;
        }

        .category-filter {
            display: flex;
            gap: 8px;
            overflow-x: auto;
            padding: 4px 0;
        }

        .category-filter button {
            padding: 8px 16px;
            border: none;
            border-radius: 40px;
            background: #2a2a2a;
            color: #ccc;
            font-weight: 500;
            font-size: 13px;
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.2s;
        }

        .category-filter button.active {
            background: #f97316;
            color: #0a0a0a;
        }

        .date-filter {
            padding: 10px 16px;
            border: 2px solid #333;
            border-radius: 40px;
            font-size: 13px;
            background: #2a2a2a;
            color: #e0e0e0;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(4px);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: #1a1a1a;
            border-radius: 24px;
            padding: 32px;
            max-width: 500px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
            border: 1px solid #333;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-header h2 {
            color: #f97316;
            font-size: 20px;
            font-weight: 700;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #888;
        }

        .modal-form {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .modal-form input,
        .modal-form select,
        .modal-form textarea {
            padding: 14px;
            border: 2px solid #333;
            border-radius: 12px;
            font-size: 14px;
            background: #2a2a2a;
            color: #e0e0e0;
            transition: border-color 0.2s;
        }

        .modal-form input:focus,
        .modal-form select:focus,
        .modal-form textarea:focus {
            outline: none;
            border-color: #f97316;
        }

        .modal-form button {
            background: #f97316;
            color: #0a0a0a;
            border: none;
            padding: 16px;
            border-radius: 12px;
            font-weight: 600;
            font-size: 15px;
            cursor: pointer;
            margin-top: 8px;
            transition: background 0.2s;
        }

        .modal-form button:hover {
            background: #fb923c;
        }

        .datetime-row {
            display: flex;
            gap: 10px;
        }

        .datetime-row input {
            flex: 1;
        }

        /* Login */
        .login-container {
            max-width: 380px;
            margin: 120px auto;
            background: #1a1a1a;
            border-radius: 32px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
            border: 1px solid #333;
        }

        .login-header {
            text-align: center;
            margin-bottom: 32px;
        }

        .login-header h1 {
            color: #f97316;
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 8px;
        }

        .login-header p {
            color: #aaa;
            font-size: 14px;
        }

        .login-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .login-form input {
            padding: 16px;
            border: 2px solid #333;
            border-radius: 16px;
            font-size: 15px;
            background: #2a2a2a;
            color: #e0e0e0;
        }

        .login-form button {
            background: #f97316;
            color: #0a0a0a;
            border: none;
            padding: 16px;
            border-radius: 16px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }

        .login-form button:hover {
            background: #fb923c;
        }

        .hidden {
            display: none !important;
        }

        .timeline {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .timeline-item {
            display: flex;
            align-items: center;
            gap: 16px;
            padding: 12px;
            background: #2a2a2a;
            border-radius: 12px;
        }

        .timeline-icon {
            width: 40px;
            height: 40px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
        }

        .timeline-content {
            flex: 1;
        }

        .timeline-content h4 {
            font-size: 14px;
            font-weight: 600;
            color: #f97316;
        }

        .timeline-content p {
            font-size: 12px;
            color: #ccc;
        }
    </style>
</head>
<body>
    <!-- Tela de Login -->
    <div id="loginScreen" class="login-container">
        <div class="login-header">
            <h1>Sistema de Estoque</h1>
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
                <span class="menu-text">Painel</span>
            </div>
            <div class="menu-item" onclick="showSection('products')">
                <span>📦</span>
                <span class="menu-text">Produtos</span>
            </div>
            <div class="menu-item" onclick="showSection('loans')">
                <span>🔧</span>
                <span class="menu-text">Empréstimos</span>
            </div>
            <div class="menu-item" onclick="showSection('permanent')">
                <span>🗑️</span>
                <span class="menu-text">Retiradas</span>
            </div>
            <div class="menu-item" onclick="showSection('history')">
                <span>📋</span>
                <span class="menu-text">Histórico</span>
            </div>
        </div>

        <!-- Conteúdo Principal -->
        <div class="main-content">
            <!-- Header -->
            <div class="header">
                <h1 id="sectionTitle">Painel</h1>
                <div class="user-info">
                    <span class="user-name">admin</span>
                    <button class="logout-btn" onclick="logout()">Sair</button>
                </div>
            </div>

            <!-- Seção Painel (agora apenas com cards clicáveis) -->
            <div id="dashboardSection">
                <div class="stats-grid">
                    <div class="stat-card" onclick="showSection('products')">
                        <div class="stat-icon">
                            <span>📦</span>
                        </div>
                        <div class="stat-info">
                            <h3>Total de Produtos</h3>
                            <div class="number" id="totalProducts">0</div>
                            <div class="label">itens ativos</div>
                        </div>
                    </div>
                    <div class="stat-card" onclick="showSection('products', 'lowStock')">
                        <div class="stat-icon">
                            <span>⚠️</span>
                        </div>
                        <div class="stat-info">
                            <h3>Estoque Baixo</h3>
                            <div class="number" id="lowStockCount">0</div>
                            <div class="label">produtos</div>
                        </div>
                    </div>
                    <div class="stat-card" onclick="showSection('loans')">
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

                <!-- Últimas Movimentações (mantido como resumo) -->
                <div class="section">
                    <div class="section-header">
                        <h2>📋 Últimas Movimentações</h2>
                        <button class="btn-secondary" onclick="showSection('history')">Ver todas</button>
                    </div>
                    <div id="recentMovementsList" class="empty-state">
                        <span>📊</span>
                        <p>Nenhuma movimentação recente</p>
                    </div>
                </div>
            </div>

            <!-- Seção Produtos -->
            <div id="productsSection" class="hidden">
                <div class="section">
                    <div class="section-header">
                        <h2>📦 Produtos Ativos</h2>
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

            <!-- Seção Retiradas -->
            <div id="permanentSection" class="hidden">
                <div class="section">
                    <div class="section-header">
                        <h2>🗑️ Retiradas Permanentes</h2>
                        <p style="color: #aaa;">Itens retirados para uso único (não serão devolvidos)</p>
                    </div>

                    <div id="permanentList"></div>
                </div>
            </div>

            <!-- Seção Histórico -->
            <div id="historySection" class="hidden">
                <div class="section">
                    <div class="section-header">
                        <h2>📋 Histórico de Movimentações</h2>
                        <div>
                            <input type="date" id="historyDate" class="date-filter" onchange="loadHistory()">
                        </div>
                    </div>

                    <div id="historyList"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modais (mantidos iguais) -->
    <div id="productModal" class="modal">...</div>
    <div id="loanModal" class="modal">...</div>
    <div id="returnModal" class="modal">...</div>
    <div id="permanentModal" class="modal">...</div>

    <script>
        // (todo o JavaScript permanece o mesmo, apenas adicionei um parâmetro opcional na showSection)
        
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
                loadPermanentItems();
                loadHistory();
            } else {
                alert('Usuário ou senha incorretos! Use admin / 123456');
            }
        }

        function logout() {
            currentUser = null;
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('appScreen').classList.add('hidden');
        }

        // NAVEGAÇÃO (agora com parâmetro opcional para filtrar)
        function showSection(section, filter) {
            document.querySelectorAll('.menu-item').forEach(item => item.classList.remove('active'));
            
            // Ativar o item do menu correspondente
            const menuMap = {
                'dashboard': 0,
                'products': 1,
                'loans': 2,
                'permanent': 3,
                'history': 4
            };
            if (menuMap[section] !== undefined) {
                document.querySelectorAll('.menu-item')[menuMap[section]].classList.add('active');
            }
            
            document.getElementById('dashboardSection').classList.add('hidden');
            document.getElementById('productsSection').classList.add('hidden');
            document.getElementById('loansSection').classList.add('hidden');
            document.getElementById('historySection').classList.add('hidden');
            document.getElementById('permanentSection').classList.add('hidden');
            
            document.getElementById(section + 'Section').classList.remove('hidden');
            
            const titles = {
                'dashboard': 'Painel',
                'products': 'Produtos',
                'loans': 'Empréstimos',
                'history': 'Histórico',
                'permanent': 'Retiradas'
            };
            document.getElementById('sectionTitle').textContent = titles[section];
            
            if (section === 'products') {
                loadProducts();
                loadCategoryFilter();
                // Se veio do filtro de estoque baixo, podemos destacar ou filtrar
                if (filter === 'lowStock') {
                    // Opcional: aplicar filtro de estoque baixo
                    document.getElementById('searchProduct').value = '';
                    currentCategory = 'todos';
                    filterProducts();
                }
            } else if (section === 'loans') {
                loadAllLoans();
            } else if (section === 'history') {
                loadHistory();
            } else if (section === 'permanent') {
                loadPermanentItems();
            }
        }

        // DASHBOARD
        function updateDashboard() {
            document.getElementById('totalProducts').textContent = products.length;
            
            const lowStock = products.filter(p => p.quantity <= p.minQuantity);
            document.getElementById('lowStockCount').textContent = lowStock.length;
            
            const activeLoans = loans.filter(l => !l.returned);
            document.getElementById('loanedCount').textContent = activeLoans.length;
            
            // Últimas movimentações
            const recentMovements = movements.slice(-5).reverse();
            const recentList = document.getElementById('recentMovementsList');
            if (recentMovements.length > 0) {
                recentList.innerHTML = recentMovements.map(m => {
                    let icon = m.type === 'entry' ? '📥' : m.type === 'exit' ? '📤' : m.type === 'loan' ? '🔧' : m.type === 'return' ? '↩️' : '🗑️';
                    let color = m.type === 'entry' ? '#4caf50' : m.type === 'exit' ? '#f44336' : m.type === 'loan' ? '#42a5f5' : m.type === 'return' ? '#4caf50' : '#f97316';
                    return `
                        <div class="timeline-item">
                            <div class="timeline-icon" style="background: ${color}20; color: ${color}">
                                ${icon}
                            </div>
                            <div class="timeline-content">
                                <h4>${m.productName}</h4>
                                <p>${m.type === 'entry' ? 'Entrada' : m.type === 'exit' ? 'Saída' : m.type === 'loan' ? 'Empréstimo' : m.type === 'return' ? 'Devolução' : 'Retirada'} • ${m.quantity} unid.</p>
                                <small>${formatDateTime(m.datetime)}</small>
                            </div>
                        </div>
                    `;
                }).join('');
            } else {
                recentList.innerHTML = `
                    <div class="empty-state">
                        <span>📊</span>
                        <p>Nenhuma movimentação recente</p>
                    </div>
                `;
            }
        }

        // Utilitário para formatar data/hora
        function formatDateTime(datetimeStr) {
            if (!datetimeStr) return '';
            const [date, time] = datetimeStr.split(' ');
            return `${date} ${time}`;
        }

        // PRODUTOS (funções mantidas iguais)
        function loadCategoryFilter() { /* ... */ }
        function filterByCategory(cat) { /* ... */ }
        function filterProducts() { /* ... */ }
        function displayProducts(list) { /* ... */ }
        function loadProducts() { filterProducts(); }
        function openProductModal() { /* ... */ }
        function editProduct(id) { /* ... */ }
        function saveProduct() { /* ... */ }
        function deleteProduct(id) { /* ... */ }

        // EMPRÉSTIMOS (funções mantidas iguais)
        function loadLoanProductSelect() { /* ... */ }
        function openLoanModal(productId = null) { /* ... */ }
        function saveLoan() { /* ... */ }
        function loadAllLoans() { /* ... */ }
        function openReturnModal(loanId) { /* ... */ }
        function saveReturn() { /* ... */ }

        // RETIRADAS (funções mantidas iguais)
        function openPermanentModal(productId) { /* ... */ }
        function savePermanent() { /* ... */ }
        function loadPermanentItems() { /* ... */ }

        // HISTÓRICO (funções mantidas iguais)
        function loadHistory() { /* ... */ }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
        }

        // Para economizar espaço, as funções repetidas devem ser mantidas do código anterior.
        // Aqui estamos apenas mostrando a estrutura modificada.
    </script>
</body>
</html>
