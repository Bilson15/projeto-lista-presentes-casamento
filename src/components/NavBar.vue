<template>
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  
  <div class="container-fluid">
    <a v-on:click="navs" class="navbar-brand" href="#">Seja Bem-vindo(a)</a>
    <button v-on:click="navsButton" class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a v-on:click="navs" class="nav-link active" href="#top" data-toggle="collapse" role="button" aria-expanded="true" aria-controls="collapse">Início</a>
        </li>
        <li class="nav-item">
          <a v-on:click="navs" class="nav-link" href="#foo">Confirme sua presença</a>
        </li>
        <li class="nav-item dropdown">
          <a v-on:click="dropdown" class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Categorias
          </a>
          <ul class="dropdown-menu bg-dark" aria-labelledby="navbarDropdown">
            <li><a v-on:click="navs" class="dropdown-item" href="#cozinha">Cozinha</a></li>
            <li><a v-on:click="navs" class="dropdown-item" href="#salaquarto">Sala e quarto</a></li>
            <li><a v-on:click="navs" class="dropdown-item" href="#banheiro">Banheiro</a></li>
            <li><a v-on:click="navs" class="dropdown-item" href="#utensilios">Utensílios Domésticos</a></li>
          </ul>
        </li>
      </ul>

    </div>
  </div>

  
</nav>
</template>

<script>

export default({

  methods: {
    navs: () => {
        $('#navbarNav').collapse('hide');
    },
    navsButton: () => {
      $('.nav-item').collapse('toggle');
    },
    dropdown: () => {
      $('.dropdown-menu').collapse('toggle');
    }
  }
})
</script>

<style scoped>
  .container-fluid {
    background-image: #ff6f9c;
  }

  .navv{
    align-items: center;
    align-content: center;
    justify-content: center;
  }

  a {
    color: white;
  }

  .dropdown-menu > li > a:hover{
      background-color: #ff6f9c;
  }
</style>
