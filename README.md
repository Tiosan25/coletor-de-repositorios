<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de anexos de documentações assinadas - GRUPO MASTERLOG</title>
    <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
    <script>
        (function() {
            emailjs.init('sxauGQUDf6ZzE-1ni');
        })();
    </script>
    <style>
        :root {
            --primary-color: #bb463c;
            --background-color: #ADADAD;
            --success-color: #5cb85c;
            --error-color: #dc3545;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 15px;
            background-color: var(--background-color);
            position: relative;
            min-height: 100vh;
            padding-bottom: 120px;
        }
        
        .container {
            max-width: 100%;
            margin: 0 auto;
            padding-bottom: 70px;
        }
        
        .step-container {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .step-content {
            width: 100%;
        }
        
        .step-image {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }
        
        .step-image img {
            max-width: 200px;
            max-height: 120px;
            object-fit: contain;
        }
        
        .step {
            margin-bottom: 20px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background-color: white;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        #step2, #step3, #listContainer {
            display: none;
        }
        
        .employee-item {
            display: flex;
            flex-direction: column;
            margin-bottom: 15px;
            gap: 10px;
            padding: 10px;
            background-color: white;
            border-radius: 5px;
        }
        
        .employee-name {
            font-weight: bold;
        }
        
        select, input, button {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            margin: 8px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        
        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: #a03a32;
        }
        
        #progressBar {
            width: 100%;
            height: 8px;
            background-color: #e0e0e0;
            border-radius: 5px;
            margin-bottom: 20px;
            overflow: hidden;
        }
        
        #progress {
            height: 100%;
            width: 0%;
            background-color: var(--primary-color);
            transition: width 0.5s;
        }
        
        .progress-steps {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            overflow-x: auto;
            white-space: nowrap;
        }
        
        .progress-step {
            text-align: center;
            min-width: 80px;
            position: relative;
            font-size: 14px;
        }
        
        .progress-step:before {
            content: attr(data-step);
            width: 25px;
            height: 25px;
            line-height: 25px;
            border-radius: 50%;
            background-color: #bdc3c7;
            color: white;
            display: block;
            margin: 0 auto 5px;
            font-weight: bold;
            font-size: 12px;
        }
        
        .progress-step.active:before {
            background-color: var(--primary-color);
        }
        
        .progress-step.complete:before {
            background-color: var(--success-color);
            content: "✓";
        }
        
        #confirmation {
            display: none;
            text-align: center;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            margin-top: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .checkmark {
            font-size: 50px;
            color: var(--success-color);
            margin-bottom: 15px;
        }
        
        .signature {
            position: fixed;
            bottom: 10px;
            left: 10px;
            font-size: 11px;
            color: #555;
            opacity: 0.7;
        }
        
        h1 {
            font-size: 20px;
            color: #2c3e50;
            text-align: center;
            margin: 15px 0;
        }
        
        h2 {
            font-size: 18px;
            color: #333;
            margin-top: 0;
        }
        
        .button-group {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        .button-group button {
            flex: 1;
        }
        
        .file-info {
            font-size: 14px;
            color: var(--primary-color);
            margin: 5px 0;
            word-break: break-all;
        }
        
        .remove-button {
            background-color: var(--error-color);
            padding: 5px 10px;
            font-size: 14px;
            margin: 5px 0;
            width: auto;
        }
        
        .remove-button:hover {
            background-color: #c82333;
        }
        
        .file-input-container {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .search-container {
            margin-bottom: 20px;
        }
        
        #searchInput {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 10px;
        }
        
        .no-results {
            text-align: center;
            padding: 20px;
            color: #666;
            display: none;
        }
        
        .loading {
            text-align: center;
            padding: 20px;
            color: var(--primary-color);
            font-weight: bold;
        }
        
        /* Estilos para a parte 4 com botões fixos */
        #listContainer {
            display: none;
            position: relative;
            padding-bottom: 70px;
        }
        
        .fixed-buttons {
            position: fixed;
            bottom: 15px;
            left: 15px;
            right: 15px;
            background-color: white;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
            z-index: 100;
        }
        
        .employees-list-container {
            max-height: calc(100vh - 250px);
            overflow-y: auto;
            margin-bottom: 15px;
        }
        
        @media (min-width: 768px) {
            .container {
                max-width: 800px;
            }
            
            .step-container {
                flex-direction: row;
                align-items: center;
            }
            
            .step-content {
                flex: 2;
            }
            
            .step-image {
                flex: 1;
                margin: 0;
            }
            
            .employee-item {
                flex-direction: row;
                align-items: center;
            }
            
            .employee-name {
                min-width: 200px;
            }
            
            .file-input {
                min-width: 250px;
            }
            
            h1 {
                font-size: 24px;
            }
            
            .file-input-container {
                flex-direction: row;
                align-items: center;
            }
            
            .remove-button {
                margin-left: 10px;
                margin-top: 0;
            }
            
            .fixed-buttons {
                left: 50%;
                transform: translateX(-50%);
                max-width: 800px;
                width: calc(100% - 30px);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Sistema de anexos de documentações assinadas - GRUPO MASTERLOG</h1>

        <div id="progressBar">
            <div id="progress"></div>
        </div>

        <div class="progress-steps">
            <div class="progress-step active" data-step="1">Operação</div>
            <div class="progress-step" data-step="2">Tipo Doc.</div>
            <div class="progress-step" data-step="3">Mês Ref.</div>
            <div class="progress-step" data-step="4">Anexos</div>
        </div>

        <div id="step1" class="step">
            <div class="step-container">
                <div class="step-content">
                    <h2>1. Selecione a Operação</h2>
                    <select id="operationSelect">
                        <option value="" disabled selected>Selecione uma operação</option>
                    </select>
                    <div class="button-group">
                        <button id="nextStep1">Próximo</button>
                    </div>
                </div>
                <div class="step-image">
                    <img src="https://www.grupomasterlog.com.br/imagens/terceirizacao-de-mao-de-obra-limpeza-pos-obra-masterlog-logo.png" alt="Logo Masterlog">
                </div>
            </div>
        </div>

        <div id="step2" class="step">
            <div class="step-container">
                <div class="step-content">
                    <h2>2. Selecione o Tipo de Documento</h2>
                    <select id="documentTypeSelect">
                        <option value="" disabled selected>Selecione o tipo de documento</option>
                        <option value="holerite">HOLERITE DE PAGAMENTO (assinado)</option>
                        <option value="espelho">ESPELHO DE PONTO (assinado)</option>
                    </select>
                    <div class="button-group">
                        <button id="previousStep2">Voltar</button>
                        <button id="nextStep2">Próximo</button>
                    </div>
                </div>
                <div class="step-image">
                    <img src="https://www.grupomasterlog.com.br/imagens/terceirizacao-de-mao-de-obra-limpeza-pos-obra-masterlog-logo.png" alt="Logo Masterlog">
                </div>
            </div>
        </div>

        <div id="step3" class="step">
            <div class="step-container">
                <div class="step-content">
                    <h2>3. Selecione o Mês de Referência</h2>
                    <select id="monthReference">
                        <option value="" disabled selected>Selecione o mês/ano</option>
                    </select>
                    <div class="button-group">
                        <button id="previousStep3">Voltar</button>
                        <button id="nextStep3">Confirmar</button>
                    </div>
                </div>
                <div class="step-image">
                    <img src="https://www.grupomasterlog.com.br/imagens/terceirizacao-de-mao-de-obra-limpeza-pos-obra-masterlog-logo.png" alt="Logo Masterlog">
                </div>
            </div>
        </div>

        <div id="listContainer">
            <h2 id="listTitle"></h2>
            <div class="search-container">
                <input type="text" id="searchInput" placeholder="Digite o nome do funcionário para buscar...">
                <div class="no-results" id="noResults">Nenhum funcionário encontrado com esse nome</div>
            </div>
            <div class="employees-list-container">
                <form id="mainForm">
                    <ul id="employeesList"></ul>
                </form>
            </div>
            <div class="fixed-buttons">
                <div class="button-group">
                    <button id="previousStep4" type="button">Voltar</button>
                    <button type="submit" form="mainForm">Enviar Documentos</button>
                </div>
            </div>
        </div>

        <div id="confirmation">
            <div class="checkmark">✓</div>
            <h2>Processo Concluído com Sucesso!</h2>
            <p id="summary"></p>
            <button id="newProcess">Iniciar Novo Processo</button>
        </div>
    </div>

    <div class="signature">by. sanderson souza</div>

    <script>
        // Employee data
        let employees = ["Ana Silva", "Pedro Souza", "Mariana Oliveira", "Lucas Santos", "Juliana Costa"];
        
        // Operations list with column mapping
        const operations = {
            "aguia_branca": { name: "ÁGUIA BRANCA", column: "A" },
            "alfa_bauru": { name: "ALFA BAURU", column: "B" },
            "alfa_guarulhos": { name: "ALFA GUARULHOS", column: "C" },
            "alfa_ribeirao": { name: "ALFA RIBEIRÃO", column: "D" },
            "alfa_sumare": { name: "ALFA SUMARÉ", column: "E" },
            "amanco_sumare": { name: "AMANCO SUMARÉ", column: "G" },
            "ampm_cajamar": { name: "AMPM CAJAMAR", column: "H" },
            "ampm_parana": { name: "AMPM PARANÁ", column: "I" },
            "andorinhas": { name: "ANDORINHAS", column: "F" },
            "decorlux": { name: "DECORLUX", column: "J" },
            "escritorio": { name: "ESCRITÓRIO", column: "L" },
            "europack_master": { name: "EUROPACK MASTER", column: "K" },
            "europack_volpi": { name: "EUROPACK - VOLPI", column: null },
            "mara_supermercados": { name: "MARA SUPERMERCADOS", column: null },
            "mello": { name: "MELLO", column: "O" },
            "ns_log_campinas": { name: "NS LOG CAMPINAS / SUMARÉ", column: "R" },
            "ns_log_guarulhos": { name: "NS LOG GUARULHOS / SP", column: "P" },
            "ns_log_ribeirao": { name: "NS LOG RIBEIRÃO", column: "Q" },
            "penske_cajamar": { name: "PENSKE CAJAMAR", column: "S" },
            "penske_itupeva": { name: "PENSKE ITUPEVA", column: "T" },
            "resil": { name: "RESIL", column: "AA" },
            "ricambi": { name: "RICAMBI", column: null },
            "samsung_cd": { name: "SAMSUNG C&D", column: "W" },
            "samsung_service": { name: "SAMSUNG SERVICE", column: "V" },
            "tondo": { name: "TONDO", column: "U" },
            "upper_trade": { name: "UPPER TRADE", column: "Z" },
            "vedacit": { name: "VEDACIT", column: "Y" },
            "vex_hunter": { name: "VEX - HUNTER", column: null },
            "vidara": { name: "VIDARA", column: "X" }
        };

        // Months for selection
        const months = [
            { value: '01/2025', name: 'Janeiro/2025' },
            { value: '02/2025', name: 'Fevereiro/2025' },
            { value: '03/2025', name: 'Março/2025' },
            { value: '04/2025', name: 'Abril/2025' },
            { value: '05/2025', name: 'Maio/2025' },
            { value: '06/2025', name: 'Junho/2025' },
            { value: '07/2025', name: 'Julho/2025' },
            { value: '08/2025', name: 'Agosto/2025' },
            { value: '09/2025', name: 'Setembro/2025' },
            { value: '10/2025', name: 'Outubro/2025' },
            { value: '11/2025', name: 'Novembro/2025' },
            { value: '12/2025', name: 'Dezembro/2025' }
        ];

        // DOM Elements
        const step1 = document.getElementById("step1");
        const step2 = document.getElementById("step2");
        const step3 = document.getElementById("step3");
        const listContainer = document.getElementById("listContainer");
        const confirmation = document.getElementById("confirmation");
        const operationSelect = document.getElementById("operationSelect");
        const documentTypeSelect = document.getElementById("documentTypeSelect");
        const monthReference = document.getElementById("monthReference");
        const listTitle = document.getElementById("listTitle");
        const employeesList = document.getElementById("employeesList");
        const mainForm = document.getElementById("mainForm");
        const progressBar = document.getElementById("progress");
        const progressSteps = document.querySelectorAll(".progress-step");
        const summary = document.getElementById("summary");
        const searchInput = document.getElementById("searchInput");
        const noResults = document.getElementById("noResults");

        // Stores attached files
        let attachedFiles = {};

        // Populate operations dropdown
        for (const [value, op] of Object.entries(operations)) {
            const option = document.createElement("option");
            option.value = value;
            option.textContent = op.name;
            operationSelect.appendChild(option);
        }

        // Populate months dropdown
        months.forEach(month => {
            const option = document.createElement("option");
            option.value = month.value;
            option.textContent = month.name;
            monthReference.appendChild(option);
        });

        // Function to fetch employees from Google Sheets starting from row 2
        async function fetchEmployeesFromSheet(columnLetter) {
            try {
                // Show loading indicator
                employeesList.innerHTML = '<div class="loading">Carregando lista de funcionários...</div>';
                
                // Google Sheets API URL (public mode)
                const spreadsheetId = '1_7zhBnvIMxXgEP8TxI5c5YJyXv6FU37_oYzNrgCVMJg';
                const sheetName = 'CONSOLE FUNC.';
                
                // Using the public Google Sheets API with range starting from row 2
                const url = `https://docs.google.com/spreadsheets/d/${spreadsheetId}/gviz/tq?tqx=out:json&sheet=${encodeURIComponent(sheetName)}&range=${columnLetter}2:${columnLetter}`;
                
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro ao acessar a planilha');
                
                const text = await response.text();
                const jsonText = text.match(/google\.visualization\.Query\.setResponse\(([\s\S]+)\);/)[1];
                const data = JSON.parse(jsonText);
                
                if (data.table && data.table.rows && data.table.rows.length > 0) {
                    // Extract names from specified column (starting from row 2)
                    const names = data.table.rows
                        .map(row => row.c && row.c[0] ? row.c[0].v.trim() : null)
                        .filter(name => name) // Remove null/empty values
                        .filter((name, index, self) => self.indexOf(name) === index); // Remove duplicates
                    
                    if (names.length === 0) {
                        throw new Error('Nenhum nome encontrado na coluna ' + columnLetter);
                    }
                    
                    return names;
                } else {
                    throw new Error('Estrutura de dados inesperada na planilha');
                }
            } catch (error) {
                console.error('Error fetching employees from Google Sheets:', error);
                alert('Erro ao carregar lista de funcionários. Usando lista padrão. Detalhes: ' + error.message);
                return ["Ana Silva", "Pedro Souza", "Mariana Oliveira", "Lucas Santos", "Juliana Costa"];
            }
        }

        // Update progress bar and steps
        function updateProgress(currentStep) {
            const progressPercentage = (currentStep / 4) * 100;
            progressBar.style.width = `${progressPercentage}%`;
            
            progressSteps.forEach((step, index) => {
                if (index < currentStep - 1) {
                    step.classList.add("complete");
                    step.classList.remove("active");
                } else if (index === currentStep - 1) {
                    step.classList.add("active");
                    step.classList.remove("complete");
                } else {
                    step.classList.remove("active", "complete");
                }
            });
        }

        // Show specific step
        function showStep(stepNumber) {
            step1.style.display = "none";
            step2.style.display = "none";
            step3.style.display = "none";
            listContainer.style.display = "none";
            confirmation.style.display = "none";
            
            switch(stepNumber) {
                case 1:
                    step1.style.display = "block";
                    updateProgress(1);
                    break;
                case 2:
                    step2.style.display = "block";
                    updateProgress(2);
                    break;
                case 3:
                    step3.style.display = "block";
                    updateProgress(3);
                    break;
                case 4:
                    listContainer.style.display = "block";
                    updateProgress(4);
                    // Scroll to top when showing the list
                    window.scrollTo(0, 0);
                    break;
                case 5:
                    confirmation.style.display = "block";
                    break;
            }
        }

        // Filter names in search
        function filterNames() {
            const searchTerm = searchInput.value.toLowerCase();
            const listItems = document.querySelectorAll("#employeesList li");
            let hasResults = false;

            listItems.forEach(item => {
                const employeeName = item.querySelector(".employee-name").textContent.toLowerCase();
                if (employeeName.includes(searchTerm)) {
                    item.style.display = "flex";
                    hasResults = true;
                } else {
                    item.style.display = "none";
                }
            });

            noResults.style.display = hasResults ? "none" : "block";
        }

        // Rename file before sending
        function renameFile(originalFile, employeeName, operation, documentType, monthReference) {
            const extension = originalFile.name.split('.').pop();
            const formattedName = employeeName.replace(/ /g, '_');
            const formattedOperation = operation.replace(/ /g, '_');
            const formattedDocumentType = documentType.replace(/ /g, '_');
            const formattedMonth = monthReference.replace('/', '_');
            
            const newName = `${formattedName}_${formattedOperation}_${formattedDocumentType}_${formattedMonth}.${extension}`;
            
            return new File([originalFile], newName, {
                type: originalFile.type,
                lastModified: originalFile.lastModified
            });
        }

        // Step 1 button event
        document.getElementById("nextStep1").addEventListener("click", async function() {
            if (!operationSelect.value) {
                alert("Por favor, selecione uma operação");
                return;
            }
            
            const selectedOperation = operations[operationSelect.value];
            
            // If operation has a column defined, fetch employees from Google Sheets
            if (selectedOperation.column) {
                try {
                    employees = await fetchEmployeesFromSheet(selectedOperation.column);
                } catch (error) {
                    console.error("Error fetching employees:", error);
                    // Fallback to default employees
                    employees = ["Ana Silva", "Pedro Souza", "Mariana Oliveira", "Lucas Santos", "Juliana Costa"];
                }
            } else {
                // For operations without column, use default employees
                employees = ["Ana Silva", "Pedro Souza", "Mariana Oliveira", "Lucas Santos", "Juliana Costa"];
            }
            
            showStep(2);
        });

        // Step 2 button event
        document.getElementById("nextStep2").addEventListener("click", function() {
            if (!documentTypeSelect.value) {
                alert("Por favor, selecione o tipo de documento");
                return;
            }
            showStep(3);
        });

        // Step 3 button event
        document.getElementById("nextStep3").addEventListener("click", function() {
            if (!monthReference.value) {
                alert("Por favor, selecione o mês de referência");
                return;
            }
            
            showStep(4);
            const selectedOperation = operations[operationSelect.value];
            const selectedMonth = monthReference.selectedOptions[0].text;
            listTitle.textContent = `${selectedOperation.name} - ${documentTypeSelect.selectedOptions[0].text} - ${selectedMonth}`;
            
            employeesList.innerHTML = "";
            
            employees.forEach(employee => {
                const listItem = document.createElement("li");
                listItem.className = "employee-item";
                const employeeKey = employee.toLowerCase().replace(/ /g, '_');
                
                const nameSpan = document.createElement("span");
                nameSpan.className = "employee-name";
                nameSpan.textContent = employee;
                
                const fileContainer = document.createElement("div");
                fileContainer.className = "file-input-container";
                
                const fileInput = document.createElement("input");
                fileInput.type = "file";
                fileInput.className = "file-input";
                fileInput.name = `file_${employeeKey}`;
                fileInput.accept = ".pdf,.png,.jpg,.jpeg,.JPEG,.doc,.docx";
                
                if (attachedFiles[employeeKey]) {
                    const fileInfo = document.createElement("div");
                    fileInfo.className = "file-info";
                    fileInfo.textContent = `Arquivo anexado: ${attachedFiles[employeeKey].name}`;
                    
                    const removeButton = document.createElement("button");
                    removeButton.type = "button";
                    removeButton.textContent = "Remover";
                    removeButton.className = "remove-button";
                    removeButton.addEventListener("click", () => {
                        delete attachedFiles[employeeKey];
                        fileInput.value = "";
                        fileContainer.removeChild(fileInfo);
                        fileContainer.removeChild(removeButton);
                    });
                    
                    fileContainer.appendChild(fileInfo);
                    fileContainer.appendChild(removeButton);
                }
                
                fileInput.addEventListener("change", (e) => {
                    if (e.target.files.length > 0) {
                        attachedFiles[employeeKey] = e.target.files[0];
                        document.getElementById("nextStep3").click();
                    }
                });
                
                fileContainer.appendChild(fileInput);
                
                const hiddenOperation = document.createElement("input");
                hiddenOperation.type = "hidden";
                hiddenOperation.name = "operation";
                hiddenOperation.value = operationSelect.value;
                
                const hiddenDocumentType = document.createElement("input");
                hiddenDocumentType.type = "hidden";
                hiddenDocumentType.name = "document_type";
                hiddenDocumentType.value = documentTypeSelect.value;
                
                const hiddenMonth = document.createElement("input");
                hiddenMonth.type = "hidden";
                hiddenMonth.name = "month_reference";
                hiddenMonth.value = monthReference.value;
                
                listItem.appendChild(nameSpan);
                listItem.appendChild(fileContainer);
                listItem.appendChild(hiddenOperation);
                listItem.appendChild(hiddenDocumentType);
                listItem.appendChild(hiddenMonth);
                
                employeesList.appendChild(listItem);
            });

            searchInput.value = "";
            noResults.style.display = "none";
        });

        // Previous step buttons
        document.getElementById("previousStep2").addEventListener("click", () => showStep(1));
        document.getElementById("previousStep3").addEventListener("click", () => showStep(2));
        document.getElementById("previousStep4").addEventListener("click", () => showStep(3));

        // Search input event
        searchInput.addEventListener("input", filterNames);

        // Form submit event
        mainForm.addEventListener("submit", async function(e) {
            e.preventDefault();
            
            // Validate file types
            const invalidFiles = [];
            const allowedExtensions = ['.pdf', '.png', '.jpg', '.jpeg', '.JPEG', '.doc', '.docx'];
            
            Object.entries(attachedFiles).forEach(([employeeKey, file]) => {
                const extension = file.name.substring(file.name.lastIndexOf('.')).toLowerCase();
                if (!allowedExtensions.includes(extension)) {
                    invalidFiles.push({
                        fileName: file.name
                    });
                }
            });
            
            if (invalidFiles.length > 0) {
                alert(`Os seguintes arquivos têm formatos não permitidos:\n\n${
                    invalidFiles.map(f => `• ${f.fileName}`).join('\n')
                }\n\nPor favor, anexe apenas arquivos nos formatos: PDF, PNG, JPG, JPEG ou Word (DOC/DOCX).`);
                return;
            }
            
            const formData = new FormData();
            const selectedOperation = operations[operationSelect.value];
            const documentType = documentTypeSelect.value === "holerite" ? "Holerite_de_Pagamento" : "Espelho_de_Ponto";
            const monthRef = monthReference.value;
            
            // Process and rename each file
            const renamedFiles = [];
            
            Object.entries(attachedFiles).forEach(([employeeKey, originalFile]) => {
                const employeeName = employeeKey.replace(/_/g, ' ');
                const renamedFile = renameFile(
                    originalFile, 
                    employeeName,
                    selectedOperation.name,
                    documentType,
                    monthRef
                );
                
                formData.append(`file_${employeeKey}`, renamedFile);
                renamedFiles.push({
                    employee: employeeName,
                    file_name: renamedFile.name
                });
            });
            
            // Add other fields
            formData.append("operation", operationSelect.value);
            formData.append("document_type", documentTypeSelect.value);
            formData.append("month_reference", monthReference.value);
            
            const sendData = {
                operation: selectedOperation.name,
                document_type: documentType.replace(/_/g, ' '),
                month_reference: monthReference.value,
                files: renamedFiles
            };
            
            // Prepare summary
            const selectedMonth = monthReference.selectedOptions[0].text;
            const summaryText = `
                <strong>Operação:</strong> ${sendData.operation}<br>
                <strong>Tipo de Documento:</strong> ${sendData.document_type}<br>
                <strong>Mês de Referência:</strong> ${selectedMonth}<br>
                <strong>Documentos Anexados:</strong> ${sendData.files.length} de ${employees.length} funcionários<br><br>
                <strong>Arquivos enviados:</strong><br>
                ${sendData.files.map(f => `• ${f.file_name}`).join('<br>')}
            `;
            
            summary.innerHTML = summaryText;
            showStep(5);
            
            // Send email notification
            const emailSent = await emailjs.send(
                'service_w05fip5',
                'template_mdtofyt',
                {
                    operation: sendData.operation,
                    document_type: sendData.document_type,
                    month_reference: selectedMonth,
                    total_employees: sendData.files.length,
                    recipients: "leticia.azevedo@grupomasterlog.com.br, vitoria.souza@grupomasterlog.com.br, vinicius.lima@grupomasterlog.com.br, taysa.oliveira@grupomasterlog.com.br, sanderson.oliveira@grupomasterlog.com.br"
                }
            );
            
            if (emailSent) {
                alert('Notificação enviada com sucesso para a equipe!');
            } else {
                alert('Os documentos foram salvos, mas houve um erro ao enviar a notificação. Por favor, avise a equipe manualmente.');
            }
        });

        // New process button
        document.getElementById("newProcess").addEventListener("click", function() {
            attachedFiles = {};
            mainForm.reset();
            operationSelect.value = "";
            documentTypeSelect.value = "";
            monthReference.value = "";
            showStep(1);
        });

        // Initialize showing first step
        showStep(1);
    </script>
</body>
</html>
