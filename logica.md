# Lógica do Programa de matemática

Código completo

```python
from flask import Flask, render_template, request
import sqlite3
import webbrowser
import threading

# Criação da instância da aplicação Flask
app = Flask(__name__)

# Função para abrir o navegador automaticamente
def open_browser():
    webbrowser.open('http://127.0.0.1:5000')

@app.route("/")
def home():
    # Renderiza o template sem resultado inicialmente
    return render_template("index.html", resultado=None)

@app.route("/código_fonte")
def codigo():
    return render_template("codigo.html")
# Define a rota para lidar com o formulário enviado (com método POST)
@app.route('/button', methods=['POST'])
def submit():
    # Pega os valores do formulário
    numero1 = request.form['numero1']
    numero2 = request.form['numero2']
    operacao = request.form['operacao']
    
    # Inicializa uma variável para o resultado
    resultado = None
    
    # Realiza a operação de soma
    if operacao == "+": 
        resultado = f'{numero1} + {numero2} = {float(numero1) + float(numero2)}'
    elif operacao == "-":
        resultado = f'{numero1} - {numero2} = {float(numero1) - float(numero2)}'
    elif operacao == "*":
        resultado = f'{numero1} * {numero2} = {float(numero1) * float(numero2)}'
    elif operacao == "//":
        resultado = f'{numero1} // {numero2} = {float(numero1) // float(numero2)}'
    elif operacao == "/":
        resultado = f'{numero1} / {numero2} = {float(numero1) / float(numero2)}'
    elif operacao == "**":
        resultado = f'{numero1} ** {numero2} = {float(numero1) ** float(numero2)}'
    elif operacao == "%":
        resultado = f'{numero1} % {numero2} = {float(numero1) % float(numero2)}'
    else:
        resultado = f'ERRO: o sinal "{operacao}", não existe!'
    
    # Renderiza o template passando o resultado
    return render_template("index.html", resultado=resultado)

if __name__ == "__main__":
    # Inicia o servidor e abre o navegador em uma nova thread
    threading.Timer(0.1, open_browser).start()
    app.run(debug=True)

```

Código html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Código fonte</title>
</head>
<body>
    <a href="/"><<< Voltar</a>
    <p> PYTHON<br><br>

        from flask import Flask, render_template, request<br>
        import sqlite3<br>
        import webbrowser<br>
        import threading<br>
        
        # Criação da instância da aplicação Flask<br>
        app = Flask(__name__)<br>
        
        # Função para abrir o navegador automaticamente<br>
        def open_browser():<br>
        ....webbrowser.open('http://127.0.0.1:5000')<br>
        
        @app.route("/")<br>
        def home():<br>
        ....# Renderiza o template sem resultado inicialmente<br>
        ....return render_template("index.html", resultado=None)<br>
        
        @app.route("/código_fonte")<br>
        def codigo():<br>
        ....return render_template("codigo.html")<br>
        # Define a rota para lidar com o formulário enviado (com método POST)<br>
        @app.route('/button', methods=['POST'])<br>
        def submit():<br>
        ....# Pega os valores do formulário<br>
        ....numero1 = request.form['numero1']<br>
        ....numero2 = request.form['numero2']<br>
        ....operacao = request.form['operacao']<br>
            
        ....# Inicializa uma variável para o resultado<br>
        ....resultado = None<br>
            
        ....# Realiza a operação de soma<br>
        ....if operacao == "+":<br>
        .......resultado = f'{numero1} + {numero2} = {float(numero1) + float(numero2)}'<br>
        ....elif operacao == "-":<br>
        .......resultado = f'{numero1} - {numero2} = {float(numero1) - float(numero2)}'<br>
        ....elif operacao == "*":<br>
        .......resultado = f'{numero1} * {numero2} = {float(numero1) * float(numero2)}'<br>
        ....elif operacao == "//":<br>
        .......resultado = f'{numero1} // {numero2} = {float(numero1) // float(numero2)}'<br>
        ....elif operacao == "/":<br>
        ........resultado = f'{numero1} / {numero2} = {float(numero1) / float(numero2)}'<br>
        ....elif operacao == "**":<br>
        .......resultado = f'{numero1} ** {numero2} = {float(numero1) ** float(numero2)}'<br>
        ....elif operacao == "%":<br>
        .......resultado = f'{numero1} % {numero2} = {float(numero1) % float(numero2)}'<br>
        ....else:<br>
        .......resultado = f'ERRO: o sinal "{operacao}", não existe!'<br>
            
        ....# Renderiza o template passando o resultado<br>
        ....return render_template("index.html", resultado=resultado)<br>
        
        if __name__ == "__main__":<br>
        ....# Inicia o servidor e abre o navegador em uma nova thread<br>
        ....threading.Timer(0.1, open_browser).start()<br>
        ....app.run(host='0.0.0.0', port=5000, debug=True)
 


        </p>

