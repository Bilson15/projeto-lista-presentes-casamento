<template>
    <div class="footer bg-dark">
        <div class="confirm">
            <h5 id="foo">Confirme sua presença!</h5>
            <div class="input-group mb-3 botao">
                <input v-model="name" type="text" class="form-control input-color" placeholder="Digite seu nome" aria-label="Recipient's username" aria-describedby="button-addon2">
                <button class="btn btn-light" type="button" id="button-addon2" v-on:click.prevent="saveConfirmar">Confirmar</button>
            </div>
        </div>

    </div>  
</template>

<script>

export default{
data: () => {
    return {
      name: '',
    };
},
methods: {
    confirmaPresenca() {
    fetch("https://6143926cc5b553001717d00e.mockapi.io/confirmacao", {
        method: "POST",
        body: JSON.stringify({ 
        nome: this.name,
        }),
        headers: { "Content-Type": "application/json; charset=UTF-8" },

    })
        .then(response => response.json())
        .then(data => (swal("S2", "Obrigado por confirmar, aguardo você lá", "success")));
    },
    saveConfirmar() {
        let nome = localStorage.getItem('nomeStorage');
        if(nome) {
            this.name = nome;
            swal("Você já me confirmou sua presença ;)")
            .then((value) => {
            swal(`Você confirmou como: ${this.name}`);
            });
        }else {

            swal (  "Confirme seu nome e o de cada membro que irá comparecer. Isso deve ser feito apenas uma única vez.\n"+
                    "Digite cada nome separado apenas por vírgulas. Exemplo: Gabriel, Dalila\n"+
                    "Deseja confirmar? Lembrando que você deverá confirmar até 01/03/2022." , { 
            buttons: {
                cancel: "Cancelar",
                Confimar: true,
            },
            })
            .then((value) => {
            switch (value) {
                case "Confimar":
                    if(this.name === ""){
                        swal("Atenção!", "Você não digitou seu nome", "warning");
                    }else{
                        nome = [this.name];
                        localStorage.setItem('nomeStorage', nome);
                        this.confirmaPresenca();
                    }

                break;
            
                case "cancel":
                    console.log('canelei');
                break;
            
                default:
            }
            });
        }

        
    }
}
}
</script>

<style scoped>
    .footer {
        width: 100%;
        height: 200px;
    }
    .confirm {
        display: flex;
        flex-direction: column;
        align-content: center;
        align-items: center;
    }
    h5{
        display: block;
        color: #ffffff;
        text-align: center;
        margin-top: 20px;
    }
    .botao {
        margin: 25px;
        width: 500px;
    }
    .btn {
        background-color: #ff6f9c;
    }

    input:active, input:focus {
        box-shadow: 0 0 0 0;
    }


    @media(max-width: 500px){
        .botao {
            width: 80%;
        }

    }

</style>


