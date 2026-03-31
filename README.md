<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal de Saúde SulAmérica | LCGBR</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Chosen Palette: Corporate Health (Blue-600, Teal-500, Gray-50, White) -->
    <!-- Application Structure Plan: The SPA is structured as a tabbed dashboard. This prevents overwhelming the user with a long wall of text. 
         - "Visão Geral" provides a quick summary and a visual representation of holistic care.
         - "Saúde Física" and "Saúde Mental" separate the core services logically.
         - "Saúde Mental" uses an interactive toggle to compare the two distinct psychological programs.
         - "Como Acessar" offers a step-by-step guide and an interactive checklist to prepare for online consultations. -->
    <!-- Visualization & Content Choices: 
         - Goal: Inform (Holistic Care) -> Donut Chart -> Visually represents that physical and mental health are equally supported -> Chart.js.
         - Goal: Compare (Mental Health) -> Interactive Toggle -> Allows user to digest one program at a time without clutter -> Vanilla JS.
         - Goal: Change/Process (Preparation) -> Interactive Checklist -> Encourages active user engagement before a consultation -> Vanilla JS.
         - CONFIRMING: NO SVG used (Unicode emojis used for icons). NO Mermaid JS used. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; background-color: #F9FAFB; }
        
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 350px;
        }

        .tab-btn.active {
            border-bottom: 4px solid #2563EB;
            color: #1D4ED8;
            font-weight: 600;
        }
        
        .fade-in {
            animation: fadeIn 0.4s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .checklist-item.checked {
            text-decoration: line-through;
            color: #9CA3AF;
        }
    </style>
</head>
<body class="text-gray-800 antialiased">

    <header class="bg-white shadow-sm sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center py-4">
                <div>
                    <h1 class="text-2xl font-bold text-blue-700">🏥 Portal de Cuidado</h1>
                    <p class="text-sm text-gray-500">Parceria LCGBR & SulAmérica</p>
                </div>
                <div class="hidden sm:block text-right">
                    <p class="text-sm font-semibold text-gray-600">Dúvidas? Ligue para nós:</p>
                    <p class="text-lg font-bold text-blue-600">📞 0800-970-0500</p>
                </div>
            </div>
            
            <nav class="flex overflow-x-auto whitespace-nowrap mt-2 border-b border-gray-200 hide-scrollbar" id="tabs">
                <button onclick="switchTab('visao-geral')" class="tab-btn active px-4 py-3 text-sm text-gray-600 hover:text-blue-600 focus:outline-none transition-colors duration-200">Visão Geral</button>
                <button onclick="switchTab('saude-fisica')" class="tab-btn px-4 py-3 text-sm text-gray-600 hover:text-blue-600 focus:outline-none transition-colors duration-200">👨‍⚕️ Saúde Física</button>
                <button onclick="switchTab('saude-mental')" class="tab-btn px-4 py-3 text-sm text-gray-600 hover:text-blue-600 focus:outline-none transition-colors duration-200">🧠 Saúde Mental</button>
                <button onclick="switchTab('como-acessar')" class="tab-btn px-4 py-3 text-sm text-gray-600 hover:text-blue-600 focus:outline-none transition-colors duration-200">📲 Como Acessar</button>
            </nav>
        </div>
    </header>

    <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-8 min-h-[70vh]">

        <section id="visao-geral" class="tab-content fade-in block">
            <div class="text-center max-w-3xl mx-auto mb-10">
                <h2 class="text-3xl font-bold text-gray-900 mb-4">Cuidar de você é nossa prioridade!</h2>
                <p class="text-lg text-gray-600">A <strong>LCGBR Consultoria e Serviços de Internet S/A</strong>, em parceria com a <strong>SulAmérica</strong>, garante que você tenha acesso ao melhor cuidado, onde quer que esteja. Explore as ferramentas digitais disponíveis no seu plano.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                    <h3 class="text-xl font-bold text-gray-800 mb-4 text-center">Espectro de Cuidado Integrado</h3>
                    <p class="text-sm text-gray-500 mb-6 text-center">Seu plano cobre integralmente todas as esferas da sua saúde digitalmente.</p>
                    <div class="chart-container">
                        <canvas id="cuidadoChart"></canvas>
                    </div>
                </div>

                <div class="space-y-4">
                    <div onclick="switchTab('saude-fisica')" class="cursor-pointer bg-blue-50 hover:bg-blue-100 transition p-5 rounded-xl border border-blue-100 flex items-center shadow-sm">
                        <div class="text-4xl mr-4">👨‍⚕️</div>
                        <div>
                            <h4 class="font-bold text-blue-800 text-lg">Médico na Tela</h4>
                            <p class="text-sm text-blue-600">Pronto atendimento 24h e especialistas direto no celular.</p>
                        </div>
                    </div>
                    
                    <div onclick="switchTab('saude-mental')" class="cursor-pointer bg-teal-50 hover:bg-teal-100 transition p-5 rounded-xl border border-teal-100 flex items-center shadow-sm">
                        <div class="text-4xl mr-4">🧠</div>
                        <div>
                            <h4 class="font-bold text-teal-800 text-lg">Saúde Mental</h4>
                            <p class="text-sm text-teal-600">Psicólogos por vídeo e acompanhamento multidisciplinar.</p>
                        </div>
                    </div>

                    <div onclick="switchTab('como-acessar')" class="cursor-pointer bg-indigo-50 hover:bg-indigo-100 transition p-5 rounded-xl border border-indigo-100 flex items-center shadow-sm">
                        <div class="text-4xl mr-4">📲</div>
                        <div>
                            <h4 class="font-bold text-indigo-800 text-lg">Praticidade Digital</h4>
                            <p class="text-sm text-indigo-600">Acesse tudo pelo aplicativo SulAmérica Saúde facilmente.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="saude-fisica" class="tab-content fade-in hidden">
            <div class="mb-8 border-b border-gray-200 pb-6">
                <h2 class="text-3xl font-bold text-blue-800 flex items-center">
                    <span class="text-4xl mr-3">👨‍⚕️</span> Médico na Tela (Saúde na Tela)
                </h2>
                <p class="mt-4 text-lg text-gray-600">Esta seção detalha o serviço de telemedicina focado na sua saúde física. Esqueça as filas de pronto-socorro para casos simples; agora o médico vai até você com total segurança e conforto.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <div class="bg-white p-6 rounded-xl shadow-sm border-t-4 border-blue-500">
                    <div class="text-3xl mb-3">⏱️</div>
                    <h4 class="font-bold text-gray-800 mb-2">Pronto Atendimento 24h</h4>
                    <p class="text-sm text-gray-600">Consultas com Clínicos Gerais e Pediatras disponíveis a qualquer hora, 7 dias por semana.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-sm border-t-4 border-blue-500">
                    <div class="text-3xl mb-3">🩺</div>
                    <h4 class="font-bold text-gray-800 mb-2">Especialistas</h4>
                    <p class="text-sm text-gray-600">Agendamento de consultas com mais de 50 especialidades médicas diferentes.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-sm border-t-4 border-blue-500">
                    <div class="text-3xl mb-3">📄</div>
                    <h4 class="font-bold text-gray-800 mb-2">Documentos Digitais</h4>
                    <p class="text-sm text-gray-600">Receba receitas, guias de exames e atestados por SMS ou e-mail, válidos em todo o Brasil.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-sm border-t-4 border-blue-500">
                    <div class="text-3xl mb-3">🛡️</div>
                    <h4 class="font-bold text-gray-800 mb-2">Segurança</h4>
                    <p class="text-sm text-gray-600">Atendimento no conforto de casa, evitando exposição a riscos em ambientes hospitalares.</p>
                </div>
            </div>
        </section>

        <section id="saude-mental" class="tab-content fade-in hidden">
            <div class="mb-8 border-b border-gray-200 pb-6">
                <h2 class="text-3xl font-bold text-teal-700 flex items-center">
                    <span class="text-4xl mr-3">🧠</span> Saúde Mental Integrada
                </h2>
                <p class="mt-4 text-lg text-gray-600">O bem-estar emocional é fundamental para uma vida equilibrada. Compare abaixo as duas modalidades de suporte especializado oferecidas para cuidar da sua mente de forma sigilosa e segura.</p>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-gray-200 overflow-hidden">
                <div class="flex flex-col sm:flex-row border-b border-gray-200 bg-gray-50">
                    <button onclick="toggleMentalHealth('psicologo')" id="btn-psicologo" class="flex-1 py-4 px-6 text-center font-bold text-teal-700 bg-white border-b-2 border-teal-500 focus:outline-none transition">
                        🛋️ 1. Psicólogo na Tela
                    </button>
                    <button onclick="toggleMentalHealth('unicamente')" id="btn-unicamente" class="flex-1 py-4 px-6 text-center font-semibold text-gray-500 hover:text-teal-600 focus:outline-none transition">
                        🧩 2. Programa Única Mente
                    </button>
                </div>

                <div class="p-8 min-h-[250px] flex items-center">
                    <div id="content-psicologo" class="w-full fade-in block">
                        <h3 class="text-2xl font-bold text-gray-800 mb-4">Sessões de Psicoterapia por Vídeo</h3>
                        <p class="text-gray-600 mb-6">Ideal para ajudar você a lidar com estresse, ansiedade, luto ou questões desafiadoras do dia a dia.</p>
                        <ul class="space-y-4">
                            <li class="flex items-start">
                                <span class="text-teal-500 mr-3 text-xl">⚙️</span>
                                <div>
                                    <strong class="text-gray-800">Como funciona:</strong>
                                    <span class="text-gray-600"> Com um pedido médico em mãos, você agenda sua sessão pelo app e escolhe o profissional de sua preferência.</span>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-teal-500 mr-3 text-xl">🔒</span>
                                <div>
                                    <strong class="text-gray-800">Comodidade:</strong>
                                    <span class="text-gray-600"> Consultas sigilosas e 100% seguras sem precisar se deslocar.</span>
                                </div>
                            </li>
                        </ul>
                    </div>

                    <div id="content-unicamente" class="w-full fade-in hidden">
                        <h3 class="text-2xl font-bold text-gray-800 mb-4">Acompanhamento Multidisciplinar</h3>
                        <p class="text-gray-600 mb-6">Um programa estruturado para quem precisa de um acompanhamento mais próximo, contínuo e aprofundado.</p>
                        <ul class="space-y-4">
                            <li class="flex items-start">
                                <span class="text-teal-500 mr-3 text-xl">🎯</span>
                                <div>
                                    <strong class="text-gray-800">Foco:</strong>
                                    <span class="text-gray-600"> Diagnóstico e tratamento de condições como depressão, ansiedade generalizada, burnout e síndrome do pânico.</span>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-teal-500 mr-3 text-xl">🤝</span>
                                <div>
                                    <strong class="text-gray-800">Diferencial:</strong>
                                    <span class="text-gray-600"> Além de psicólogos, o programa conta com suporte de psiquiatras e um plano de cuidado personalizado.</span>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-teal-500 mr-3 text-xl">📈</span>
                                <div>
                                    <strong class="text-gray-800">Monitoramento:</strong>
                                    <span class="text-gray-600"> Acompanhamento contínuo para garantir sua evolução real e bem-estar a longo prazo.</span>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="como-acessar" class="tab-content fade-in hidden">
            <div class="mb-8 border-b border-gray-200 pb-6">
                <h2 class="text-3xl font-bold text-indigo-700 flex items-center">
                    <span class="text-4xl mr-3">📲</span> Como acessar esses benefícios?
                </h2>
                <p class="mt-4 text-lg text-gray-600">Tudo o que você precisa está na palma da sua mão através do Aplicativo SulAmérica Saúde. Siga os passos e prepare-se para sua consulta virtual.</p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
                
                <div>
                    <h3 class="text-xl font-bold text-gray-800 mb-6">Passo a Passo de Acesso</h3>
                    <div class="space-y-6 relative before:absolute before:inset-0 before:ml-5 before:-translate-x-px md:before:mx-auto md:before:translate-x-0 before:h-full before:w-0.5 before:bg-gradient-to-b before:from-indigo-500 before:to-indigo-100">
                        
                        <div class="relative flex items-center justify-between md:justify-normal md:odd:flex-row-reverse group is-active">
                            <div class="flex items-center justify-center w-10 h-10 rounded-full border border-white bg-indigo-500 text-white font-bold shrink-0 md:order-1 md:group-odd:-translate-x-1/2 md:group-even:translate-x-1/2 shadow">1</div>
                            <div class="w-[calc(100%-4rem)] md:w-[calc(50%-2.5rem)] bg-white p-4 rounded border border-gray-200 shadow-sm">
                                <h4 class="font-bold text-gray-800">Baixe o App</h4>
                                <p class="text-sm text-gray-600 mt-1">Disponível gratuitamente nas lojas Google Play e App Store. Faça seu login com a carteirinha.</p>
                            </div>
                        </div>
                        
                        <div class="relative flex items-center justify-between md:justify-normal md:odd:flex-row-reverse group is-active">
                            <div class="flex items-center justify-center w-10 h-10 rounded-full border border-white bg-indigo-500 text-white font-bold shrink-0 md:order-1 md:group-odd:-translate-x-1/2 md:group-even:translate-x-1/2 shadow">2</div>
                            <div class="w-[calc(100%-4rem)] md:w-[calc(50%-2.5rem)] bg-white p-4 rounded border border-gray-200 shadow-sm">
                                <h4 class="font-bold text-gray-800">Acesse "Telemedicina"</h4>
                                <p class="text-sm text-gray-600 mt-1">No menu principal, você encontrará as opções <em>Médico na Tela</em> e <em>Psicólogo na Tela</em>.</p>
                            </div>
                        </div>

                        <div class="relative flex items-center justify-between md:justify-normal md:odd:flex-row-reverse group is-active">
                            <div class="flex items-center justify-center w-10 h-10 rounded-full border border-white bg-indigo-500 text-white font-bold shrink-0 md:order-1 md:group-odd:-translate-x-1/2 md:group-even:translate-x-1/2 shadow">3</div>
                            <div class="w-[calc(100%-4rem)] md:w-[calc(50%-2.5rem)] bg-white p-4 rounded border border-gray-200 shadow-sm">
                                <h4 class="font-bold text-gray-800">Portal Única Mente</h4>
                                <p class="text-sm text-gray-600 mt-1">Para o programa específico, acesse o portal <a href="https://painel.programasaudeativa.com.br/iniciativa/unica-mente" target="_blank" class="text-indigo-600 underline">Saúde Ativa</a> ou verifique adesão no app.</p>
                            </div>
                        </div>

                    </div>
                </div>

                <div class="bg-indigo-50 rounded-2xl p-8 border border-indigo-100">
                    <h3 class="text-xl font-bold text-indigo-900 mb-2">Checklist da Boa Consulta</h3>
                    <p class="text-sm text-indigo-700 mb-6">Marque os itens abaixo antes de iniciar sua vídeo chamada para garantir a melhor experiência.</p>
                    
                    <div class="space-y-3" id="interactive-checklist">
                        <label class="flex items-center p-3 bg-white rounded-lg shadow-sm cursor-pointer hover:bg-gray-50 transition border border-gray-200">
                            <input type="checkbox" class="w-5 h-5 text-indigo-600 rounded border-gray-300 focus:ring-indigo-500 checklist-checkbox">
                            <span class="ml-3 text-gray-700 font-medium">Estou em um local silencioso e bem iluminado.</span>
                        </label>
                        <label class="flex items-center p-3 bg-white rounded-lg shadow-sm cursor-pointer hover:bg-gray-50 transition border border-gray-200">
                            <input type="checkbox" class="w-5 h-5 text-indigo-600 rounded border-gray-300 focus:ring-indigo-500 checklist-checkbox">
                            <span class="ml-3 text-gray-700 font-medium">Minha conexão com a internet está estável (Wi-Fi preferencialmente).</span>
                        </label>
                        <label class="flex items-center p-3 bg-white rounded-lg shadow-sm cursor-pointer hover:bg-gray-50 transition border border-gray-200">
                            <input type="checkbox" class="w-5 h-5 text-indigo-600 rounded border-gray-300 focus:ring-indigo-500 checklist-checkbox">
                            <span class="ml-3 text-gray-700 font-medium">Tenho em mãos documentos e anotações sobre sintomas/dúvidas.</span>
                        </label>
                    </div>

                    <div class="mt-8 bg-white p-4 rounded-lg border-l-4 border-yellow-400">
                        <p class="text-sm text-gray-700"><strong>Lembre-se:</strong> A prevenção é o melhor caminho. Use a tecnologia a favor da sua saúde!</p>
                    </div>
                </div>

            </div>
        </section>

    </main>

    <footer class="bg-gray-900 text-white py-8 mt-12">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 text-center md:text-left flex flex-col md:flex-row justify-between items-center">
            <div class="mb-4 md:mb-0">
                <p class="text-lg font-bold">LCGBR Consultoria e Serviços de Internet S/A</p>
                <p class="text-gray-400 text-sm mt-1">Em parceria com SulAmérica</p>
            </div>
            <div class="bg-gray-800 px-6 py-3 rounded-lg border border-gray-700">
                <p class="text-sm text-gray-300 mb-1">Canais de atendimento SulAmérica:</p>
                <p class="text-xl font-bold text-blue-400">0800-970-0500</p>
                <p class="text-xs text-gray-500 mt-2">Dúvidas? Entre em contato com o seu RH.</p>
            </div>
        </div>
    </footer>

    <script>
        // Tab Navigation Logic
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.add('hidden');
                tab.classList.remove('block');
            });
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active', 'border-b', 'border-blue-600', 'text-blue-600', 'font-bold');
            });
            
            const activeContent = document.getElementById(tabId);
            activeContent.classList.remove('hidden');
            activeContent.classList.add('block');
            
            const activeBtn = Array.from(document.querySelectorAll('.tab-btn')).find(btn => btn.getAttribute('onclick').includes(tabId));
            if(activeBtn) {
                activeBtn.classList.add('active', 'border-b', 'border-blue-600', 'text-blue-600', 'font-bold');
            }
        }

        // Mental Health Toggle Logic
        function toggleMentalHealth(selection) {
            const btnPsi = document.getElementById('btn-psicologo');
            const btnUni = document.getElementById('btn-unicamente');
            const contentPsi = document.getElementById('content-psicologo');
            const contentUni = document.getElementById('content-unicamente');

            if (selection === 'psicologo') {
                btnPsi.className = "flex-1 py-4 px-6 text-center font-bold text-teal-700 bg-white border-b-2 border-teal-500 focus:outline-none transition";
                btnUni.className = "flex-1 py-4 px-6 text-center font-semibold text-gray-500 bg-gray-50 hover:text-teal-600 focus:outline-none transition border-b border-gray-200";
                
                contentPsi.classList.remove('hidden');
                contentPsi.classList.add('block');
                contentUni.classList.remove('block');
                contentUni.classList.add('hidden');
            } else {
                btnUni.className = "flex-1 py-4 px-6 text-center font-bold text-teal-700 bg-white border-b-2 border-teal-500 focus:outline-none transition";
                btnPsi.className = "flex-1 py-4 px-6 text-center font-semibold text-gray-500 bg-gray-50 hover:text-teal-600 focus:outline-none transition border-b border-gray-200";
                
                contentUni.classList.remove('hidden');
                contentUni.classList.add('block');
                contentPsi.classList.remove('block');
                contentPsi.classList.add('hidden');
            }
        }

        // Checklist Interaction Logic
        const checkboxes = document.querySelectorAll('.checklist-checkbox');
        checkboxes.forEach(box => {
            box.addEventListener('change', function() {
                const labelText = this.nextElementSibling;
                if(this.checked) {
                    labelText.classList.add('line-through', 'text-gray-400');
                    labelText.classList.remove('text-gray-700');
                } else {
                    labelText.classList.remove('line-through', 'text-gray-400');
                    labelText.classList.add('text-gray-700');
                }
            });
        });

        // Chart.js Initialization
        document.addEventListener('DOMContentLoaded', function() {
            const ctx = document.getElementById('cuidadoChart').getContext('2d');
            
            // Configuring chart plugin to wrap long text if needed
            Chart.defaults.font.family = "'Inter', sans-serif";
            Chart.defaults.color = '#6B7280';

            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: [
                        'Pronto Atend. 24h',
                        'Especialidades',
                        'Psicoterapia',
                        'Psiquiatria'
                    ],
                    datasets: [{
                        data: [25, 25, 25, 25], // Equal segments representing full spectrum of care
                        backgroundColor: [
                            '#3B82F6', // Blue (Physical/Urgency)
                            '#60A5FA', // Light Blue (Physical/Specialties)
                            '#14B8A6', // Teal (Mental/Therapy)
                            '#5EEAD4'  // Light Teal (Mental/Psychiatry)
                        ],
                        borderWidth: 2,
                        borderColor: '#ffffff',
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '65%',
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                usePointStyle: true,
                                pointStyle: 'circle'
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ' ' + context.label + ': Cobertura Integrada';
                                }
                            }
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>
