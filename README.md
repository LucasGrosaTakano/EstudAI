<div align="center">

# 🧠📚 Plataforma de Estudo com IA para Vestibulares

![](https://media.tenor.com/PefkNzNeTtoAAAAM/the-simpsons-bart-simpson.gif)

### 💡 Estude de forma inteligente com tecnologia de ponta e uma abordagem totalmente personalizada.

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![Status](https://img.shields.io/badge/status-Em%20Desenvolvimento-yellow)
![Plataforma](https://img.shields.io/badge/plataforma-Web%20e%20Mobile-00c853)

</div>

---

## 🎯 Objetivo

O ensino tradicional para vestibulares é **engessado, estressante e desatualizado**. Segundo a USP, **70% dos vestibulandos sofrem com ansiedade** causada por métodos ineficazes.

> 🎓 **Nossa proposta**: Usar **inteligência artificial** para criar uma plataforma que:
> - Gera questões sob medida para cada aluno
> - Corrige respostas com explicações detalhadas
> - Fornece relatórios de progresso
> - Oferece um verdadeiro **tutor digital** que aprende com o aluno

---

## 🚀 Funcionalidades Principais

| 🔧 Funcionalidade               | ✅ Descrição                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| 🎯 Geração de Questões         | Adaptadas ao conteúdo, vestibular e nível do aluno                          |
| 📈 Relatórios Personalizados   | Com gráficos de desempenho e recomendações de estudo                        |
| 💬 Chat com IA                 | Esclarece dúvidas, ensina conteúdos e orienta a preparação                  |
| 🧠 Correção Inteligente        | Feedback detalhado sobre acertos e erros                                   |
| 📚 Biblioteca de Materiais     | Acesso rápido a conteúdos filtrados por tema e tipo de exame               |
| 🔐 Login Seguro                | Autenticação via e-mail e recuperação de senha                             |

---

## 🧰 Tecnologias Utilizadas

```python
# Backend
- Python + FastAPI
- Node.js
- PostgreSQL + MongoDB

# Inteligência Artificial
- OpenAI GPT-4
- IBM Watson

# Frontend
- React.js (Web)
- Flutter (Mobile)

# Infraestrutura
- AWS ou Azure
```


# 🔐 Requisitos
# Funcionais
## 🔑 Autenticação com conta e e-mail

## 🧠 Geração e correção de questões por IA

## 📈 Painel de progresso com insights

## 🗂️ Acesso a materiais atualizados

## 🤖 Chatbot inteligente para suporte

# Não Funcionais
## 📱 Compatível com mobile e web

## ⚡ Alta performance com muitos usuários

## 🔒 Proteção de dados pessoais (LGPD/GDPR)

## 📊 Exemplo de Relatório Gerado
```python
text
Copiar
Editar
Aluno: João da Silva
Exame: ENEM
Pontos fortes: Biologia, História
Necessita reforço: Matemática, Física

Recomendação:
  - Refaça exercícios de cinemática
  - Estude progressões aritméticas
  - Veja vídeo: "Como interpretar gráficos no ENEM"

📈 Diferenciais

✅ Inteligência Artificial de última geração
✅ 100% personalizável para o aluno
✅ Relatórios pedagógicos de verdade
✅ Design acessível e interface inclusiva
✅ Equipe de educadores validando o conteúdo
```
# 💻 Códigos
## 🐍Python
´´´python

python

from flask import Flask, request, jsonify, render_template
from flask_cors import CORS
import google.generativeai as genai
import os

app = Flask(__name__)
CORS(app)

# Configure sua chave de API do Gemini
GOOGLE_API_KEY = "AIzaSyBZd8MDuFNpqxOfcFXJOh4TnE3RF0tppYA"
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
