<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sistema de Login</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #4e73df, #1cc88a);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    background: white;
    padding: 30px;
    border-radius: 10px;
    width: 300px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

h2 {
    text-align: center;
}

input {
    width: 100%;
    padding: 10px;
    margin: 8px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
}

button {
    width: 100%;
    padding: 10px;
    background: #4e73df;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background: #2e59d9;
}

.link {
    text-align: center;
    margin-top: 10px;
    cursor: pointer;
    color: blue;
}

.hidden {
    display: none;
}

.success {
    color: green;
    text-align: center;
}

.error {
    color: red;
    text-align: center;
}
</style>
</head>
<body>

<div class="container">

    <!-- LOGIN -->
    <div id="loginBox">
        <h2>Login</h2>
        <input type="email" id="loginEmail" placeholder="Email">
        <input type="password" id="loginSenha" placeholder="Senha">
        <button onclick="login()">Entrar</button>
        <p class="link" onclick="mostrarCadastro()">Criar conta</p>
        <p id="loginMsg"></p>
    </div>

    <!-- CADASTRO -->
    <div id="cadastroBox" class="hidden">
        <h2>Cadastrar</h2>
        <input type="email" id="cadEmail" placeholder="Email">
        <input type="password" id="cadSenha" placeholder="Senha">
        <button onclick="cadastrar()">Cadastrar</button>
        <p class="link" onclick="mostrarLogin()">Já tenho conta</p>
        <p id="cadMsg"></p>
    </div>

    <!-- AREA LOGADA -->
    <div id="areaLogada" class="hidden">
        <h2>Bem-vindo 🎉</h2>
        <p id="usuarioLogado"></p>
        <button onclick="logout()">Sair</button>
    </div>

</div>

<script>
function mostrarCadastro() {
    loginBox.classList.add("hidden");
    cadastroBox.classList.remove("hidden");
}

function mostrarLogin() {
    cadastroBox.classList.add("hidden");
    loginBox.classList.remove("hidden");
}

function cadastrar() {
    const email = document.getElementById("cadEmail").value;
    const senha = document.getElementById("cadSenha").value;

    if(email === "" || senha === ""){
        cadMsg.innerHTML = "Preencha todos os campos";
        cadMsg.className = "error";
        return;
    }

    localStorage.setItem("usuario", JSON.stringify({email, senha}));
    cadMsg.innerHTML = "Cadastro realizado com sucesso!";
    cadMsg.className = "success";
}

function login() {
    const email = document.getElementById("loginEmail").value;
    const senha = document.getElementById("loginSenha").value;
    const usuario = JSON.parse(localStorage.getItem("usuario"));

    if(!usuario){
        loginMsg.innerHTML = "Nenhum usuário cadastrado!";
        loginMsg.className = "error";
        return;
    }

    if(email === usuario.email && senha === usuario.senha){
        loginBox.classList.add("hidden");
        areaLogada.classList.remove("hidden");
        usuarioLogado.innerHTML = "Logado como: " + usuario.email;
    } else {
        loginMsg.innerHTML = "Email ou senha incorretos!";
        loginMsg.className = "error";
    }
}

function logout() {
    areaLogada.classList.add("hidden");
    loginBox.classList.remove("hidden");
}
</script>

</body>
</html>