</body>
</html>
```
```html
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Operação Matemática, com operações do Python</title>
    <style>
        tt {
            color: white;
        }
        a, button, input[type="submit"] {
            font-family: 'Courier New', Courier, monospace;
            width: 100%;
            height: 30px;
            color: rgb(0, 255, 136);
            background-color: rgb(0, 0, 0);
            border-color: rgb(54, 0, 68);
        }
        input {
            font-family: 'Courier New', Courier, monospace;
            width: 100%;
            height: 30px;
            color: rgb(0, 255, 136);
            background-color: rgb(0, 0, 0);
            border-color: rgb(54, 0, 68);
        }

        .rectangle {
            width: 600px; /* Largura do retângulo */
            height: 1000px; /* Altura do retângulo */
            background-color: rgb(43, 43, 43); /* Cor de fundo */
            padding: 20px; /* Espaçamento interno */
            margin: 20px auto; /* Centraliza horizontalmente */
            text-align: center; /* Alinha o conteúdo ao centro */
        }



        /* O body será um contêiner flexbox */
        body {
            display: flex;
            flex-direction: column; /* Alinha os elementos verticalmente */
            justify-content: center; /* Centraliza horizontalmente */
            align-items: center; /* Centraliza verticalmente */
            height: 100vh; /* A altura do body será 100% da altura da viewport */
            margin: 0; /* Remove a margem padrão do body */
        }

        h1 {
            font-family: 'Courier New', Courier, monospace;
            font-size: 3em;
            color: rgb(255, 255, 255);
            opacity: 0; /* Começa invisível */
            transform: translateY(-100%); /* Começa fora da tela, acima */
            transition: opacity 1.5s ease, transform 1.5s ease; /* Transições suaves */
            margin: 0;
            position: absolute;
            top: 20px; /* Posição inicial fora do centro da tela */
            left: 50%; /* Centraliza horizontalmente com relação à largura da tela */
            transform: translate(-50%, -100%); /* Corrige o alinhamento horizontal e inicia fora da tela */
        }
        body {
            background-color: rgb(56, 56, 56); /* Cor de fundo do site */
            margin: 0;
            padding: 0;
        }
        /* Quando a página carrega, o H1 vai aparecer */
        body.loaded h1 {
            opacity: 1; /* Totalmente visível */
            transform: translate(-50%, 0); /* Desce para a posição final */
        }
    </style>
</head>
<body>
    <div class="rectangle">
        <h1>Operação Matemática,<br> com operações do Python</h1>
        <br><br><br><br><br>
        <form action="/button" method="POST">
            <p><tt>Digita o primeiro valor: </tt></p>
            <input type="number" placeholder="1º número" name="numero1" required />
            
            <p><tt>Digita o segundo valor:</tt></p>
            <input type="number" placeholder="2º número" name="numero2" required />
            
            <p><tt>Digita a operação (+, -, //, /, ...)</tt></p>
            <input type="text" placeholder="operação" name="operacao" required />
            
            <br><br>
            <input type="submit" value="Enviar">
        </form>
        {% if resultado %}
        <br><br>
        <p><tt>Resultado da operação: {{ resultado }}</tt></p>
        {% endif %}


        <br>
        <br>
        <a href="/código_fonte">código fonte >>></a>

    </div>

    <script>
        // Quando o conteúdo da página estiver carregado, adicionar a classe "loaded" ao body
        window.addEventListener('load', function() {
            document.body.classList.add('loaded');
        });
    </script>
    
</body>
</html>

```


Guarda seu arquivo html desta forma:

```bash
\templates
   codigo.html
   index.html
app.py
```

Básicamente com o html criei uma parte grafica depois eu criei uma lógica de conta