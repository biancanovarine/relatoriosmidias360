<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard de Performance - Dr. Rogério Saint-Clair Pimentel Mafra</title>
    
    <!-- Google Fonts: Plus Jakarta Sans -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0fdfa',
                            100: '#ccfbf1',
                            500: '#0d9488', /* Teal */
                            600: '#0f766e',
                            700: '#115e59',
                            900: '#134e4a',
                        },
                        accent: {
                            50: '#fffbeb',
                            500: '#d97706', /* Amber */
                            600: '#b45309',
                        }
                    }
                }
            }
        }
    </script>

    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        /* Custom scrollbar and subtle print styling */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        
        @media print {
            .no-print {
                display: none !important;
            }
            body {
                background-color: #ffffff !important;
                font-size: 12px;
            }
            .print-card {
                border: 1px solid #e2e8f0 !important;
                box-shadow: none !important;
                page-break-inside: avoid;
            }
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen antialiased flex flex-col">

    <!-- HEADER / NAVIGATION BAR -->
    <header class="sticky top-0 z-50 bg-white/85 backdrop-blur-md border-b border-slate-100/80 no-print transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Left Side: Doctor's Identity -->
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-brand-500 flex items-center justify-center text-white font-bold text-lg shadow-sm shadow-brand-500/20">
                    RM
                </div>
                <div>
                    <h1 class="text-lg font-extrabold tracking-tight text-slate-900 leading-tight">
                        Dr. Rogério Saint-Clair P. Mafra
                    </h1>
                    <p class="text-xs font-semibold text-brand-500 tracking-wider uppercase">Urologista • Performance Digital</p>
                </div>
            </div>

            <!-- Right Side: Chancelas / Trust Logos -->
            <div class="flex items-center space-x-6">
                <!-- Google Partner SVG -->
                <div class="hidden md:flex items-center space-x-2 bg-slate-50 px-3 py-1.5 rounded-lg border border-slate-100">
                    <svg class="h-4 w-auto" viewBox="0 0 100 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M8.2 12c0-2.3 1.9-4.2 4.2-4.2s4.2 1.9 4.2 4.2-1.9 4.2-4.2 4.2-4.2-1.9-4.2-4.2zm10.4 0c0-3.4-2.8-6.2-6.2-6.2S6.2 8.6 6.2 12s2.8 6.2 6.2 6.2 6.2-2.8 6.2-6.2z" fill="#EA4335"/>
                        <path d="M23.1 12c0-2.3 1.9-4.2 4.2-4.2s4.2 1.9 4.2 4.2-1.9 4.2-4.2 4.2-4.2-1.9-4.2-4.2zm10.4 0c0-3.4-2.8-6.2-6.2-6.2s-6.2 2.8-6.2 6.2 2.8 6.2 6.2 6.2 6.2-2.8 6.2-6.2z" fill="#FBBC05"/>
                        <path d="M38.5 12c0-2.3 1.9-4.2 4.2-4.2s4.2 1.9 4.2 4.2-1.9 4.2-4.2 4.2-4.2-1.9-4.2-4.2zm10.4 0c0-3.4-2.8-6.2-6.2-6.2s-6.2 2.8-6.2 6.2 2.8 6.2 6.2 6.2 6.2-2.8 6.2-6.2z" fill="#4285F4"/>
                        <path d="M53.8 12c0-2.3 1.9-4.2 4.2-4.2s4.2 1.9 4.2 4.2c0 .3 0 .5-.1.8l-4.1-4.1c1.2-1.2 3.1-1.2 4.3 0s1.2 3.1 0 4.3l-4.3-1.2zm6.2 0c0-3.4-2.8-6.2-6.2-6.2s-6.2 2.8-6.2 6.2 2.8 6.2 6.2 6.2h2v-2h-2c-2.3 0-4.2-1.9-4.2-4.2s1.9-4.2 4.2-4.2 4.2 1.9 4.2 4.2c0 .4-.1.8-.2 1.1l2.2.6c.1-.5.2-1.1.2-1.7z" fill="#34A853"/>
                        <text x="63" y="16" font-family="sans-serif" font-weight="bold" font-size="10" fill="#5F6368">Partner</text>
                    </svg>
                </div>

                <!-- Doctoralia Star Badge -->
                <div class="flex items-center space-x-2 bg-emerald-50/60 px-3 py-1.5 rounded-lg border border-emerald-100/50">
                    <svg class="w-4 h-4 text-emerald-600" fill="currentColor" viewBox="0 0 20 20">
                        <path d="M9 2a1 1 0 000 2h2a1 1 0 100-2H9z" />
                        <path fill-rule="evenodd" d="M4 5a2 2 0 012-2 3 3 0 003 3h2a3 3 0 003-3 2 2 0 012 2v11a2 2 0 01-2 2H6a2 2 0 01-2-2V5zm3 4a1 1 0 000 2h.01a1 1 0 100-2H7zm3 0a1 1 0 000 2h3a1 1 0 100-2h-3zm-3 4a1 1 0 100 2h.01a1 1 0 100-2H7zm3 0a1 1 0 100 2h3a1 1 0 100-2h-3z" clip-rule="evenodd" />
                    </svg>
                    <span class="text-xs font-bold text-emerald-800">Doctoralia Premium</span>
                    <!-- 5 Stars -->
                    <div class="flex items-center space-x-0.5 text-amber-500">
                        <svg class="w-3 h-3 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                        <svg class="w-3 h-3 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                        <svg class="w-3 h-3 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                        <svg class="w-3 h-3 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                        <svg class="w-3 h-3 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN BODY CONTAINER -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-10">

        <!-- SUB-HEADER CONTROL BAR -->
        <div class="bg-white rounded-[1.5rem] border border-slate-100 shadow-sm p-5 md:p-6 flex flex-col md:flex-row md:items-center justify-between gap-4 print-card">
            <div class="flex flex-wrap items-center gap-3">
                <span class="inline-flex items-center px-4 py-1.5 rounded-full text-xs font-bold bg-brand-50 text-brand-700 border border-brand-100/80">
                    <span class="w-2 h-2 rounded-full bg-brand-500 mr-2 animate-pulse"></span>
                    Período Consolidado: Junho 2026
                </span>
                <span class="text-sm font-medium text-slate-500">
                    01 de Junho de 2026 - 30 de Junho de 2026
                </span>
            </div>
            
            <div class="flex items-center gap-4 justify-between md:justify-end">
                <div class="text-left md:text-right">
                    <p class="text-[10px] font-bold tracking-wider text-slate-400 uppercase">CPC Médio Consolidado</p>
                    <p class="text-lg font-extrabold text-slate-900">R$ 3,39</p>
                </div>
                <div class="h-8 w-[1px] bg-slate-100 hidden md:block"></div>
                
                <button onclick="handleExport()" class="no-print bg-brand-500 hover:bg-brand-600 active:bg-brand-700 text-white font-semibold text-sm px-5 py-2.5 rounded-xl shadow-md shadow-brand-500/15 transition-all duration-200 flex items-center space-x-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                    </svg>
                    <span>Exportar Relatório</span>
                </button>
            </div>
        </div>

        <!-- NOTIFICATION CONTAINER (Custom Modal Alert) -->
        <div id="notification-modal" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm">
            <div class="bg-white rounded-[2rem] max-w-md w-full p-8 shadow-2xl border border-slate-100 animate-[bounce_0.5s_ease-out]">
                <div class="w-14 h-14 bg-emerald-50 text-emerald-600 rounded-full flex items-center justify-center mx-auto mb-4">
                    <svg class="w-7 h-7" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7" />
                    </svg>
                </div>
                <h3 class="text-xl font-bold text-center text-slate-900 mb-2">Relatório Preparado!</h3>
                <p class="text-sm text-center text-slate-500 mb-6 leading-relaxed">
                    A versão executiva foi otimizada para impressão. O diálogo de visualização e salvamento em formato PDF será aberto agora.
                </p>
                <button onclick="closeNotification()" class="w-full bg-slate-900 hover:bg-slate-800 text-white font-semibold py-3 rounded-xl transition duration-150">
                    Continuar e Imprimir
                </button>
            </div>
        </div>

        <!-- SECTION 1: ALCANCE DO ANÚNCIO NO GOOGLE -->
        <section class="space-y-6">
            <div class="space-y-2">
                <h2 class="text-2xl font-extrabold tracking-tight text-slate-900 flex items-center gap-2">
                    <span class="w-2.5 h-6 bg-brand-500 rounded-full inline-block"></span>
                    Alcance do Anúncio no Google Ads
                </h2>
                <p class="text-sm text-slate-500 max-w-3xl leading-relaxed">
                    Atração ativa de novos pacientes de Belo Horizonte através de pesquisas altamente qualificadas. O posicionamento geográfico cirúrgico maximiza a conversão direta de consultas.
                </p>
            </div>

            <!-- KPI GRID (5 Columns Desktop, Grid on Mobile) -->
            <div class="grid grid-cols-2 lg:grid-cols-5 gap-4 md:gap-6">
                <!-- KPI 1: Impressões -->
                <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 hover:shadow-md transition-shadow duration-300 print-card">
                    <div class="flex justify-between items-start mb-4">
                        <div class="p-2.5 rounded-xl bg-slate-50 text-slate-600">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                            </svg>
                        </div>
                        <span class="text-[10px] font-bold text-emerald-600 bg-emerald-50 px-2.5 py-1 rounded-full">+12.4% vs Mai</span>
                    </div>
                    <p class="text-2xl font-extrabold tracking-tight text-slate-900">8.171</p>
                    <p class="text-xs font-semibold text-slate-400 mt-1 uppercase tracking-wider">Impressões Totais</p>
                    <p class="text-[10px] text-slate-400 mt-2">Vezes que os anúncios foram exibidos nas buscas</p>
                </div>

                <!-- KPI 2: Cliques Diretos -->
                <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 hover:shadow-md transition-shadow duration-300 print-card">
                    <div class="flex justify-between items-start mb-4">
                        <div class="p-2.5 rounded-xl bg-brand-50 text-brand-500">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 15l-2 5L9 9l11 4-5 2zm0 0l5 5M7.188 2.239l.777 2.897M5.136 7.965l-2.898-.777M13.95 4.05l-2.122 2.122m-5.657 5.656l-2.12 2.122" />
                            </svg>
                        </div>
                        <span class="text-[10px] font-bold text-emerald-600 bg-emerald-50 px-2.5 py-1 rounded-full">+8.9% vs Mai</span>
                    </div>
                    <p class="text-2xl font-extrabold tracking-tight text-slate-900">399</p>
                    <p class="text-xs font-semibold text-slate-400 mt-1 uppercase tracking-wider">Cliques Diretos</p>
                    <p class="text-[10px] text-slate-400 mt-2">Volume de potenciais pacientes direcionados</p>
                </div>

                <!-- KPI 3: CTR Médio -->
                <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 hover:shadow-md transition-shadow duration-300 relative overflow-hidden print-card">
                    <!-- Amber highlighting border for ultra importance -->
                    <div class="absolute top-0 left-0 right-0 h-1 bg-amber-500"></div>
                    <div class="flex justify-between items-start mb-4">
                        <div class="p-2.5 rounded-xl bg-amber-50 text-amber-600">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
                            </svg>
                        </div>
                        <span class="text-[10px] font-bold text-amber-700 bg-amber-50 px-2.5 py-1 rounded-full">Excepcional</span>
                    </div>
                    <p class="text-2xl font-extrabold tracking-tight text-amber-600">4,88%</p>
                    <p class="text-xs font-semibold text-slate-400 mt-1 uppercase tracking-wider">CTR de Performance</p>
                    <p class="text-[10px] text-slate-400 mt-2">Média saudável do setor: <strong>3,17%</strong></p>
                </div>

                <!-- KPI 4: Acessos ao Perfil -->
                <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 hover:shadow-md transition-shadow duration-300 print-card">
                    <div class="flex justify-between items-start mb-4">
                        <div class="p-2.5 rounded-xl bg-slate-50 text-slate-600">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                            </svg>
                        </div>
                        <span class="text-[10px] font-bold text-brand-600 bg-brand-50 px-2.5 py-1 rounded-full">87,5% via Ads</span>
                    </div>
                    <p class="text-2xl font-extrabold tracking-tight text-slate-900">456</p>
                    <p class="text-xs font-semibold text-slate-400 mt-1 uppercase tracking-wider">Acessos ao Perfil</p>
                    <p class="text-[10px] text-slate-400 mt-2">399 dos 456 acessos vieram diretamente dos anúncios</p>
                </div>

                <!-- KPI 5: Cliques no Telefone -->
                <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 hover:shadow-md transition-shadow duration-300 print-card">
                    <div class="flex justify-between items-start mb-4">
                        <div class="p-2.5 rounded-xl bg-teal-50 text-teal-600">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.94.725l.548 2.2a1 1 0 01-.321.988l-1.305.98a10.582 10.582 0 004.872 4.872l.98-1.305a1 1 0 01.988-.321l2.2.548a1 1 0 01.725.94V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                            </svg>
                        </div>
                        <span class="text-[10px] font-bold text-emerald-600 bg-emerald-50 px-2.5 py-1 rounded-full">Contatos Diretos</span>
                    </div>
                    <p class="text-2xl font-extrabold tracking-tight text-slate-900">189</p>
                    <p class="text-xs font-semibold text-slate-400 mt-1 uppercase tracking-wider">Cliques no Telefone</p>
                    <p class="text-[10px] text-slate-400 mt-2">Soma de ligações diretas do perfil + site</p>
                </div>
            </div>
        </section>

        <!-- SECTION 2: BENCHMARK DE EFICIÊNCIA E DOMÍNIO DE BUSCA -->
        <section class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            
            <!-- Column Left (1/3): CTR Benchmark Chart -->
            <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 flex flex-col justify-between print-card">
                <div>
                    <h3 class="text-base font-extrabold text-slate-900 mb-1">Média de Cliques (CTR)</h3>
                    <p class="text-xs text-slate-400 leading-normal">Seu desempenho comparado com a média saudável nacional de clínicas e médicos (Urologistas).</p>
                </div>
                
                <!-- Chart Container -->
                <div class="my-6 relative flex items-center justify-center" style="height: 180px;">
                    <canvas id="ctrChart"></canvas>
                </div>

                <div class="bg-slate-50 rounded-2xl p-4 text-center">
                    <p class="text-xs font-semibold text-slate-600">
                        Seu CTR está <span class="text-brand-500 font-bold">+53.9% acima</span> da média saudável de mercado.
                    </p>
                </div>
            </div>

            <!-- Column Right (2/3): Search Dominance (Share of Voice) -->
            <div class="bg-slate-900 text-white rounded-[2rem] p-8 flex flex-col justify-between shadow-lg shadow-slate-950/20 relative overflow-hidden print-card">
                <!-- Abstract glowing circles in bg -->
                <div class="absolute -top-12 -right-12 w-48 h-48 bg-brand-500/10 rounded-full blur-2xl pointer-events-none"></div>
                <div class="absolute -bottom-12 -left-12 w-48 h-48 bg-amber-500/5 rounded-full blur-2xl pointer-events-none"></div>

                <div class="space-y-4">
                    <div class="flex items-center justify-between">
                        <span class="text-[10px] font-bold tracking-widest text-brand-500 uppercase">Share of Voice</span>
                        <span class="text-xs font-semibold text-slate-400 flex items-center">
                            <span class="w-1.5 h-1.5 rounded-full bg-brand-500 mr-2"></span>
                            Posições de Liderança
                        </span>
                    </div>
                    <h3 class="text-xl font-extrabold tracking-tight">Dominância nos Resultados de Busca</h3>
                    <p class="text-xs text-slate-400 leading-relaxed max-w-xl">
                        A Parcela de Impressão na rede de pesquisa mede com que frequência seu anúncio aparece nas primeiras posições quando elegível. Suas campanhas ocupam de forma sólida a fatia premium da página.
                    </p>
                </div>

                <!-- Progress bars layout -->
                <div class="my-6 space-y-5">
                    <!-- Progress Item 1 -->
                    <div class="space-y-2">
                        <div class="flex justify-between text-xs">
                            <span class="font-bold text-slate-300">Top 3 (Parte Superior da Página)</span>
                            <span class="font-extrabold text-brand-500">81,84%</span>
                        </div>
                        <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden">
                            <div class="bg-brand-500 h-full rounded-full transition-all duration-1000" style="width: 81.84%"></div>
                        </div>
                        <p class="text-[10px] text-slate-500">Percentual de anúncios mostrados acima dos resultados orgânicos gerais.</p>
                    </div>

                    <!-- Progress Item 2 -->
                    <div class="space-y-2">
                        <div class="flex justify-between text-xs">
                            <span class="font-bold text-slate-300">Top 1 (Primeira Posição Absoluta)</span>
                            <span class="font-extrabold text-amber-500">34,39%</span>
                        </div>
                        <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden">
                            <div class="bg-amber-500 h-full rounded-full transition-all duration-1000" style="width: 34.39%"></div>
                        </div>
                        <p class="text-[10px] text-slate-500">Seu anúncio é o Primeiríssimo resultado visível na tela para 1 em cada 3 buscas.</p>
                    </div>
                </div>

                <div class="border-t border-slate-800 pt-4 flex items-center justify-between text-xs text-slate-400">
                    <span>Média de Ganho em Leilões Real:</span>
                    <span class="font-bold text-white">40,28%</span>
                </div>
            </div>
        </section>

        <!-- SECTION 3: % GANHO EM LEILÕES (SHARE OF VOICE) -->
        <section class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 md:p-8 space-y-6 print-card">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                <div class="space-y-1">
                    <h3 class="text-lg font-extrabold text-slate-900">Análise Consolidada de Campanhas Ativas</h3>
                    <p class="text-xs text-slate-500">Métricas operacionais detalhadas extraídas diretamente da conta do Google Ads.</p>
                </div>
                <!-- Mini Badge indicating status -->
                <span class="self-start md:self-center bg-slate-100 text-slate-700 text-[10px] font-extrabold px-3 py-1.5 rounded-xl border border-slate-200">
                    2 Campanhas Estruturadas
                </span>
            </div>

            <!-- Table Wrapper for Responsiveness -->
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="border-b border-slate-100 text-[10px] font-extrabold text-slate-400 uppercase tracking-wider">
                            <th class="py-4 px-4">Campanha</th>
                            <th class="py-4 px-3 text-right">Impressões</th>
                            <th class="py-4 px-3 text-right">Cliques</th>
                            <th class="py-4 px-3 text-right">CTR</th>
                            <th class="py-4 px-3 text-right">CPC Médio</th>
                            <th class="py-4 px-3 text-right">% Topo (Top 3)</th>
                            <th class="py-4 px-3 text-right">% 1ª Posição</th>
                            <th class="py-4 px-4 text-right">Ganho em Leilão</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-slate-100 text-xs text-slate-700">
                        <!-- Row 1: Serviços -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 font-bold text-slate-900">
                                Serviços <span class="text-[9px] font-medium text-slate-400 block mt-0.5">Foco em Procedimentos</span>
                            </td>
                            <td class="py-4 px-3 text-right font-medium">5.894</td>
                            <td class="py-4 px-3 text-right font-medium">289</td>
                            <td class="py-4 px-3 text-right font-bold text-slate-900">4,90%</td>
                            <td class="py-4 px-3 text-right font-medium text-slate-600">R$ 3,34</td>
                            <td class="py-4 px-3 text-right font-medium">80,67%</td>
                            <td class="py-4 px-3 text-right font-medium">33,74%</td>
                            <td class="py-4 px-4 text-right">
                                <span class="inline-flex items-center px-2 py-0.5 rounded bg-brand-50 text-brand-700 font-bold text-[10px]">51,49%</span>
                            </td>
                        </tr>
                        <!-- Row 2: Especialidade -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 font-bold text-slate-900">
                                Especialidade <span class="text-[9px] font-medium text-slate-400 block mt-0.5">Foco em Consultas por "Urologista"</span>
                            </td>
                            <td class="py-4 px-3 text-right font-medium">2.277</td>
                            <td class="py-4 px-3 text-right font-medium">110</td>
                            <td class="py-4 px-3 text-right font-bold text-slate-900">4,83%</td>
                            <td class="py-4 px-3 text-right font-medium text-slate-600">R$ 3,50</td>
                            <td class="py-4 px-3 text-right font-medium">84,87%</td>
                            <td class="py-4 px-3 text-right font-medium">36,07%</td>
                            <td class="py-4 px-4 text-right">
                                <span class="inline-flex items-center px-2 py-0.5 rounded bg-slate-100 text-slate-700 font-bold text-[10px]">11,28%</span>
                            </td>
                        </tr>
                        <!-- Consolidado Total Row -->
                        <tr class="bg-slate-50 font-bold text-slate-900">
                            <td class="py-4 px-4 rounded-l-2xl">Total Consolidado</td>
                            <td class="py-4 px-3 text-right">8.171</td>
                            <td class="py-4 px-3 text-right">399</td>
                            <td class="py-4 px-3 text-right text-brand-600">4,88%</td>
                            <td class="py-4 px-3 text-right text-slate-700">R$ 3,39</td>
                            <td class="py-4 px-3 text-right">81,84%</td>
                            <td class="py-4 px-3 text-right">34,39%</td>
                            <td class="py-4 px-4 text-right rounded-r-2xl">
                                <span class="inline-flex items-center px-2.5 py-1 rounded bg-brand-500 text-white font-bold text-[10px]">40,28%</span>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Technical Analytics Note -->
            <div class="p-4 bg-slate-50/70 border border-slate-100 rounded-2xl flex items-start gap-3">
                <div class="p-1 rounded bg-brand-100 text-brand-600 mt-0.5">
                    <svg class="w-4.5 h-4.5" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"></path>
                    </svg>
                </div>
                <div>
                    <p class="text-[11px] font-bold text-slate-800">Nota de Análise Técnica — Mídias 360:</p>
                    <p class="text-[10px] text-slate-500 mt-0.5 leading-relaxed">
                        A campanha de "Serviços" apresenta uma dominância espetacular de leilão (51,49%), capitaneando o volume principal de cliques. Em paralelo, a campanha de "Especialidade" possui uma taxa de 1ª posição absoluta ainda maior (36,07%), garantindo que, para termos clínicos avançados, o Dr. Rogério surja imediatamente na vanguarda visual do paciente.
                    </p>
                </div>
            </div>
        </section>

        <!-- SECTION 4: PERFORMANCE DE PALAVRAS-CHAVE -->
        <section class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 md:p-8 space-y-6 print-card">
            <div class="space-y-1">
                <h3 class="text-lg font-extrabold text-slate-900">Termos de Busca de Maior Conversão</h3>
                <p class="text-xs text-slate-500">Exibição de palavras-chave qualificadas de acordo com as necessidades de atendimento do consultório em Belo Horizonte.</p>
            </div>

            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="border-b border-slate-100 text-[10px] font-extrabold text-slate-400 uppercase tracking-wider">
                            <th class="py-4 px-4">Palavra-Chave</th>
                            <th class="py-4 px-3 text-right">Impressões</th>
                            <th class="py-4 px-3 text-right">Cliques</th>
                            <th class="py-4 px-4 text-right">CTR (%)</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-slate-100 text-xs text-slate-700">
                        <!-- Term 1: Highlighted Translucent Turquoise -->
                        <tr class="bg-brand-50/70 hover:bg-brand-50 transition duration-150 font-semibold text-brand-900">
                            <td class="py-4 px-4 rounded-l-2xl flex items-center gap-2">
                                <span class="w-2 h-2 rounded-full bg-brand-500"></span>
                                urologistas belo horizonte
                            </td>
                            <td class="py-4 px-3 text-right">2.183</td>
                            <td class="py-4 px-3 text-right">110</td>
                            <td class="py-4 px-4 text-right rounded-r-2xl font-bold text-brand-700">5,04%</td>
                        </tr>
                        <!-- Term 2 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">aumento peniano cirúrgico</td>
                            <td class="py-4 px-3 text-right">1.953</td>
                            <td class="py-4 px-3 text-right">93</td>
                            <td class="py-4 px-4 text-right font-bold text-slate-900">4,76%</td>
                        </tr>
                        <!-- Term 3 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">próteses peniana</td>
                            <td class="py-4 px-3 text-right">589</td>
                            <td class="py-4 px-3 text-right">27</td>
                            <td class="py-4 px-4 text-right font-bold text-slate-900">4,58%</td>
                        </tr>
                        <!-- Term 4 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">prótese peniana preço</td>
                            <td class="py-4 px-3 text-right">259</td>
                            <td class="py-4 px-3 text-right">23</td>
                            <td class="py-4 px-4 text-right font-bold text-brand-600">8,88%</td>
                        </tr>
                        <!-- Term 5 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">especialista disfunção erétil</td>
                            <td class="py-4 px-3 text-right">236</td>
                            <td class="py-4 px-3 text-right">22</td>
                            <td class="py-4 px-4 text-right font-bold text-brand-600">9,32%</td>
                        </tr>
                        <!-- Term 6 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">especialista em fimose</td>
                            <td class="py-4 px-3 text-right">405</td>
                            <td class="py-4 px-3 text-right">21</td>
                            <td class="py-4 px-4 text-right font-bold text-slate-900">5,19%</td>
                        </tr>
                        <!-- Term 7 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">implante peniano</td>
                            <td class="py-4 px-3 text-right">490</td>
                            <td class="py-4 px-3 text-right">13</td>
                            <td class="py-4 px-4 text-right font-bold text-slate-900">2,65%</td>
                        </tr>
                        <!-- Term 8 -->
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-4 px-4 pl-8">implante peniano bh</td>
                            <td class="py-4 px-3 text-right">42</td>
                            <td class="py-4 px-3 text-right">13</td>
                            <td class="py-4 px-4 text-right font-bold text-amber-600">30,95%</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <!-- SECTION 5 & 6 DUPLEX: DOCTORALIA AGENDAMENTOS & PROVA SOCIAL -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            
            <!-- Doctoralia Agendamentos Table (Left) -->
            <div class="bg-white rounded-[2rem] border border-slate-100 shadow-sm p-6 md:p-8 flex flex-col justify-between print-card">
                <div class="space-y-4">
                    <div class="space-y-1">
                        <span class="text-[10px] font-bold text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-full inline-block">Conversão Final</span>
                        <h3 class="text-lg font-extrabold text-slate-900">Agendamentos Clínicos (Doctoralia)</h3>
                        <p class="text-xs text-slate-500">Histórico de agendamentos diretos e aquisição de pacientes de primeira consulta.</p>
                    </div>

                    <div class="overflow-x-auto pt-2">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-100 text-[10px] font-extrabold text-slate-400 uppercase tracking-wider">
                                    <th class="py-3 px-2">Período</th>
                                    <th class="py-3 px-2 text-center">Agendamentos Totais</th>
                                    <th class="py-3 px-2 text-right">Novos Pacientes</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-100 text-xs text-slate-700">
                                <!-- Month 1 -->
                                <tr class="hover:bg-slate-50/50 transition duration-150">
                                    <td class="py-3.5 px-2 font-bold text-slate-900">Abril 2026</td>
                                    <td class="py-3.5 px-2 text-center font-medium">76</td>
                                    <td class="py-3.5 px-2 text-right">
                                        <span class="font-bold text-emerald-600">21</span>
                                        <span class="text-[9px] text-slate-400 block italic">Primeira Consulta</span>
                                    </td>
                                </tr>
                                <!-- Month 2 -->
                                <tr class="hover:bg-slate-50/50 transition duration-150">
                                    <td class="py-3.5 px-2 font-bold text-slate-900">Maio 2026</td>
                                    <td class="py-3.5 px-2 text-center font-medium">57</td>
                                    <td class="py-3.5 px-2 text-right">
                                        <span class="font-bold text-emerald-600">10</span>
                                        <span class="text-[9px] text-slate-400 block italic">Primeira Consulta</span>
                                    </td>
                                </tr>
                                <!-- Month 3 -->
                                <tr class="hover:bg-slate-50/50 transition duration-150">
                                    <td class="py-3.5 px-2 font-bold text-slate-900">Junho 2026</td>
                                    <td class="py-3.5 px-2 text-center font-medium">58</td>
                                    <td class="py-3.5 px-2 text-right">
                                        <span class="font-bold text-emerald-600">7</span>
                                        <span class="text-[9px] text-slate-400 block italic">Primeira Consulta</span>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <p class="text-[10px] text-slate-400 mt-4 italic leading-normal">
                    * Os agendamentos englobam consultas presenciais presenciais em Belo Horizonte e telemedicina agendada de forma automatizada pelo perfil.
                </p>
            </div>

            <!-- Reputation & Social Proof (Right) -->
            <div class="bg-gradient-to-br from-brand-900 to-brand-950 text-white rounded-[2rem] p-8 flex flex-col justify-between shadow-lg shadow-brand-950/15 print-card">
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <span class="text-[10px] font-bold tracking-widest text-emerald-400 uppercase">Reputação & Presença</span>
                        <div class="flex items-center space-x-0.5 text-amber-500">
                            <!-- Star Icons SVG -->
                            <svg class="w-3.5 h-3.5 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                            <svg class="w-3.5 h-3.5 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                            <svg class="w-3.5 h-3.5 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                            <svg class="w-3.5 h-3.5 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                            <svg class="w-3.5 h-3.5 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
                        </div>
                    </div>

                    <div class="flex items-center gap-6">
                        <div>
                            <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Avaliação no Mês</p>
                            <p class="text-3xl font-extrabold text-emerald-400 mt-1">+1 opinião</p>
                        </div>
                        <div class="w-[1px] h-10 bg-brand-800"></div>
                        <div>
                            <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Histórico Acumulado</p>
                            <p class="text-3xl font-extrabold text-white mt-1">290 opiniões</p>
                        </div>
                    </div>

                    <p class="text-xs text-brand-100 leading-relaxed font-normal">
                        A excelência digital do Dr. Rogério cria um **círculo virtuoso sólido**. Estudos de comportamento mostram que cerca de **70% dos novos pacientes** que acessam o perfil urológico urologista interagem intensivamente e analisam a área de opiniões e depoimentos antes de finalizar o agendamento de consultas.
                    </p>
                </div>

                <div class="border-t border-brand-800/80 pt-4 text-[10px] text-brand-300">
                    Posicionamento Premium: Reconhecido entre os urologistas mais bem avaliados de Minas Gerais.
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="mt-auto bg-white border-t border-slate-100 py-6 no-print">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs text-slate-400">
            <div class="flex items-center space-x-2">
                <span class="font-bold text-slate-600">Mídias 360</span>
                <span>•</span>
                <span>Consultoria Especializada de Marketing Médico</span>
            </div>
            <div>
                © 2026 Dr. Rogério Saint-Clair P. Mafra. Todos os direitos reservados.
            </div>
        </div>
    </footer>

    <!-- JS LOGIC AND CHART.JS RENDERING -->
    <script>
        // Wait until document loads to render Chart
        window.onload = function() {
            renderChart();
        }

        function renderChart() {
            const ctx = document.getElementById('ctrChart').getContext('2d');
            
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Sua Performance', 'Média Saudável de Mercado'],
                    datasets: [{
                        data: [4.88, 3.17],
                        backgroundColor: [
                            'rgba(13, 148, 136, 0.95)', // Teal #0D9488
                            'rgba(148, 163, 184, 0.4)'  // Slate-400
                        ],
                        borderWidth: 0,
                        borderRadius: 12,
                        borderSkipped: false,
                        barThickness: 32
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ' CTR: ' + context.raw.toFixed(2) + '%';
                                }
                            },
                            backgroundColor: '#1e293b',
                            titleFont: { family: 'Plus Jakarta Sans', size: 11 },
                            bodyFont: { family: 'Plus Jakarta Sans', size: 12, weight: 'bold' },
                            padding: 10,
                            cornerRadius: 8
                        }
                    },
                    scales: {
                        x: {
                            grid: {
                                display: false
                            },
                            ticks: {
                                font: {
                                    family: 'Plus Jakarta Sans',
                                    size: 10,
                                    weight: '600'
                                },
                                color: '#64748b'
                            }
                        },
                        y: {
                            grid: {
                                color: '#f1f5f9'
                            },
                            ticks: {
                                callback: function(value) {
                                    return value + '%';
                                },
                                font: {
                                    family: 'Plus Jakarta Sans',
                                    size: 10
                                },
                                color: '#94a3b8'
                            }
                        }
                    }
                }
            });
        }

        // Action: Export/Print Handler
        function handleExport() {
            // Display custom modal alert
            document.getElementById('notification-modal').classList.remove('hidden');
        }

        function closeNotification() {
            // Hide custom modal alert
            document.getElementById('notification-modal').classList.add('hidden');
            // Trigger standard print
            window.print();
        }
    </script>
</body>
</html>
