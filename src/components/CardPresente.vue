<template>
    <div class="card">
    <div class="card-body">
        <h5 class="card-title">{{presente}}</h5>
    </div>
    <div>
        <a class="btnn" v-on:click="escolhido"><img class="icon-presente" src="../assets/gift.svg" alt="Quero presentear com esse!"></a>
    </div>
    </div>
</template>

<script>

export default {
    data: function() {
        return  {
            quantidade: this.qtd,
            nome: this.presente,
            category: this.categoria,
            idp: this.id
        }
    },
    methods: {
        escolhido: function() {
         let jsonPresente = JSON.parse(localStorage.getItem('presenteApp'));
            if(jsonPresente) {
                swal (`Você já escolheu o presente "${jsonPresente.nome}", deseja trocar ?`, { 
                buttons: {
                    cancel: "Cancelar",
                    Confimar: true,
                },
                })
                .then((value) => {
                switch (value) {
                    case "Confimar":
                        this.quantidade += 1;
                        this.updatedNovaEscolha(jsonPresente.id);
                    break;
                
                    case "cancel":
                        console.log('vai escolher outro');
                    break;
                
                    default:
                }
                });  
            }else {
                swal ( `${this.palavraMagica()} posso registrar ?`, { 
                buttons: {
                    cancel: "Cancelar",
                    Confimar: true,
                },
                })
                .then((value) => {
                switch (value) {
                    case "Confimar":
                        if(this.quantidade > 0){
                            this.quantidade -= 1;
                            this.updated();
                            localStorage.setItem('presenteApp', JSON.stringify({id: this.id, nome:this.nome}));
                        }else{
                            swal("Esse produto já escolheram a quantidade que desejamos, fique a vontade para escolher outro ou talvez um que não esteja na lista ;)");
                        }
                    break;
                
                    case "cancel":
                        console.log('vai escolher outro');
                    break;
                
                    default:
                }
                });
            }


        },

        palavraMagica() {
            var palavras = ['Arassou!','Boa escolha! ', 'Aí simmm!', 'Escolha top!!','Boaaaa!!'];
            return palavras[Math.floor(Math.random() * palavras.length)];
        },
        updated() {
            fetch("https://6143926cc5b553001717d00e.mockapi.io/produto/" + this.idp, {
            method: "PUT",
            body: JSON.stringify({ 
                name: this.nome,
                qtd: this.quantidade,
                categoria: this.category,
            }),
            headers: { "Content-Type": "application/json; charset=UTF-8" },
            })
            .then(response => response.json())
            .then(data => swal("S2", "Muito obrigado!!", "success"));
        },
        updatedNovaEscolha(idp) {
            fetch("https://6143926cc5b553001717d00e.mockapi.io/produto/" + idp, {
            method: "PUT",
            body: JSON.stringify({ 
                qtd: this.quantidade,
            }),
            headers: { "Content-Type": "application/json; charset=UTF-8" },
            })
            .then(response => response.json())
            .then(localStorage.removeItem('presenteApp'))
            .then(data => swal("S2", "Fique a vontade para escolher outro :D !!", "success"));
        }  
    },

    props: {
        presente: String,
        qtd: Number,
        categoria: String,
        id: String
    }
}
</script>

<style scoped>
    .card {
        display: flex;
        border: 1px solid var(--bg-rosa-padrao);
        border-radius: 15px;
        margin: 15px;
        width: 500px;
        height: 70px;
        color: var(--bg-fonte);
        background-image: var(--bg-card);
        flex-direction: row;
        justify-content: space-around;
        justify-items: center;
        align-content: center;
        align-items: center;
    }
    .btnn {
        display: flex;
        background: var(--bg-rosa-padrao);
        text-decoration: none;
        color: white;
        height: 70px;
        width: 105%;
        border-radius: 0px 14px 14px 0px;
        align-items: center;
        cursor: pointer;
    }
    .card-body {
        width: 110%;
    }

    .card-title {
        font-size: 1em;
        margin: 0;
    }

    img {
        margin: 25px;
        width: 35px;
        height: 35px;
    }

    .icon-presente{
        filter: var(--bg-card-icon);
    }


    @media(max-width: 500px){
    .card {
        margin: 15px;
        width: 90vw;
        height: 70px;
    }


    .card-body {
        margin: 5px;
        width: 110%;
    }

   }

</style>
