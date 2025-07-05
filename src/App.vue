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

<script>

  export default {
    name: 'App',
    data(){
      return {
        numero: 0,
        botao: "GO",
        time: 0,
        crono: null,
        run: false
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
            // Inicia o cronômetro
            this.crono = setInterval(() => {
              this.time += 10; // incrementa de 10 em 10 milissegundos
            }, 10);

          } else {

            this.botao = "GO";
            this.run = false;
            // Para o cronômetro
            clearInterval(this.crono);
            this.crono = null;
            
          }
        },
        clear(){
          this.time = 0;
          this.botao = "GO";
          this.run = false;
          clearInterval(this.crono);
        }
    }
  };

</script>


<style>
  #app{
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .img{
    width: 600px;
    height: 600px;
    padding-top: 100px;
  }

  .timer{
    font-size: 50px;
    font-weight: 600;
    margin-top: -330px;
    font-family: 'Courier New', Courier, monospace;
    
  }

  .areaBtn{
    margin-top: 255px;
  }

  .botao{
    width: 150px;
    height: 50px;
    font-size: 15px;
    font-weight: bold;
    margin-left: 15px;
    margin-right: 15px;
    border-radius: 10px;
    background-color: #f0f0f0;
    border: none;
    cursor: pointer;
  }

  #btnGo{
    color: #fff;
    background-color: #45bb57;
  }

  #btnGo.go {
  background-color: #45bb57; /* Cor quando pressionado */
  }

  #btnGo.stop {
  background-color: #e67e22; /* cor laranja, por exemplo */
  }
  
  #btnClear{
    color: #fff;
    background-color: #f44336;
  }

  .botao:hover{
    background-color: #d0d0d0;
    transition: 0.25s 0.5s;
  }

  #btnGo:hover{
    background-color: #3a9f4a;
  }

  #btnClear:hover{
    background-color: #c62828;
  }

</style>
