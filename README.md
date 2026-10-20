<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ebim Barbeiro - Agendamento</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-color: #121212;
            --card-bg: #1e1e1e;
            --accent-gold: #d4af37;
            --accent-gold-hover: #b8962e;
            --text-light: #f5f5f5;
            --text-muted: #aaaaaa;
            --border-color: #333333;
            --danger: #e74c3c;
            --success: #2ecc71;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Montserrat', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-light);
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            padding: 15px;
        }

        .app-container {
            width: 100%;
            max-width: 480px;
            background-color: var(--card-bg);
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(212, 175, 55, 0.2);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            margin-bottom: 20px;
        }

        header {
            background: linear-gradient(180deg, rgba(30,30,30,1) 0%, rgba(18,18,18,1) 100%);
            padding: 25px 20px;
            text-align: center;
            border-bottom: 2px solid var(--accent-gold);
            position: relative;
        }

        .barber-icon {
            font-size: 38px;
            color: var(--accent-gold);
            margin-bottom: 8px;
        }

        h1 {
            font-family: 'Playfair Display', serif;
            font-size: 26px;
            color: var(--accent-gold);
            letter-spacing: 1px;
            margin-bottom: 4px;
            text-transform: uppercase;
        }

        .subtitle {
            font-size: 12px;
            color: var(--text-muted);
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .admin-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(212, 175, 55, 0.15);
            color: var(--accent-gold);
            border: 1px solid var(--accent-gold);
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 11px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .admin-badge:hover {
            background: var(--accent-gold);
            color: #000;
        }

        main {
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        label {
            font-size: 13px;
            font-weight: 600;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        label i {
            color: var(--accent-gold);
        }

        input[type="text"],
        input[type="date"],
        input[type="password"] {
            width: 100%;
            padding: 12px 15px;
            background-color: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: #fff;
            font-size: 15px;
            outline: none;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus,
        input[type="date"]:focus,
        input[type="password"]:focus {
            border-color: var(--accent-gold);
        }

        .services-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .service-card {
            border: 1px solid var(--border-color);
            border-radius: 10px;
            padding: 12px 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: all 0.2s ease;
            background-color: rgba(255, 255, 255, 0.02);
        }

        .service-card:hover {
            border-color: rgba(212, 175, 55, 0.5);
        }

        .service-card.selected {
            border-color: var(--accent-gold);
            background-color: rgba(212, 175, 55, 0.1);
        }

        .service-info {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .service-icon {
            width: 38px;
            height: 38px;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.05);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-gold);
            font-size: 16px;
        }

        .service-name {
            font-weight: 600;
            font-size: 14px;
        }

        .service-duration {
            font-size: 11px;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .service-price {
            font-weight: 700;
            color: var(--accent-gold);
            font-size: 15px;
        }

        .slots-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
        }

        .time-slot {
            padding: 12px 5px;
            background-color: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: #fff;
            text-align: center;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .time-slot:hover:not(.disabled) {
            border-color: var(--accent-gold);
        }

        .time-slot.selected {
            background-color: var(--accent-gold);
            color: #000;
            border-color: var(--accent-gold);
        }

        .time-slot.disabled {
            opacity: 0.25;
            cursor: not-allowed;
            text-decoration: line-through;
            background-color: rgba(231, 76, 60, 0.1);
            border-color: rgba(231, 76, 60, 0.3);
            color: #e74c3c;
        }

        .day-info {
            font-size: 12px;
            color: var(--accent-gold);
            margin-top: 4px;
            font-weight: 500;
        }

        .closed-notice {
            background-color: rgba(231, 76, 60, 0.1);
            border: 1px solid var(--danger);
            color: #ff6b6b;
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            font-size: 13px;
            display: none;
        }

        .btn-submit {
            background: linear-gradient(135deg, #25D366 0%, #128C7E 100%);
            color: white;
            border: none;
            padding: 15px;
            border-radius: 10px;
            font-size: 15px;
            font-weight: 700;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 15px rgba(37, 211, 102, 0.3);
            transition: transform 0.2s, box-shadow 0.2s;
            margin-top: 10px;
        }

        .btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(37, 211, 102, 0.4);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.85);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background-color: var(--card-bg);
            border: 1px solid var(--accent-gold);
            border-radius: 16px;
            width: 100%;
            max-width: 440px;
            max-height: 85vh;
            overflow-y: auto;
            padding: 20px;
            position: relative;
        }

        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: var(--text-muted);
            font-size: 20px;
            cursor: pointer;
        }

        .modal-title {
            color: var(--accent-gold);
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .pass-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            padding: 10px 0;
        }

        .btn-gold {
            background-color: var(--accent-gold);
            color: #000;
            border: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: 700;
            cursor: pointer;
            transition: background 0.3s;
        }

        .btn-gold:hover {
            background-color: var(--accent-gold-hover);
        }

        .error-msg {
            color: var(--danger);
            font-size: 12px;
            display: none;
        }

        .appointment-item {
            background-color: rgba(255, 255, 255, 0.03);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .appointment-info h4 {
            font-size: 14px;
            color: #fff;
        }

        .appointment-info p {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .btn-cancel {
            background-color: rgba(231, 76, 60, 0.2);
            color: var(--danger);
            border: 1px solid var(--danger);
            padding: 6px 10px;
            border-radius: 6px;
            font-size: 11px;
            cursor: pointer;
        }

        .btn-cancel:hover {
            background-color: var(--danger);
            color: #fff;
        }

        footer {
            text-align: center;
            padding: 15px;
            font-size: 11px;
            color: var(--text-muted);
            border-top: 1px solid rgba(255,255,255,0.05);
        }
    </style>
</head>
<body>

    <div class="app-container">
        <header>
            <button class="admin-badge" id="btnOpenAdmin">
                <i class="fa-solid fa-lock"></i> Barbeiro
            </button>
            <div class="barber-icon">
                <i class="fa-solid fa-scissors"></i>
            </div>
            <h1>Ebim Barbeiro</h1>
            <p class="subtitle">Agendamento Online</p>
        </header>

        <main>
            <!-- Nome do Cliente -->
            <div class="form-group">
                <label for="clientName"><i class="fa-solid fa-user"></i> Seu Nome Completo</label>
                <input type="text" id="clientName" placeholder="Digite seu nome..." autocomplete="off">
            </div>

            <!-- Seleção do Serviço -->
            <div class="form-group">
                <label><i class="fa-solid fa-list-check"></i> Selecione o Serviço</label>
                <div class="services-grid">
                    <div class="service-card selected" data-service="Cabelo" data-price="35">
                        <div class="service-info">
                            <div class="service-icon"><i class="fa-solid fa-scissors"></i></div>
                            <div>
                                <div class="service-name">Cabelo</div>
                                <div class="service-duration">Atendimento: até 1 hora</div>
                            </div>
                        </div>
                        <div class="service-price">R$ 35</div>
                    </div>

                    <div class="service-card" data-service="Barba" data-price="30">
                        <div class="service-info">
                            <div class="service-icon"><i class="fa-solid fa-user-ninja"></i></div>
                            <div>
                                <div class="service-name">Barba</div>
                                <div class="service-duration">Atendimento: até 1 hora</div>
                            </div>
                        </div>
                        <div class="service-price">R$ 30</div>
                    </div>

                    <div class="service-card" data-service="Cabelo + Barba" data-price="50">
                        <div class="service-info">
                            <div class="service-icon"><i class="fa-solid fa-crown"></i></div>
                            <div>
                                <div class="service-name">Combo Cabelo + Barba</div>
                                <div class="service-duration">Atendimento: até 1 hora</div>
                            </div>
                        </div>
                        <div class="service-price">R$ 50</div>
                    </div>
                </div>
            </div>

            <!-- Seleção de Data -->
            <div class="form-group">
                <label for="appointmentDate"><i class="fa-solid fa-calendar-days"></i> Escolha o Dia</label>
                <input type="date" id="appointmentDate">
                <div id="dayInfo" class="day-info"></div>
            </div>

            <!-- Seleção de Horários -->
            <div class="form-group">
                <label><i class="fa-solid fa-clock"></i> Escolha o Horário</label>
                <div class="closed-notice" id="closedNotice">
                    <i class="fa-solid fa-store-slash"></i> Barbearia fechada aos domingos.
                </div>
                <div class="slots-grid" id="slotsGrid"></div>
            </div>

            <!-- Botão Enviar WhatsApp -->
            <button class="btn-submit" id="btnSubmit">
                <i class="fa-brands fa-whatsapp"></i> Confirmar via WhatsApp
            </button>
        </main>

        <footer>
            Ebim Barbeiro &copy; Todos os direitos reservados.
        </footer>
    </div>

    <!-- Modal Autenticação Barbeiro -->
    <div class="modal" id="modalAuth">
        <div class="modal-content">
            <button class="close-modal" id="closeAuthModal">&times;</button>
            <div class="modal-title">
                <i class="fa-solid fa-shield-halved"></i> ÁREA DO BARBEIRO
            </div>
            <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">
                Digite a senha de administrador para gerenciar:
            </p>
            <div class="pass-container">
                <input type="password" id="inputPassword" placeholder="Senha (ex: 0070)" maxlength="8">
                <div class="error-msg" id="authError">Senha incorreta. Tente novamente!</div>
                <button class="btn-gold" id="btnVerifyPass">Entrar</button>
            </div>
        </div>
    </div>

    <!-- Modal Painel do Barbeiro -->
    <div class="modal" id="modalAdmin">
        <div class="modal-content">
            <button class="close-modal" id="closeAdminModal">&times;</button>
            <div class="modal-title">
                <i class="fa-solid fa-sliders"></i> Painel Ebim Barbeiro
            </div>
            <div class="modal-title" style="font-size: 15px;">
                <i class="fa-solid fa-list"></i> Horários Agendados
            </div>
            <div id="appointmentsList" style="margin-top: 10px;"></div>
        </div>
    </div>

    <script>
        const BARBER_PHONE = "5535974001097";
        const ADMIN_PASS = "0070";

        let selectedService = { name: "Cabelo", price: 35 };
        let selectedTime = null;

        // Horários exatos conforme solicitado
        const WEEKDAY_SLOTS = ["09:00", "10:00", "11:00", "14:00", "15:00", "16:00"]; // Seg-Sex
        const SATURDAY_SLOTS = ["09:00", "10:00", "11:00", "12:00"]; // Sábado

        // Elementos DOM
        const clientNameInput = document.getElementById('clientName');
        const appointmentDateInput = document.getElementById('appointmentDate');
        const dayInfoText = document.getElementById('dayInfo');
        const slotsGrid = document.getElementById('slotsGrid');
        const closedNotice = document.getElementById('closedNotice');
        const btnSubmit = document.getElementById('btnSubmit');

        const btnOpenAdmin = document.getElementById('btnOpenAdmin');
        const modalAuth = document.getElementById('modalAuth');
        const closeAuthModal = document.getElementById('closeAuthModal');
        const inputPassword = document.getElementById('inputPassword');
        const btnVerifyPass = document.getElementById('btnVerifyPass');
        const authError = document.getElementById('authError');

        const modalAdmin = document.getElementById('modalAdmin');
        const closeAdminModal = document.getElementById('closeAdminModal');
        const appointmentsList = document.getElementById('appointmentsList');

        document.addEventListener('DOMContentLoaded', () => {
            initDateInput();
            setupServiceSelection();
            renderSlots();
        });

        function initDateInput() {
            const today = new Date();
            const yyyy = today.getFullYear();
            const mm = String(today.getMonth() + 1).padStart(2, '0');
            const dd = String(today.getDate()).padStart(2, '0');
            
            appointmentDateInput.value = `${yyyy}-${mm}-${dd}`;
            appointmentDateInput.min = `${yyyy}-${mm}-${dd}`;
            
            appointmentDateInput.addEventListener('change', () => {
                selectedTime = null;
                renderSlots();
            });
        }

        function setupServiceSelection() {
            const cards = document.querySelectorAll('.service-card');
            cards.forEach(card => {
                card.addEventListener('click', () => {
                    cards.forEach(c => c.classList.remove('selected'));
                    card.classList.add('selected');
                    selectedService = {
                        name: card.getAttribute('data-service'),
                        price: card.getAttribute('data-price')
                    };
                });
            });
        }

        // Busca e grava no banco de memória permanente
        function getAppointments() {
            const data = localStorage.getItem('ebim_barber_db_v2');
            return data ? JSON.parse(data) : [];
        }

        function saveAppointment(item) {
            const db = getAppointments();
            db.push(item);
            localStorage.setItem('ebim_barber_db_v2', JSON.stringify(db));
        }

        function deleteAppointment(id) {
            let db = getAppointments();
            db = db.filter(a => a.id !== id);
            localStorage.setItem('ebim_barber_db_v2', JSON.stringify(db));
            renderAdminAppointment