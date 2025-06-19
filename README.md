<div align="center">

# 🧠📚 Plataforma de Estudo com IA para Vestibulares

![](https://media.tenor.com/PefkNzNeTtoAAAAM/the-simpsons-bart-simpson.gif)

### 💡 É mais fácil aprender com tarefas práticas.

![Status](https://img.shields.io/badge/status-Em%20Desenvolvimento-yellow)

</div>

---

## 🎯 Objetivo

O ensino tradicional para vestibulares é **engessado, estressante e desatualizado**. Segundo a USP, **70% dos vestibulandos sofrem com ansiedade** causada por métodos ineficazes.

> 🎓 **Nossa proposta**: Usar **inteligência artificial** para criar uma plataforma que:
> - Gera questões sob medida para cada aluno
> - Corrige respostas com explicações detalhadas

---

## 🚀 Funcionalidades Principais

| 🔧 Funcionalidade               | ✅ Descrição                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| 🎯 Geração de Questões         | Adaptadas ao conteúdo, vestibular e nível do aluno                          |
| 🧠 Correção Inteligente        | Feedback detalhado sobre acertos e erros                                   |


---

## 🧰 Tecnologias Utilizadas

```python
- Java
- HTML
- Python

# Inteligência Artificial
- Gemini Google AI


```


# 🔐 Requisitos Funcionais

## 🧠 Geração e correção de questões por IA

## 🤖 Chatbot inteligente para suporte




# 💻 Códigos

## 🐍Python

```python

from flask import Flask, request, jsonify, render_template
from flask_cors import CORS
import google.generativeai as genai
import os

app = Flask(__name__)
CORS(app)

# Configure sua chave de API do Gemini
GOOGLE_API_KEY = "Insira Sua Chave de API"
print(os.environ)
genai.configure(api_key=GOOGLE_API_KEY)

# Selecione o modelo Gemini que você deseja usar
model = genai.GenerativeModel("gemini-2.0-flash")

gemini_disponivel = True if GOOGLE_API_KEY else False
if not gemini_disponivel:
    print("Erro: A variável de ambiente GOOGLE_API_KEY não está configurada.")
else:
    print("Chave de API do Gemini configurada com sucesso.")


@app.route('/')
def index():
    return render_template('index.html')


@app.route('/gerar_questao', methods=['POST'])
def gerar_questao_endpoint():
    data = request.get_json()
    materia = data.get('materia')
    unidade = data.get('unidade')
    dificuldade = data.get('dificuldade')
   
    if not all([materia, unidade, dificuldade]):
        return jsonify({'erro': 'Parâmetros incompletos'}), 400

    if gemini_disponivel:
        prompt = (
            f"Gere uma pergunta de múltipla escolha sobre {materia}, especificamente sobre o tema '{unidade}', com um nível de dificuldade {dificuldade}. "
            f"A pergunta deve ter quatro opções (A, B, C, D) e indicar a resposta correta. "
            f"Formate a resposta da seguinte maneira:\n\n"
            f"Pergunta: [texto da pergunta]\n"

            f"A) [opção A]\n"

            f"B) [opção B]\n"

            f"C) [opção C]\n"

            f"D) [opção D]\n"

            f"Resposta correta: [Letra da opção correta] Explicação:"
        )

        try:
            response = model.generate_content(prompt)
            texto_gerado = response.text.strip()
            print(f"Questão gerada pelo Gemini:\n{texto_gerado}")
            return jsonify({'questao': texto_gerado})

        except Exception as e:
            erro = f"Erro ao gerar a questão com o Gemini: {e}"
            print(f"Detalhes do erro do Gemini: {e}")
            return jsonify({'erro': 'Ocorreu um erro ao gerar a questão com o Gemini.'}), 500
    else:
        return jsonify({'erro': e}), 503


if __name__ == "__main__":
    app.run(debug=True)
```
## ☕Java
```java

async function buscarQuestao() {
    const materiaSelecionada = document.getElementById('materia').value;
    const unidadeSelecionada = document.getElementById('unidade').value;
    const dificuldadeSelecionada = document.getElementById('dificuldade').value;

    if (!unidadeSelecionada.trim()) {
        alert('Por favor, insira a unidade da matéria.');
        return;
    }

    const data = {
        materia: materiaSelecionada,
        unidade: unidadeSelecionada,
        dificuldade: dificuldadeSelecionada
    };

    try {
        const response = await fetch('/gerar_questao', { // Rota para a API
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        });

        if (!response.ok) {
            throw new Error(`Erro HTTP! Status: ${response.status}`);
        }

        const result = await response.json();
        // Substitui as quebras de linha por <br>
        const questaoComBreaks = result.questao.replace(/\n/g, '<br>');
        document.getElementById('areaDaQuestao').innerHTML = `<p style="text-align: left; font-style: normal;">${questaoComBreaks}</p>`;

    } catch (error) {
        console.error('Erro ao buscar a questão:', error);
        document.getElementById('areaDaQuestao').textContent = 'Ocorreu um erro ao gerar a questão. Verifique a conexão com o servidor e se a API está rodando corretamente.';
    }
}

document.getElementById('gerarQuestao').addEventListener('click', buscarQuestao);

// ... (o restante do seu código JavaScript, como a animação de fundo e a lógica da explicação)
```
## 📟HTML
````html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Gerador de Questões</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
    <link href="https://fonts.googleapis.com/css2?family=Cal+Sans&display=swap" rel="stylesheet" />
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(45deg, #000080, #ADD8E6);
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 70px 20px 20px 20px;
            box-shadow: 10px 10px 40px #7ba6d8;
            overflow: hidden;
        }

        .top-bar {
            width: 100%;
            background-color: #363f8d;
            padding: 10px 20px;
            position: absolute;
            top: 0;
            left: 0;
            box-shadow: 0 10px 5px rgba(0, 0, 0, 0.3);
            display: flex;
            justify-content: space-between;
            align-items: center;
            text-decoration: none;
            z-index: 10;
        }

        .site-title {
            color: #ffffff;
            font-size: 1.4em;
            font-family: 'Cal Sans', sans-serif;
        }

        .top-right-img {
            height: 35px;
            width: auto;
        }

        .container {
            background-color: #225db6;
            border-radius: 8px;
            box-shadow: 20px 20px 20px 20px rgba(0, 0, 0, 0.4);
            padding: 30px;
            width: 100%;
            max-width: 600px;
            z-index: 10;
        }

        h1 {
            color: #ffffff;
            text-align: center;
            margin-bottom: 20px;
            z-index: 10;
        }

        form {
            margin-bottom: 20px;
            z-index: 10;
        }

        .form-group {
            margin-bottom: 15px;
            z-index: 10;
        }

        label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
            color: #e3f2fd;
            z-index: 10;
        }

        select, input {
            width: 100%;
            padding: 10px;
            border: 1px solid #7986cb;
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 1em;
            background-color: #e8eaf6;
            color: #212121;
            z-index: 10;
        }

        button {
            background-color: #192069;
            color: rgb(255, 255, 255);
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: block;
            width: 100%;
            font-size: 1em;
            transition: background-color 0.3s ease;
            z-index: 10;
        }

        button:hover {
            background-color: #7ba6d8;
        }

        #areaDaQuestao {
            border: 1px solid #7986cb;
            border-radius: 5px;
            padding: 15px;
            background-color: #e8eaf6;
            margin-top: 20px;
            font-size: 1.1em;
            color: #212121;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            z-index: 10;
        }

        #areaDaQuestao p {
            text-align: left;
            font-style: normal;
            z-index: 10;
        }

        canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            pointer-events: none;
        }

        /* Estilos para a barra de pesquisa */
        #search-container {
            position: absolute;
            top: 80px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 11;
            width: 70%; /* Largura um pouco menor */
            max-width: 500px; /* Largura máxima menor */
            display: flex;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        #search-input {
            flex: 1;
            padding: 8px; /* Padding menor */
            border: none;
            font-size: 0.9em; /* Fonte menor */
            border-radius: 8px 0 0 8px;
            outline: none;
            background-color: #fff; /* Cor de fundo branca */
            color: #212121;
        }

        #search-button {
            background-color: #363f8d;
            color: #fff;
            padding: 8px 12px; /* Padding menor */
            border: none;
            font-size: 0.9em; /* Fonte menor */
            border-radius: 0 8px 8px 0;
            cursor: pointer;
            transition: background-color 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #search-button:hover {
            background-color: #2a4080;
        }

        #search-button img {
            height: 18px; /* Altura do ícone menor */
            width: auto;
        }

        /* Estilos para o texto de explicação */
        #explanacao-container {
            position: absolute;
            top: 120px; /* Ajuste a posição para ficar mais perto da barra de pesquisa */
            left: 50%;
            transform: translateX(-50%);
            z-index: 11;
            background-color: rgba(0, 0, 0, 0.8);
            border-radius: 8px;
            padding: 15px; /* Padding menor */
            color: #fff;
            width: 70%; /* Largura menor */
            max-width: 500px; /* Largura máxima menor */
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease, visibility 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }

        #explanacao-container.mostrar {
            opacity: 1;
            visibility: visible;
        }

        #explanacao-container h2 {
            font-size: 1em; /* Fonte menor */
            margin-bottom: 8px; /* Margem menor */
            font-weight: bold;
        }

        #explanacao-container p {
            font-size: 0.8em; /* Fonte menor */
            line-height: 1.4; /* Espaçamento entre linhas menor */
        }

        @media (max-width: 640px) {
            .container {
                padding: 15px;
            }

            select, input, button {
                font-size: 16px;
            }

            #search-container {
                width: 95%;
            }

            #explanacao-container {
                width: 95%;
                padding: 10px; /* Padding menor em telas pequenas */
            }
        }
    </style>
