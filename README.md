
<!DOCTYPE html>
<html lang="pt-BR">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Site com Layout Ajustável</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <script src="https://unpkg.com/@dotlottie/player-component@2.7.12/dist/dotlottie-player.mjs" type="module"></script>
  <style>
    /* Estilos gerais */
    *,
    *:before,
    *:after {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 0;
      background-color: #f8f3f3;
      font-family: Arial, sans-serif;
    }

    /* Layout principal */
    .main-container {
      display: flex;
      height: 95vh;
    }

    .content {
      flex: 100%;
      display: flex;
      flex-direction: column;
      gap: 1px;
      padding: 1px;
    }

    .container {
      padding: 30px;
      background-color: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      border: 1px solid rgba(128, 128, 128, 0.3);
      position: relative;
    }

    .flex-container {
      display: flex;
      gap: 10px;
      flex: 1;
    }

    .left-column {
      flex: 15%;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .right-column {
      flex: 85%;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .container2 {
      flex: 0.5;
    }

    .container3 {
      flex: 2.5;
    }

    .container4 {
      flex: 1;
    }

    .container5 {
      height: 150px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 10px;
    }

    .container6 {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: center;
    }

    /* Sidebar global */
    nav {
      position: fixed;
      top: 70%;
      left: 0;
      transform: translateY(-50%);
      background: transparent;
      width: 70px;
      height: 70%;
      z-index: 100;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    nav ul {
      text-align: center;
      list-style: none;
      padding: 0;
      margin: 0;
      font-size: 12px;
    }

    nav ul li {
      position: relative;
      width: 70px;
      height: 70px;
      cursor: pointer;
      background: crimson;
      text-transform: uppercase;
      transition: all 0.4s ease-out;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    nav ul li:after {
      position: absolute;
      background: white;
      color: crimson;
      top: 0;
      left: 70px;
      width: 70px;
      height: 100%;
      opacity: .5;
      transform: perspective(400px) rotateY(90deg);
      transform-origin: 0 100%;
      transition: all 0.4s ease-out;
    }

    nav ul li:nth-child(1):after {
      content: "Status";
      line-height: 88px;
    }

    nav ul li:nth-child(2):after {
      content: "Agenda";
      line-height: 88px;
    }

    nav ul li:nth-child(3):after {
      content: "Registro";
      line-height: 85px;
    }

    nav ul li:nth-child(4):after {
      content: "Ação";
      line-height: 70px;
    }

    nav ul li:hover {
      transform: translateX(-70px);
    }

    nav ul li:hover:after {
      opacity: 1;
      transform: perspective(400px) rotateY(0deg) scale(1);
    }

    .fa-home,
    .fa-calendar,
    .fa-clipboard-list,
    .fa-bullhorn {
      font-size: 32px;
      color: white;
    }

    nav ul li:hover .fa-home,
    nav ul li:hover .fa-calendar,
    nav ul li:hover .fa-clipboard-list,
    nav ul li:hover .fa-bullhorn {
      color: crimson;
      text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
    }

    /* Seções */
    section {
      margin-left: 70px;
      padding: 20px;
      display: none;
      height: 100vh;
    }

    section.active {
      display: block;
    }

    nav ul li.active {
      background-color: #444;
    }

    /* Estilos do Título */
    .container5 h2 {
      font-size: 40px;
      font-weight: bold;
      margin: 0;
    }

    .container5 .sub-title {
      font-size: 20px;
      font-weight: normal;
      margin-top: 5px;
    }

    /* Container da página Ação */
    .acao-container {
      display: flex;
      flex-direction: column;
      height: 100%;
      padding: 20px;
      background-color: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      border: 1px solid rgba(128, 128, 128, 0.3);
      position: relative;
      overflow: hidden;
    }

    /* Sidebar dentro do container Ação */
    .acao-sidebar {
      position: absolute;
      top: 0;
      right: 0;
      width: auto;
      background: transparent;
      z-index: 10;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 10px;
    }

    .acao-sidebar ul {
      list-style: none;
      padding: 0;
      margin: 0;
      display: flex;
      justify-content: space-around;
    }

    .acao-sidebar ul li {
      position: relative;
      width: 100px;
      height: 60px;
      cursor: pointer;
      background: crimson;
      text-transform: uppercase;
      transition: all 0.4s ease-out;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 0 !important;
    }

    /* Estado selecionado no sidebar */
    .acao-sidebar ul li.selecionado {
      background-color: #333 !important; /* Cinza escuro */
    }

    .acao-sidebar ul li.selecionado img {
      filter: white /* Inverte a cor da imagem para branco */
    }

    /* Estilos para os logos das marcas */
    .acao-sidebar ul li img {
      width: 80px;
      height: 80px;
      object-fit: contain;
      transition: opacity 0.4s ease-out;
    }

    /* Arredondar bordas específicas */
    .acao-sidebar ul li:first-child {
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
    }

    .acao-sidebar ul li:last-child {
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
    }

    /* Esconde o logo ao passar o mouse */
    .acao-sidebar ul li:hover img {
      opacity: 0;
    }

    /* Remove estilos desnecessários */
    .acao-sidebar ul li:after {
      position: absolute;
      background: white;
      color: crimson;
      top: 100%;
      left: 0;
      width: 100%;
      height: 100%;
      opacity: 0;
      transform: translateY(0);
      transition: all 0.4s ease-out;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 16px;
      font-weight: bold;
    }

    .acao-sidebar ul li:nth-child(1):after {
      content: "ASICS";
    }

    .acao-sidebar ul li:nth-child(2):after {
      content: "FILA";
    }

    .acao-sidebar ul li:nth-child(3):after {
      content: "UMBRO";
    }

    .acao-sidebar ul li:hover {
      background: transparent;
    }

    .acao-sidebar ul li:hover:after {
      opacity: 1;
      transform: translateY(-100%);
    }

    /* Estilos da tabela */
    #tabela-producao {
      flex: 1;
      overflow-y: auto;
      margin-top: 20px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      table-layout: auto;
      font-size: px;
    }

    th,
    table td {
      padding: 10px;
      border: 1px solid #ccc;
      text-align: center;
    }

    th {
      background-color: crimson;
      color: white;
      position: sticky;
      top: 0;
      z-index: 1;
    }

    table tr:nth-child(even) {
      background-color: #f9f9f9;
    }

    table tr:hover {
      background-color: #f1f1f1;
    }

    /* Fixar o título da tabela */
    .fixed-title {
      position: sticky;
      top: 0;
      background-color: white;
      z-index: 1;
      padding: 10px;
      border-bottom: 1px solid #ccc;
    }

    /* Ícone de agrupar/desagrupar */
    .toggle-icon {
      cursor: pointer;
      color: #007bff;
      font-size: 24px;
    }

    /* Linha de total */
    .linha-total {
      font-weight: bold;
      background-color: #e0e0e0;
    }

    /* Animação de carregamento */
    .loading-animation2 {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      background-color: rgba(255, 255, 255, 0.911);
      z-index: 100;
    }
    


    #data-hora-registro {
      font-size: 14px;
      color: gray;
      margin-left: 10px;
      font-style: italic;
    }

  </style>
</head>

<body>
  <!-- Sidebar -->
  <nav>
    <ul>
      <li id="statusNav" onclick="showPage('status')">
        <div>
          <i class="fas fa-home"></i>
        </div>
      </li>
      <li id="agendaNav" onclick="showPage('agenda')">
        <div>
          <i class="fas fa-calendar"></i>
        </div>
      </li>
      <li id="registroNav" onclick="showPage('registro')">
        <div>
          <i class="fas fa-clipboard-list"></i>
        </div>
      </li>
      <li id="acaoNav" onclick="showPage('acao')">
        <div>
          <i class="fas fa-bullhorn"></i>
        </div>
      </li>
    </ul>
  </nav>

  <!-- Seções -->
  <section id="status" class="page active">
    <div class="main-container">
      <div class="content">
        <div class="flex-container">
          <div class="left-column">
            <div class="container container2">
              <div class="barcode-field">
                <i class="fas fa-barcode"></i>
                <input type="text" placeholder="Digite o código de barras">
              </div>
            </div>
            <div class="container container3">
              <h2>Container 3</h2>
            </div>
            <div class="container container4">
              <h2>Container 4</h2>
            </div>
          </div>
          <div class="right-column">
            <div class="container container5">
              <h2>SIGA</h2>
              <div class="sub-title">Sistema integrado de gestão aplicada</div>
            </div>
            <div class="container container6">
              <h2>Container 6</h2>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="agenda" class="page">
    <div class="acao-container">
      <h2>Calendário de Apresentação de Gerenciamento Diário</h2>
    </div>
  </section>

  <section id="registro" class="page">
    <div class="acao-container">
      <h2>Plano de Ação</h2>
    </div>
  </section>

  <section id="acao" class="page">
    <span id="data-hora-registro"></span>
    <div class="acao-container">
      <h2 class="fixed-title">Acompanhamento Semanal</h2>

      <!-- Sidebar dentro do container Ação -->
      <div class="acao-sidebar">
        <ul>
          <li id="filtroASICS" onclick="filtrarTabela('ASICS')">
            <div>
              <img src="https://i.postimg.cc/gkYJWM1C/logo-das-marcas-page-0003-removebg-preview.png" alt="ASICS">
            </div>
          </li>
          <li id="filtroFILA" onclick="filtrarTabela('FILA')">
            <div>
              <img src="https://i.postimg.cc/HW0xFGv0/logo-das-marcas-page-0001-removebg-preview.png" alt="FILA">
            </div>
          </li>
          <li id="filtroUMBRO" onclick="filtrarTabela('UMBRO')">
            <div>
              <img src="https://i.postimg.cc/nrxLMTrQ/logo-das-marcas-page-0002-removebg-preview-1.png" alt="UMBRO">
            </div>
          </li>
        </ul>
      </div>

      <!-- Animação de carregamento -->
      <div class="loading-animation2">
        <dotlottie-player  src="https://lottie.host/c306cfff-12a7-48cd-a5c4-5bc0f80f6003/6X1VG6ZT4B.lottie"
          background="transparent" speed="1" style="width: 300px; height: 300px" loop autoplay>
        </dotlottie-player>
      </div>

      <!-- Tabela de Acompanhamento Semanal -->
      <div id="tabela-producao"></div>
    </div>
  </section>

  <script>
    let dadosTabela = []; // Variável global para armazenar os dados da tabela
    let cabecalho = []; // Variável global para armazenar o cabeçalho da tabela

    function showPage(page) {
      var sections = document.querySelectorAll('.page');
      sections.forEach(function (section) {
        section.classList.remove('active');
      });
      var activePage = document.getElementById(page);
      activePage.classList.add('active');
      var navItems = document.querySelectorAll('nav ul li');
      navItems.forEach(function (item) {
        item.classList.remove('active');
      });
      var activeNavItem = document.getElementById(page + "Nav");
      activeNavItem.classList.add('active');
    }

    // Função para carregar os dados da API do Google Apps Script
    async function carregarDadosPlanilha() {
      const url = "https://script.google.com/macros/s/AKfycbwESLf8Xf98nhKuSM9xwDBg0PUdnWfISKSRydtUOHh4po135_d6zmpWC-AFee2N4UiMEw/exec"; // URL do Web App

      try {
        const response = await fetch(url);

        if (!response.ok) {
          throw new Error(`Erro na requisição: ${response.status} ${response.statusText}`);
        }

        const data = await response.json();
        dadosTabela = data; // Armazena os dados na variável global
        cabecalho = Object.keys(data[0]); // Armazena o cabeçalho
        console.log("Dados da API:", dadosTabela); // Debug
        criarTabelaComSubtotal(dadosTabela); // Cria a tabela com subtotais

      } catch (error) {
        console.error("Erro ao carregar os dados da API:", error);

        // Exibe uma mensagem de erro no container da tabela
        const containerTabela = document.getElementById("tabela-producao");
        containerTabela.innerHTML = `<p style="color: red; text-align: center;">Erro ao carregar os dados. Por favor, tente novamente mais tarde.</p>`;
      } finally {
        // Remove a animação de carregamento
        const loadingAnimation = document.querySelector(".loading-animation2");
        if (loadingAnimation) {
          loadingAnimation.style.display = "none";
        }
      }
      
    }
    // Função para carregar os dados da planilha
    async function carregarDadosPlanilha2() {
      const url = "https://script.google.com/macros/s/AKfycbz6wo1LkiwLOInDyNJA0LAx0NtuMmVQpDr4jOdhPS0w0mcd3SxLbiSMopwqySG9lfg5Dw/exec"; // URL do Web App

      try {
        const response = await fetch(url);

        if (!response.ok) {
          throw new Error(`Erro na requisição: ${response.status} ${response.statusText}`);
        }

        const data = await response.json();
        console.log("Dados da API:", data); // Debug

        // Exibir a data e hora ao lado do título
        const dataHoraElement = document.getElementById("data-hora-registro");
        if (dataHoraElement && data.lastUpdated) {
          const dataFormatada = new Date(data.lastUpdated).toLocaleString(); // Formata a data e hora
          dataHoraElement.textContent = `Última atualização: ${dataFormatada}`;
        }

      } catch (error) {
        console.error("Erro ao carregar os dados da API:", error);

        // Exibe uma mensagem de erro
        const dataHoraElement = document.getElementById("data-hora-registro");
        if (dataHoraElement) {
          dataHoraElement.textContent = "Erro ao carregar a data e hora.";
          dataHoraElement.style.color = "red";
        }
      }
    }


    // Função para criar a tabela com subtotais e total geral
    function criarTabelaComSubtotal(dados) {
      if (!dados || dados.length === 0) {
        const containerTabela = document.getElementById("tabela-producao");
        containerTabela.innerHTML = `<p style="color: gray; text-align: center;">Nenhum dado disponível para exibição.</p>`;
        return;
      }

      const tabela = document.createElement("table");
      const thead = document.createElement("thead");
      const tbody = document.createElement("tbody");

      // Cabeçalho da tabela
      const trHead = document.createElement("tr");
      const thToggle = document.createElement("th"); // Coluna para o ícone de toggle
      thToggle.textContent = "Sub"; // Deixar vazio para o ícone
      trHead.appendChild(thToggle);
      cabecalho.forEach(coluna => {
        const th = document.createElement("th");
        th.textContent = coluna;
        trHead.appendChild(th);
      });
      thead.appendChild(trHead);
      tabela.appendChild(thead);

      let totalGeral = {}; // Objeto para armazenar o total geral por coluna numérica

      // Agrupa os dados por semana
      const dadosPorSemana = {};
      dados.forEach(linha => {
        const semana = linha["Semana"];
        if (!dadosPorSemana[semana]) {
          dadosPorSemana[semana] = [];
        }
        dadosPorSemana[semana].push(linha);
      });

      // Preenche a tabela com os dados e subtotais
      Object.keys(dadosPorSemana).sort((a, b) => a - b).forEach(semana => {
        const linhasDaSemana = dadosPorSemana[semana];

        // Linha de subtotal
        const trSubtotal = document.createElement("tr");
        trSubtotal.setAttribute("data-semana", semana);
        trSubtotal.style.fontWeight = "bold";
        trSubtotal.style.backgroundColor = "#f0f0f0";

        const tdToggle = document.createElement("td");
        const iconToggle = document.createElement("i");
        iconToggle.classList.add("fas", "fa-angle-down", "toggle-icon");
        iconToggle.onclick = () => toggleSemana(semana);
        tdToggle.appendChild(iconToggle);
        trSubtotal.appendChild(tdToggle);

        cabecalho.forEach(coluna => {
          const td = document.createElement("td");
          if (coluna === "Semana") {
            td.textContent = `Sem  ${semana}`;
          } else if (!isNaN(parseFloat(linhasDaSemana[0][coluna]))) {
            // Soma os valores da coluna se forem numéricos
            const subtotal = linhasDaSemana.reduce((acc, linha) => acc + parseFloat(linha[coluna] || 0), 0);
            td.textContent = Math.round(subtotal); // Exibe sem casas decimais
            totalGeral[coluna] = (totalGeral[coluna] || 0) + subtotal; // Acumula para o total geral
          } else {
            td.textContent = "";
          }
          trSubtotal.appendChild(td);
        });
        tbody.appendChild(trSubtotal);

        // Linhas da semana (ocultas por padrão)
        linhasDaSemana.forEach(linha => {
          const tr = document.createElement("tr");
          tr.setAttribute("data-semana", semana);
          tr.style.display = "none"; // Oculta as linhas detalhadas por padrão

          const tdEmpty = document.createElement("td");
          tdEmpty.textContent = ""; // Deixar vazio para alinhar com o ícone
          tr.appendChild(tdEmpty);

          cabecalho.forEach(coluna => {
            const td = document.createElement("td");
            if (!isNaN(parseFloat(linha[coluna]))) {
              td.textContent = Math.round(linha[coluna]); // Exibe sem casas decimais
            } else {
              td.textContent = linha[coluna];
            }
            tr.appendChild(td);
          });
          tbody.appendChild(tr);
        });
      });

      // Linha de total geral
      const trTotal = document.createElement("tr");
      trTotal.classList.add("linha-total");

      const tdVazio = document.createElement("td");
      tdVazio.colSpan = 4; // Ocupa quatro colunas (ícone + "Semana" + "Marcas" + "Modelos")
      tdVazio.textContent = "Total Geral";
      trTotal.appendChild(tdVazio);

      cabecalho.forEach(coluna => {
        if (coluna !== "Semana" && coluna !== "Marcas" && coluna !== "Modelos" && !isNaN(parseFloat(totalGeral[coluna]))) {
          const td = document.createElement("td");
          td.textContent = Math.round(totalGeral[coluna]); // Exibe sem casas decimais
          trTotal.appendChild(td);
        }
      });

      tbody.appendChild(trTotal); // Adiciona a linha de total geral

      tabela.appendChild(tbody);

      // Adicionar a tabela ao container
      const containerTabela = document.getElementById("tabela-producao");
      containerTabela.innerHTML = ""; // Limpa o conteúdo anterior
      containerTabela.appendChild(tabela);
    }

    // Função para alternar o estado de exibição das linhas de uma semana
    function toggleSemana(semana) {
      const linhas = document.querySelectorAll(`[data-semana="${semana}"]`);
      const primeiroElemento = linhas[0]; // Subtotal
      const iconeToggle = primeiroElemento.querySelector(".toggle-icon");

      linhas.forEach((linha, index) => {
        if (index > 0) { // Ignorar a linha de subtotal
          if (linha.style.display === "none") {
            linha.style.display = "table-row";
            iconeToggle.classList.remove("fa-angle-up");
            iconeToggle.classList.add("fa-angle-down");
          } else {
            linha.style.display = "none";
            iconeToggle.classList.remove("fa-angle-down");
            iconeToggle.classList.add("fa-angle-up");
          }
        }
      });
    }

    // Função para filtrar a tabela
    function filtrarTabela(filtro) {
      // Filtra os dados com base na coluna "Marcas"
      const dadosFiltrados = dadosTabela.filter(linha => linha["Marcas"] === filtro);
      console.log("Dados filtrados:", dadosFiltrados); // Debug

      // Recria a tabela com os dados filtrados
      criarTabelaComSubtotal(dadosFiltrados);

      // Remove a classe 'selecionado' de todos os blocos
      document.querySelectorAll('.acao-sidebar ul li').forEach(item => {
        item.classList.remove('selecionado');
      });

      // Adiciona a classe 'selecionado' ao bloco clicado
      const filtroElement = document.getElementById('filtro' + filtro);
      if (filtroElement) {
        filtroElement.classList.add('selecionado');
      }
    }

    // Adiciona um evento de clique para cada item do menu
    document.addEventListener('DOMContentLoaded', function () {
      const menuItems = document.querySelectorAll('.acao-sidebar ul li');

      menuItems.forEach(item => {
        item.addEventListener('click', function () {
          // Remover a classe 'selecionado' de todos os itens
          menuItems.forEach(menuItem => {
            menuItem.classList.remove('selecionado');
          });

          // Adicionar a classe 'selecionado' ao item clicado
          this.classList.add('selecionado');
        });
      });

      // Carrega os dados da planilha ao carregar a página
      carregarDadosPlanilha();
      carregarDadosPlanilha2();
    });
  </script>
</body>

</html>
