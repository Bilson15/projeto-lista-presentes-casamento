<template>
  <div class="main">
  <div class="offcanvas offcanvas-bottom show" tabindex="-1" id="offcanvasBottom" aria-labelledby="offcanvasBottomLabel" >
    <div class="offcanvas-header">
      <h5 class="offcanvas-title" id="offcanvasBottomLabel">Instruções e dicas de uso</h5>
      <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
    </div>
    <div class="offcanvas-body small" id="canvas">
      <p class="dicas">
        <b>Seja Bem-vindo(a)</b><br>
        <b>Dica de confirmação:</b> confirmar sua presença, basta clicar no menu a cima e clicar em confimar sua presença, você irá direto para o campo de confirmação.
        basta digitar os nomes e confirmar, lembrando que só pode confirmar uma vez<br>
      </p>
      <p class="dicas">
        <b>Dica de escolha do presente:</b> Ao decidir qual presente quer nos dá, basta clicar no ícone de presente ao lado do nome do presente, irá solicitar uma confirmação. basta confirmar e pronto.
        caso queira trocar de presente basta clicar em qualquer presente e confirmar que deseja trocar e logo em seguida será habilitado para escolha de um novo presente.
      </p>

      <p class="dicas">
        <b>Desde já conto com você lá, muito obrigado &#128150;</b>
      </p>

      <h4 class="casal">Gabriel & Dalila</h4>
    </div>
  </div>

    <NavBar id="nav" class="nav-bar"/>
    <h1 class="titulo" id="inicio-lista">Lista de Presentes</h1>
    <a href="#top"><img src="./assets/arrow-up-circle.svg" alt="topo" id="icon-topo" class="icon-topo"></a> 

    <div class="conjunto-pre-cat">
      <div class="categoria">
        <h4 id="cozinha">Cozinha</h4>
      </div>
      <Load v-if="loading"/>
      <div v-else class="card-presente" v-bind:key="presente.id" v-for="presente in presentes">
        <div v-if="presente.categoria === 'cozinha'">
            <CardPresente 
              :presente="presente.name" 
              :qtd="presente.qtd" 
              :categoria="presente.categoria"
              :id="presente.id"
            /> 
        </div>
      </div>
    </div>

    <div class="conjunto-pre-cat">
      <div class="categoria">
        <h4 id="salaquarto">Sala e Quarto</h4>
      </div>
      <Load v-if="loading"/>
      <div v-else class="card-presente" v-bind:key="presente.id" v-for="presente in presentes">
        <div v-if="presente.categoria === 'salaquarto'">
            <CardPresente 
              :presente="presente.name" 
              :qtd="presente.qtd" 
              :categoria="presente.categoria"
              :id="presente.id"
            /> 
        </div>
      </div>
    </div>
    <div class="conjunto-pre-cat">
      <div class="categoria">
        <h4 id="banheiro">Banheiro</h4>
      </div>
      <Load v-if="loading"/>
      <div v-else class="card-presente" v-bind:key="presente.id" v-for="presente in presentes">
        <div v-if="presente.categoria === 'banheiro'">
            <CardPresente 
              :presente="presente.name" 
              :qtd="presente.qtd" 
              :categoria="presente.categoria"
              :id="presente.id"
            /> 
        </div>
      </div>
    </div>

    <div class="conjunto-pre-cat">
      <div class="categoria">
        <h4 id="utensilios">Utensílios Domésticos</h4>
      </div>
      <Load v-if="loading"/>
      <div v-else class="card-presente" v-bind:key="presente.id" v-for="presente in presentes">
        <div v-if="presente.categoria === 'utensilios'">
            <CardPresente 
              :presente="presente.name" 
              :qtd="presente.qtd" 
              :categoria="presente.categoria"
              :id="presente.id"
            /> 
        </div>
      </div>
    </div>
    <div class="foooter">
      <FooterConfirm />
    </div>
    <p class="dev">Developed by Bilson</p>
  </div>
   
</template>

<script>
import NavBar from './components/NavBar.vue'
import CardPresente from './components/CardPresente.vue'
import FooterConfirm from './components/FooterConfirm.vue'
import Load from './components/Load.vue'

export default {
  data: () => {
    return {
      presentes: [],
      loading: true
    };
  },
  name: 'App',
  components: {
    NavBar,
    CardPresente,
    FooterConfirm,
    Load
  },

  mounted() {
    document.addEventListener('scroll', this.onScroll);
  },

  methods: {
    onScroll: () => {
      if (document.documentElement.scrollTop > 100) {
          document.getElementById("icon-topo").style.display = "inline";
          document.getElementById("icon-topo").style.transform = "translateX(-20px)";
          document.getElementById("icon-topo").style.transition = "transform 0.5s";
      } else {
          document.getElementById("icon-topo").style.transition = "transform 2s";
          document.getElementById("icon-topo").style.transform = "translateX(10px)";
          document.getElementById("icon-topo").style.display = "none";
      } 
    }
  },
  created() {
    fetch("https://6143926cc5b553001717d00e.mockapi.io/produto")
      .then((response) => response.json())
      .then((json) => {
        this.presentes = json;
      })
      .finally( () => this.loading = false)
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Mono:wght@300&family=Open+Sans&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
}

#canvas > p {
  font-family: 'Open Sans', sans-serif;
}

.offcanvas {
  height: 35vh;
}
.offcanvas-body{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.dicas{
  width: 500px;
}

body {
  text-align: center;
  margin-top: 15px;
  margin-bottom: 15px;
}

.main {
  overflow: scroll;
}

.nav-bar {
  font-family: 'Open Sans', sans-serif;
  position: fixed;
  width: 100%;
  z-index: 1;
}

.titulo {
  margin-top: 75px;
  margin-bottom: 25px;
  font-family: 'Pacifico', cursive;
  background: #ff6f9c;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-size: 2.5rem;
}
.casal{
  font-family: 'Pacifico', cursive;
  background: #ff6f9c;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-size: 1.5rem;
  height: 100%;
  padding-bottom: 10px;
}

.icon-topo {
  position: fixed;
  width: 50px;
  height: 50px;
  right: 30px;
  bottom: 35px;
  border-radius: 25px;
  z-index: 1;
  display: none;
  background-image: linear-gradient(to bottom, #ffcbdb,#f9d2de, #f3d8e1,  #eddfe3, #e7e5e6, #e0ece9, #d8f2ec);
  cursor: pointer;
}
.dev {
  position: absolute;
  font-family: 'Open Sans', sans-serif;
  left: 43%;
  font-size: 0.8em;
}

.card-presente{
  display: flex;
  flex-direction: column;
  align-items: center;
}

.foooter {
  font-family: 'Open Sans', sans-serif;
  position: relative;
  z-index: 2;
}

.categoria {
  display: flex;
  font-family: 'Open Sans', sans-serif;
  border-bottom: #ff6f9c 1px solid;
  width: 500px;
  margin-bottom: 15px;
  
  justify-items: center;
  justify-content: center;
}

.conjunto-pre-cat{
  display: flex;
  flex-direction: column;
  align-content: center;
  align-items: center;
}

@media(max-width: 500px){
    .icon-topo {
      right: 5px;
      bottom: 20px;
      width: 40px;
      height: 40px;
    }
    .categoria {
      width: 90vw;
    }
    .dev {
      left: 32%;
    }
    .offcanvas {
      height: 85vh;
    }

    .dicas{
      width: 90%;
    }
}

</style>
