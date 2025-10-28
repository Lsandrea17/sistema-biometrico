# sistema-biometrico
pruebas del sistema
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Registro Biométrico - CICPC</title>
    <style>
        :root {
            --primary-color: #062e5f; /* Azul oscuro CICPC */
            --secondary-color: #062e5f; /* Azul medio */
            --accent-color: #c5a71f; /* dorado CICPC */
            --light-color: #f7fafc;
            --success-color: #27ae60;
            --warning-color: #f39c12;
            --news-bg: #c5a71f; /* Fondo dorado para noticias */
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
            background: #1a6fc9;
            background: linear-gradient(90deg,rgba(26, 111, 201, 1) 0%, rgba(87, 122, 199, 1) 47%, rgba(237, 221, 83, 1) 100%);
        }
        
        /* Estilos para el sistema de autenticación */
        .auth-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .auth-card {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            width: 100%;
            max-width: 450px;
            padding: 30px;
        }
        
        .auth-logo {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .auth-logo img {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            object-fit: cover;
            border: 2px solid var(--primary-color);
        }
        
        .auth-title {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 25px;
            font-size: 1.5rem;
        }
        
        .auth-form .form-group {
            margin-bottom: 20px;
        }
        
        .auth-form label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #444;
        }
        
        .auth-form input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        .auth-form input:focus {
            border-color: var(--primary-color);
            outline: none;
        }
        
        .auth-btn {
            width: 100%;
            padding: 12px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .auth-btn:hover {
            background-color: var(--secondary-color);
        }
        
        .auth-links {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
            font-size: 0.9rem;
        }
        
        .auth-links a {
            color: var(--primary-color);
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .auth-links a:hover {
            text-decoration: underline;
        }
        
        .alert {
            padding: 10px 15px;
            border-radius: 5px;
            margin-bottom: 15px;
            font-size: 0.9rem;
        }
        
        .alert-danger {
            background-color: rgba(197, 48, 48, 0.2);
            border: 1px solid var(--accent-color);
            color: var(--accent-color);
        }
        
        .alert-success {
            background-color: rgba(39, 174, 96, 0.2);
            border: 1px solid var(--success-color);
            color: var(--success-color);
        }
        
        .alert-warning {
            background-color: rgba(243, 156, 18, 0.2);
            border: 1px solid var(--warning-color);
            color: var(--warning-color);
        }
        
        /* Estilos para modales */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background-color: white;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .modal-title {
            color: var(--primary-color);
            font-size: 1.3rem;
            font-weight: bold;
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }
        
        .close-modal:hover {
            color: var(--accent-color);
        }
        
        .modal-footer {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            margin-top: 20px;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }
        
        /* Estilos para el contenido principal (oculto inicialmente) */
        .main-app {
            display: none;
        }
        
        /* Resto de estilos existentes para la aplicación principal */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .cicpc-header {
            background-color: var(--primary-color);
            color: white;
            padding: 15px 0 0 0;
            box-shadow: 0 5px 5px #f5f5f5;
        }
        
        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px 15px 20px;
            border-bottom: 2px solid var(--accent-color);
        }
        
        .logo-section {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo-cicpc {
            width: 80px;
            height: 80px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            color: white;
            font-size: 0.9rem;
            text-align: center;
            background-color: rgba(255, 255, 255, 0.1);
            position: relative;
            border-radius: 50%;
            overflow: hidden;
            border: 2px solid rgba(255, 255, 255, 0.3);
        }
        
        .logo-cicpc img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 50%;
        }
        
        .org-title {
            display: flex;
            flex-direction: column;
        }
        
        .org-name {
            font-weight: bold;
            font-size: 1.2rem;
            line-height: 1.2;
        }
        
        .org-subtitle {
            font-size: 0.8rem;
            margin-top: 3px;
            opacity: 0.9;
        }
        
        .directiva {
            text-align: right;
            font-size: 0.8rem;
        }
        
        .directiva div {
            margin-bottom: 3px;
        }
        
        .news-bar {
            background-color: var(--news-bg);
            padding: 8px 20px;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .news-label {
            font-weight: bold;
            font-size: 0.9rem;
            white-space: nowrap;
        }
        
        .news-items {
            display: flex;
            gap: 20px;
            overflow: hidden;
            flex-grow: 1;
        }
        
        .news-item {
            white-space: nowrap;
            font-size: 0.85rem;
        }
        
        .news-item:before {
            content: "•";
            margin-right: 5px;
        }
        
        .main-nav {
            background-color: var(--secondary-color);
            padding: 0 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .main-nav ul {
            display: flex;
            list-style: none;
        }
        
        .main-nav a {
            color: white;
            text-decoration: none;
            padding: 12px 20px;
            display: block;
            transition: background-color 0.3s;
            font-weight: 500;
        }
        
        .main-nav a:hover, .main-nav a.active {
            background-color: var(--primary-color);
        }
        
        .logout-btn {
            background-color: var(--accent-color);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: background-color 0.3s;
        }
        
        .logout-btn:hover {
            background-color: #b3961c;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 20px;
            margin-top: 20px;
        }
        
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .card h2 {
            color: var(--primary-color);
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-row {
            display: flex;
            gap: 15px;
        }
        
        .form-row .form-group {
            flex: 1;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        .required::after {
            content: " *";
            color: var(--accent-color);
        }
        
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #062e5f;
            border-radius: 4px;
            font-size: 1rem;
        }
        
        textarea {
            min-height: 80px;
            resize: vertical;
        }
        
        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: var(--secondary-color);
        }
        
        .btn-danger {
            background-color: var(--accent-color);
        }
        
        .btn-danger:hover {
            background-color: #9c2626;
        }
        
        .btn-warning {
            background-color: var(--warning-color);
        }
        
        .btn-warning:hover {
            background-color: #e67e22;
        }
        
        .biometric-capture {
            border: 2px dashed #ddd;
            padding: 20px;
            text-align: center;
            border-radius: 8px;
            margin-bottom: 20px;
            cursor: pointer;
            transition: border-color 0.3s;
        }
        
        .biometric-capture:hover {
            border-color: var(--primary-color);
        }
        
        .fingerprint-scanner {
            width: 200px;
            height: 200px;
            margin: 0 auto;
            position: relative;
            background-color: #f0f0f0;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }
        
        .fingerprint-image {
            width: 150px;
            height: 150px;
            background: linear-gradient(45deg, #333 25%, transparent 25%, transparent 75%, #333 75%, #333),
                        linear-gradient(45deg, #333 25%, transparent 25%, transparent 75%, #333 75%, #333);
            background-size: 10px 10px;
            background-position: 0 0, 5px 5px;
            border-radius: 50%;
            position: relative;
        }
        
        .fingerprint-lines {
            position: absolute;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 30% 40%, transparent 20%, #333 20%, #333 25%, transparent 25%),
                radial-gradient(circle at 70% 40%, transparent 20%, #333 20%, #333 25%, transparent 25%),
                radial-gradient(circle at 50% 70%, transparent 20%, #333 20%, #333 25%, transparent 25%);
            opacity: 0.7;
        }
        
        .scan-animation {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background-color: var(--primary-color);
            animation: scan 2s linear infinite;
            opacity: 0;
        }
        
        @keyframes scan {
            0% {
                top: 0;
                opacity: 1;
            }
            100% {
                top: 100%;
                opacity: 1;
            }
        }
        
        .scanning .scan-animation {
            opacity: 1;
        }
        
        .face-capture {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .face-preview {
            width: 150px;
            height: 190px;
            border: 2px solid #ddd;
            border-radius: 8px;
            margin: 0 auto 10px;
            background-color: #f9f9f9;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .face-preview img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        
        .face-preview.carnet::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border: 2px solid var(--primary-color);
            border-radius: 4px;
            pointer-events: none;
        }
        
        .file-input {
            display: none;
        }
        
        .file-label {
            display: inline-block;
            background-color: var(--primary-color);
            color: white;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .file-label:hover {
            background-color: var(--secondary-color);
        }
        
        .file-name {
            margin-top: 10px;
            font-size: 0.9rem;
            color: #666;
        }
        
        .inmate-list {
            max-height: 500px;
            overflow-y: auto;
        }
        
        .inmate-item {
            display: flex;
            align-items: flex-start;
            padding: 15px;
            border-bottom: 1px solid #eee;
            transition: background-color 0.3s;
            background-color: white;
            border-radius: 8px;
            margin-bottom: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        
        .inmate-item:hover {
            background-color: #f9f9f9;
            box-shadow: 0 3px 8px rgba(0,0,0,0.1);
        }
        
        .inmate-photo {
            width: 120px;
            height: 150px;
            border-radius: 4px;
            object-fit: cover;
            margin-right: 15px;
            background-color: #eee;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 16px;
            color: #666;
            border: 1px solid #ddd;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
        }
        
        .inmate-photo img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .inmate-photo::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border: 2px solid var(--primary-color);
            border-radius: 3px;
            pointer-events: none;
        }
        
        .inmate-info {
            flex-grow: 1;
        }
        
        .inmate-name {
            font-weight: bold;
            margin-bottom: 5px;
            color: var(--primary-color);
            font-size: 1.1rem;
        }
        
        .inmate-details {
            font-size: 0.9rem;
            color: #666;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 5px 15px;
        }
        
        .inmate-details .detail-label {
            font-weight: 500;
            color: #444;
        }
        
        .inmate-actions {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        
        .search-box {
            margin-bottom: 20px;
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }
        
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
        }
        
        .tab.active {
            border-bottom: 3px solid var(--primary-color);
            font-weight: bold;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .verification-result {
            text-align: center;
            padding: 20px;
        }
        
        .match-found {
            color: var(--success-color);
            font-weight: bold;
            font-size: 1.2rem;
        }
        
        .no-match {
            color: var(--accent-color);
            font-weight: bold;
            font-size: 1.2rem;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background-color: white;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            color: var(--primary-color);
        }
        
        .stat-label {
            font-size: 0.9rem;
            color: #666;
        }
        
        .fingerprint-status {
            margin-top: 10px;
            font-weight: bold;
        }
        
        .status-captured {
            color: var(--success-color);
        }
        
        .status-scanning {
            color: var(--warning-color);
        }
        
        .fingerprint-mini {
            width: 30px;
            height: 30px;
            background-color: #333;
            border-radius: 50%;
            display: inline-block;
            margin-right: 10px;
            position: relative;
        }
        
        .fingerprint-mini::after {
            content: "";
            position: absolute;
            top: 5px;
            left: 5px;
            right: 5px;
            bottom: 5px;
            background: 
                radial-gradient(circle, transparent 30%, #333 30%, #333 40%, transparent 40%),
                linear-gradient(90deg, transparent 45%, #333 45%, #333 55%, transparent 55%);
            border-radius: 50%;
        }
        
        .section-divider {
            border-top: 1px solid #ddd;
            margin: 20px 0;
            padding-top: 15px;
        }
        
        .physical-characteristics {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 15px;
        }
        
        .photo-instructions {
            text-align: center;
            margin-top: 10px;
            font-size: 0.85rem;
            color: #666;
        }
        
        .photo-instructions ul {
            text-align: left;
            display: inline-block;
            margin-top: 5px;
        }
        
        /* Modal de edición */
        .edit-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .edit-modal-content {
            background-color: white;
            border-radius: 8px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        
        .edit-modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .edit-modal-title {
            color: var(--primary-color);
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .close-edit-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }
        
        .close-edit-modal:hover {
            color: var(--accent-color);
        }
        
        .edit-modal-footer {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            margin-top: 20px;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }
        
        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
            
            .physical-characteristics {
                grid-template-columns: 1fr;
            }
            
            .form-row {
                flex-direction: column;
            }
            
            .header-top {
                flex-direction: column;
                text-align: center;
                gap: 10px;
            }
            
            .directiva {
                text-align: center;
            }
            
            .news-items {
                flex-direction: column;
                gap: 5px;
            }
            
            .news-item {
                white-space: normal;
            }
            
            .inmate-details {
                grid-template-columns: 1fr;
            }
            
            .inmate-photo {
                width: 100px;
                height: 125px;
            }
            
            .inmate-actions {
                flex-direction: row;
            }
            
            .auth-card {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <!-- Fondo con opacidad -->
    <div>
        <img src="sistema bio/img/cicpc logo.jpg" alt="imagen de Fondo" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; z-index: -1; opacity: 0.1;">
    </div>

    <!-- Sistema de Autenticación (Login o Registro) -->
    <div class="auth-container" id="auth-container">
        <div class="auth-card">
            <div class="auth-logo">
                <img src="sistema bio/img/cicpc logo.jpg" alt="Logo CICPC">
            </div>
            <h2 class="auth-title" id="auth-title">Sistema de Registro Biométrico</h2>
            
            <!-- Formulario de Login (mostrado por defecto) -->
            <form class="auth-form" id="login-form">
                <div class="form-group">
                    <label for="username">Usuario</label>
                    <input type="text" id="username" placeholder="Ingrese su usuario" required>
                </div>
                <div class="form-group">
                    <label for="password">Contraseña</label>
                    <input type="password" id="password" placeholder="Ingrese su contraseña" required>
                </div>
                <button type="submit" class="auth-btn" id="login-btn">Iniciar Sesión</button>
                <div class="auth-links">
                    <a href="#" id="forgot-password-link">¿Olvidó su contraseña?</a>
                    <a href="#" id="register-link">Registrarse</a>
                </div>
            </form>
            
            <!-- Formulario de Registro (oculto inicialmente) -->
            <form class="auth-form" id="register-form" style="display: none;">
                <div class="form-group">
                    <label for="register-name">Nombre Completo</label>
                    <input type="text" id="register-name" placeholder="Ingrese su nombre completo" required>
                </div>
                <div class="form-group">
                    <label for="register-username">Usuario</label>
                    <input type="text" id="register-username" placeholder="Cree un nombre de usuario" required>
                </div>
                <div class="form-group">
                    <label for="register-email">Correo Electrónico</label>
                    <input type="email" id="register-email" placeholder="Ingrese su correo electrónico" required>
                </div>
                <div class="form-group">
                    <label for="register-password">Contraseña</label>
                    <input type="password" id="register-password" placeholder="Cree una contraseña" required>
                </div>
                <div class="form-group">
                    <label for="register-confirm-password">Confirmar Contraseña</label>
                    <input type="password" id="register-confirm-password" placeholder="Confirme su contraseña" required>
                </div>
                <button type="submit" class="auth-btn" id="register-btn">Registrarse</button>
                <div class="auth-links">
                    <a href="#" id="login-link">¿Ya tiene cuenta? Iniciar Sesión</a>
                </div>
            </form>
            
            <div id="auth-alert" class="alert" style="display: none;"></div>
        </div>
    </div>

    <!-- Aplicación Principal (oculta inicialmente) -->
    <div class="main-app" id="main-app">
        <!-- Header estilo CICPC -->
        <header class="cicpc-header">
            <div class="header-top">
                <div class="logo-section">
                    <div class="logo-cicpc" id="logo-container">
                        <img src="sistema bio/img/cicpc logo.jpg" alt="Logo CICPC">
                        <span id="logo-text" style="display:none;">CICPC</span>
                    </div>
                    <div class="org-title">
                        <div class="org-name">CICPC</div>
                        <div class="org-subtitle">INVESTIGACIONES CIENTÍFICAS, PENALES Y CRIMINALÍSTICAS</div>
                    </div>
                </div>
                <div class="directiva">
                    <div>Sistema Biométrico</div>
                    <div>Usuario: <span id="current-user">Administrador</span></div>
                </div>
            </div>
            
            <div class="news-bar">
                <div class="news-label">NOTICIAS:</div>
                <div class="news-items">
                    <div class="news-item">Sistema de registro biométrico implementado exitosamente</div>
                    <div class="news-item">Mejoras en seguridad del sistema de identificación</div>
                </div>
            </div>
            
            <nav class="main-nav">
                <ul>
                    <li><a href="#" class="active" data-tab="register">Registro</a></li>
                    <li><a href="#" data-tab="verify">Verificación</a></li>
                    <li><a href="#" data-tab="inmates">Lista de Reclusos</a></li>
                </ul>
                <button class="logout-btn" id="logout-btn">Cerrar Sesión</button>
            </nav>
        </header>

        <div class="container">
            <div class="stats">
                <div class="stat-card">
                    <div class="stat-value" id="total-inmates">0</div>
                    <div class="stat-label">Total Reclusos</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="today-registrations">0</div>
                    <div class="stat-label">Registros Hoy</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="repeat-offenders">0</div>
                    <div class="stat-label">Reincidentes</div>
                </div>
            </div>

            <div class="tabs">
                <div class="tab active" data-tab="register">Registro de Detenido</div>
                <div class="tab" data-tab="verify">Verificación de Huella</div>
                <div class="tab" data-tab="inmates">Lista de Reclusos</div>
            </div>

            <div class="tab-content active" id="register-tab">
                <div class="card">
                    <h2>Registro de Nuevo Detenido</h2>
                    <form id="inmate-form">
                        <h3>Datos Personales</h3>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label for="inmate-name" class="required">Nombre</label>
                                <input type="text" id="inmate-name" required>
                            </div>
                            
                            <div class="form-group">
                                <label for="inmate-lastname" class="required">Apellido</label>
                                <input type="text" id="inmate-lastname" required>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label for="inmate-id" class="required">Documento de Identidad</label>
                                <input type="text" id="inmate-id" required>
                        </div>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label for="inmate-birthdate">Fecha de Nacimiento</label>
                                <input type="date" id="inmate-birthdate">
                            </div>
                            
                            <div class="form-group">
                                <label for="inmate-nationality">Nacionalidad</label>
                                <input type="text" id="inmate-nationality" value="venezolano">
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label for="inmate-crime" class="required">Delito o Causa de Ingreso</label>
                                <input type="text" id="inmate-crime" required>
                        </div>
                        
                        <div class="section-divider"></div>
                        
                        <h3>Datos Biométricos</h3>
                        
                        <div class="form-group">
                            <label class="required">Foto de Rostro (Formato Carnet)</label>
                            <div class="face-capture">
                                <div class="face-preview carnet" id="face-preview">
                                    <span>Vista previa de la foto carnet</span>
                                    <img id="face-image" src="" alt="Foto de rostro">
                                </div>
                                <input type="file" id="face-file" class="file-input" accept="image/*">
                                <label for="face-file" class="file-label">Seleccionar archivo</label>
                                <div class="file-name" id="file-name">Sin archivos seleccionados</div>
                                <div class="photo-instructions">
                                    <p><strong>Requisitos para foto carnet:</strong></p>
                                    <ul>
                                        <li>Fondo blanco o claro</li>
                                        <li>Rostro frontal y bien iluminado</li>
                                        <li>Sin gorras, gafas oscuras o accesorios que oculten el rostro</li>
                                        <li>Expresión neutra</li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        
                        <h4>Características Físicas</h4>
                        
                        <div class="physical-characteristics">
                            <div class="form-group">
                                <label for="inmate-gender">Sexo</label>
                                <select id="inmate-gender">
                                    <option value="">Seleccionar</option>
                                    <option value="Masculino">Masculino</option>
                                    <option value="Femenino">Femenino</option>
                                    <option value="Otro">Otro</option>
                                </select>
                            </div>
                            
                            <div class="form-group">
                                <label for="inmate-height">Estatura (cm)</label>
                                <input type="number" id="inmate-height" min="100" max="250">
                            </div>
                            
                            <div class="form-group">
                                <label for="inmate-weight">Peso (kg)</label>
                                <input type="number" id="inmate-weight" min="30" max="200">
                            </div>
                        </div>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label for="inmate-eyes">Color de Ojos</label>
                                <input type="text" id="inmate-eyes">
                            </div>
                            
                            <div class="form-group">
                                <label for="inmate-skin">Color de Piel</label>
                                <input type="text" id="inmate-skin">
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label for="inmate-marks">Marcas Particulares</label>
                            <textarea id="inmate-marks" placeholder="Describa marcas particulares"></textarea>
                        </div>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label for="inmate-tattoos">Tatuajes</label>
                                <textarea id="inmate-tattoos" placeholder="Describa tatuajes"></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label for="inmate-scars">Cicatrices</label>
                                <textarea id="inmate-scars" placeholder="Describa cicatrices"></textarea>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">Captura de Huella Dactilar</label>
                            <div class="biometric-capture" id="biometric-capture">
                                <div class="fingerprint-scanner">
                                    <div class="fingerprint-image">
                                        <div class="fingerprint-lines"></div>
                                    </div>
                                    <div class="scan-animation"></div>
                                </div>
                                <p>Coloque el dedo en el escáner</p>
                                <div class="fingerprint-status" id="fingerprint-status">Esperando captura...</div>
                            </div>
                        </div>
                        
                        <button type="submit">Registrar Detenido</button>
                    </form>
                </div>
            </div>

            <div class="tab-content" id="verify-tab">
                <div class="card">
                    <h2>Verificación de Huella Dactilar</h2>
                    <div class="biometric-capture" id="verify-biometric">
                        <div class="fingerprint-scanner">
                            <div class="fingerprint-image">
                                <div class="fingerprint-lines"></div>
                            </div>
                            <div class="scan-animation"></div>
                        </div>
                        <p>Coloque el dedo en el escáner para verificación</p>
                        <div class="fingerprint-status" id="verify-fingerprint-status">Esperando captura...</div>
                    </div>
                    <button id="verify-btn">Verificar Identidad</button>
                    <div id="verification-result" class="verification-result" style="display:none;"></div>
                </div>
            </div>

            <div class="tab-content" id="inmates-tab">
                <div class="card">
                    <h2>Lista de Reclusos Registrados</h2>
                    <div class="search-box">
                        <input type="text" id="search-inmate" placeholder="Buscar por nombre, apellido o documento...">
                    </div>
                    <div class="inmate-list" id="inmate-list">
                        <!-- Los reclusos se cargarán aquí dinámicamente -->
                    </div>
                </div>
            </div>
        </div>

        <!-- Modal para editar recluso -->
        <div class="edit-modal" id="edit-modal">
            <div class="edit-modal-content">
                <div class="edit-modal-header">
                    <h2 class="edit-modal-title">Editar Datos del Recluso</h2>
                    <button class="close-edit-modal">&times;</button>
                </div>
                <form id="edit-inmate-form">
                    <input type="hidden" id="edit-inmate-id">
                    
                    <h3>Datos Personales</h3>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="edit-inmate-name" class="required">Nombre</label>
                            <input type="text" id="edit-inmate-name" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="edit-inmate-lastname" class="required">Apellido</label>
                            <input type="text" id="edit-inmate-lastname" required>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="edit-inmate-id" class="required">Documento de Identidad</label>
                        <input type="text" id="edit-inmate-id" required readonly>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="edit-inmate-birthdate">Fecha de Nacimiento</label>
                            <input type="date" id="edit-inmate-birthdate">
                        </div>
                        
                        <div class="form-group">
                            <label for="edit-inmate-nationality">Nacionalidad</label>
                            <input type="text" id="edit-inmate-nationality">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="edit-inmate-crime" class="required">Delito o Causa de Ingreso</label>
                        <input type="text" id="edit-inmate-crime" required>
                    </div>
                    
                    <div class="section-divider"></div>
                    
                    <h3>Datos Biométricos</h3>
                    
                    <div class="form-group">
                        <label class="required">Foto de Rostro (Formato Carnet)</label>
                        <div class="face-capture">
                            <div class="face-preview carnet" id="edit-face-preview">
                                <span>Vista previa de la foto carnet</span>
                                <img id="edit-face-image" src="" alt="Foto de rostro">
                            </div>
                            <input type="file" id="edit-face-file" class="file-input" accept="image/*">
                            <label for="edit-face-file" class="file-label">Cambiar foto</label>
                            <div class="file-name" id="edit-file-name">Sin archivos seleccionados</div>
                        </div>
                    </div>
                    
                    <h4>Características Físicas</h4>
                    
                    <div class="physical-characteristics">
                        <div class="form-group">
                            <label for="edit-inmate-gender">Sexo</label>
                            <select id="edit-inmate-gender">
                                <option value="">Seleccionar</option>
                                <option value="Masculino">Masculino</option>
                                <option value="Femenino">Femenino</option>
                                <option value="Otro">Otro</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label for="edit-inmate-height">Estatura (cm)</label>
                            <input type="number" id="edit-inmate-height" min="100" max="250">
                        </div>
                        
                        <div class="form-group">
                            <label for="edit-inmate-weight">Peso (kg)</label>
                            <input type="number" id="edit-inmate-weight" min="30" max="200">
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="edit-inmate-eyes">Color de Ojos</label>
                            <input type="text" id="edit-inmate-eyes">
                        </div>
                        
                        <div class="form-group">
                            <label for="edit-inmate-skin">Color de Piel</label>
                            <input type="text" id="edit-inmate-skin">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="edit-inmate-marks">Marcas Particulares</label>
                        <textarea id="edit-inmate-marks" placeholder="Describa marcas particulares"></textarea>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="edit-inmate-tattoos">Tatuajes</label>
                            <textarea id="edit-inmate-tattoos" placeholder="Describa tatuajes"></textarea>
                        </div>
                        
                        <div class="form-group">
                            <label for="edit-inmate-scars">Cicatrices</label>
                            <textarea id="edit-inmate-scars" placeholder="Describa cicatrices"></textarea>
                        </div>
                    </div>
                    
                    <div class="edit-modal-footer">
                        <button type="button" class="btn-danger" id="cancel-edit">Cancelar</button>
                        <button type="submit" class="btn-warning">Actualizar Datos</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Modal para recuperación de contraseña -->
    <div class="modal" id="forgot-password-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Recuperar Contraseña</h2>
                <button class="close-modal">&times;</button>
            </div>
            <form id="forgot-password-form">
                <div class="form-group">
                    <label for="recovery-email">Correo Electrónico</label>
                    <input type="email" id="recovery-email" placeholder="Ingrese su correo electrónico" required>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn-danger" id="cancel-recovery">Cancelar</button>
                    <button type="submit" class="auth-btn">Enviar Instrucciones</button>
                </div>
            </form>
            <div id="recovery-alert" class="alert" style="display: none;"></div>
        </div>
    </div>

    <script>
        // Backend simulado para el sistema de autenticación
        const authBackend = {
            // Usuarios almacenados (en un sistema real, esto estaría en una base de datos)
            users: JSON.parse(localStorage.getItem('prisonSystemUsers')) || [],
            
            // Verificar si hay usuarios registrados
            hasUsers: function() {
                return this.users.length > 0;
            },
            
            // Verificar credenciales
            login: function(username, password) {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        const user = this.users.find(u => u.username === username && u.password === password);
                        if (user) {
                            resolve({
                                success: true,
                                user: {
                                    id: user.id,
                                    username: user.username,
                                    name: user.name,
                                    role: user.role
                                }
                            });
                        } else {
                            reject({
                                success: false,
                                message: 'Usuario o contraseña incorrectos'
                            });
                        }
                    }, 1000); // Simular tiempo de respuesta del servidor
                });
            },
            
            // Registrar nuevo usuario
            register: function(userData) {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        // Verificar si el usuario ya existe
                        const existingUser = this.users.find(u => u.username === userData.username);
                        if (existingUser) {
                            reject({
                                success: false,
                                message: 'El nombre de usuario ya está en uso'
                            });
                            return;
                        }
                        
                        // Verificar si el correo ya está registrado
                        const existingEmail = this.users.find(u => u.email === userData.email);
                        if (existingEmail) {
                            reject({
                                success: false,
                                message: 'El correo electrónico ya está registrado'
                            });
                            return;
                        }
                        
                        // Verificar que las contraseñas coincidan
                        if (userData.password !== userData.confirmPassword) {
                            reject({
                                success: false,
                                message: 'Las contraseñas no coinciden'
                            });
                            return;
                        }
                        
                        // Crear nuevo usuario
                        const newUser = {
                            id: this.users.length + 1,
                            username: userData.username,
                            password: userData.password, // En un sistema real, esto debería estar encriptado
                            email: userData.email,
                            name: userData.name,
                            role: 'administrador', // El primer usuario siempre será administrador
                            registrationDate: new Date().toISOString()
                        };
                        
                        // Agregar a la lista de usuarios
                        this.users.push(newUser);
                        this.saveUsers();
                        
                        resolve({
                            success: true,
                            message: 'Usuario registrado exitosamente',
                            user: {
                                id: newUser.id,
                                username: newUser.username,
                                name: newUser.name,
                                role: newUser.role
                            }
                        });
                    }, 1000);
                });
            },
            
            // Recuperar contraseña
            recoverPassword: function(email) {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        const user = this.users.find(u => u.email === email);
                        if (user) {
                            // En un sistema real, aquí se enviaría un correo con instrucciones
                            resolve({
                                success: true,
                                message: 'Se han enviado las instrucciones para recuperar su contraseña a su correo electrónico.'
                            });
                        } else {
                            reject({
                                success: false,
                                message: 'No se encontró ningún usuario con ese correo electrónico.'
                            });
                        }
                    }, 1000);
                });
            },
            
            // Guardar usuarios en localStorage
            saveUsers: function() {
                localStorage.setItem('prisonSystemUsers', JSON.stringify(this.users));
            }
        };

        // Base de datos simulada (en un caso real, esto estaría en un servidor)
        let inmates = JSON.parse(localStorage.getItem('prisonInmates')) || [];
        let todayRegistrations = JSON.parse(localStorage.getItem('todayRegistrations')) || { count: 0, date: new Date().toDateString() };
        
        // Verificar si es un nuevo día para resetear el contador
        if (todayRegistrations.date !== new Date().toDateString()) {
            todayRegistrations = { count: 0, date: new Date().toDateString() };
            localStorage.setItem('todayRegistrations', JSON.stringify(todayRegistrations));
        }
        
        // Elementos del DOM para el sistema de autenticación
        const authContainer = document.getElementById('auth-container');
        const mainApp = document.getElementById('main-app');
        const loginForm = document.getElementById('login-form');
        const registerForm = document.getElementById('register-form');
        const authAlert = document.getElementById('auth-alert');
        const authTitle = document.getElementById('auth-title');
        const registerLink = document.getElementById('register-link');
        const loginLink = document.getElementById('login-link');
        const forgotPasswordLink = document.getElementById('forgot-password-link');
        const forgotPasswordModal = document.getElementById('forgot-password-modal');
        const forgotPasswordForm = document.getElementById('forgot-password-form');
        const recoveryAlert = document.getElementById('recovery-alert');
        const cancelRecoveryBtn = document.getElementById('cancel-recovery');
        const logoutBtn = document.getElementById('logout-btn');
        const currentUserElement = document.getElementById('current-user');
        
        // Elementos del DOM para la aplicación principal
        const inmateForm = document.getElementById('inmate-form');
        const inmateList = document.getElementById('inmate-list');
        const searchInmate = document.getElementById('search-inmate');
        const biometricCapture = document.getElementById('biometric-capture');
        const verifyBiometric = document.getElementById('verify-biometric');
        const verifyBtn = document.getElementById('verify-btn');
        const verificationResult = document.getElementById('verification-result');
        const fingerprintStatus = document.getElementById('fingerprint-status');
        const verifyFingerprintStatus = document.getElementById('verify-fingerprint-status');
        const faceFileInput = document.getElementById('face-file');
        const facePreview = document.getElementById('face-preview');
        const faceImage = document.getElementById('face-image');
        const fileName = document.getElementById('file-name');
        const tabs = document.querySelectorAll('.tab');
        const tabContents = document.querySelectorAll('.tab-content');
        
        // Elementos del modal de edición
        const editModal = document.getElementById('edit-modal');
        const editInmateForm = document.getElementById('edit-inmate-form');
        const editInmateId = document.getElementById('edit-inmate-id');
        const editInmateName = document.getElementById('edit-inmate-name');
        const editInmateLastname = document.getElementById('edit-inmate-lastname');
        const editInmateIdField = document.getElementById('edit-inmate-id');
        const editInmateBirthdate = document.getElementById('edit-inmate-birthdate');
        const editInmateNationality = document.getElementById('edit-inmate-nationality');
        const editInmateCrime = document.getElementById('edit-inmate-crime');
        const editInmateGender = document.getElementById('edit-inmate-gender');
        const editInmateHeight = document.getElementById('edit-inmate-height');
        const editInmateWeight = document.getElementById('edit-inmate-weight');
        const editInmateEyes = document.getElementById('edit-inmate-eyes');
        const editInmateSkin = document.getElementById('edit-inmate-skin');
        const editInmateMarks = document.getElementById('edit-inmate-marks');
        const editInmateTattoos = document.getElementById('edit-inmate-tattoos');
        const editInmateScars = document.getElementById('edit-inmate-scars');
        const editFaceFileInput = document.getElementById('edit-face-file');
        const editFacePreview = document.getElementById('edit-face-preview');
        const editFaceImage = document.getElementById('edit-face-image');
        const editFileName = document.getElementById('edit-file-name');
        const closeEditModalBtn = document.querySelector('.close-edit-modal');
        const cancelEditBtn = document.getElementById('cancel-edit');
        
        // Elementos del logo
        const logoImage = document.getElementById('logo-image');
        const logoText = document.getElementById('logo-text');
        
        // Estadísticas
        const totalInmatesElement = document.getElementById('total-inmates');
        const todayRegistrationsElement = document.getElementById('today-registrations');
        const repeatOffendersElement = document.getElementById('repeat-offenders');
        
        // Variables para el estado de captura
        let isScanning = false;
        let fingerprintData = null;
        let verifyFingerprintData = null;
        let facePhotoData = null;
        let editFacePhotoData = null;
        
        // Estado de autenticación
        let currentUser = null;
        
        // Inicializar la aplicación
        function init() {
            // Verificar si ya hay una sesión activa
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                showMainApp();
            } else {
                // Verificar si hay usuarios registrados
                if (authBackend.hasUsers()) {
                    showLogin();
                } else {
                    showRegistration();
                }
            }
            
            setupEventListeners();
        }
        
        // Configurar event listeners
        function setupEventListeners() {
            // Login
            loginForm.addEventListener('submit', handleLogin);
            registerForm.addEventListener('submit', handleRegistration);
            registerLink.addEventListener('click', showRegistration);
            loginLink.addEventListener('click', showLogin);
            forgotPasswordLink.addEventListener('click', showForgotPasswordModal);
            forgotPasswordForm.addEventListener('submit', handlePasswordRecovery);
            cancelRecoveryBtn.addEventListener('click', closeForgotPasswordModal);
            logoutBtn.addEventListener('click', handleLogout);
            
            // Envío del formulario
            inmateForm.addEventListener('submit', handleFormSubmit);
            
            // Búsqueda
            searchInmate.addEventListener('input', renderInmateList);
            
            // Captura de huella dactilar
            biometricCapture.addEventListener('click', startFingerprintCapture);
            verifyBiometric.addEventListener('click', startVerificationCapture);
            
            // Verificación
            verifyBtn.addEventListener('click', verifyInmate);
            
            // Carga de foto de rostro
            faceFileInput.addEventListener('change', handleFacePhotoUpload);
            editFaceFileInput.addEventListener('change', handleEditFacePhotoUpload);
            
            // Pestañas
            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    const tabId = tab.getAttribute('data-tab');
                    switchTab(tabId);
                });
            });
            
            // Modal de edición
            closeEditModalBtn.addEventListener('click', closeEditModal);
            cancelEditBtn.addEventListener('click', closeEditModal);
            editInmateForm.addEventListener('submit', handleEditFormSubmit);
            
            // Cerrar modal al hacer clic fuera del contenido
            editModal.addEventListener('click', (e) => {
                if (e.target === editModal) {
                    closeEditModal();
                }
            });
            
            // Cerrar modal de recuperación al hacer clic fuera
            forgotPasswordModal.addEventListener('click', (e) => {
                if (e.target === forgotPasswordModal) {
                    closeForgotPasswordModal();
                }
            });
        }
        
        // Mostrar pantalla de login
        function showLogin() {
            loginForm.style.display = 'block';
            registerForm.style.display = 'none';
            authTitle.textContent = 'Iniciar Sesión';
            authAlert.style.display = 'none';
        }
        
        // Mostrar pantalla de registro
        function showRegistration() {
            loginForm.style.display = 'none';
            registerForm.style.display = 'block';
            authTitle.textContent = 'Registro de Administrador';
            authAlert.style.display = 'none';
        }
        
        // Mostrar aplicación principal
        function showMainApp() {
            authContainer.style.display = 'none';
            mainApp.style.display = 'block';
            currentUserElement.textContent = currentUser.name;
            updateStats();
            renderInmateList();
        }
        
        // Manejar inicio de sesión
        function handleLogin(e) {
            e.preventDefault();
            
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            // Mostrar indicador de carga
            const loginBtn = loginForm.querySelector('.auth-btn');
            const originalText = loginBtn.textContent;
            loginBtn.textContent = 'Iniciando sesión...';
            loginBtn.disabled = true;
            
            authBackend.login(username, password)
                .then(response => {
                    if (response.success) {
                        currentUser = response.user;
                        localStorage.setItem('currentUser', JSON.stringify(currentUser));
                        showMainApp();
                        showAuthAlert('Inicio de sesión exitoso', 'success');
                    }
                })
                .catch(error => {
                    showAuthAlert(error.message, 'danger');
                })
                .finally(() => {
                    // Restaurar el botón
                    loginBtn.textContent = originalText;
                    loginBtn.disabled = false;
                });
        }
        
        // Manejar registro de usuario
        function handleRegistration(e) {
            e.preventDefault();
            
            const name = document.getElementById('register-name').value;
            const username = document.getElementById('register-username').value;
            const email = document.getElementById('register-email').value;
            const password = document.getElementById('register-password').value;
            const confirmPassword = document.getElementById('register-confirm-password').value;
            
            // Mostrar indicador de carga
            const registerBtn = registerForm.querySelector('.auth-btn');
            const originalText = registerBtn.textContent;
            registerBtn.textContent = 'Registrando...';
            registerBtn.disabled = true;
            
            authBackend.register({
                name,
                username,
                email,
                password,
                confirmPassword
            })
                .then(response => {
                    if (response.success) {
                        currentUser = response.user;
                        localStorage.setItem('currentUser', JSON.stringify(currentUser));
                        showMainApp();
                        showAuthAlert(response.message, 'success');
                    }
                })
                .catch(error => {
                    showAuthAlert(error.message, 'danger');
                })
                .finally(() => {
                    // Restaurar el botón
                    registerBtn.textContent = originalText;
                    registerBtn.disabled = false;
                });
        }
        
        // Manejar cierre de sesión
        function handleLogout() {
            currentUser = null;
            localStorage.removeItem('currentUser');
            // Verificar si hay usuarios registrados para mostrar login o registro
            if (authBackend.hasUsers()) {
                showLogin();
            } else {
                showRegistration();
            }
            authContainer.style.display = 'flex';
            mainApp.style.display = 'none';
            loginForm.reset();
            registerForm.reset();
        }
        
        // Mostrar modal de recuperación de contraseña
        function showForgotPasswordModal(e) {
            e.preventDefault();
            forgotPasswordModal.style.display = 'flex';
        }
        
        // Cerrar modal de recuperación de contraseña
        function closeForgotPasswordModal() {
            forgotPasswordModal.style.display = 'none';
            recoveryAlert.style.display = 'none';
            forgotPasswordForm.reset();
        }
        
        // Manejar recuperación de contraseña
        function handlePasswordRecovery(e) {
            e.preventDefault();
            
            const email = document.getElementById('recovery-email').value;
            
            // Mostrar indicador de carga
            const submitBtn = forgotPasswordForm.querySelector('.auth-btn');
            const originalText = submitBtn.textContent;
            submitBtn.textContent = 'Enviando...';
            submitBtn.disabled = true;
            
            authBackend.recoverPassword(email)
                .then(response => {
                    if (response.success) {
                        showAuthAlert(response.message, 'success', recoveryAlert);
                        setTimeout(() => {
                            closeForgotPasswordModal();
                        }, 3000);
                    }
                })
                .catch(error => {
                    showAuthAlert(error.message, 'danger', recoveryAlert);
                })
                .finally(() => {
                    // Restaurar el botón
                    submitBtn.textContent = originalText;
                    submitBtn.disabled = false;
                });
        }
        
        // Mostrar alerta en el sistema de autenticación
        function showAuthAlert(message, type, container = authAlert) {
            container.textContent = message;
            container.className = `alert alert-${type}`;
            container.style.display = 'block';
            
            // Ocultar después de 3 segundos
            setTimeout(() => {
                container.style.display = 'none';
            }, 3000);
        }
        
        // Cambiar pestañas
        function switchTab(tabId) {
            // Actualizar pestañas activas
            tabs.forEach(tab => {
                if (tab.getAttribute('data-tab') === tabId) {
                    tab.classList.add('active');
                } else {
                    tab.classList.remove('active');
                }
            });
            
            // Actualizar contenido activo
            tabContents.forEach(content => {
                if (content.id === `${tabId}-tab`) {
                    content.classList.add('active');
                } else {
                    content.classList.remove('active');
                }
            });
            
            // Actualizar navegación
            document.querySelectorAll('.main-nav a').forEach(link => {
                if (link.getAttribute('data-tab') === tabId) {
                    link.classList.add('active');
                } else {
                    link.classList.remove('active');
                }
            });
        }
        
        // Manejar carga de foto de rostro
        function handleFacePhotoUpload(e) {
            const file = e.target.files[0];
            if (file) {
                fileName.textContent = file.name;
                
                const reader = new FileReader();
                reader.onload = function(event) {
                    faceImage.src = event.target.result;
                    faceImage.style.display = 'block';
                    facePreview.querySelector('span').style.display = 'none';
                    facePhotoData = event.target.result;
                };
                reader.readAsDataURL(file);
            }
        }
        
        // Manejar carga de foto de rostro en edición
        function handleEditFacePhotoUpload(e) {
            const file = e.target.files[0];
            if (file) {
                editFileName.textContent = file.name;
                
                const reader = new FileReader();
                reader.onload = function(event) {
                    editFaceImage.src = event.target.result;
                    editFaceImage.style.display = 'block';
                    editFacePreview.querySelector('span').style.display = 'none';
                    editFacePhotoData = event.target.result;
                };
                reader.readAsDataURL(file);
            }
        }
        
        // Iniciar captura de huella dactilar
        function startFingerprintCapture() {
            if (isScanning) return;
            
            isScanning = true;
            biometricCapture.classList.add('scanning');
            fingerprintStatus.textContent = "Escaneando huella...";
            fingerprintStatus.className = "fingerprint-status status-scanning";
            
            // Simular proceso de escaneo
            setTimeout(() => {
                biometricCapture.classList.remove('scanning');
                fingerprintData = generateFingerprintData();
                fingerprintStatus.textContent = "Huella capturada correctamente";
                fingerprintStatus.className = "fingerprint-status status-captured";
                isScanning = false;
                
                showMainAlert('Huella dactilar capturada exitosamente', 'success');
            }, 2000);
        }
        
        // Iniciar captura para verificación
        function startVerificationCapture() {
            if (isScanning) return;
            
            isScanning = true;
            verifyBiometric.classList.add('scanning');
            verifyFingerprintStatus.textContent = "Escaneando huella...";
            verifyFingerprintStatus.className = "fingerprint-status status-scanning";
            
            // Simular proceso de escaneo
            setTimeout(() => {
                verifyBiometric.classList.remove('scanning');
                verifyFingerprintData = generateFingerprintData();
                verifyFingerprintStatus.textContent = "Huella capturada correctamente";
                verifyFingerprintStatus.className = "fingerprint-status status-captured";
                isScanning = false;
                
                showMainAlert('Huella dactilar capturada para verificación', 'success');
            }, 2000);
        }
        
        // Generar datos de huella dactilar simulados
        function generateFingerprintData() {
            // Sistema de ejemplo, En un sistema real, esto vendría de un escáner de huellas
            // Genere un identificador único para la huella
            return 'fingerprint_' + Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15);
        }
        
        // Manejar envío del formulario
        function handleFormSubmit(e) {
            e.preventDefault();
            
            const name = document.getElementById('inmate-name').value;
            const lastname = document.getElementById('inmate-lastname').value;
            const id = document.getElementById('inmate-id').value;
            const birthdate = document.getElementById('inmate-birthdate').value;
            const nationality = document.getElementById('inmate-nationality').value;
            const crime = document.getElementById('inmate-crime').value;
            const gender = document.getElementById('inmate-gender').value;
            const height = document.getElementById('inmate-height').value;
            const weight = document.getElementById('inmate-weight').value;
            const eyes = document.getElementById('inmate-eyes').value;
            const skin = document.getElementById('inmate-skin').value;
            const marks = document.getElementById('inmate-marks').value;
            const tattoos = document.getElementById('inmate-tattoos').value;
            const scars = document.getElementById('inmate-scars').value;
            
            // Verificar si ya existe un recluso con el mismo ID
            const existingInmate = inmates.find(inmate => inmate.id === id);
            if (existingInmate) {
                alert('Ya existe un recluso con este número de identificación');
                return;
            }
            
            // Verificar que se haya capturado la huella
            if (!fingerprintData) {
                alert('Debe capturar la huella dactilar antes de registrar al recluso');
                return;
            }
            
            // Verificar que se haya cargado la foto
            if (!facePhotoData) {
                alert('Debe cargar una foto de rostro antes de registrar al recluso');
                return;
            }
            
            // Crear nuevo recluso
            const newInmate = {
                id,
                name: `${name} ${lastname}`,
                firstName: name,
                lastName: lastname,
                birthdate,
                nationality,
                crime,
                gender,
                height,
                weight,
                eyes,
                skin,
                marks,
                tattoos,
                scars,
                fingerprintData,
                facePhoto: facePhotoData,
                registrationDate: new Date().toISOString(),
                visits: 1 // Contador de ingresos al penal
            };
            
            // Agregar a la base de datos
            inmates.push(newInmate);
            localStorage.setItem('prisonInmates', JSON.stringify(inmates));
            
            // Actualizar estadísticas
            todayRegistrations.count++;
            localStorage.setItem('todayRegistrations', JSON.stringify(todayRegistrations));
            
            // Mostrar mensaje de éxito
            showMainAlert('Recluso registrado exitosamente', 'success');
            
            // Limpiar formulario
            inmateForm.reset();
            fingerprintData = null;
            facePhotoData = null;
            fingerprintStatus.textContent = "Esperando captura...";
            fingerprintStatus.className = "fingerprint-status";
            faceImage.style.display = 'none';
            facePreview.querySelector('span').style.display = 'block';
            fileName.textContent = 'Sin archivos seleccionados';
            
            // Actualizar lista y estadísticas
            updateStats();
            renderInmateList();
        }
        
        // Verificar identidad mediante huella dactilar
        function verifyInmate() {
            if (!verifyFingerprintData) {
                alert('Debe capturar una huella para verificar');
                return;
            }
            
            // Buscar coincidencia en la base de datos
            const matchedInmate = inmates.find(inmate => inmate.fingerprintData === verifyFingerprintData);
            
            if (matchedInmate) {
                // Incrementar contador de visitas
                matchedInmate.visits++;
                localStorage.setItem('prisonInmates', JSON.stringify(inmates));
                
                verificationResult.innerHTML = `
                    <div class="match-found">¡COINCIDENCIA ENCONTRADA!</div>
                    <p>Recluso identificado: ${matchedInmate.name}</p>
                    <p>Número de identificación: ${matchedInmate.id}</p>
                    <p>Delito: ${matchedInmate.crime}</p>
                    <p>Esta es su visita número: ${matchedInmate.visits} al penal</p>
                `;
                
                showMainAlert('Recluso identificado. Es un reincidente.', 'warning');
            } else {
                verificationResult.innerHTML = `
                    <div class="no-match">NO SE ENCONTRARON COINCIDENCIAS</div>
                    <p>Esta huella dactilar no está registrada en el sistema.</p>
                `;
                
                showMainAlert('No se encontraron coincidencias en la base de datos', 'danger');
            }
            
            verificationResult.style.display = 'block';
            updateStats();
        }
        
        // Renderizar lista de reclusos
        function renderInmateList() {
            const searchTerm = searchInmate.value.toLowerCase();
            
            // Filtrar reclusos según término de búsqueda
            const filteredInmates = inmates.filter(inmate => 
                inmate.name.toLowerCase().includes(searchTerm) || 
                inmate.id.toLowerCase().includes(searchTerm)
            );
            
            // Generar HTML
            inmateList.innerHTML = '';
            
            if (filteredInmates.length === 0) {
                inmateList.innerHTML = '<p>No se encontraron reclusos</p>';
                return;
            }
            
            filteredInmates.forEach(inmate => {
                const inmateElement = document.createElement('div');
                inmateElement.className = 'inmate-item';
                
                // Crear iniciales para la foto
                const initials = inmate.name.split(' ').map(n => n[0]).join('').toUpperCase();
                
                // Formatear fecha de nacimiento para mostrar
                const formattedBirthdate = inmate.birthdate ? new Date(inmate.birthdate).toLocaleDateString() : 'No registrada';
                
                inmateElement.innerHTML = `
                    <div class="inmate-photo">
                        ${inmate.facePhoto ? `<img src="${inmate.facePhoto}" alt="${inmate.name}">` : initials}
                    </div>
                    <div class="inmate-info">
                        <div class="inmate-name">${inmate.name}</div>
                        <div class="inmate-details">
                            <div><span class="detail-label">ID:</span> ${inmate.id}</div>
                            <div><span class="detail-label">Fecha Nac.:</span> ${formattedBirthdate}</div>
                            <div><span class="detail-label">Nacionalidad:</span> ${inmate.nationality}</div>
                            <div><span class="detail-label">Delito:</span> ${inmate.crime}</div>
                            <div><span class="detail-label">Sexo:</span> ${inmate.gender || 'No registrado'}</div>
                            <div><span class="detail-label">Estatura:</span> ${inmate.height || 'N/A'} cm</div>
                            <div><span class="detail-label">Peso:</span> ${inmate.weight || 'N/A'} kg</div>
                            <div><span class="detail-label">Fecha registro:</span> ${new Date(inmate.registrationDate).toLocaleDateString()}</div>
                            <div><span class="detail-label">Visitas:</span> ${inmate.visits}</div>
                        </div>
                    </div>
                    <div class="inmate-actions">
                        <button class="btn-warning edit-btn" data-id="${inmate.id}">Editar</button>
                        <button class="btn-danger delete-btn" data-id="${inmate.id}">Eliminar</button>
                    </div>
                `;
                
                inmateList.appendChild(inmateElement);
            });
            
            // Agregar event listeners a los botones de eliminar
            document.querySelectorAll('.delete-btn').forEach(button => {
                button.addEventListener('click', function() {
                    const inmateId = this.getAttribute('data-id');
                    deleteInmate(inmateId);
                });
            });
            
            // Agregar event listeners a los botones de editar
            document.querySelectorAll('.edit-btn').forEach(button => {
                button.addEventListener('click', function() {
                    const inmateId = this.getAttribute('data-id');
                    openEditModal(inmateId);
                });
            });
        }
        
        // Abrir modal de edición
        function openEditModal(inmateId) {
            const inmate = inmates.find(inmate => inmate.id === inmateId);
            if (!inmate) return;
            
            // Llenar el formulario con los datos del recluso
            editInmateId.value = inmate.id;
            editInmateName.value = inmate.firstName;
            editInmateLastname.value = inmate.lastName;
            editInmateIdField.value = inmate.id;
            editInmateBirthdate.value = inmate.birthdate;
            editInmateNationality.value = inmate.nationality;
            editInmateCrime.value = inmate.crime;
            editInmateGender.value = inmate.gender;
            editInmateHeight.value = inmate.height;
            editInmateWeight.value = inmate.weight;
            editInmateEyes.value = inmate.eyes;
            editInmateSkin.value = inmate.skin;
            editInmateMarks.value = inmate.marks;
            editInmateTattoos.value = inmate.tattoos;
            editInmateScars.value = inmate.scars;
            
            // Cargar la foto si existe
            if (inmate.facePhoto) {
                editFaceImage.src = inmate.facePhoto;
                editFaceImage.style.display = 'block';
                editFacePreview.querySelector('span').style.display = 'none';
                editFacePhotoData = inmate.facePhoto;
            } else {
                editFaceImage.style.display = 'none';
                editFacePreview.querySelector('span').style.display = 'block';
                editFacePhotoData = null;
            }
            
            // Mostrar el modal
            editModal.style.display = 'flex';
        }
        
        // Cerrar modal de edición
        function closeEditModal() {
            editModal.style.display = 'none';
            editFacePhotoData = null;
            editFileName.textContent = 'Sin archivos seleccionados';
        }
        
        // Manejar envío del formulario de edición
        function handleEditFormSubmit(e) {
            e.preventDefault();
            
            const inmateId = editInmateId.value;
            const name = editInmateName.value;
            const lastname = editInmateLastname.value;
            const id = editInmateIdField.value;
            const birthdate = editInmateBirthdate.value;
            const nationality = editInmateNationality.value;
            const crime = editInmateCrime.value;
            const gender = editInmateGender.value;
            const height = editInmateHeight.value;
            const weight = editInmateWeight.value;
            const eyes = editInmateEyes.value;
            const skin = editInmateSkin.value;
            const marks = editInmateMarks.value;
            const tattoos = editInmateTattoos.value;
            const scars = editInmateScars.value;
            
            // Buscar el recluso a actualizar
            const inmateIndex = inmates.findIndex(inmate => inmate.id === inmateId);
            if (inmateIndex === -1) {
                alert('Error: Recluso no encontrado');
                return;
            }
            
            // Actualizar los datos del recluso
            inmates[inmateIndex] = {
                ...inmates[inmateIndex],
                id,
                name: `${name} ${lastname}`,
                firstName: name,
                lastName: lastname,
                birthdate,
                nationality,
                crime,
                gender,
                height,
                weight,
                eyes,
                skin,
                marks,
                tattoos,
                scars,
                facePhoto: editFacePhotoData || inmates[inmateIndex].facePhoto,
                // Incrementar el contador de visitas al editar
                visits: inmates[inmateIndex].visits + 1
            };
            
            // Guardar en localStorage
            localStorage.setItem('prisonInmates', JSON.stringify(inmates));
            
            // Mostrar mensaje de éxito
            showMainAlert('Datos del recluso actualizados exitosamente', 'success');
            
            // Cerrar el modal
            closeEditModal();
            
            // Actualizar lista y estadísticas
            updateStats();
            renderInmateList();
        }
        
        // Eliminar recluso
        function deleteInmate(id) {
            if (confirm('¿Está seguro de que desea eliminar este recluso del sistema?')) {
                inmates = inmates.filter(inmate => inmate.id !== id);
                localStorage.setItem('prisonInmates', JSON.stringify(inmates));
                updateStats();
                renderInmateList();
                showMainAlert('Recluso eliminado del sistema', 'success');
            }
        }
        
        // Actualizar estadísticas
        function updateStats() {
            totalInmatesElement.textContent = inmates.length;
            todayRegistrationsElement.textContent = todayRegistrations.count;
            
            // Contar reincidentes (más de una visita)
            const repeatOffenders = inmates.filter(inmate => inmate.visits > 1).length;
            repeatOffendersElement.textContent = repeatOffenders;
        }
        
        // Mostrar alerta en la aplicación principal
        function showMainAlert(message, type) {
            // Crear elemento de alerta
            const alert = document.createElement('div');
            alert.className = `alert alert-${type}`;
            alert.textContent = message;
            
            // Insertar después del header
            document.querySelector('.cicpc-header').after(alert);
            
            // Remover después de 3 segundos
            setTimeout(() => {
                alert.remove();
            }, 3000);
        }
        
        // Inicializar la aplicación cuando se carga la página
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
