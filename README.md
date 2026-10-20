# Ebim-barbearia
App de barbearia
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Barba & Estilo - Agendamento</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: {
                            400: '#facc15',
                            500: '#eab308',
                            600: '#ca8a04',
                            700: '#a16207',
                        },
                        dark: {
                            900: '#0f0f11',
                            800: '#18181b',
                            700: '#27272a',
                            600: '#3f3f46',
                        }
                    },
                    fontFamily: {
                        heading: ['Cinzel', 'serif'],
                        body: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f0f11;
            color: #f4f4f5;
        }
        .font-heading {
            font-family: 'Cinzel', serif;
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #18181b;
        }
        ::-webkit-scrollbar-thumb {
            background: #3f3f46;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #ca8a04;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between antialiased">

    <!-- Header Navigation -->
    <header class="bg-dark-800 border-b border-dark-700 sticky top-0 z-50 shadow-lg">
        <div class="max-w-md mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <i class="fa-solid fa-scissors text-gold-500 text-xl transform -rotate-45"></i>
                <span class="font-heading font-bold text-lg tracking-wider text-white">BARBA <span class="text-gold-500">&</span> ESTILO</span>
            </div>
            <button onclick="toggleView('barber')" id="toggle-view-btn" class="text-xs bg-dark-700 hover:bg-gold-500 hover:text-black text-gold-400 font-semibold py-1.5 px-3 rounded-lg border border-gold-500/30 transition duration-200 flex items-center gap-1.5">
                <i class="fa-solid fa-user-gear"></i>
                <span>Área do Barbeiro</span>
            </button>
        </div>
    </header>

    <main class="max-w-md mx-auto w-full px-4 py-6 flex-grow">

        <!-- ALERTA / MENSAGEM -->
        <div id="toast" class="hidden fixed top-16 left-1/2 transform -translate-x-1/2 z-50 bg-gold-500 text-black px-4 py-2 rounded-lg shadow-xl font-medium text-sm flex items-center gap-2">
            <i id="toast-icon" class="fa-solid fa-circle-info"></i>
            <span id="toast-msg">Mensagem</span>
        </div>

        <!-- ================= VISÃO DO CLIENTE (AGENDAMENTO) ================= -->
        <section id="client-view" class="space-y-6">
            
            <!-- Banner Inicial -->
            <div class="text-center py-2 border-b border-dark-700">
                <h1 class="font-heading text-2xl font-bold text-white tracking-wide">Agende seu Horário</h1>
                <p class="text-xs text-zinc-400 mt-1">Rápido, prático e sem filas. Atendimento exclusivo.</p>
            </div>

            <form id="booking-form" onsubmit="handleBooking(event)" class="space-y-5">
                
                <!-- 1. Dados Pessoais -->
                <div class="bg-dark-800 p-4 rounded-xl border border-dark-700 shadow-md space-y-3">
                    <h2 class="text-sm font-semibold text-gold-400 uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-user text-xs"></i> 1. Seus Dados
                    </h2>
                    <div>
                        <label class="block text-xs text-zinc-300 mb-1">Nome Completo *</label>
                        <input type="text" id="client-name" required placeholder="Ex: João Silva" 
                            class="w-full bg-dark-900 border border-dark-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-gold-500 transition">
                    </div>
                    <div>
                        <label class="block text-xs text-zinc-300 mb-1">Telefone / WhatsApp *</label>
                        <input type="tel" id="client-phone" required placeholder="(35) 99999-9999" 
                            class="w-full bg-dark-900 border border-dark-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-gold-500 transition">
                    </div>
                </div>

                <!-- 2. Escolha do Serviço -->
                <div class="bg-dark-800 p-4 rounded-xl border border-dark-700 shadow-md space-y-3">
                    <h2 class="text-sm font-semibold text-gold-400 uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-cut text-xs"></i> 2. Escolha o Serviço
                    </h2>
                    <div class="grid grid-cols-1 gap-2.5">
                        
                        <!-- Opção Cabelo -->
                        <label class="relative flex items-center justify-between p-3 rounded-lg border border-dark-700 bg-dark-900 cursor-pointer hover:border-gold-500/50 transition">
                            <div class="flex items-center gap-3">
                                <input type="radio" name="service" value="Cabelo" data-price="35" class="accent-gold-500 text-gold-500" required checked onchange="updateTotal()">
                                <div>
                                    <p class="font-medium text-sm text-white">Apenas Cabelo</p>
                                    <p class="text-xs text-zinc-400">Corte social, degradê ou tesoura</p>
                                </div>
                            </div>
                            <span class="font-bold text-gold-400 text-sm">R$ 35,00</span>
                        </label>

                        <!-- Opção Barba -->
                        <label class="relative flex items-center justify-between p-3 rounded-lg border border-dark-700 bg-dark-900 cursor-pointer hover:border-gold-500/50 transition">
                            <div class="flex items-center gap-3">
                                <input type="radio" name="service" value="Barba" data-price="30" class="accent-gold-500 text-gold-500" onchange="updateTotal()">
                                <div>
                                    <p class="font-medium text-sm text-white">Apenas Barba</p>
                                    <p class="text-xs text-zinc-400">Modelagem com toalha quente</p>
                                </div>
                            </div>
                            <span class="font-bold text-gold-400 text-sm">R$ 30,00</span>
                        </label>

                        <!-- Opção Combo -->
                        <label class="relative flex items-center justify-between p-3 rounded-lg border-2 border-gold-500/40 bg-gold-500/5 cursor-pointer hover:border-gold-500 transition">
                            <div class="flex items-center gap-3">
                                <input type="radio" name="service" value="Cabelo + Barba (Combo)" data-price="50" class="accent-gold-500 text-gold-500" onchange="updateTotal()">
                                <div>
                                    <div class="flex items-center gap-1.5">
                                        <p class="font-medium text-sm text-white">Cabelo + Barba</p>
                                        <span class="bg-gold-500 text-black font-extrabold text-[10px] px-1.5 py-0.5 rounded uppercase">Economize</span>
                                    </div>
                                    <p class="text-xs text-zinc-400">Serviço completo VIP</p>
                                </div>
                            </div>
                            <span class="font-bold text-gold-400 text-sm">R$ 50,00</span>
                        </label>

                    </div>
                </div>

                <!-- 3. Data e Horário -->
                <div class="bg-dark-800 p-4 rounded-xl border border-dark-700 shadow-md space-y-3">
                    <h2 class="text-sm font-semibold text-gold-400 uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-calendar-days text-xs"></i> 3. Data e Horário
                    </h2>
                    
                    <div>
                        <label class="block text-xs text-zinc-300 mb-1">Escolha o Dia (Segunda a Sexta) *</label>
                        <input type="date" id="booking-date" required onchange="handleDateChange()" 
                            class="w-full bg-dark-900 border border-dark-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-gold-500 transition">
                        <p id="date-warning" class="text-xs text-red-400 mt-1 hidden">Por favor, escolha apenas dias úteis (Segunda a Sexta).</p>
                    </div>

                    <div>
                        <label class="block text-xs text-zinc-300 mb-2">Horários Disponíveis *</label>
                        <div id="slots-container" class="grid grid-cols-3 gap-2">
                            <!-- Horários gerados via JS -->
                            <p class="text-xs text-zinc-500 col-span-3 text-center py-3">Selecione uma data válida primeiro.</p>
                        </div>
                        <input type="hidden" id="selected-slot" required>
                    </div>
                </div>

                <!-- Resumo e Botão de Envio -->
                <div class="bg-dark-800 p-4 rounded-xl border border-dark-700 space-y-3">
                    <div class="flex justify-between items-center text-sm border-b border-dark-700 pb-2">
                        <span class="text-zinc-400">Duração estimada:</span>
                        <span class="text-white font-medium">Até 1 hora</span>
                    </div>
                    <div class="flex justify-between items-center text-base font-bold">
                        <span class="text-white">Total a pagar:</span>
                        <span id="total-price" class="text-gold-400 text-lg">R$ 35,00</span>
                    </div>

                    <button type="submit" class="w-full bg-green-600 hover:bg-green-500 text-white font-bold py-3.5 px-4 rounded-xl shadow-lg hover:shadow-green-900/30 transition duration-200 flex items-center justify-center gap-2 text-sm">
                        <i class="fa-brands fa-whatsapp text-lg"></i>
                        <span>Confirmar via WhatsApp</span>
                    </button>
                    <p class="text-[11px] text-center text-zinc-500">Ao clicar, o WhatsApp será aberto para enviar a confirmação para a barbearia.</p>
                </div>

            </form>
        </section>

        <!-- ================= VISÃO DO BARBEIRO (PAINEL DE CONTROLE) ================= -->
        <section id="barber-view" class="space-y-6 hidden">
            
            <div class="flex justify-between items-center border-b border-dark-700 pb-3">
                <div>
                    <h1 class="font-heading text-xl font-bold text-white">Painel do Barbeiro</h1>
                    <p class="text-xs text-zinc-400">Gerencie horários e receba agendamentos</p>
                </div>
                <button onclick="toggleView('client')" class="text-xs text-zinc-400 hover:text-white underline">
                    Voltar ao site
                </button>
            </div>

            <!-- Configuração do Telefone -->
            <div class="bg-dark-800 p-4 rounded-xl border border-dark-700 space-y-3">
                <h2 class="text-sm font-semibold text-gold-400 flex items-center gap-2">
                    <i class="fa-solid fa-gear"></i> Configuração de Recebimento
                </h2>
                <div>
                    <label class="block text-xs text-zinc-300 mb-1">Seu Número de WhatsApp (com DDD)</label>
                    <div class="flex gap-2">
                        <input type="tel" id="barber-phone-config" placeholder="5535999999999" 
                            class="flex-1 bg-dark-900 border border-dark-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-gold-500">
                        <button onclick="saveBarberPhone()" class="bg-gold-500 hover:bg-gold-600 text-black font-bold px-4 py-2 rounded-lg text-xs transition">
                            Salvar
                        </button>
                    </div>
                    <p class="text-[11px] text-zinc-500 mt-1">Formato: 55 + DDD + Número (Apenas números).</p>
                </div>
            </div>

            <!-- Lista de Agendamentos -->
            <div class="bg-dark-800 p-4 rounded-xl border border-dark-700 space-y-3">
                <div class="flex justify-between items-center">
                    <h2 class="text-sm font-semibold text-gold-400 flex items-center gap-2">
                        <i class="fa-solid fa-list-check"></i> Horários Agendados
                    </h2>
                    <button onclick="clearAllAppointments()" class="text-xs text-red-400 hover:text-red-300">
                        Limpar Todos
                    </button>
                </div>

                <div id="appointments-list" class="space-y-2 mt-2">
                    <!-- Agendamentos injetados via JS -->
                </div>
            </div>

        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-dark-800 border-t border-dark-700 py-4 text-center text-xs text-zinc-500">
        <p>© <span id="year"></span> Barba & Estilo - Sistema de Agendamentos</p>
    </footer>

    <!-- SCRIPT DA APLICAÇÃO -->
    <script>
        // Configurações e Estado
        const AVAILABLE_TIMES = ["09:00", "10:00", "11:00", "14:00", "15:00", "16:00"];
        let defaultBarberPhone = "5535999999999"; // Valor padrão editável no painel
        
        // Elementos DOM
        const clientView = document.getElementById('client-view');
        const barberView = document.getElementById('barber-view');
        const toggleBtn = document.getElementById('toggle-view-btn');
        const dateInput = document.getElementById('booking-date');
        const slotsContainer = document.getElementById('slots-container');
        const selectedSlotInput = document.getElementById('selected-slot');
        const dateWarning = document.getElementById('date-warning');
        const barberPhoneConfig = document.getElementById('barber-phone-config');

        // Inicialização
        document.getElementById('year').textContent = new Date().getFullYear();
        
        // Configurar data mínima (hoje)
        const today = new Date().toISOString().split('T')[0];
        dateInput.min = today;

        // Carregar telefone salvo
        const savedPhone = localStorage.getItem('barber_whatsapp');
        if (savedPhone) {
            defaultBarberPhone = savedPhone;
        }
        barberPhoneConfig.value = defaultBarberPhone;

        // Função de Alertas (Toast)
        function showToast(msg, isError = false) {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toast-msg');
            const toastIcon = document.getElementById('toast-icon');

            toastMsg.textContent = msg;
            if(isError) {
                toast.classList.remove('bg-gold-500', 'text-black');
                toast.classList.add('bg-red-600', 'text-white');
                toastIcon.className = "fa-solid fa-circle-exclamation";
            } else {
                toast.classList.remove('bg-red-600', 'text-white');
                toast.classList.add('bg-gold-500', 'text-black');
                toastIcon.className = "fa-solid fa-circle-check";
            }

            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3000);
        }

        // Alternar entre Telas (Cliente / Barbeiro)
        function toggleView(view) {
            if(view === 'barber') {
                clientView.classList.add('hidden');
                barberView.classList.remove('hidden');
                toggleBtn.innerHTML = `<i class="fa-solid fa-calendar"></i><span>Ver Agendamento</span>`;
                loadBarberAppointments();
            } else {
                barberView.classList.add('hidden');
                clientView.classList.remove('hidden');
                toggleBtn.innerHTML = `<i class="fa-solid fa-user-gear"></i><span>Área do Barbeiro</span>`;
            }
        }

        // Atualizar Valor Total
        function updateTotal() {
            const selectedService = document.querySelector('input[name="service"]:checked');
            if(selectedService) {
                const price = selectedService.getAttribute('data-price');
                document.getElementById('total-price').textContent = `R$ ${parseFloat(price).toFixed(2).replace('.', ',')}`;
            }
        }

        // Validar e Renderizar Horários ao Alterar a Data
        function handleDateChange() {
            const selectedDateVal = dateInput.value;
            if(!selectedDateVal) return;

            // Criar objeto Data local
            const parts = selectedDateVal.split('-');
            const selectedDate = new Date(parts[0], parts[1] - 1, parts[2]);
            const dayOfWeek = selectedDate.getDay(); // 0 = Domingo, 6 = Sábado

            // Verificar se é fim de semana (0 ou 6)
            if(dayOfWeek === 0 || dayOfWeek === 6) {
                dateWarning.classList.remove('hidden');
                slotsContainer.innerHTML = `<p class="text-xs text-red-400 col-span-3 text-center py-2">Barbearia fechada aos fins de semana. Escolha de segunda a sexta.</p>`;
                selectedSlotInput.value = '';
                return;
            } else {
                dateWarning.classList.add('hidden');
            }

            renderTimeSlots(selectedDateVal);
        }

        // Renderizar Grade de Horários
        function renderTimeSlots(dateStr) {
            slotsContainer.innerHTML = '';
            selectedSlotInput.value = '';

            // Buscar agendamentos salvos no localStorage
            const appointments = JSON.parse(localStorage.getItem('barber_appointments') || '[]');
            
            // Filtrar horários ocupados para a data selecionada
            const occupiedTimes = appointments
                .filter(app => app.date === dateStr)
                .map(app => app.time);

            AVAILABLE_TIMES.forEach(time => {
                const isOccupied = occupiedTimes.includes(time);
                
                const btn = document.createElement('button');
                btn.type = 'button';
                btn.className = `py-2 px-3 text-xs font-semibold rounded-lg border transition duration-150 flex flex-col items-center justify-center gap-1 ${
                    isOccupied 
                    ? 'bg-dark-900 border-dark-700 text-zinc-600 cursor-not-allowed line-through' 
                    : 'b