</head>
<body>
    <canvas id="backgroundCanvas"></canvas>
    <a href="/" class="top-bar">
        <span class="site-title">Estud-AI</span>
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/1024px-React-icon.svg.png" alt="Ícone" class="top-right-img" />
    </a>

    <div id="search-container">
        <input type="text" id="search-input" placeholder="Pesquisar funcionamento do site..." />
        <button id="search-button">
            <img src="https://cdn-icons-png.flaticon.com/512/622/622669.png" alt="Pesquisar" />
        </button>
    </div>

    <div id="explanacao-container">
        <h2>Bem-vindo ao Gerador de Questões Estud-AI!</h2>
        <p>
            Este site foi desenvolvido para auxiliar estudantes e educadores na criação de questões personalizadas.
            Você pode selecionar a matéria, a unidade e a dificuldade desejada, e o site irá gerar uma questão para você.
            As questões são geradas de forma dinâmica, com o objetivo de fornecer um material de estudo eficiente e
            adaptado às suas necessidades. No momento, o site exibe questões simuladas.
        </p>
        <p>
            Utilize a barra de pesquisa acima para saber mais sobre o funcionamento do site.
        </p>
    </div>

    <div class="container">
        <h1>Gerador de Questões</h1>
        <form id="questionForm">
            <div class="form-group">
                <label for="materia">Matéria:</label>
                <select id="materia">
                    <option value="matematica">Matemática</option>
                    <option value="historia">História</option>
                    <option value="biologia">Biologia</option>
                    <option value="portugues">Português</option>
                    <option value="geografia">Geografia</option>
                    <option value="quimica">Química</option>
                    <option value="fisica">Física</option>
                </select>
            </div>
            <div class="form-group">
                <label for="unidade">Unidade:</label>
                <input type="text" id="unidade" placeholder="Ex: Revolução Francesa, Cálculo I, Sistema Nervoso" />
            </div>
            <div class="form-group">
                <label for="dificuldade">Dificuldade:</label>
                <select id="dificuldade">
                    <option value="facil">Fácil</option>
                    <option value="medio">Médio</option>
                    <option value="dificil">Difícil</option>
                </select>
            </div>
            <button type="button" id="gerarQuestao">Gerar Questão</button>
        </form>
        <div id="areaDaQuestao">
            <p>A questão gerada aparecerá aqui...</p>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('backgroundCanvas');
        const ctx = canvas.getContext('2d');
        let width = window.innerWidth;
        let height = window.innerHeight;
        canvas.width = width;
        canvas.height = height;

        const particles = [];
        const particleCount = 75;
        const letters = "abcdefghijklmnopqrstuvwxyzçãõúéíóáàüqwertyuiopasdfghjklzxcvbnm";
        const formulasQuimica = ["H₂O", "CO₂", "O₂", "NaCl", "C₆H₁₂O₆", "NH₃", "H₂SO₄", "HCl"];
        const formulasMatematica = ["E=mc²", "πr²", "F=ma", "PV=nRT", "ΔS = Q/T", "y=ax+b", "a²+b²=c²"];
        const elementosTabelaPeriodica = ["H", "He", "C", "N", "O", "Na", "Mg", "Al", "Si", "P", "S", "Cl", "K", "Ca", "Fe", "Cu", "Zn", "Br", "Ag", "Au"];
        const numeros = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"];
        const cells = ["🦠", "🧬", "🔬", "🧪", "🧫", "🧰"];
        const allSymbols = [...letters, ...formulasQuimica, ...formulasMatematica, ...elementosTabelaPeriodica, ...numeros, ...cells];


        function createParticle() {
            const symbol = allSymbols[Math.floor(Math.random() * allSymbols.length)];
            return {
                x: Math.random() * width,
                y: Math.random() * height,
                size: Math.random() * 25 + 12,
                speedX: (Math.random() - 0.5) * 0.7,
                speedY: (Math.random() - 0.5) * 0.7,
                symbol: symbol,
                opacity: Math.random() * 0.7 + 0.3,
                color: `rgba(255, 255, 255, ${Math.random() * 0.5 + 0.5})`
            };
        }

        for (let i = 0; i < particleCount; i++) {
            particles.push(createParticle());
        }

        function drawParticle(particle) {
            ctx.font = `${particle.size}px sans-serif`;
            ctx.fillStyle = particle.color;
            ctx.shadowColor = particle.color;
            ctx.shadowBlur = Math.random() * 10 + 5;
            ctx.fillText(particle.symbol, particle.x, particle.y);
            ctx.shadowBlur = 0;
        }

        function updateParticles() {
            for (const particle of particles) {
                particle.x += particle.speedX;
                particle.y += particle.speedY;

                if (particle.x < -particle.size) particle.x = width + particle.size;
                if (particle.x > width + particle.size) particle.x = -particle.size;
                if (particle.y < -particle.size) particle.y = height + particle.size;
                if (particle.y > height + particle.size) particle.y = -particle.size;
            }
        }

        function animate() {
            ctx.clearRect(0, 0, width, height);
            for (const particle of particles) {
                drawParticle(particle);
            }
            updateParticles();
            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', () => {
            width = window.innerWidth;
            height = window.innerHeight;
            canvas.width = width;
            canvas.height = height;
        });

        animate();

        // Lógica para mostrar/esconder a explicação
        const searchInput = document.getElementById('search-input');
        const explicacaoContainer = document.getElementById('explanacao-container');

        searchInput.addEventListener('focus', () => {
            explicacaoContainer.classList.add('mostrar');
        });

        searchInput.addEventListener('blur', () => {
            explicacaoContainer.classList.remove('mostrar');
        });

        // Adiciona evento de clique ao botão de pesquisa para garantir que a explicação apareça também
        const searchButton = document.getElementById('search-button');
        searchButton.addEventListener('click', () => {
            explicacaoContainer.classList.add('mostrar');
            searchInput.focus();
        });
    </script>

</body>
<script src="../static/script.js"></script>
</html>
