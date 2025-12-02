Conversation opened. 1 unread message.

Skip to content
Using Gmail with screen readers
Enable desktop notifications for Gmail.
   OK  No thanks
1 of 24
(no subject)
Inbox

Cria Do Sistema <dosistemacria@gmail.com>
Attachments
Dec 2, 2025, 5:45 PM (3 days ago)
to me

 One attachment
  •  Scanned by Gmail
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aki Salgados - Sistema Integrado (Online)</title>
    <style>
        :root {
            --laranja: #FF6B35;
            --amarelo: #FFB238;
            --vermelho: #D1495B;
            --azul: #2B4162;
            --roxo: #6a0dad;
            --verde: #4CAF50;
            --cinza-claro: #f5f5f5;
            --cinza-escuro: #333;
        }
        
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--cinza-claro); color: var(--cinza-escuro); }
        
        /* LOGIN SCREEN */
        #login-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100vh;
            background: linear-gradient(135deg, var(--laranja), var(--amarelo));
            display: flex; align-items: center; justify-content: center; z-index: 9999;
        }
        .login-box {
            background: white; padding: 40px; border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2); text-align: center; width: 90%; max-width: 400px;
        }
        .login-box input { width: 100%; margin: 15px 0; padding: 12px; border: 1px solid #ccc; border-radius: 5px; }
        .login-box button { width: 100%; padding: 12px; font-size: 1.1rem; }

        /* APP CONTENT */
        #app-content { display: none; } /* Escondido até login */

        .container { max-width: 1200px; margin: 0 auto; padding: 20px; }
        header {
            background: linear-gradient(to right, var(--laranja), var(--amarelo));
            color: white; padding: 20px 0; text-align: center;
            border-radius: 0 0 10px 10px; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        h1 { font-size: 2.5rem; margin-bottom: 10px; }
        
        nav { display: flex; justify-content: center; margin: 20px 0; flex-wrap: wrap; }
        .nav-btn {
            background-color: white; color: var(--laranja); border: 2px solid var(--laranja);
            padding: 10px 20px; margin: 5px; border-radius: 5px; cursor: pointer; font-weight: bold;
            transition: all 0.3s ease;
        }
        .nav-btn:hover, .nav-btn.active { background-color: var(--laranja); color: white; }
        .nav-btn.hidden { display: none; } /* Classe para ocultar via permissão */

        .section { display: none; background-color: white; padding: 20px; border-radius: 10px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); margin-bottom: 20px; }
        .section.active { display: block; }
        
        h2 { color: var(--laranja); margin-bottom: 15px; border-bottom: 2px solid var(--amarelo); padding-bottom: 5px; }
        h3 { margin-top: 20px; margin-bottom: 15px; color: var(--cinza-escuro); }
        
        form { display: grid; gap: 15px; }
        .form-group { display: flex; flex-direction: column; }
        label { margin-bottom: 5px; font-weight: bold; }
        input, select, textarea { padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-size: 1rem; }
        
        button {
            background-color: var(--laranja); color: white; border: none; padding: 10px 15px;
            border-radius: 5px; cursor: pointer; font-weight: bold; transition: background-color 0.3s;
        }
        button:hover { opacity: 0.9; }
        button:disabled { background-color: #ccc; cursor: not-allowed; }
        
        .btn-grande {
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            width: 200px; height: 120px; margin: 10px; font-size: 1.2rem;
            background-color: var(--laranja); border-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .btn-grande:hover { transform: translateY(-2px); box-shadow: 0 6px 8px rgba(0,0,0,0.15); }
        .btn-secundario { background-color: #6c757d; }
        .btn-voltar { background-color: transparent; color: var(--cinza-escuro); border: 1px solid #ddd; margin-bottom: 15px; display: inline-block; }
        .btn-voltar:hover { background-color: #eee; }
        
        table { width: 100%; border-collapse: collapse; margin-top: 15px; }
        th, td { padding: 12px 15px; text-align: left; border-bottom: 1px solid #ddd; }
        th { background-color: var(--amarelo); color: var(--cinza-escuro); }
        tr:hover { background-color: rgba(255, 182, 56, 0.1); }
        
        /* Status Badges */
        .status-badge { display: inline-block; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; font-weight: bold; }
        .status-recebido { background-color: #e0e0e0; }
        .status-producao { background-color: var(--amarelo); }
        .status-embalagem { background-color: var(--roxo); color: white; }
        .status-distribuicao { background-color: var(--laranja); color: white; }
        .status-entregue { background-color: var(--verde); color: white; }
        
        /* Alertas */
        .alert { padding: 10px; border-radius: 5px; margin: 10px 0; }
        .alert-warning { background-color: #fff3cd; border: 1px solid #ffecb5; color: #856404; }
        
        /* Sub-Abas Estoque */
        .tab-buttons { display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 1px solid #ddd; padding-bottom: 10px; }
        .tab-btn { background: none; color: #666; border: none; padding: 10px 20px; font-size: 1rem; border-radius: 5px 5px 0 0; }
        .tab-btn.active { background-color: var(--azul); color: white; }
        .estoque-tab { display: none; }
        .estoque-tab.active { display: block; }

        /* Filtros Histórico */
        .filtros-container {
            display: flex; gap: 10px; flex-wrap: wrap; background: #f9f9f9; padding: 15px; border-radius: 5px; margin-bottom: 15px; align-items: end;
        }

        @media (max-width: 768px) {
            .container { padding: 10px; }
            h1 { font-size: 2rem; }
            .btn-grande { width: 100%; height: 80px; flex-direction: row; gap: 10px; }
            th, td { padding: 8px 10px; font-size: 0.9rem; }
        }
    </style>
</head>
<body>
    <div id="login-screen">
        <div class="login-box">
            <h2 style="border:none; margin-bottom: 10px;">Acesso ao Sistema</h2>
            <p style="margin-bottom: 20px; color: #666;">Digite sua senha de acesso</p>
            <input type="password" id="login-pass" placeholder="Senha" onkeyup="if(event.key === 'Enter') realizarLogin()">
            <button onclick="realizarLogin()">Entrar</button>
            <p id="login-error" style="color: red; margin-top: 10px; display: none;">Senha incorreta!</p>
        </div>
    </div>

    <div id="app-content">
        <header>
            <div class="container">
                <h1>Aki Salgados</h1>
                <p>Sistema Online (Multi-usuário)</p>
                <div style="position: absolute; top: 10px; right: 10px;">
                    <span id="user-role-display" style="background: rgba(255,255,255,0.2); padding: 5px 10px; border-radius: 15px; font-size: 0.8rem;"></span>
                    <button onclick="location.reload()" style="padding: 5px 10px; font-size: 0.8rem; background: var(--vermelho);">Sair</button>
                </div>
            </div>
        </header>
        
        <div class="container">
            <nav id="main-nav">
                <button class="nav-btn active" data-section="home" id="nav-home">Início</button>
                <button class="nav-btn" data-section="pedidos" id="nav-pedidos">Pedidos</button>
                <button class="nav-btn" data-section="produtos" id="nav-produtos">Produtos</button>
                <button class="nav-btn" data-section="estoque" id="nav-estoque">Estoque</button>
                <button class="nav-btn hidden" data-section="historico" id="nav-historico" style="border-color: var(--roxo); color: var(--roxo);">📜 Histórico (Adm)</button>
            </nav>
            
            <section id="home" class="section active">
                <h2>Bem-vindo ao Sistema</h2>
                <p>Sistema conectado ao servidor. Todas as alterações são salvas automaticamente.</p>
                <div class="backup-area">
                    <h3>💾 Dados</h3>
                    <div style="display: flex; gap: 10px; flex-wrap: wrap; margin-top: 10px;">
                        <button onclick="baixarBackup()" style="background-color: var(--azul);">⬇️ Baixar Relatório (JSON)</button>
                    </div>
                </div>
            </section>
            
            <section id="historico" class="section">
                <h2>Histórico de Atividades</h2>
                <div class="filtros-container">
                    <div style="flex-grow: 1;">
                        <label style="font-size: 0.9rem;">Filtrar por Usuário:</label>
                        <select id="filtro-hist-user" onchange="atualizarTabelaHistorico()" style="width: 100%;">
                            <option value="todos">Todos</option>
                            <option value="adm">Administrador</option>
                            <option value="producao">Produção</option>
                            <option value="entrega">Entrega</option>
                            <option value="comercial">Comercial</option>
                        </select>
                    </div>
                    <div style="flex-grow: 1;">
                        <label style="font-size: 0.9rem;">Tipo de Ação:</label>
                        <select id="filtro-hist-tipo" onchange="atualizarTabelaHistorico()" style="width: 100%;">
                            <option value="todos">Todos</option>
                            <option value="pedido">Pedidos</option>
                            <option value="estoque">Estoque</option>
                            <option value="produto">Produtos/Receitas</option>
                            <option value="sistema">Sistema/Login</option>
                        </select>
                    </div>
                    <button onclick="atualizarTabelaHistorico()" style="height: 42px;">Atualizar</button>
                </div>
                <table id="tabela-historico">
                    <thead>
                        <tr>
                            <th>Data/Hora</th>
                            <th>Usuário</th>
                            <th>Ação</th>
                            <th>Detalhes</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </section>

            <section id="pedidos" class="section">
                <h2>Gestão de Pedidos</h2>
                <div id="pedidos-dashboard" style="display: block;">
                    <div style="display: flex; justify-content: center; flex-wrap: wrap; margin-top: 20px;">
                        <button class="btn-grande" id="btn-dash-novo">
                            <span style="font-size: 2rem;">📝</span> Registrar Novo
                        </button>
                        <button class="btn-grande" id="btn-dash-ver" style="background-color: var(--amarelo); color: var(--cinza-escuro);">
                            <span style="font-size: 2rem;">📋</span> Ver Lista/Status
                        </button>
                    </div>
                </div>
                
                <div id="novo-pedido-container" class="subsection" style="display: none;">
                    <button class="btn-voltar" onclick="mostrarDashboardPedidos()">← Voltar</button>
                    <h3>Registrar Novo Pedido</h3>
                    <form id="form-pedido">
                        <div class="form-group">
                            <label for="cliente">Nome do Cliente:</label>
                            <input type="text" id="cliente" required placeholder="Digite ou selecione um cliente" list="lista-clientes-sugestao" autocomplete="off">
                            <datalist id="lista-clientes-sugestao"></datalist>
                        </div>
                        <div class="form-group">
                            <label for="data-entrega">Data de Entrega:</label>
                            <input type="date" id="data-entrega" required>
                        </div>
                        <div class="form-group">
                            <label for="observacao">Observação:</label>
                            <textarea id="observacao" rows="2"></textarea>
                        </div>
                        
                        <div class="form-group" style="background: #f9f9f9; padding: 15px; border-radius: 5px; border: 1px solid #eee;">
                            <label style="color: var(--laranja); font-size: 1.1rem;">Seleção de Produtos:</label>
                            <p style="font-size: 0.85rem; color: #666; margin-bottom: 10px;">
                                Indique a <strong>Quantidade Total</strong> do pedido. Se quiser usar produtos já prontos do estoque, indique quanto em <strong>Usar do Estoque</strong>.
                            </p>
                            <div id="produtos-pedido"></div>
                        </div>
                        
                        <button type="submit" style="margin-top: 10px;">Confirmar Pedido</button>
                    </form>
                </div>
                
                <div id="ver-pedidos-container" class="subsection" style="display: none;">
                    <button class="btn-voltar" onclick="mostrarDashboardPedidos()">← Voltar</button>
                    
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px;">
                        <h3>Histórico de Pedidos</h3>
                        <div style="display: flex; gap: 10px; align-items: center; flex-wrap: wrap;">
                            <div style="display:flex; flex-direction: column;">
                                <label style="font-size: 0.8rem;">Cliente:</label>
                                <select id="filtro-cliente" onchange="atualizarTabelaPedidos()" style="padding: 5px; width: 150px;">
                                    <option value="todos" selected>Todos</option>
                                </select>
                            </div>
                            <div style="display:flex; flex-direction: column;">
                                <label style="font-size: 0.8rem;">Status:</label>
                                <select id="filtro-status" onchange="atualizarTabelaPedidos()" style="padding: 5px;">
                                    <option value="ativos" selected>Ativos</option>
                                    <option value="todos">Todos</option>
                                    <option value="recebido">Recebido</option>
                                    <option value="em produção">Em Produção</option>
                                    <option value="embalagem">Embalagem</option>
                                    <option value="em distribuição">Em Distribuição</option>
                                    <option value="entregue">Entregue</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <table id="tabela-pedidos">
                        <thead>
                            <tr>
                                <th>ID/Cliente</th>
                                <th>Data</th>
                                <th>Status</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                    <p id="msg-sem-pedidos" style="text-align: center; margin-top: 20px; color: #666; display: none;">Nenhum pedido encontrado.</p>
                </div>
            </section>
            
            <section id="produtos" class="section">
                <h2>Catálogo de Produtos</h2>
                <div id="area-cadastro-produto">
                    <p>Cadastrar Receita (Base 10kg):</p>
                    <form id="form-produto" style="margin-bottom: 20px; background: #fff; padding: 15px; border: 1px solid #eee; border-radius: 5px;">
                        <div class="form-group">
                            <label>Nome do Produto:</label>
                            <input type="text" id="nome-produto" required placeholder="Ex: Coxinha">
                        </div>
                        <div class="form-group">
                            <label>Ingredientes (p/ 10kg):</label>
                            <div id="ingredientes-produto"></div>
                            <button type="button" id="adicionar-ingrediente" class="btn-secundario" style="margin-top: 10px; width: auto;">+ Ingrediente</button>
                        </div>
                        <button type="submit">Salvar Receita</button>
                    </form>
                </div>
            
                <h3>Produtos Cadastrados</h3>
                <table id="tabela-produtos">
                    <thead><tr><th>Nome</th><th>Receita (10kg)</th><th>Ações</th></tr></thead>
                    <tbody></tbody>
                </table>
            </section>
            
            <section id="estoque" class="section">
                <h2>Controle de Estoque</h2>
                
                <div class="tab-buttons">
                    <button class="tab-btn active" onclick="mudarAbaEstoque('mp')">Matéria-Prima</button>
                    <button class="tab-btn" onclick="mudarAbaEstoque('prontos')">Produtos Prontos</button>
                </div>

                <div id="estoque-mp" class="estoque-tab active">
                    <div id="area-cadastro-mp">
                        <form id="form-estoque" style="margin-bottom: 20px; background: #fff; padding: 15px; border: 1px solid #eee;">
                            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                                <input type="text" id="nome-material" required placeholder="Material (Ex: Farinha)">
                                <select id="unidade-material" required>
                                    <option value="kg">kg</option>
                                    <option value="L">Litros</option>
                                    <option value="un">Unidade</option>
                                </select>
                                <input type="number" id="quantidade-material" step="0.01" min="0" required placeholder="Qtd Atual">
                                <input type="number" id="quantidade-minima" step="0.01" min="0" required placeholder="Mínimo">
                            </div>
                            <button type="submit">Adicionar MP</button>
                        </form>
                    </div>
                    <div id="alertas-estoque"></div>
                    <table id="tabela-estoque-mp">
                        <thead><tr><th>Material</th><th>Qtd</th><th>Mín</th><th>Ações</th></tr></thead>
                        <tbody></tbody>
                    </table>
                </div>

                <div id="estoque-prontos" class="estoque-tab">
                    <p class="alert alert-warning" style="display:inline-block">
                        💡 Este estoque representa produtos já produzidos esperando venda/entrega.
                    </p>
                    <table id="tabela-estoque-prontos">
                        <thead><tr><th>Produto</th><th>Qtd Pronta (kg)</th><th>Ações</th></tr></thead>
                        <tbody></tbody>
                    </table>
                </div>
            </section>
        </div>
    </div>

    <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-firestore-compat.js"></script>

    <script>
        // --- CONFIGURAÇÃO DO FIREBASE ---
        // COLE SUAS CHAVES DO FIREBASE AQUI
        const firebaseConfig = {
            apiKey: "AIzaSyBx4fjnzedfFHhdjpxjGwuNba-Fe-HDeJs",
            authDomain: "aki-salgados-b825a.firebaseapp.com",
            projectId: "aki-salgados-b825a",
            storageBucket: "aki-salgados-b825a.firebasestorage.app",
            messagingSenderId: "168592966050",
            appId: "1:168592966050: web:61c034be14a933a4ddb2fb"
        };

        // Inicializa o Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        // --- VARIÁVEIS GLOBAIS (Preenchidas pelo Firebase) ---
        let produtos = [];
        let estoqueMP = [];
        let estoqueProntos = [];
        let pedidos = [];
        let historicoAcoes = [];
        // Clientes: Vamos derivar dos pedidos existentes para simplificar
        let clientes = [];
        
        let currentUserRole = ''; 

        const statusFlow = ['recebido', 'em produção', 'embalagem', 'em distribuição', 'entregue'];

        // --- SISTEMA DE SINCRONIZAÇÃO (LISTENERS) ---
        function iniciarSincronizacao() {
            // 1. Produtos
            db.collection("produtos").onSnapshot((querySnapshot) => {
                produtos = [];
                querySnapshot.forEach((doc) => {
                    produtos.push({ id: doc.id, ...doc.data() });
                });
                atualizarTabelaProdutos();
                renderizarFormularioProdutos();
                atualizarTabelaEstoqueProntos(); // Nomes podem mudar
            });

            // 2. Estoque MP
            db.collection("estoqueMP").onSnapshot((querySnapshot) => {
                estoqueMP = [];
                querySnapshot.forEach((doc) => {
                    estoqueMP.push({ id: doc.id, ...doc.data() });
                });
                atualizarTabelaEstoqueMP();
                carregarMateriasPrimasNosSelects();
            });

            // 3. Estoque Prontos
            db.collection("estoqueProntos").onSnapshot((querySnapshot) => {
                estoqueProntos = [];
                querySnapshot.forEach((doc) => {
                    estoqueProntos.push({ id: doc.id, ...doc.data() });
                });
                atualizarTabelaEstoqueProntos();
            });

            // 4. Pedidos (e Clientes)
            db.collection("pedidos").onSnapshot((querySnapshot) => {
                pedidos = [];
                clientes = [];
                querySnapshot.forEach((doc) => {
                    const p = { id: doc.id, ...doc.data() };
                    pedidos.push(p);
                    if(p.cliente && !clientes.includes(p.cliente)) clientes.push(p.cliente);
                });
                atualizarTabelaPedidos();
                atualizarUIClientes();
            });

            // 5. Histórico (Ordenado)
            db.collection("historico").orderBy("data", "desc").limit(100).onSnapshot((querySnapshot) => {
                historicoAcoes = [];
                querySnapshot.forEach((doc) => {
                    historicoAcoes.push({ id: doc.id, ...doc.data() });
                });
                if(document.getElementById('historico').classList.contains('active')) {
                    atualizarTabelaHistorico();
                }
            });
        }

        // --- FUNÇÃO DE LOG (ENVIAR PARA FIREBASE) ---
        function registrarLog(acao, detalhe, tipo) {
            db.collection("historico").add({
                data: new Date().toISOString(),
                usuario: currentUserRole || 'Desconhecido',
                acao: acao,
                detalhe: detalhe,
                tipo: tipo 
            }).catch(e => console.error("Erro ao logar", e));
        }

        // --- SISTEMA DE LOGIN ---
        function realizarLogin() {
            const pass = document.getElementById('login-pass').value;
            const errorMsg = document.getElementById('login-error');
            const loginScreen = document.getElementById('login-screen');
            const appContent = document.getElementById('app-content');
            const roleDisplay = document.getElementById('user-role-display');

            let role = '';
            let roleName = '';

            if (pass === '@adm123') { role = 'adm'; roleName = 'Administrador'; }
            else if (pass === '@entrega123') { role = 'entrega'; roleName = 'Entregador'; }
            else if (pass === '@comercial123') { role = 'comercial'; roleName = 'Vendas/Comercial'; }
            else if (pass === '@producao123') { role = 'producao'; roleName = 'Produção'; }
            else {
                errorMsg.style.display = 'block';
                return;
            }

            currentUserRole = role;
            roleDisplay.textContent = roleName;
            loginScreen.style.display = 'none';
            appContent.style.display = 'block';
            
            registrarLog('Login', `Usuário ${role} entrou no sistema`, 'sistema');
            aplicarPermissoes(role);
            
            // INICIA A CONEXÃO COM O SERVIDOR
            iniciarSincronizacao();
        }

        function aplicarPermissoes(role) {
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('hidden'));
            document.getElementById('area-cadastro-produto').style.display = 'block';
            document.getElementById('area-cadastro-mp').style.display = 'block';
            
            if (role !== 'adm') {
                document.getElementById('nav-historico').classList.add('hidden');
            }

            if (role === 'entrega') {
                document.getElementById('nav-home').classList.add('hidden');
                document.getElementById('nav-produtos').classList.add('hidden');
                document.getElementById('nav-estoque').classList.add('hidden');
                document.querySelector('[data-section="pedidos"]').click();
                document.getElementById('btn-dash-novo').style.display = 'none';
                mostrarVerPedidos();
                document.getElementById('filtro-status').value = 'em distribuição';
            }
            else if (role === 'producao') {
                document.getElementById('nav-home').classList.add('hidden');
                document.getElementById('nav-produtos').classList.add('hidden');
                document.getElementById('nav-estoque').classList.add('hidden');
                document.querySelector('[data-section="pedidos"]').click();
                document.getElementById('btn-dash-novo').style.display = 'none';
                mostrarVerPedidos();
            }
            else if (role === 'comercial') {
                document.getElementById('nav-produtos').classList.add('hidden');
                document.querySelector('button[onclick="mudarAbaEstoque(\'mp\')"]').style.display = 'none';
                document.querySelector('button[onclick="mudarAbaEstoque(\'prontos\')"]').click();
            }
        }

        // --- INICIALIZAÇÃO DA INTERFACE ---
        document.addEventListener('DOMContentLoaded', () => {
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const target = this.getAttribute('data-section');
                    document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
                    document.getElementById(target).classList.add('active');
                    
                    if(target === 'pedidos') mostrarDashboardPedidos();
                    if(target === 'historico') atualizarTabelaHistorico();
                });
            });

            document.getElementById('btn-dash-novo').addEventListener('click', mostrarNovoPedido);
            document.getElementById('btn-dash-ver').addEventListener('click', mostrarVerPedidos);
            document.getElementById('form-produto').addEventListener('submit', salvarProduto);
            document.getElementById('form-estoque').addEventListener('submit', salvarMP);
            document.getElementById('form-pedido').addEventListener('submit', salvarPedido);
            document.getElementById('adicionar-ingrediente').addEventListener('click', adicionarIngredienteUI);
            
            document.addEventListener('click', (e) => {
                if (e.target.classList.contains('remover-ingrediente')) e.target.parentElement.remove();
            });
        });

        // --- FUNÇÕES DE INTERFACE AUXILIARES ---
        function atualizarUIClientes() {
            const datalist = document.getElementById('lista-clientes-sugestao');
            datalist.innerHTML = '';
            clientes.sort().forEach(c => {
                const opt = document.createElement('option');
                opt.value = c;
                datalist.appendChild(opt);
            });

            const selectFiltro = document.getElementById('filtro-cliente');
            const valorAtual = selectFiltro.value;
            while (selectFiltro.options.length > 1) { selectFiltro.remove(1); }

            clientes.sort().forEach(c => {
                const opt = document.createElement('option');
                opt.value = c;
                opt.textContent = c;
                selectFiltro.appendChild(opt);
            });
            if(valorAtual && valorAtual !== 'todos') { selectFiltro.value = valorAtual; }
        }

        // --- ABA HISTÓRICO ---
        function atualizarTabelaHistorico() {
            const tbody = document.querySelector('#tabela-historico tbody');
            tbody.innerHTML = '';
            
            const filtroUser = document.getElementById('filtro-hist-user').value;
            const filtroTipo = document.getElementById('filtro-hist-tipo').value;

            const logsFiltrados = historicoAcoes.filter(log => {
                let userOk = (filtroUser === 'todos') ? true : log.usuario === filtroUser;
                let tipoOk = (filtroTipo === 'todos') ? true : log.tipo === filtroTipo;
                return userOk && tipoOk;
            });

            if (logsFiltrados.length === 0) {
                tbody.innerHTML = '<tr><td colspan="4" style="text-align:center; padding:20px;">Nenhum registro encontrado.</td></tr>';
                return;
            }

            logsFiltrados.forEach(log => {
                const dataFormatada = new Date(log.data).toLocaleString('pt-BR');
                let corTipo = '#666';
                if(log.tipo === 'pedido') corTipo = 'var(--azul)';
                if(log.tipo === 'estoque') corTipo = 'var(--amarelo)';
                if(log.tipo === 'produto') corTipo = 'var(--roxo)';
                if(log.tipo === 'sistema') corTipo = '#333';

                tbody.innerHTML += `
                    <tr>
                        <td style="font-size:0.9rem">${dataFormatada}</td>
                        <td><strong>${log.usuario}</strong></td>
                        <td>
                            <span style="background:${corTipo}; color:white; padding:2px 6px; border-radius:4px; font-size:0.7rem; margin-right:5px;">${log.tipo.toUpperCase()}</span>
                            ${log.acao}
                        </td>
                        <td style="font-size:0.9rem; color:#555;">${log.detalhe}</td>
                    </tr>
                `;
            });
        }

        // --- ABA ESTOQUE ---
        function mudarAbaEstoque(aba) {
            document.querySelectorAll('.estoque-tab').forEach(d => d.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            if(aba === 'mp') {
                document.getElementById('estoque-mp').classList.add('active');
                document.querySelector('button[onclick="mudarAbaEstoque(\'mp\')"]').classList.add('active');
            } else {
                document.getElementById('estoque-prontos').classList.add('active');
                document.querySelector('button[onclick="mudarAbaEstoque(\'prontos\')"]').classList.add('active');
            }
        }

        function salvarMP(e) {
            e.preventDefault();
            const nome = document.getElementById('nome-material').value;
            const qtd = parseFloat(document.getElementById('quantidade-material').value);
            
            db.collection("estoqueMP").add({
                nome: nome,
                unidade: document.getElementById('unidade-material').value,
                quantidade: qtd,
                quantidadeMinima: parseFloat(document.getElementById('quantidade-minima').value)
            }).then(() => {
                registrarLog('Adicionar MP', `Adicionou ${qtd} de ${nome}`, 'estoque');
                document.getElementById('form-estoque').reset();
                alert('Material salvo!');
            });
        }

        function atualizarTabelaEstoqueMP() {
            const tbody = document.querySelector('#tabela-estoque-mp tbody');
            const alertasDiv = document.getElementById('alertas-estoque');
            tbody.innerHTML = ''; alertasDiv.innerHTML = '';
            estoqueMP.forEach(mp => {
                if (mp.quantidade <= mp.quantidadeMinima) {
                    alertasDiv.innerHTML += `<div class="alert alert-warning">⚠️ ${mp.nome} baixo (${mp.quantidade}${mp.unidade})</div>`;
                }
                const acoes = (currentUserRole === 'adm') 
                    ? `<button onclick="editarQtdMP('${mp.id}')" style="font-size:0.8rem">Editar</button>
                       <button onclick="excluirMP('${mp.id}')" style="font-size:0.8rem; background:var(--vermelho); margin-left:5px">X</button>`
                    : `<span style="color:#999; font-size:0.8rem">Acesso Restrito</span>`;

                tbody.innerHTML += `
                    <tr>
                        <td>${mp.nome}</td>
                        <td style="${mp.quantidade <= mp.quantidadeMinima ? 'color:red;font-weight:bold' : ''}">${mp.quantidade} ${mp.unidade}</td>
                        <td>${mp.quantidadeMinima}</td>
                        <td>${acoes}</td>
                    </tr>
                `;
            });
        }

        function editarQtdMP(id) {
            const mp = estoqueMP.find(m => m.id === id);
            const nova = prompt(`Nova quantidade para ${mp.nome}:`, mp.quantidade);
            if (nova && !isNaN(nova)) {
                db.collection("estoqueMP").doc(id).update({
                    quantidade: parseFloat(nova)
                }).then(() => {
                    registrarLog('Editar MP', `Alterou ${mp.nome} para ${nova}`, 'estoque');
                });
            }
        }

        function excluirMP(id) {
            if(!confirm('Excluir?')) return;
            const mp = estoqueMP.find(m => m.id === id);
            // Verifica se está sendo usado em alguma receita
            const emUso = produtos.some(p => p.ingredientes.some(i => i.materiaPrimaId == id));
            if(emUso) { alert('Material usado em uma receita. Não pode excluir.'); return; }
            
            db.collection("estoqueMP").doc(id).delete().then(() => {
                registrarLog('Excluir MP', `Removeu ${mp.nome} do estoque`, 'estoque');
            });
        }

        function atualizarTabelaEstoqueProntos() {
            const tbody = document.querySelector('#tabela-estoque-prontos tbody');
            tbody.innerHTML = '';
            
            produtos.forEach(prod => {
                // Procura o item no array sincronizado
                let itemEstoque = estoqueProntos.find(e => e.produtoId === prod.id);
                // Se não existir, não cria no banco ainda, só mostra 0
                let qtd = itemEstoque ? itemEstoque.quantidade : 0;
                let idDoc = itemEstoque ? itemEstoque.id : null;

                const podeEditar = (currentUserRole === 'adm' || currentUserRole === 'comercial');
                
                // Botão chama função passando o ID do Produto e o ID do Documento de Estoque (se houver)
                tbody.innerHTML += `
                    <tr>
                        <td>${prod.nome}</td>
                        <td style="font-size: 1.1rem; font-weight: bold; color: var(--azul);">${qtd} kg</td>
                        <td>
                            ${podeEditar ? `<button onclick="ajustarEstoquePronto('${prod.id}', '${idDoc || ''}')" style="padding:5px 10px; font-size:0.8rem">Ajustar Manual</button>` : '-'}
                        </td>
                    </tr>
                `;
            });
        }

        function ajustarEstoquePronto(prodId, docId) {
            const nomeProd = produtos.find(p=>p.id === prodId).nome;
            const item = estoqueProntos.find(e => e.produtoId === prodId);
            const atual = item ? item.quantidade : 0;

            const nova = prompt(`Definir quantidade EXATA de ${nomeProd} no estoque (kg):`, atual);
            if (nova !== null && !isNaN(nova)) {
                const novaQtd = parseFloat(nova);
                
                if (docId && docId !== '') {
                    // Atualiza existente
                    db.collection("estoqueProntos").doc(docId).update({ quantidade: novaQtd });
                } else {
                    // Cria novo registro de estoque para este produto
                    db.collection("estoqueProntos").add({
                        produtoId: prodId,
                        quantidade: novaQtd
                    });
                }
                registrarLog('Ajuste Prontos', `Alterou ${nomeProd} para ${novaQtd}kg`, 'estoque');
            }
        }

        // --- PRODUTOS & RECEITAS ---
        function carregarMateriasPrimasNosSelects() {
            const selects = document.querySelectorAll('.materia-prima-select');
            selects.forEach(sel => {
                const val = sel.value;
                sel.innerHTML = '<option value="">Selecione...</option>';
                estoqueMP.forEach(mp => {
                    sel.innerHTML += `<option value="${mp.id}">${mp.nome} (${mp.unidade})</option>`;
                });
                if(val) sel.value = val;
            });
        }

        function adicionarIngredienteUI() {
            const div = document.createElement('div');
            div.className = 'ingrediente-item';
            div.style.marginBottom = '10px';
            div.innerHTML = `
                <select class="materia-prima-select" style="width: 180px; padding: 5px;"></select>
                <input type="number" class="qtd-ing" placeholder="Qtd" step="0.01" style="width: 80px; padding: 5px;">
                <button type="button" class="remover-ingrediente" style="background:var(--vermelho); padding: 5px 8px;">X</button>
            `;
            document.getElementById('ingredientes-produto').appendChild(div);
            carregarMateriasPrimasNosSelects();
        }

        function salvarProduto(e) {
            e.preventDefault();
            const nome = document.getElementById('nome-produto').value;
            const ings = [];
            
            document.querySelectorAll('.ingrediente-item').forEach(div => {
                const mpId = div.querySelector('select').value;
                const qtd = div.querySelector('input').value;
                if(mpId && qtd) {
                    const mp = estoqueMP.find(m => m.id == mpId);
                    ings.push({ materiaPrimaId: mpId, nome: mp.nome, quantidade: parseFloat(qtd), unidade: mp.unidade });
                }
            });
            if(ings.length === 0) { alert('Adicione ingredientes.'); return; }
            
            db.collection("produtos").add({
                nome: nome,
                ingredientes: ings
            }).then(() => {
                registrarLog('Novo Produto', `Cadastrou receita: ${nome}`, 'produto');
                document.getElementById('form-produto').reset();
                document.getElementById('ingredientes-produto').innerHTML = '';
                adicionarIngredienteUI();
                alert('Produto salvo!');
            });
        }

        function atualizarTabelaProdutos() {
            const tbody = document.querySelector('#tabela-produtos tbody');
            tbody.innerHTML = '';
            produtos.forEach(p => {
                const receita = p.ingredientes.map(i => `${i.nome}: ${i.quantidade}${i.unidade}`).join(', ');
                const acao = currentUserRole === 'adm' 
                    ? `<button onclick="excluirProduto('${p.id}')" style="background:var(--vermelho); padding:5px; font-size:0.8rem">Excluir</button>` 
                    : '-';
                tbody.innerHTML += `<tr><td>${p.nome}</td><td>${receita}</td><td>${acao}</td></tr>`;
            });
        }
        
        function excluirProduto(id) {
            if(currentUserRole !== 'adm') return;
            if(confirm('Excluir este produto?')) {
                db.collection("produtos").doc(id).delete().then(()=> {
                     // Tenta apagar estoque pronto associado
                     const est = estoqueProntos.find(e => e.produtoId === id);
                     if(est) db.collection("estoqueProntos").doc(est.id).delete();
                     
                     registrarLog('Excluir Produto', `Removeu receita`, 'produto');
                });
            }
        }

        // --- PEDIDOS ---
        function mostrarDashboardPedidos() {
            document.getElementById('pedidos-dashboard').style.display = 'block';
            document.getElementById('novo-pedido-container').style.display = 'none';
            document.getElementById('ver-pedidos-container').style.display = 'none';
            atualizarUIClientes();
        }
        function mostrarNovoPedido() {
            document.getElementById('pedidos-dashboard').style.display = 'none';
            document.getElementById('novo-pedido-container').style.display = 'block';
            renderizarFormularioProdutos();
        }
        function mostrarVerPedidos() {
            document.getElementById('pedidos-dashboard').style.display = 'none';
            document.getElementById('ver-pedidos-container').style.display = 'block';
            atualizarTabelaPedidos();
        }

        function renderizarFormularioProdutos() {
            const container = document.getElementById('produtos-pedido');
            container.innerHTML = '';
            if(produtos.length === 0) { container.innerHTML = 'Nenhum produto cadastrado.'; return; }

            produtos.forEach(p => {
                const emEstoque = estoqueProntos.find(e => e.produtoId === p.id)?.quantidade || 0;
                
                const div = document.createElement('div');
                div.style.borderBottom = "1px solid #ddd";
                div.style.padding = "10px 0";
                div.innerHTML = `
                    <div style="font-weight:bold; margin-bottom:5px;">${p.nome}</div>
                    <div style="display:flex; gap:15px; align-items:center; flex-wrap:wrap;">
                        <div>
                            <label style="font-size:0.8rem">Qtd Total (kg):</label><br>
                            <input type="number" class="qtd-total" data-id="${p.id}" min="0" step="0.1" style="width:100px;">
                        </div>
                        <div style="background:#e9ecef; padding:5px; border-radius:5px;">
                            <label style="font-size:0.8rem; color:#666;">Disponível Pronto:</label> 
                            <strong>${emEstoque} kg</strong><br>
                            <label style="font-size:0.8rem">Usar do Estoque:</label>
                            <input type="number" class="qtd-estoque-uso" data-id="${p.id}" min="0" max="${emEstoque}" step="0.1" style="width:100px;" placeholder="0">
                        </div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        async function salvarPedido(e) {
            e.preventDefault();
            const cliente = document.getElementById('cliente').value.trim();
            const dataEntrega = document.getElementById('data-entrega').value;
            const obs = document.getElementById('observacao').value;

            const itensPedido = [];
            let inputsTotal = document.querySelectorAll('.qtd-total');
            let temErro = false;
            let msgErro = '';

            inputsTotal.forEach(input => {
                const total = parseFloat(input.value) || 0;
                if(total > 0) {
                    const prodId = input.getAttribute('data-id');
                    const inputEstoque = document.querySelector(`.qtd-estoque-uso[data-id="${prodId}"]`);
                    const usarEstoque = parseFloat(inputEstoque.value) || 0;
                    
                    const disponivel = estoqueProntos.find(ep => ep.produtoId === prodId)?.quantidade || 0;
                    
                    if (usarEstoque > disponivel) {
                        temErro = true;
                        msgErro += `- ${produtos.find(p=>p.id===prodId).nome}: Estoque insuficiente.\n`;
                    }
                    if (usarEstoque > total) {
                        temErro = true;
                        msgErro += `- Erro na quantidade de estoque > total.\n`;
                    }

                    itensPedido.push({
                        produtoId: prodId,
                        quantidadeTotal: total,
                        usadoEstoque: usarEstoque,
                        aProduzir: total - usarEstoque
                    });
                }
            });

            if (itensPedido.length === 0) { alert('Selecione algum produto.'); return; }
            if (temErro) { alert('Erro:\n' + msgErro); return; }

            // Verificação de MP
            const faltaMP = verificarMPNecessaria(itensPedido);
            if (faltaMP.length > 0) {
                alert('Matéria-Prima Insuficiente:\n' + faltaMP.join('\n'));
                return;
            }

            // --- OPERAÇÃO DE BANCO DE DADOS (Executa Baixas) ---
            try {
                // 1. Baixa Estoque Prontos
                itensPedido.forEach(item => {
                    if (item.usadoEstoque > 0) {
                        const ep = estoqueProntos.find(e => e.produtoId === item.produtoId);
                        if(ep) {
                            db.collection("estoqueProntos").doc(ep.id).update({
                                quantidade: ep.quantidade - item.usadoEstoque
                            });
                        }
                    }
                });

                // 2. Baixa Matéria Prima (Produção)
                itensPedido.forEach(item => {
                    if (item.aProduzir > 0) {
                        const prod = produtos.find(p => p.id === item.produtoId);
                        prod.ingredientes.forEach(ing => {
                            const mp = estoqueMP.find(m => m.id == ing.materiaPrimaId);
                            if(mp) {
                                db.collection("estoqueMP").doc(mp.id).update({
                                    quantidade: mp.quantidade - ((item.aProduzir / 10) * ing.quantidade)
                                });
                            }
                        });
                    }
                });

                // 3. Salva o Pedido
                await db.collection("pedidos").add({
                    cliente: cliente,
                    dataEntrega: dataEntrega,
                    observacao: obs,
                    itens: itensPedido,
                    status: 'recebido',
                    criadoEm: new Date().toISOString()
                });

                registrarLog('Novo Pedido', `Cliente: ${cliente}`, 'pedido');
                document.getElementById('form-pedido').reset();
                alert('Pedido Registrado!');
                mostrarVerPedidos();

            } catch (error) {
                console.error("Erro ao salvar pedido:", error);
                alert("Erro ao salvar pedido. Verifique conexão.");
            }
        }

        function verificarMPNecessaria(itens) {
            const erros = [];
            // Simula o estoque atual
            const tempEstoque = JSON.parse(JSON.stringify(estoqueMP));
            itens.forEach(item => {
                if (item.aProduzir > 0) {
                    const prod = produtos.find(p => p.id === item.produtoId);
                    prod.ingredientes.forEach(ing => {
                        const mp = tempEstoque.find(m => m.id == ing.materiaPrimaId);
                        if(mp) {
                            const qtdNecessaria = (item.aProduzir / 10) * ing.quantidade;
                            mp.quantidade -= qtdNecessaria;
                        }
                    });
                }
            });
            tempEstoque.forEach(mp => {
                if (mp.quantidade < 0) {
                    erros.push(`${mp.nome}: Faltam ${Math.abs(mp.quantidade).toFixed(2)} ${mp.unidade}`);
                }
            });
            return erros;
        }

        function atualizarTabelaPedidos() {
            const tbody = document.querySelector('#tabela-pedidos tbody');
            const filtroStatus = document.getElementById('filtro-status').value;
            const filtroCliente = document.getElementById('filtro-cliente').value;
            tbody.innerHTML = '';
            
            // Ordenação (Local, já que o listener traz tudo)
            const pedidosFiltrados = pedidos.sort((a,b) => (a.criadoEm < b.criadoEm) ? 1 : -1).filter(p => {
                let statusOk = false;
                if (filtroStatus === 'ativos') statusOk = p.status !== 'entregue';
                else if (filtroStatus === 'todos') statusOk = true;
                else statusOk = p.status === filtroStatus;

                let clienteOk = true;
                if (filtroCliente !== 'todos') {
                    clienteOk = (p.cliente === filtroCliente);
                }
                return statusOk && clienteOk;
            });

            if(pedidosFiltrados.length === 0) {
                document.getElementById('msg-sem-pedidos').style.display = 'block';
                return;
            }
            document.getElementById('msg-sem-pedidos').style.display = 'none';
            pedidosFiltrados.forEach(p => {
                const idVisivel = p.id.slice(0,4); // Mostra só o começo do ID do Firebase
                let botoes = `<button onclick="verDetalhes('${p.id}')" style="padding:5px; font-size:0.8rem; margin-right:5px;">Info</button>`;
                
                if (currentUserRole === 'adm' || currentUserRole === 'producao' || (currentUserRole === 'entrega' && p.status === 'em distribuição')) {
                    const idx = statusFlow.indexOf(p.status);
                    
                    if (idx > 0 && currentUserRole !== 'entrega') {
                        botoes += `<button onclick="mudarStatus('${p.id}', -1)" style="padding:5px; font-size:0.8rem; background:#6c757d; margin-right:2px;">↩️</button>`;
                    }
                    if (idx < statusFlow.length - 1) {
                         if (currentUserRole === 'entrega' && p.status !== 'em distribuição') {
                         } else {
                             const proxStatus = statusFlow[idx+1];
                             let btnText = "Avançar";
                             if(proxStatus === 'entregue') btnText = "✅ Entregue";
                             if(proxStatus === 'embalagem') btnText = "📦 Embalar";
                             if(proxStatus === 'em distribuição') btnText = "🚚 Enviar";
                             
                             botoes += `<button onclick="mudarStatus('${p.id}', 1)" style="padding:5px; font-size:0.8rem; background:var(--azul);">${btnText}</button>`;
                        }
                    }
                }

                tbody.innerHTML += `
                    <tr>
                        <td>
                            <strong>${p.cliente}</strong><br>
                            <span style="font-size:0.8rem; color:#666">#${idVisivel}</span>
                        </td>
                        <td>${new Date(p.dataEntrega).toLocaleDateString('pt-BR')}</td>
                        <td><span class="status-badge status-${p.status.replace(' ', '-').replace('ç','c').replace('ã','a')}">${p.status}</span></td>
                        <td>${botoes}</td>
                    </tr>
                `;
            });
        }

        function verDetalhes(id) {
            const p = pedidos.find(x => x.id === id);
            const lista = p.itens.map(i => {
                const nome = produtos.find(prod => prod.id === i.produtoId)?.nome || "Produto removido";
                return `${nome}: ${i.quantidadeTotal}kg (Estoque: ${i.usadoEstoque}kg | Produzir: ${i.aProduzir.toFixed(2)}kg)`;
            }).join('\n');
            alert(`CLIENTE: ${p.cliente}\nOBS: ${p.observacao}\nSTATUS: ${p.status}\n\nITENS:\n${lista}`);
        }

        function mudarStatus(id, direcao) {
            const p = pedidos.find(x => x.id === id);
            const atualIdx = statusFlow.indexOf(p.status);
            const novoIdx = atualIdx + direcao;
            if (novoIdx >= 0 && novoIdx < statusFlow.length) {
                const novoStatus = statusFlow[novoIdx];
                if (confirm(`Alterar status de "${p.status}" para "${novoStatus}"?`)) {
                    db.collection("pedidos").doc(id).update({ status: novoStatus });
                    registrarLog('Mudar Status', `Pedido ${p.cliente}: ${novoStatus}`, 'pedido');
                }
            }
        }

        // --- BACKUP (AGORA GERA JSON DOS DADOS NA TELA) ---
        function baixarBackup() {
            const data = { 
                dataBackup: new Date(), 
                produtos, 
                estoqueMP, 
                estoqueProntos, 
                pedidos, 
                historico: historicoAcoes 
            };
            const a = document.createElement('a');
            a.href = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(data));
            a.download = "backup_aki_salgados_firebase.json";
            a.click();
        }
    </script>
</body>
</html>
FireAtt.txt
Displaying FireAtt.txt.
