<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bot de Sinais Aviator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: black;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        .password-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .password-box {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            color: black;
        }
        .password-box input {
            padding: 10px;
            margin-top: 10px;
            width: 80%;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .password-box button {
            background-color: red;
            color: white;
            border: none;
            padding: 10px;
            margin-top: 10px;
            cursor: pointer;
            border-radius: 5px;
        }
        .loader {
            border: 4px solid transparent;
            border-top: 4px solid white;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 2s linear infinite;
            margin-top: 10px;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .bot-container {
            display: none;
            position: fixed;
            bottom: 20px;
            right: 20px;
            width: 350px;
            background: white;
            color: black;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }
        .bot-header {
            font-size: 18px;
            font-weight: bold;
        }
        .bot-messages {
            max-height: 200px;
            overflow-y: auto;
            margin-bottom: 10px;
        }
        .bot-footer {
            margin-top: 10px;
            text-align: center;
            font-size: 12px;
        }
        .bot-footer a {
            color: blue;
            text-decoration: none;
            font-weight: bold;
        }
        .message-success {
            color: black;
            font-size: 18px;
            font-weight: bold;
        }
        .account-message {
            font-size: 16px;
            font-weight: bold;
        }
        .generate-button {
            background-color: red;
            color: white;
            border: none;
            padding: 10px 20px;
            margin-top: 10px;
            cursor: pointer;
            border-radius: 5px;
            font-size: 16px;
            text-decoration: underline;
            font-weight: bold;
        }
        .info-box {
            margin-top: 20px;
            background-color: white;
            color: black;
            padding: 15px;
            border-radius: 10px;
            border: 2px solid #ccc;
            text-align: left;
            font-size: 14px;
        }
        .info-box div {
            margin-bottom: 10px;
        }
        .info-box .label {
            font-weight: bold;
        }
        .whatsapp-link {
            margin-top: 20px;
            font-size: 14px;
            text-decoration: none;
            font-weight: bold;
            color: green;
        }
    </style>
</head>
<body>
    <div class="password-container" id="password-container">
        <div class="password-box">
            <h2>🔒 Acesso Restrito</h2>
            <p>Digite a senha para continuar:</p>
            <input type="password" id="password-input" placeholder="Digite a senha...">
            <button onclick="verificarSenha()">Fazer Login</button>
            <div id="loader" class="loader" style="display:none;"></div>
            <p id="error-message" style="color: red; display: none;">Senha incorreta! ❌</p>
        </div>
    </div>

    <div class="bot-container" id="bot">
        <div class="bot-header">Bot de Sinais Aviator</div>
        <div class="bot-messages" id="messages"></div>
        <div class="info-box">
            <div><span class="label">Proteção:</span> <span id="proteção" style="color: black;"></span></div>
            <div><span class="label">Entrada:</span> <span id="entrada"></span></div>
            <div><span class="label">Saída:</span> <span id="saída" style="color: green;"></span></div>
            <div><span class="label">Hora:</span> <span id="hora"></span></div>
        </div>
        <button class="generate-button" onclick="gerarSinal()">Gerar Sinais</button>
        <div class="bot-footer">
            <p class="account-message">Para que o bot funcione 100%, sem interrupções, crie sua conta agora: 
            <a href="https://abre.ai/lRn5" target="_blank">Clique aqui</a></p>
            <a href="https://wa.me/846738036" target="_blank" class="whatsapp-link">Fale com a gente no WhatsApp ✅</a>
        </div>
    </div>

    <script>
        function verificarSenha() {
            const senhaCorreta = "bot2025";  // Senha alterada para bot2025
            const senhaDigitada = document.getElementById("password-input").value;
            document.getElementById("loader").style.display = "inline-block";  // Mostrar o carregamento

            setTimeout(function() {
                if (senhaDigitada === senhaCorreta) {
                    document.getElementById("loader").style.display = "none";
                    document.getElementById("password-container").style.display = "none";
                    document.getElementById("bot").style.display = "block";
                    alert("Para que o bot funcione sem interrupções, crie sua conta agora.");
                    const successMessage = document.createElement("div");
                    successMessage.classList.add("message-success");
                    successMessage.innerHTML = "Login com sucesso! ✅";
                    document.getElementById("bot").appendChild(successMessage);
                } else {
                    document.getElementById("loader").style.display = "none";
                    document.getElementById("error-message").style.display = "block";
                }
            }, 2000); // Tempo de espera para mostrar o carregamento
        }

        function gerarSinal() {
            const agora = new Date();
            const horaAtual = agora.toLocaleTimeString("pt-MZ", { hour: '2-digit', minute: '2-digit', second: '2-digit' });
            let protecao, saida, cor, alerta, entrada;

            const faixa = Math.random();
            if (faixa < 0.33) {
                entrada = "Entrada Não Confirmada";
                protecao = Math.random() < 0.5 ? 1.02 : 0.03;
                saida = Math.random() * (2 - 1.50) + 1.50;
                cor = "blue"; // Azul para entrada não confirmada
                alerta = "Entrada Não Confirmada (Azul)";
            } else if (faixa < 0.66) {
                entrada = "Entrada Confirmada";
                protecao = Math.random() < 0.5 ? 2.00 : 3.00;
                saida = Math.random() * (10 - 3) + 3;
                cor = "purple"; // Roxo para sinais de 2.00 a 10.00
                alerta = "Roxo está chegando!";
            } else {
                entrada = "Entrada Confirmada";
                protecao = Math.random() < 0.5 ? 3.00 : 10.00;
                saida = Math.random() * 100 + 10; // Rosa para sinais de 10 até mais infinito
                cor = "pink";
                alerta = "Rosa está chegando!";
            }

            const resultado = `Hora: ${horaAtual} | ${entrada} | Proteção: ${protecao.toFixed(2)}x | Saída: <span style="color:${cor}">${saida.toFixed(2)}x</span>`;
            
            // Atualizando os valores no quadro de informações
            document.getElementById("entrada").innerText = entrada;
            document.getElementById("entrada").style.color = cor; // Colorir Entrada
            document.getElementById("proteção").innerText = protecao.toFixed(2) + "x";
            document.getElementById("saída").innerText = saida.toFixed(2) + "x";
            document.getElementById("hora").innerText = horaAtual; // Exibindo a hora, minutos e segundos
        }
    </script>
</body
