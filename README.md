<!DOCTYPE html>
<html lang="es-CO">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌞 Evaluador Energético Colombia - Tu Proyecto Renovable</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        :root {
            --primary: #FF6B35;
            --secondary: #004E89;
            --accent: #1A936F;
            --yellow: #FFD23F;
            --dark: #1a1a2e;
            --light: #f8f9fa;
            --gradient1: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --gradient2: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            --gradient3: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            --gradient4: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            background-attachment: fixed;
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        /* Animaciones */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        @keyframes shine {
            0% { background-position: -200% center; }
            100% { background-position: 200% center; }
        }
        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Header espectacular */
        .hero {
            text-align: center;
            padding: 50px 20px;
            margin-bottom: 40px;
            background: rgba(255,255,255,0.95);
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            position: relative;
            overflow: hidden;
            animation: slideIn 0.8s ease;
        }

        .hero::before {
            content: "☀️";
            position: absolute;
            font-size: 200px;
            opacity: 0.1;
            top: -50px;
            right: -50px;
            animation: rotate 20s linear infinite;
        }

        .hero::after {
            content: "⚡";
            position: absolute;
            font-size: 150px;
            opacity: 0.1;
            bottom: -30px;
            left: -30px;
            animation: float 6s ease-in-out infinite;
        }

        .flag-co {
            font-size: 4rem;
            display: inline-block;
            animation: pulse 2s infinite;
            margin-bottom: 10px;
        }

        .hero h1 {
            font-size: 3rem;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 15px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .hero p {
            font-size: 1.3rem;
            color: #555;
            max-width: 800px;
            margin: 0 auto;
        }

        /* Contenedor principal */
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Tarjetas creativas */
        .card {
            background: rgba(255,255,255,0.98);
            border-radius: 25px;
            padding: 35px;
            margin-bottom: 30px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            animation: slideIn 0.6s ease;
            position: relative;
            overflow: hidden;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }

        .card-title {
            font-size: 1.8rem;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 15px;
            color: var(--secondary);
            border-bottom: 4px solid var(--yellow);
            padding-bottom: 15px;
        }

        .card-icon {
            font-size: 2.5rem;
            animation: float 3s ease-in-out infinite;
        }

        /* Grid layout */
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }

        @media (max-width: 900px) {
            .grid-2 { grid-template-columns: 1fr; }
            .hero h1 { font-size: 2rem; }
        }

        /* Inputs estilizados */
        .input-group {
            margin-bottom: 25px;
            position: relative;
        }

        .input-group label {
            display: block;
            font-weight: 700;
            color: var(--secondary);
            margin-bottom: 10px;
            font-size: 1rem;
        }

        .input-wrapper {
            position: relative;
            display: flex;
            align-items: center;
        }

        .input-icon {
            position: absolute;
            left: 15px;
            font-size: 1.5rem;
            z-index: 1;
        }

        .input-wrapper input {
            width: 100%;
            padding: 15px 15px 15px 50px;
            border: 3px solid #e0e0e0;
            border-radius: 15px;
            font-size: 1.1rem;
            font-weight: 600;
            transition: all 0.3s;
            background: #fafafa;
        }

        .input-wrapper input:focus {
            outline: none;
            border-color: var(--primary);
            background: white;
            box-shadow: 0 0 20px rgba(255,107,53,0.3);
            transform: scale(1.02);
        }

        .input-suffix {
            position: absolute;
            right: 15px;
            font-weight: 700;
            color: var(--primary);
            font-size: 1.1rem;
        }

        .hint {
            font-size: 0.85rem;
            color: #888;
            margin-top: 5px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        /* Sliders creativos */
        .slider-group {
            margin: 25px 0;
            padding: 20px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-radius: 15px;
        }

        .slider-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .slider-label {
            font-weight: 700;
            color: var(--secondary);
        }

        .slider-value {
            background: var(--gradient1);
            color: white;
            padding: 8px 20px;
            border-radius: 25px;
            font-weight: 700;
            font-size: 1.1rem;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        input[type="range"] {
            width: 100%;
            height: 10px;
            border-radius: 10px;
            background: #ddd;
            outline: none;
            -webkit-appearance: none;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: var(--gradient2);
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
            transition: transform 0.2s;
        }

        input[type="range"]::-webkit-slider-thumb:hover {
            transform: scale(1.2);
        }

        /* Botones espectaculares */
        .btn-container {
            display: flex;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .btn {
            flex: 1;
            min-width: 200px;
            padding: 20px 30px;
            border: none;
            border-radius: 15px;
            font-size: 1.2rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }

        .btn-primary {
            background: var(--gradient4);
            color: white;
            box-shadow: 0 10px 30px rgba(67,233,123,0.4);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(67,233,123,0.6);
        }

        .btn-secondary {
            background: var(--gradient1);
            color: white;
            box-shadow: 0 10px 30px rgba(102,126,234,0.4);
        }

        .btn-secondary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(102,126,234,0.6);
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
            transition: 0.5s;
        }

        .btn:hover::before {
            left: 100%;
        }

        /* Escenarios interactivos */
        .scenarios {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin: 30px 0;
        }

        @media (max-width: 768px) {
            .scenarios { grid-template-columns: 1fr; }
        }

        .scenario-card {
            padding: 30px 20px;
            border: 4px solid #e0e0e0;
            border-radius: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            background: white;
            position: relative;
            overflow: hidden;
        }

        .scenario-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, transparent, rgba(255,255,255,0.3));
            opacity: 0;
            transition: opacity 0.3s;
        }

        .scenario-card:hover::before {
            opacity: 1;
        }

        .scenario-card.active {
            border-color: var(--accent);
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(26,147,111,0.4);
        }

        .scenario-icon {
            font-size: 4rem;
            margin-bottom: 10px;
            display: block;
        }

        .scenario-name {
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--secondary);
            margin-bottom: 8px;
        }

        .scenario-desc {
            font-size: 0.9rem;
            color: #666;
        }

        /* Alertas visuales */
        .alerts-container {
            margin: 30px 0;
        }

        .alert {
            padding: 20px 25px;
            border-radius: 15px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 20px;
            animation: slideIn 0.5s ease;
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }

        .alert-icon {
            font-size: 2.5rem;
            flex-shrink: 0;
        }

        .alert-content h4 {
            font-size: 1.2rem;
            margin-bottom: 5px;
        }

        .alert-content p {
            font-size: 0.95rem;
        }

        .alert-success {
            background: linear-gradient(135deg, #d4edda 0%, #c3e6cb 100%);
            border-left: 6px solid #28a745;
            color: #155724;
        }

        .alert-warning {
            background: linear-gradient(135deg, #fff3cd 0%, #ffeaa7 100%);
            border-left: 6px solid #ffc107;
            color: #856404;
        }

        .alert-danger {
            background: linear-gradient(135deg, #f8d7da 0%, #f5c6cb 100%);
            border-left: 6px solid #dc3545;
            color: #721c24;
        }

        .alert-info {
            background: linear-gradient(135deg, #d1ecf1 0%, #bee5eb 100%);
            border-left: 6px solid #17a2b8;
            color: #0c5460;
        }

        /* KPIS espectaculares */
        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .kpi-card {
            background: white;
            border-radius: 20px;
            padding: 30px 25px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            border: 4px solid transparent;
        }

        .kpi-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: var(--gradient1);
        }

        .kpi-card:hover {
            transform: translateY(-8px) rotate(2deg);
            box-shadow: 0 15px 40px rgba(0,0,0,0.25);
        }

        .kpi-card.success { border-color: #28a745; }
        .kpi-card.success::before { background: var(--gradient4); }
        
        .kpi-card.warning { border-color: #ffc107; }
        .kpi-card.warning::before { background: var(--gradient2); }
        
        .kpi-card.danger { border-color: #dc3545; }
        .kpi-card.danger::before { background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); }

        .kpi-icon {
            font-size: 3rem;
            margin-bottom: 10px;
            display: block;
        }

        .kpi-label {
            font-size: 0.9rem;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }

        .kpi-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--secondary);
            margin-bottom: 5px;
        }

        .kpi-sub {
            font-size: 0.85rem;
            color: #888;
        }

        /* Tabla interactiva */
        .table-wrapper {
            overflow-x: auto;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            font-size: 0.95rem;
        }

        thead {
            background: var(--gradient1);
            color: white;
        }

        th, td {
            padding: 15px 12px;
            text-align: right;
            border-bottom: 1px solid #e0e0e0;
        }

        th:first-child, td:first-child {
            text-align: center;
        }

        th {
            font-weight: 700;
            text-transform: uppercase;
            font-size: 0.85rem;
            letter-spacing: 0.5px;
        }

        tbody tr {
            transition: all 0.2s;
        }

        tbody tr:hover {
            background: #f8f9fa;
            transform: scale(1.01);
        }

        .negative { color: #dc3545; font-weight: 700; }
        .positive { color: #28a745; font-weight: 700; }

        /* Gráficos */
        .charts-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 30px 0;
        }

        @media (max-width: 900px) {
            .charts-grid { grid-template-columns: 1fr; }
        }

        .chart-container {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }

        .chart-title {
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--secondary);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .chart-box {
            position: relative;
            height: 350px;
        }

        /* Instrucciones visuales */
        .tip-box {
            background: linear-gradient(135deg, #fff9e6 0%, #fff3cd 100%);
            border-left: 5px solid var(--yellow);
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
            display: flex;
            gap: 15px;
            align-items: start;
        }

        .tip-icon {
            font-size: 2rem;
            flex-shrink: 0;
        }

        .tip-content h4 {
            color: #856404;
            margin-bottom: 8px;
        }

        .tip-content p {
            color: #856404;
            font-size: 0.95rem;
            line-height: 1.6;
        }

        /* Fórmulas */
        .formula-box {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border-left: 5px solid var(--accent);
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
        }

        .formula-title {
            font-weight: 700;
            color: var(--accent);
            margin-bottom: 10px;
            font-size: 1.1rem;
        }

        .formula {
            background: white;
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            text-align: center;
            font-size: 1.1rem;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }

        /* Loading */
        .loading {
            display: none;
            text-align: center;
            padding: 40px;
        }

        .loading.active {
            display: block;
        }

        .spinner {
            width: 60px;
            height: 60px;
            border: 6px solid #f3f3f3;
            border-top: 6px solid var(--primary);
            border-radius: 50%;
            animation: rotate 1s linear infinite;
            margin: 0 auto 20px;
        }

        /* Error message */
        .error-box {
            background: linear-gradient(135deg, #f8d7da 0%, #f5c6cb 100%);
            color: #721c24;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            display: none;
            border-left: 6px solid #dc3545;
        }

        .error-box.show {
            display: block;
            animation: slideIn 0.5s ease;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 40px 20px;
            color: white;
            font-size: 1rem;
            margin-top: 50px;
        }

        footer .heart {
            color: #ff6b6b;
            animation: pulse 1s infinite;
        }

        /* Decoraciones */
        .decoration {
            position: fixed;
            font-size: 3rem;
            opacity: 0.1;
            pointer-events: none;
            z-index: -1;
        }

        .decoration-1 { top: 10%; left: 5%; animation: float 8s infinite; }
        .decoration-2 { top: 60%; right: 5%; animation: float 10s infinite; }
        .decoration-3 { bottom: 20%; left: 10%; animation: float 12s infinite; }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 { font-size: 1.8rem; }
            .kpi-value { font-size: 1.5rem; }
            .btn { min-width: 100%; }
        }
    </style>
</head>
<body>

<!-- Decoraciones animadas -->
<div class="decoration decoration-1">☀️</div>
<div class="decoration decoration-2"></div>
<div class="decoration decoration-3">🌱</div>

<div class="container">

<!-- HERO -->
<div class="hero">
    <div class="flag-co">🇨🇴</div>
    <h1>Evaluador de Proyectos Energéticos</h1>
    <p>Calcula la viabilidad económica de tus proyectos de energía renovable en Colombia. Analiza VAN, TIR, LCOE y más con visualizaciones interactivas.</p>
</div>

<!-- INSTRUCCIONES RÁPIDAS -->
<div class="card" style="background: linear-gradient(135deg, #fff9e6, #fff3cd); border: 3px solid #ffc107;">
    <div style="display: flex; gap: 20px; align-items: center; flex-wrap: wrap;">
        <div style="font-size: 4rem;">📖</div>
        <div style="flex: 1;">
            <h3 style="color: #856404; margin-bottom: 10px; font-size: 1.5rem;">¿Cómo usar esta herramienta?</h3>
            <ol style="color: #856404; line-height: 2; font-size: 1.05rem;">
                <li><strong>1️⃣ Ingresa</strong> los datos de tu proyecto (inversión, generación, costos)</li>
                <li><strong>2️⃣ Selecciona</strong> un escenario (Conservador, Base u Optimista)</li>
                <li><strong>3️⃣ Presiona</strong> "⚡ Calcular Proyecto" para ver resultados</li>
                <li><strong>4️⃣ Analiza</strong> los indicadores, gráficos y recomendaciones</li>
                <li><strong>5️⃣ Compara</strong> diferentes escenarios para evaluar riesgos</li>
            </ol>
        </div>
    </div>
</div>

<div class="grid-2">

<!-- DATOS DEL PROYECTO -->
<div class="card">
    <div class="card-title">
        <span class="card-icon">🏗️</span>
        Datos del Proyecto
    </div>

    <div class="input-group">
        <label>💰 Inversión Inicial Total</label>
        <div class="input-wrapper">
            <span class="input-icon">💵</span>
            <input type="number" id="inversion" value="50000000" min="0" step="1000000">
            <span class="input-suffix">COP</span>
        </div>
        <div class="hint">💡 Ej: $50.000.000 para sistema solar residencial de 10kW</div>
    </div>

    <div class="input-group">
        <label>⏱️ Vida Útil del Proyecto</label>
        <div class="input-wrapper">
            <span class="input-icon">📅</span>
            <input type="number" id="vida" value="25" min="1" max="40">
            <span class="input-suffix">años</span>
        </div>
        <div class="hint">💡 Paneles solares típicamente duran 25-30 años</div>
    </div>

    <div class="input-group">
        <label>⚡ Generación Anual Esperada</label>
        <div class="input-wrapper">
            <span class="input-icon">🔋</span>
            <input type="number" id="generacion" value="12000" min="0" step="100">
            <span class="input-suffix">kWh/año</span>
        </div>
        <div class="hint">💡 Sistema 10kW en Bogotá: ~12,000 kWh/año</div>
    </div>

    <div class="slider-group">
        <div class="slider-header">
            <span class="slider-label">📉 Degradación Anual del Sistema</span>
            <span class="slider-value" id="degradVal">0.5%</span>
        </div>
        <input type="range" id="degradacion" min="0" max="2" step="0.1" value="0.5">
        <div class="hint">💡 Los paneles pierden ~0.5% de eficiencia por año</div>
    </div>

    <div class="input-group">
        <label>💸 Precio Actual de la Energía</label>
        <div class="input-wrapper">
            <span class="input-icon">🏷️</span>
            <input type="number" id="precioEnergia" value="650" min="0" step="10">
            <span class="input-suffix">COP/kWh</span>
        </div>
        <div class="hint">💡 Promedio Colombia: $600-$800/kWh (residencial)</div>
    </div>

    <div class="slider-group">
        <div class="slider-header">
            <span class="slider-label">📈 Inflación Anual de la Energía</span>
            <span class="slider-value" id="inflVal">4.5%</span>
        </div>
        <input type="range" id="inflacion" min="0" max="15" step="0.5" value="4.5">
        <div class="hint">💡 Histórico Colombia: 3-6% anual</div>
    </div>
</div>

<!-- COSTOS Y ESCENARIOS -->
<div class="card">
    <div class="card-title">
        <span class="card-icon">💵</span>
        Costos y Financiamiento
    </div>

    <div class="input-group">
        <label>🔧 Costos Anuales de O&M</label>
        <div class="input-wrapper">
            <span class="input-icon">🛠️</span>
            <input type="number" id="om" value="500000" min="0" step="50000">
            <span class="input-suffix">COP/año</span>
        </div>
        <div class="hint">💡 Típicamente 1-2% de la inversión inicial</div>
    </div>

    <div class="input-group">
        <label>🔄 Reemplazo de Inversor</label>
        <div class="input-wrapper">
            <span class="input-icon">⚙️</span>
            <input type="number" id="reemplazo" value="8000000" min="0" step="500000">
            <span class="input-suffix">COP</span>
        </div>
        <div class="hint">💡 Vida útil del inversor: 10-15 años</div>
    </div>

    <div class="input-group">
        <label> Año del Reemplazo</label>
        <div class="input-wrapper">
            <span class="input-icon">🗓️</span>
            <input type="number" id="anioReemplazo" value="12" min="1" max="40">
            <span class="input-suffix">año</span>
        </div>
    </div>

    <div class="slider-group">
        <div class="slider-header">
            <span class="slider-label"> Tasa de Descuento (WACC)</span>
            <span class="slider-value" id="tasaVal">12%</span>
        </div>
        <input type="range" id="tasaDescuento" min="5" max="25" step="0.5" value="12">
        <div class="hint">💡 Proyectos energéticos Colombia: 10-15% típico</div>
    </div>

    <!-- ESCENARIOS -->
    <h3 style="margin: 30px 0 20px; color: var(--secondary); font-size: 1.4rem; display: flex; align-items: center; gap: 10px;">
        <span>🎯</span> Selecciona un Escenario
    </h3>
    
    <div class="scenarios">
        <div class="scenario-card" onclick="setScenario('conservador', this)">
            <span class="scenario-icon">😟</span>
            <div class="scenario-name">Conservador</div>
            <div class="scenario-desc">-20% generación<br>+2% inflación</div>
        </div>
        <div class="scenario-card active" onclick="setScenario('base', this)">
            <span class="scenario-icon">📊</span>
            <div class="scenario-name">Base</div>
            <div class="scenario-desc">Valores normales<br>Proyección realista</div>
        </div>
        <div class="scenario-card" onclick="setScenario('optimista', this)">
            <span class="scenario-icon"></span>
            <div class="scenario-name">Optimista</div>
            <div class="scenario-desc">+20% generación<br>+2% inflación</div>
        </div>
    </div>

    <div class="btn-container">
        <button class="btn btn-primary" onclick="calcularProyecto()">
             Calcular Proyecto
        </button>
        <button class="btn btn-secondary" onclick="cargarEjemplo()">
             Cargar Ejemplo
        </button>
    </div>

    <div id="errorMsg" class="error-box"></div>
</div>

</div>

<!-- ALERTAS -->
<div id="alertas" class="alerts-container"></div>

<!-- INDICADORES CLAVE -->
<h2 style="color: white; margin: 40px 0 25px; font-size: 2rem; display: flex; align-items: center; gap: 15px; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
    <span>📊</span> Indicadores Clave de Rentabilidad
</h2>

<div class="kpi-grid" id="kpis">
    <div class="kpi-card">
        <span class="kpi-icon">💵</span>
        <div class="kpi-label">Inversión Total</div>
        <div class="kpi-value">$50M</div>
        <div class="kpi-sub">Capital inicial</div>
    </div>
    <div class="kpi-card warning">
        <span class="kpi-icon">⏱️</span>
        <div class="kpi-label">Periodo de Retorno</div>
        <div class="kpi-value">--</div>
        <div class="kpi-sub">Años para recuperar</div>
    </div>
    <div class="kpi-card">
        <span class="kpi-icon"></span>
        <div class="kpi-label">VAN</div>
        <div class="kpi-value">$0</div>
        <div class="kpi-sub">Valor actual neto</div>
    </div>
    <div class="kpi-card">
        <span class="kpi-icon">📈</span>
        <div class="kpi-label">TIR</div>
        <div class="kpi-value">--</div>
        <div class="kpi-sub">Tasa interna</div>
    </div>
    <div class="kpi-card">
        <span class="kpi-icon"></span>
        <div class="kpi-label">LCOE</div>
        <div class="kpi-value">$0</div>
        <div class="kpi-sub">Costo por kWh</div>
    </div>
    <div class="kpi-card success">
        <span class="kpi-icon">💸</span>
        <div class="kpi-label">Ahorro Año 1</div>
        <div class="kpi-value">$0</div>
        <div class="kpi-sub">Primer año</div>
    </div>
</div>

<!-- FLUJO DE CAJA -->
<h2 style="color: white; margin: 40px 0 25px; font-size: 2rem; display: flex; align-items: center; gap: 15px; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
    <span>💵</span> Flujo de Caja Anual Detallado
</h2>

<div class="card">
    <div class="table-wrapper">
        <table id="tablaFlujo">
            <thead>
                <tr>
                    <th>Año</th>
                    <th>Generación<br>(kWh)</th>
                    <th>Precio<br>(COP/kWh)</th>
                    <th>Ingreso<br>(COP)</th>
                    <th>Costos<br>(COP)</th>
                    <th>Flujo Neto<br>(COP)</th>
                    <th>Acumulado<br>(COP)</th>
                    <th>Valor Presente<br>(COP)</th>
                </tr>
            </thead>
            <tbody id="tablaBody">
                <tr>
                    <td colspan="8" style="text-align: center; padding: 50px; color: #888; font-size: 1.2rem;">
                         Presiona "⚡ Calcular Proyecto" para ver los resultados detallados
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</div>

<!-- GRÁFICOS -->
<h2 style="color: white; margin: 40px 0 25px; font-size: 2rem; display: flex; align-items: center; gap: 15px; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
    <span>📈</span> Visualizaciones Interactivas
</h2>

<div class="charts-grid">
    <div class="chart-container">
        <div class="chart-title">
            <span>📊</span> Flujo de Caja Acumulado vs VAN
        </div>
        <div class="chart-box">
            <canvas id="chartAcum"></canvas>
        </div>
        <div class="tip-box">
            <span class="tip-icon"></span>
            <div class="tip-content">
                <h4>¿Cómo interpretar?</h4>
                <p>La línea azul muestra el acumulado simple. La línea punteada verde muestra el VAN. El punto donde cruzan cero es el periodo de retorno.</p>
            </div>
        </div>
    </div>

    <div class="chart-container">
        <div class="chart-title">
            <span>📊</span> Ingresos vs Costos por Año
        </div>
        <div class="chart-box">
            <canvas id="chartBarras"></canvas>
        </div>
        <div class="tip-box">
            <span class="tip-icon"></span>
            <div class="tip-content">
                <h4>¿Cómo interpretar?</h4>
                <p>Las barras verdes son los ahorros generados, las rojas son los costos. El proyecto es viable cuando los ingresos superan consistentemente los costos.</p>
            </div>
        </div>
    </div>

    <div class="chart-container">
        <div class="chart-title">
            <span>🎚️</span> Análisis de Sensibilidad del VAN
        </div>
        <div class="chart-box">
            <canvas id="chartSens"></canvas>
        </div>
        <div class="tip-box">
            <span class="tip-icon">💡</span>
            <div class="tip-content">
                <h4>¿Cómo interpretar?</h4>
                <p>Muestra cómo cambia el VAN si cada variable varía ±20%. La variable con mayor impacto es la más crítica del proyecto.</p>
            </div>
        </div>
    </div>

    <div class="chart-container">
        <div class="chart-title">
            <span></span> Comparación de Escenarios
        </div>
        <div class="chart-box">
            <canvas id="chartEsc"></canvas>
        </div>
        <div class="tip-box">
            <span class="tip-icon"></span>
            <div class="tip-content">
                <h4>¿Cómo interpretar?</h4>
                <p>Compara los KPIs principales entre escenarios. Un proyecto robusto debe ser viable incluso en el escenario conservador.</p>
            </div>
        </div>
    </div>
</div>

<!-- FÓRMULAS -->
<h2 style="color: white; margin: 40px 0 25px; font-size: 2rem; display: flex; align-items: center; gap: 15px; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
    <span>📚</span> Fórmulas y Conceptos Clave
</h2>

<div class="card">
    <div class="formula-box">
        <div class="formula-title">📍 Periodo de Retorno (Payback)</div>
        <div class="formula">Payback = Inversión / Ahorro Anual Promedio</div>
        <p style="margin-top: 10px; color: #555;">Años que tarda en recuperarse la inversión con los ahorros generados. No considera el valor del dinero en el tiempo.</p>
    </div>

    <div class="formula-box">
        <div class="formula-title">💰 Valor Actual Neto (VAN)</div>
        <div class="formula">VAN = -I₀ + Σ [(Flujo_t) / (1+r)^t]</div>
        <p style="margin-top: 10px; color: #555;">Suma de todos los flujos futuros traídos a valor presente. <strong style="color: var(--accent);">VAN > 0 → El proyecto crea valor</strong></p>
    </div>

    <div class="formula-box">
        <div class="formula-title">📈 Tasa Interna de Retorno (TIR)</div>
        <div class="formula">0 = -I₀ + Σ [Flujo_t / (1+TIR)^t]</div>
        <p style="margin-top: 10px; color: #555;">Tasa de descuento que hace que el VAN sea igual a cero. <strong style="color: var(--accent);">TIR > Tasa de descuento → Proyecto rentable</strong></p>
    </div>

    <div class="formula-box">
        <div class="formula-title">⚡ Costo Nivelado de Energía (LCOE)</div>
        <div class="formula">LCOE = Costos Totales VP / Energía Total VP</div>
        <p style="margin-top: 10px; color: #555;">Costo promedio por kWh generado durante toda la vida del proyecto. <strong style="color: var(--accent);">LCOE < Precio de red → Competitivo</strong></p>
    </div>
</div>

<!-- FOOTER -->
<footer>
    <p style="font-size: 1.3rem; margin-bottom: 10px;">Hecho con <span class="heart">❤️</span> para Colombia</p>
    <p style="opacity: 0.9;"> Herramienta para evaluación de proyectos de energía renovable</p>
    <p style="margin-top: 15px; font-size: 0.9rem; opacity: 0.8;">
        Basado en metodologías de la UPME y estándares internacionales
    </p>
</footer>

</div>

<script>
// ============ VARIABLES GLOBALES ============
let currentScenario = 'base';
let scenarioParams = {
    conservador: { mult: 0.8, infl: 6.5 },
    base: { mult: 1.0, infl: 4.5 },
    optimista: { mult: 1.2, infl: 6.5 }
};
let charts = {};

// ============ INICIALIZACIÓN ============
document.addEventListener('DOMContentLoaded', function() {
    setupSliders();
    // Calcular automáticamente al cargar
    setTimeout(() => calcularProyecto(), 500);
});

function setupSliders() {
    const sliders = [
        { id: 'degradacion', display: 'degradVal', suffix: '%' },
        { id: 'inflacion', display: 'inflVal', suffix: '%' },
        { id: 'tasaDescuento', display: 'tasaVal', suffix: '%' }
    ];

    sliders.forEach(s => {
        const slider = document.getElementById(s.id);
        const display = document.getElementById(s.display);
        
        slider.addEventListener('input', function() {
            display.textContent = this.value + s.suffix;
        });
    });
}

function setScenario(scenario, btn) {
    currentScenario = scenario;
    
    // Actualizar UI
    document.querySelectorAll('.scenario-card').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    
    // Actualizar inflación según escenario
    const params = scenarioParams[scenario];
    document.getElementById('inflacion').value = params.infl;
    document.getElementById('inflVal').textContent = params.infl + '%';
    
    // Recalcular
    calcularProyecto();
}

// ============ FORMATOS ============
function formatCOP(value) {
    return new Intl.NumberFormat('es-CO', {
        style: 'currency',
        currency: 'COP',
        minimumFractionDigits: 0,
        maximumFractionDigits: 0
    }).format(value);
}

function formatNumber(value, decimals = 0) {
    return new Intl.NumberFormat('es-CO', {
        minimumFractionDigits: decimals,
        maximumFractionDigits: decimals
    }).format(value);
}

function getVal(id) {
    return parseFloat(document.getElementById(id).value) || 0;
}

// ============ CÁLCULO PRINCIPAL ============
function calcularProyecto() {
    try {
        // Ocultar errores previos
        document.getElementById('errorMsg').classList.remove('show');
        
        // Obtener parámetros
        const inversion = getVal('inversion');
        const vida = getVal('vida');
        const generacionBase = getVal('generacion');
        const degradacion = getVal('degradacion') / 100;
        const precioBase = getVal('precioEnergia');
        const inflacion = getVal('inflacion') / 100;
        const om = getVal('om');
        const reemplazo = getVal('reemplazo');
        const anioRep = getVal('anioReemplazo');
        const tasa = getVal('tasaDescuento') / 100;
        
        // Validaciones
        if (inversion <= 0) throw new Error('La inversión debe ser mayor a cero');
        if (vida <= 0) throw new Error('La vida útil debe ser mayor a cero');
        if (generacionBase <= 0) throw new Error('La generación debe ser mayor a cero');
        
        // Ajustar por escenario
        const params = scenarioParams[currentScenario];
        const generacion = generacionBase * params.mult;
        const inflEscenario = params.infl / 100;
        
        // Calcular flujos
        const flujos = [];
        let acumulado = -inversion;
        let van = -inversion;
        let vpCostos = inversion;
        let vpEnergia = 0;
        
        for (let t = 1; t <= vida; t++) {
            const gen = generacion * Math.pow(1 - degradacion, t - 1);
            const precio = precioBase * Math.pow(1 + inflEscenario, t - 1);
            const ingreso = gen * precio;
            const costos = om + (t === anioRep ? reemplazo : 0);
            const flujoNeto = ingreso - costos;
            const factorDesc = Math.pow(1 + tasa, t);
            const flujoVP = flujoNeto / factorDesc;
            
            acumulado += flujoNeto;
            van += flujoVP;
            vpCostos += costos / factorDesc;
            vpEnergia += gen / factorDesc;
            
            flujos.push({
                t, gen, precio, ingreso, costos, flujoNeto,
                flujoVP, acumulado, van
            });
        }
        
        // Calcular TIR
        let tir = null;
        let low = -0.5, high = 1.0;
        for (let i = 0; i < 100; i++) {
            const mid = (low + high) / 2;
            let npv = -inversion;
            for (const f of flujos) {
                npv += f.flujoNeto / Math.pow(1 + mid, f.t);
            }
            if (Math.abs(npv) < 1) {
                tir = mid;
                break;
            }
            if (npv > 0) low = mid;
            else high = mid;
        }
        
        // Calcular Payback
        let payback = null;
        let acumSimple = -inversion;
        for (const f of flujos) {
            const prev = acumSimple;
            acumSimple += f.flujoNeto;
            if (acumSimple >= 0 && prev < 0 && f.flujoNeto > 0) {
                payback = f.t - 1 + (-prev) / f.flujoNeto;
                break;
            }
        }
        
        // Calcular LCOE
        const LCOE = vpEnergia > 0 ? vpCostos / vpEnergia : 0;
        
        // Renderizar resultados
        renderAlertas(flujos, van, tir, payback, LCOE, precioBase, inversion, vida);
        renderKPIs(inversion, payback, van, tir, LCOE, flujos[0]?.ingreso || 0);
        renderTabla(flujos, inversion);
        renderCharts(flujos, inversion, van, tir, LCOE, payback, {
            inversion, vida, generacion, degradacion, precioBase, inflEscenario, om, reemplazo, anioRep, tasa
        });
        
        // Scroll suave a resultados
        document.getElementById('alertas').scrollIntoView({ behavior: 'smooth', block: 'start' });
        
    } catch (error) {
        console.error('Error:', error);
        document.getElementById('errorMsg').innerHTML = '<strong>❌ Error:</strong> ' + error.message;
        document.getElementById('errorMsg').classList.add('show');
    }
}

// ============ RENDERIZADO ============
function renderAlertas(flujos, van, tir, payback, LCOE, precioBase, inversion, vida) {
    const container = document.getElementById('alertas');
    const tasa = getVal('tasaDescuento');
    let html = '';
    
    const ahorroY1 = flujos[0]?.ingreso || 0;
    
    if (ahorroY1 <= 0) {
        html += `
            <div class="alert alert-warning">
                <div class="alert-icon">⚠️</div>
                <div class="alert-content">
                    <h4>Ahorro Insuficiente</h4>
                    <p>El ahorro del primer año es muy bajo o negativo. Verifica la generación esperada y el precio de la energía.</p>
                </div>
            </div>
        `;
    }
    
    if (payback === null) {
        html += `
            <div class="alert alert-danger">
                <div class="alert-icon">⏰</div>
                <div class="alert-content">
                    <h4>No hay Retorno de Inversión</h4>
                    <p>El proyecto no recupera la inversión en ${vida} años. Los ahorros no son suficientes para cubrir la inversión inicial.</p>
                </div>
            </div>
        `;
    } else if (payback > vida * 0.7) {
        html += `
            <div class="alert alert-warning">
                <div class="alert-icon">⏱️</div>
                <div class="alert-content">
                    <h4>Retorno Muy Largo</h4>
                    <p>El periodo de retorno es de ${payback.toFixed(1)} años, lo que representa más del 70% de la vida útil del proyecto. Alto riesgo.</p>
                </div>
            </div>
        `;
    }
    
    if (van < 0) {
        html += `
            <div class="alert alert-danger">
                <div class="alert-icon">📉</div>
                <div class="alert-content">
                    <h4>VAN Negativo</h4>
                    <p>El Valor Actual Neto es ${formatCOP(van)}. El proyecto destruye valor considerando la tasa de descuento del ${tasa}%.</p>
                </div>
            </div>
        `;
    } else {
        html += `
            <div class="alert alert-success">
                <div class="alert-icon">✅</div>
                <div class="alert-content">
                    <h4>¡Proyecto Rentable!</h4>
                    <p>El VAN es ${formatCOP(van)}. El proyecto crea valor por encima de la tasa de descuento exigida.</p>
                </div>
            </div>
        `;
    }
    
    if (tir !== null && tir < tasa / 100) {
        html += `
            <div class="alert alert-warning">
                <div class="alert-icon">📊</div>
                <div class="alert-content">
                    <h4>TIR por Debajo de la Tasa</h4>
                    <p>La TIR (${(tir*100).toFixed(2)}%) es menor que la tasa de descuento (${tasa}%). El rendimiento no justifica el riesgo.</p>
                </div>
            </div>
        `;
    }
    
    if (LCOE > precioBase) {
        html += `
            <div class="alert alert-info">
                <div class="alert-icon">💡</div>
                <div class="alert-content">
                    <h4>LCOE vs Precio de Red</h4>
                    <p>El LCOE (${formatCOP(LCOE)}/kWh) es mayor que el precio actual de la red (${formatCOP(precioBase)}/kWh). Considera negociar mejores precios de equipos.</p>
                </div>
            </div>
        `;
    }
    
    container.innerHTML = html;
}

function renderKPIs(inversion, payback, van, tir, LCOE, ahorroY1) {
    const kpis = document.getElementById('kpis');
    
    const paybackClass = payback === null ? 'danger' : (payback > 10 ? 'warning' : 'success');
    const vanClass = van < 0 ? 'danger' : 'success';
    const tirClass = tir === null || tir < getVal('tasaDescuento')/100 ? 'warning' : 'success';
    
    kpis.innerHTML = `
        <div class="kpi-card">
            <span class="kpi-icon">💵</span>
            <div class="kpi-label">Inversión Total</div>
            <div class="kpi-value">${formatCOP(inversion)}</div>
            <div class="kpi-sub">Capital inicial</div>
        </div>
        <div class="kpi-card ${paybackClass}">
            <span class="kpi-icon">️</span>
            <div class="kpi-label">Periodo de Retorno</div>
            <div class="kpi-value">${payback ? payback.toFixed(1) + ' años' : 'No recupera'}</div>
            <div class="kpi-sub">Payback simple</div>
        </div>
        <div class="kpi-card ${vanClass}">
            <span class="kpi-icon">💰</span>
            <div class="kpi-label">VAN</div>
            <div class="kpi-value">${formatCOP(van)}</div>
            <div class="kpi-sub">Valor actual neto</div>
        </div>
        <div class="kpi-card ${tirClass}">
            <span class="kpi-icon">📈</span>
            <div class="kpi-label">TIR</div>
            <div class="kpi-value">${tir ? (tir*100).toFixed(2) + '%' : 'N/D'}</div>
            <div class="kpi-sub">Tasa interna</div>
        </div>
        <div class="kpi-card">
            <span class="kpi-icon">⚡</span>
            <div class="kpi-label">LCOE</div>
            <div class="kpi-value">${formatCOP(LCOE)}</div>
            <div class="kpi-sub">Por kWh generado</div>
        </div>
        <div class="kpi-card success">
            <span class="kpi-icon">💸</span>
            <div class="kpi-label">Ahorro Año 1</div>
            <div class="kpi-value">${formatCOP(ahorroY1)}</div>
            <div class="kpi-sub">Primer año</div>
        </div>
    `;
}

function renderTabla(flujos, inversion) {
    const tbody = document.getElementById('tablaBody');
    let html = '';
    
    // Fila año 0
    html += `
        <tr style="background:#f8f9fa; font-weight:600;">
            <td>0</td>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td class="negative">${formatCOP(-inversion)}</td>
            <td class="negative">${formatCOP(-inversion)}</td>
            <td class="negative">${formatCOP(-inversion)}</td>
        </tr>
    `;
    
    // Filas de años
    flujos.forEach(f => {
        const claseNeto = f.flujoNeto < 0 ? 'negative' : 'positive';
        const claseAcum = f.acumulado < 0 ? 'negative' : 'positive';
        const claseVP = f.van < 0 ? 'negative' : 'positive';
        
        html += `
            <tr>
                <td><strong>${f.t}</strong></td>
                <td>${formatNumber(f.gen, 0)}</td>
                <td>${formatCOP(f.precio)}</td>
                <td>${formatCOP(f.ingreso)}</td>
                <td>${formatCOP(f.costos)}</td>
                <td class="${claseNeto}">${formatCOP(f.flujoNeto)}</td>
                <td class="${claseAcum}">${formatCOP(f.acumulado)}</td>
                <td class="${claseVP}">${formatCOP(f.flujoVP)}</td>
            </tr>
        `;
    });
    
    tbody.innerHTML = html;
}

function renderCharts(flujos, inversion, van, tir, LCOE, payback, params) {
    // Destruir charts anteriores
    Object.values(charts).forEach(c => {
        if (c) c.destroy();
    });
    
    const labels = ['Año 0', ...flujos.map(f => `Año ${f.t}`)];
    const dataAcum = [-inversion, ...flujos.map(f => f.acumulado)];
    const dataVan = [-inversion, ...flujos.map(f => f.van)];
    
    // Configuración común
    Chart.defaults.color = '#555';
    Chart.defaults.font.family = "'Segoe UI', sans-serif";
    
    // Chart 1: Acumulado
    charts.acum = new Chart(document.getElementById('chartAcum'), {
        type: 'line',
        data: {
            labels: labels,
            datasets: [
                {
                    label: 'Flujo Acumulado',
                    data: dataAcum,
                    borderColor: '#3498db',
                    backgroundColor: 'rgba(52, 152, 219, 0.1)',
                    tension: 0.4,
                    fill: true,
                    borderWidth: 3
                },
                {
                    label: 'VAN Acumulado',
                    data: dataVan,
                    borderColor: '#28a745',
                    backgroundColor: 'rgba(40, 167, 69, 0.1)',
                    tension: 0.4,
                    fill: true,
                    borderDash: [5, 5],
                    borderWidth: 3
                }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: { position: 'top' }
            },
            scales: {
                y: {
                    ticks: {
                        callback: function(value) {
                            return '$' + (value/1000000).toFixed(1) + 'M';
                        }
                    }
                }
            }
        }
    });
    
    // Chart 2: Barras
    charts.barras = new Chart(document.getElementById('chartBarras'), {
        type: 'bar',
        data: {
            labels: labels.slice(1),
            datasets: [
                {
                    label: 'Ingresos (Ahorro)',
                    data: flujos.map(f => f.ingreso),
                    backgroundColor: '#28a745',
                    borderRadius: 8
                },
                {
                    label: 'Costos',
                    data: flujos.map(f => f.costos),
                    backgroundColor: '#dc3545',
                    borderRadius: 8
                }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: { position: 'top' }
            },
            scales: {
                y: {
                    ticks: {
                        callback: function(value) {
                            return '$' + (value/1000000).toFixed(1) + 'M';
                        }
                    }
                }
            }
        }
    });
    
    // Chart 3: Sensibilidad
    const vars = [
        {name: 'Inversión', key: 'inversion', base: params.inversion},
        {name: 'Generación', key: 'generacion', base: params.generacion},
        {name: 'Precio', key: 'precioBase', base: params.precioBase},
        {name: 'Tasa', key: 'tasa', base: params.tasa},
        {name: 'O&M', key: 'om', base: params.om}
    ];
    
    const sensData = vars.map(v => {
        const testParams = {...params};
        const up = calcularVANConCambio(testParams, v.key, v.base * 1.2);
        const down = calcularVANConCambio(testParams, v.key, v.base * 0.8);
        return {
            name: v.name,
            up: up - van,
            down: down - van
        };
    });
    
    charts.sens = new Chart(document.getElementById('chartSens'), {
        type: 'bar',
        data: {
            labels: sensData.map(s => s.name),
            datasets: [
                {
                    label: 'VAN si +20%',
                    data: sensData.map(s => s.up),
                    backgroundColor: '#28a745',
                    borderRadius: 8
                },
                {
                    label: 'VAN si -20%',
                    data: sensData.map(s => s.down),
                    backgroundColor: '#dc3545',
                    borderRadius: 8
                }
            ]
        },
        options: {
            indexAxis: 'y',
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: { position: 'top' }
            },
            scales: {
                x: {
                    ticks: {
                        callback: function(value) {
                            return '$' + (value/1000000).toFixed(1) + 'M';
                        }
                    }
                }
            }
        }
    });
    
    // Chart 4: Escenarios
    const escCons = calcularEscenario(0.8, 6.5/100, params);
    const escOpt = calcularEscenario(1.2, 6.5/100, params);
    
    charts.esc = new Chart(document.getElementById('chartEsc'), {
        type: 'bar',
        data: {
            labels: ['VAN (M COP)', 'Payback', 'TIR (%)', 'LCOE (COP)'],
            datasets: [
                {
                    label: '😟 Conservador',
                    data: [
                        escCons.van / 1000000,
                        escCons.payback || params.vida,
                        (escCons.tir || 0) * 100,
                        escCons.LCOE
                    ],
                    backgroundColor: '#dc3545',
                    borderRadius: 8
                },
                {
                    label: ' Base',
                    data: [
                        van / 1000000,
                        payback || params.vida,
                        (tir || 0) * 100,
                        LCOE
                    ],
                    backgroundColor: '#3498db',
                    borderRadius: 8
                },
                {
                    label: ' Optimista',
                    data: [
                        escOpt.van / 1000000,
                        escOpt.payback || params.vida,
                        (escOpt.tir || 0) * 100,
                        escOpt.LCOE
                    ],
                    backgroundColor: '#28a745',
                    borderRadius: 8
                }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: { position: 'top' }
            }
        }
    });
}

function calcularVANConCambio(params, key, valor) {
    const testParams = {...params, [key]: valor};
    let van = -testParams.inversion;
    
    for (let t = 1; t <= testParams.vida; t++) {
        const gen = testParams.generacion * Math.pow(1 - testParams.degradacion, t - 1);
        const precio = testParams.precioBase * Math.pow(1 + testParams.inflEscenario, t - 1);
        const ingreso = gen * precio;
        const costos = testParams.om + (t === testParams.anioRep ? testParams.reemplazo : 0);
        const flujo = ingreso - costos;
        van += flujo / Math.pow(1 + testParams.tasa, t);
    }
    
    return van;
}

function calcularEscenario(mult, infl, params) {
    const testParams = {...params, generacion: params.generacion * mult, inflEscenario: infl};
    let van = -testParams.inversion;
    let acum = -testParams.inversion;
    let vpCostos = testParams.inversion;
    let vpEnergia = 0;
    
    for (let t = 1; t <= testParams.vida; t++) {
        const gen = testParams.generacion * Math.pow(1 - testParams.degradacion, t - 1);
        const precio = testParams.precioBase * Math.pow(1 + testParams.inflEscenario, t - 1);
        const ingreso = gen * precio;
        const costos = testParams.om + (t === testParams.anioRep ? testParams.reemplazo : 0);
        const flujo = ingreso - costos;
        
        acum += flujo;
        van += flujo / Math.pow(1 + testParams.tasa, t);
        vpCostos += costos / Math.pow(1 + testParams.tasa, t);
        vpEnergia += gen / Math.pow(1 + testParams.tasa, t);
    }
    
    // Calcular TIR
    let tir = null;
    let low = -0.5, high = 1.0;
    for (let i = 0; i < 50; i++) {
        const mid = (low + high) / 2;
        let npv = -testParams.inversion;
        for (let t = 1; t <= testParams.vida; t++) {
            const gen = testParams.generacion * Math.pow(1 - testParams.degradacion, t - 1);
            const precio = testParams.precioBase * Math.pow(1 + testParams.inflEscenario, t - 1);
            const flujo = gen * precio - (testParams.om + (t === testParams.anioRep ? testParams.reemplazo : 0));
            npv += flujo / Math.pow(1 + mid, t);
        }
        if (Math.abs(npv) < 1000) { tir = mid; break; }
        if (npv > 0) low = mid; else high = mid;
    }
    
    // Calcular Payback
    let payback = null;
    let acSimple = -testParams.inversion;
    for (let t = 1; t <= testParams.vida; t++) {
        const gen = testParams.generacion * Math.pow(1 - testParams.degradacion, t - 1);
        const precio = testParams.precioBase * Math.pow(1 + testParams.inflEscenario, t - 1);
        const flujo = gen * precio - (testParams.om + (t === testParams.anioRep ? testParams.reemplazo : 0));
        const prev = acSimple;
        acSimple += flujo;
        if (acSimple >= 0 && prev < 0 && flujo > 0) {
            payback = t - 1 + (-prev) / flujo;
            break;
        }
    }
    
    const LCOE = vpEnergia > 0 ? vpCostos / vpEnergia : 0;
    
    return {van, tir, payback, LCOE};
}

function cargarEjemplo() {
    document.getElementById('inversion').value = 75000000;
    document.getElementById('vida').value = 25;
    document.getElementById('generacion').value = 18000;
    document.getElementById('degradacion').value = 0.5;
    document.getElementById('degradVal').textContent = '0.5%';
    document.getElementById('precioEnergia').value = 700;
    document.getElementById('inflacion').value = 4.5;
    document.getElementById('inflVal').textContent = '4.5%';
    document.getElementById('om').value = 750000;
    document.getElementById('reemplazo').value = 12000000;
    document.getElementById('anioReemplazo').value = 12;
    document.getElementById('tasaDescuento').value = 12;
    document.getElementById('tasaVal').textContent = '12%';
    
    document.querySelectorAll('.scenario-card').forEach((b, i) => {
        b.classList.toggle('active', i === 1);
    });
    currentScenario = 'base';
    
    calcularProyecto();
}
</script>

</body>
</html>
