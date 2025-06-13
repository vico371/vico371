# 👋 Olá! Eu sou o Vicente 

🎯 Desenvolvedor em formação com interesse em tecnologia aplicada às ciências humanas.  
📍 Novo Hamburgo, RS, Brasil.  
💼 Experiência na área da saúde e transição para o desenvolvimento de sistemas.

## 🛠️ Habilidades

- **Linguagens**: Python, HTML, CSS, JavaScript  
- **Ferramentas**: Git, GitHub, Selenium WebDriver  
- **Interesses**: Desenvolvimento de sistemas voltados para a área da saúde, automação de testes, interfaces web.

## 📂 Projetos em Destaque

- [Atividades-Selenium](https://github.com/vico371/Atividades-Selenium): Testes automatizados utilizando Selenium WebDriver em Python.  
- [PersonalWebsite](https://github.com/vico371/PersonalWebsite): Site pessoal com informações e portfólio.

## 📫 Contato

- [LinkedIn](https://www.linkedin.com/in/vicente-de-souza-146b4527a/)  
- Email: vicentedesouza.com

---

🧠 Sempre aprendendo e buscando evoluir na interseção entre tecnologia e ciências humanas.
<!-- index.html -->
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <title>Jogo da Cobrinha</title>
  <style>
    body { display: flex; justify-content: center; margin-top: 30px; }
    canvas { background: #000; display: block; }
  </style>
</head>
<body>
  <canvas id="game" width="400" height="400"></canvas>

  <script>
    const canvas = document.getElementById('game');
    const ctx = canvas.getContext('2d');

    const scale = 20;
    const rows = canvas.height / scale;
    const cols = canvas.width / scale;

    let snake;
    let food;

    (function setup() {
      snake = new Snake();
      food = randomFood();
      window.setInterval(() => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        snake.update();
        snake.draw();

        if (snake.eat(food)) {
          food = randomFood();
        }

        ctx.fillStyle = "red";
        ctx.fillRect(food.x, food.y, scale, scale);

      }, 100);
    })();

    function randomFood() {
      return {
        x: Math.floor(Math.random() * cols) * scale,
        y: Math.floor(Math.random() * rows) * scale
      };
    }

    window.addEventListener('keydown', e => {
      const direction = e.key.replace('Arrow', '');
      snake.changeDirection(direction);
    });

    function Snake() {
      this.x = 0;
      this.y = 0;
      this.xSpeed = scale * 1;
      this.ySpeed = 0;
      this.total = 0;
      this.tail = [];

      this.draw = function() {
        ctx.fillStyle = "#00FF00";

        for (let i=0; i < this.tail.length; i++) {
          ctx.fillRect(this.tail[i].x, this.tail[i].y, scale, scale);
        }

        ctx.fillRect(this.x, this.y, scale, scale);
      };

      this.update = function() {
        for (let i=0; i < this.tail.length - 1; i++) {
          this.tail[i] = this.tail[i + 1];
        }

        this.tail[this.total - 1] = { x: this.x, y: this.y };

        this.x += this.xSpeed;
        this.y += this.ySpeed;

        // colisão com as bordas (teleporte para o lado oposto)
        if (this.x >= canvas.width) this.x = 0;
        if (this.y >= canvas.height) this.y = 0;
        if (this.x < 0) this.x = canvas.width - scale;
        if (this.y < 0) this.y = canvas.height - scale;
      };

      this.changeDirection = function(direction) {
        switch(direction) {
          case 'Up':
            if (this.ySpeed === 0) {
              this.xSpeed = 0;
              this.ySpeed = -scale;
            }
            break;
          case 'Down':
            if (this.ySpeed === 0) {
              this.xSpeed = 0;
              this.ySpeed = scale;
            }
            break;
          case 'Left':
            if (this.xSpeed === 0) {
              this.xSpeed = -scale;
              this.ySpeed = 0;
            }
            break;
          case 'Right':
            if (this.xSpeed === 0) {
              this.xSpeed = scale;
              this.ySpeed = 0;
            }
            break;
        }
      };

      this.eat = function(food) {
        if (this.x === food.x && this.y === food.y) {
          this.total++;
          return true;
        }
        return false;
      };
    }
  </script>
</body>
</html>
