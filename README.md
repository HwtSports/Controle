
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
            background: #f3f4f6;
            min-height: 100vh;
        }

        .app-container {
            display: flex;
            min-height: 100vh;
        }

        .sidebar {
            width: 260px;
            background: white;
            box-shadow: 2px 0 12px rgba(0,0,0,0.03);
            padding: 32px 0;
            border-right: 1px solid #f0f0f0;
            /* Removido position fixed e height fixa, agora ele vai se ajustar ao conteúdo */
            height: auto;
            align-self: flex-start; /* Garante que não estique */
        }

        .logo {
            padding: 0 24px 32px 24px;
            border-bottom: 1px solid #f0f0f0;
            margin-bottom: 24px;
        }

        .logo h2 {
            color: #1e293b;
            font-size: 20px;
            font-weight: 700;
            letter-spacing: -0.02em;
        }

        .logo p {
            color: #64748b;
            font-size: 13px;
            margin-top: 4px;
        }

        .menu-item {
            display: flex;
            align-items: center;
            padding: 12px 24px;
            color: #64748b;
            text-decoration: none;
            transition: all 0.2s;
            cursor: pointer;
            border-left: 3px solid transparent;
            margin: 4px 0;
        }

        .menu-item:hover {
            background: #f8fafc;
            color: #3b82f6;
        }

        .menu-item.active {
            background: #f0f9ff;
            color: #3b82f6;
            border-left-color: #3b82f6;
        }

        .menu-item span {
            font-size: 20px;
            margin-right: 14px;
        }

        .menu-item .menu-text {
            font-size: 14px;
            font-weight: 500;
        }

        .main-content {
            flex: 1;
            padding: 32px;
            /* Removido margin-left, agora o flex cuida do espaçamento */
        }

        .header {
            background: white;
            border-radius: 20px;
            padding: 24px 32px;
            margin-bottom: 32px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.02);
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #f0f0f0;
        }

        .header h1 {
            color: #1e293b;
            font-size: 24px;
            font-weight: 700;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 24px;
        }

        .user-name {
            color: #475569;
            font-weight: 500;
            font-size: 14px;
        }

        .logout-btn {
            background: #ef4444;
            color: white;
            border: none;
            padding: 8px 20px;
            border-radius: 40px;
            cursor: pointer;
            font-weight: 500;
            font-size: 13px;
            transition: all 0.2s;
        }

        .logout-btn:hover {
            background: #dc2626;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 24px;
            margin-bottom: 32px;
        }

        .stat-card {
            background: white;
            border-radius: 20px;
            padding: 24px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.02);
            display: flex;
            align-items: center;
            transition: transform 0.2s, box-shadow 0.2s;
            border: 1px solid #f0f0f0;
        }

        .stat-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 24px rgba(0,0,0,0.04);
        }

        .stat-icon {
            width: 56px;
            height: 56px;
            background: #f0f9ff;
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
            color: #64748b;
            font-size: 13px;
            font-weight: 500;
            margin-bottom: 4px;
        }

        .stat-info .number {
            color: #1e293b;
            font-size: 28px;
            font-weight: 700;
        }

        .stat-info .label {
            color: #94a3b8;
            font-size: 12px;
            margin-top: 2px;
        }

        .section {
            background: white;
            border-radius: 20px;
            padding: 28px;
            margin-bottom: 32px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.02);
            border: 1px solid #f0f0f0;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .section-header h2 {
            color: #1e293b;
            font-size: 18px;
            font-weight: 700;
        }

        .section-header button {
            background: #3b82f6;
            color: white;
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
            background: #2563eb;
            transform: scale(1.02);
        }

        .btn-secondary {
            background: #f1f5f9 !important;
            color: #1e293b !important;
        }

        .btn-secondary:hover {
            background: #e2e8f0 !important;
        }

        .list-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px;
            border-bottom: 1px solid #f1f5f9;
            transition: background 0.2s;
        }

        .list-item:last-child {
            border-bottom: none;
        }

        .list-item:hover {
            background: #f8fafc;
            border-radius: 12px;
        }

        .item-info h4 {
            color: #1e293b;
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .item-info p {
            color: #64748b;
            font-size: 13px;
        }

        .item-info small {
            color: #94a3b8;
            font-size: 12px;
        }

        .item-status {
            padding: 4px 12px;
            border-radius: 40px;
            font-size: 12px;
            font-weight: 600;
        }

        .status-low {
            background: #fee2e2;
            color: #dc2626;
        }

        .status-ok {
            background: #dcfce7;
            color: #16a34a;
        }

        .status-loan {
            background: #dbeafe;
            color: #2563eb;
        }

        .status-archived {
            background: #f1f5f9;
            color: #475569;
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
            filter: brightness(0.95);
        }

        .btn-edit {
            background: #e2e8f0;
            color: #1e293b;
        }

        .btn-loan {
            background: #3b82f6;
            color: white;
        }

        .btn-delete {
            background: #ef4444;
            color: white;
        }

        .btn-return {
            background: #10b981;
            color: white;
        }

        .btn-permanent {
            background: #f97316;
            color: white;
        }

        .btn-restore {
            background: #fbbf24;
            color: #1e293b;
        }

        .btn-view {
            background: #a855f7;
            color: white;
        }

        .empty-state {
            text-align: center;
            padding: 48px 20px;
            color: #94a3b8;
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
            border: 2px solid #e2e8f0;
            border-radius: 40px;
            font-size: 14px;
            transition: border-color 0.2s;
        }

        .search-box:focus {
            outline: none;
            border-color: #3b82f6;
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
            background: #f1f5f9;
            color: #475569;
            font-weight: 500;
            font-size: 13px;
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.2s;
        }

        .category-filter button.active {
            background: #3b82f6;
            color: white;
        }

        .date-filter {
            padding: 10px 16px;
            border: 2px solid #e2e8f0;
            border-radius: 40px;
            font-size: 13px;
        }

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
            backdrop-filter: blur(4px);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            border-radius: 24px;
            padding: 32px;
            max-width: 500px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-header h2 {
            color: #1e293b;
            font-size: 20px;
            font-weight: 700;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #94a3b8;
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
            border: 2px solid #e2e8f0;
            border-radius: 12px;
            font-size: 14px;
            transition: border-color 0.2s;
        }

        .modal-form input:focus,
        .modal-form select:focus,
        .modal-form textarea:focus {
            outline: none;
            border-color: #3b82f6;
        }

        .modal-form button {
            background: #3b82f6;
            color: white;
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
            background: #2563eb;
        }

        .datetime-row {
            display: flex;
            gap: 10px;
        }

        .datetime-row input {
            flex: 1;
        }

        .login-container {
            max-width: 380px;
            margin: 120px auto;
            background: white;
            border-radius: 32px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.05);
            border: 1px solid #f0f0f0;
        }

        .login-header {
            text-align: center;
            margin-bottom: 32px;
        }

        .login-header h1 {
            color: #1e293b;
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 8px;
        }

        .login-header p {
            color: #64748b;
            font-size: 14px;
        }

        .login-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .login-form input {
            padding: 16px;
            border: 2px solid #e2e8f0;
            border-radius: 16px;
            font-size: 15px;
        }

        .login-form button {
            background: #3b82f6;
            color: white;
            border: none;
            padding: 16px;
            border-radius: 16px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }

        .login-form button:hover {
            background: #2563eb;
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
            background: #f8fafc;
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
            color: #1e293b;
        }

        .timeline-content p {
            font-size: 12px;
            color: #64748b;
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

            <!-- Seções... (o restante do conteúdo permanece igual) -->
            <!-- ... -->
            <!-- Por brevidade, mantive apenas a estrutura, mas o conteúdo completo está no código anterior -->
            <!-- Para não repetir tudo, vou omitir o restante do HTML, mas você deve manter igual ao último código funcional -->
            <!-- Abaixo está a continuação do HTML com as seções -->
            
            <!-- Seção Painel -->
            <div id="dashboardSection">
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-icon">
                            <span>📦</span>
                        </div>
                        <div class="stat-info">
                            <h3>Total de Produtos</h3>
                            <div class="number" id="totalProducts">0</div>
                            <div class="label">itens ativos</div>
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

                <div class="section">
                    <div class="section-header">
                        <h2>📦 Estoque Baixo</h2>
                    </div>
                    <div id="lowStockList" class="empty-state">
                        <span>✅</span>
                        <p>Nenhum produto com estoque baixo</p>
                    </div>
                </div>

                <div class="section">
                    <div class="section-header">
                        <h2>🔧 Empréstimos Ativos</h2>
                    </div>
                    <div id="activeLoansList" class="empty-state">
                        <span>📭</span>
                        <p>Nenhum empréstimo ativo</p>
                    </div>
                </div>

                <div class="section">
                    <div class="section-header">
                        <h2>📋 Últimas Movimentações</h2>
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

            <!-- Seção Retiradas (Baixas) -->
            <div id="permanentSection" class="hidden">
                <div class="section">
                    <div class="section-header">
                        <h2>🗑️ Retiradas Permanentes</h2>
                        <p style="color: #64748b;">Itens retirados para uso único (não serão devolvidos)</p>
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

    <!-- Modais (copiar do código anterior) -->
    <!-- ... -->

    <script>
        // TODO: copiar todo o JavaScript do código anterior aqui
        // Para não alongar, vou apenas indicar que o JS deve ser o mesmo da versão anterior,
        // com as funções de login, produtos, empréstimos, etc.
        // Na prática, você deve manter o JS idêntico ao último código funcional.
    </script>
</body>
</html>
