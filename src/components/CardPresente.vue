<template>
    <div class="card">
    <div class="card-body">
        <h5 class="card-title">{{presente}}</h5>
    </div>
    <div>
        <a href="#" class="btnn" v-on:click="escolhido"><img class="icon-presente" src="../assets/gift.svg" alt="Quero presentear com esse!"></a>
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
                swal (`Você já escolheu o presente ${jsonPresente.nome}, deseja trocar ?`, { 
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
                swal ( "Boa escolha! posso registrar ?", { 
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
        border: 1px solid #ff6f9c;
        border-radius: 15px;
        margin: 15px;
        width: 500px;
        height: 70px;
        background-image: linear-gradient(to bottom, #ffcbdb,#f9d2de, #f3d8e1,  #eddfe3, #e7e5e6, #e0ece9, #d8f2ec);
        flex-direction: row;
        justify-content: space-around;
        justify-items: center;
        align-content: center;
        align-items: center;
    }
    .btnn {
        display: flex;
        background: #ff6f9c;
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
    }

    img {
        margin: 25px;
        width: 35px;
        height: 35px;
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
