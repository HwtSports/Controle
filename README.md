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

        /* Container principal */
        .app-container {
            display: flex;
            min-height: 100vh;
        }

        /* Menu Lateral */
        .sidebar {
            width: 260px;
            background: white;
            box-shadow: 2px 0 12px rgba(0,0,0,0.03);
            padding: 32px 0;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
            z-index: 100;
            border-right: 1px solid #f0f0f0;
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

        /* Conteúdo Principal */
        .main-content {
            flex: 1;
            margin-left: 260px;
            padding: 32px;
            min-height: 100vh;
        }

        /* Header */
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

        /* Cards de Estatísticas */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1
