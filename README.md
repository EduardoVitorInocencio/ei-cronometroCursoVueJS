Perfeito! Aqui está a documentação completa e exata do seu código, já incluindo instruções para clonar o repositório e executar o projeto localmente.

---

# Documentação do Projeto Cronômetro (Estudos sobre Vue.Js)

---

## Visão Geral

Cronômetro digital simples construído com **Vue 3** e **Vite**, exibindo o tempo no formato `MM:SS,CC`, com botões para iniciar/parar e limpar o tempo.

---

## Como Clonar e Executar o Projeto

### 1. Clonar o repositório

```bash
git clone https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
cd SEU_REPOSITORIO
```

(Substitua `SEU_USUARIO` e `SEU_REPOSITORIO` pela URL correta do seu repositório.)

### 2. Instalar dependências

```bash
npm install
```

### 3. Rodar o servidor de desenvolvimento

```bash
npm run dev
```

Abra no navegador o endereço mostrado no terminal, normalmente `http://localhost:3000`.

---

## Estrutura do Código

---

### Template (HTML + Vue)

```vue
<template>
  <div id="app">

    <img src="./assets/cronometro.png" class="img">
    <a class="timer">{{ tempoFormatado }}</a>

    <div class="areaBtn">
      <button 
        class="botao" 
        id="btnGo" 
        :class="{ stop: botao === 'STOP' }"
        @click="start"
      > 
        {{ botao }}
      </button>

      <button 
        class="botao" 
        id="btnClear"
        @click="clear"
      >
        CLEAR
      </button>
    </div>

  </div>
</template>
```

* Imagem estática do cronômetro.
* Mostra o tempo formatado com reatividade.
* Botão `GO/STOP` para iniciar/parar o cronômetro, altera classe para cor laranja no estado `STOP`.
* Botão `CLEAR` para zerar o tempo.

---

### Script (JavaScript)

```js
export default {
  name: 'App',
  data(){
    return {
      numero: 0,          // variável não usada no momento
      botao: "GO",        // texto atual do botão principal
      time: 0,            // tempo acumulado em milissegundos
      crono: null,        // referência do setInterval do cronômetro
      run: false          // flag que indica se o cronômetro está rodando
    }
  },
  computed: {
    tempoFormatado() {
      const totalCent = Math.floor(this.time / 10);
      const cent = String(totalCent % 100).padStart(2, '0');
      const seg = String(Math.floor(this.time / 1000) % 60).padStart(2, '0');
      const min = String(Math.floor(this.time / 60000)).padStart(2, '0');
      return `${min}:${seg},${cent}`;
    }
  },
  methods: {
    start() {
      if (this.botao === "GO") {
        this.botao = "STOP";
        this.run = true;
        this.crono = setInterval(() => {
          this.time += 10;
        }, 10);
      } else {
        this.botao = "GO";
        this.run = false;
        clearInterval(this.crono);
        this.crono = null;
      }
    },
    clear(){
      this.time = 0;
      this.botao = "GO";
      this.run = false;
      clearInterval(this.crono);
      this.crono = null;
    }
  }
};
```

* `data()` retorna o estado inicial com o tempo zerado e botão com texto `GO`.
* `tempoFormatado`: calcula a string formatada `MM:SS,CC` com base no tempo acumulado.
* `start()`: inicia ou pausa o cronômetro, alterando o texto do botão e controlando o `setInterval`.
* `clear()`: zera o tempo, reseta estado e limpa o intervalo.

---

### CSS (Estilos)

```css
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
}

.img {
  width: 600px;
  height: 600px;
  padding-top: 100px;
}

.timer {
  font-family: 'Courier New', Courier, monospace;
  font-size: 50px;
  font-weight: 600;
  margin-top: -330px;
}

.areaBtn {
  margin-top: 255px;
}

.botao {
  width: 150px;
  height: 50px;
  font-size: 15px;
  font-weight: bold;
  margin: 0 15px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  background-color: #f0f0f0;
}

#btnGo {
  color: #fff;
  background-color: #45bb57;
}

#btnGo.stop {
  background-color: #e67e22;
}

#btnClear {
  color: #fff;
  background-color: #f44336;
}

.botao:hover {
  background-color: #d0d0d0;
  transition: 0.25s 0.5s;
}

#btnGo:hover {
  background-color: #3a9f4a;
}

#btnClear:hover {
  background-color: #c62828;
}
```

* Estilo para container, imagem, texto e botões.
* Botão GO verde, botão STOP laranja (classe `.stop`).
* Botão CLEAR vermelho.
* Transições suaves em hover.

