<script setup>
import { reactive } from 'vue';


 const nome = 'Johni Cassere';
 

 const estado = reactive({
    contador: 0,
    nome: 'johni',
    filme: 'once',
    email: '',
    saldo: 5000,
    transferindo: 0,
    nomes : ["Aa", "Bb", "Cc", "Dd",],
    nomeAInserir : ''
 })


 function dizOi(){
    return `Olá ${estado.nome}`
 }

 const img = 'https://cdn.pixabay.com/photo/2023/01/06/02/01/ai-generated-7700259_1280.jpg';


function alteraEmail (evento){
    //console.log(evento.target.value);
    estado.email = evento.target.value
}

function incrementar(){
    estado.contador++
}
function decrementar(){
    estado.contador--
}

function mostraSaldoFuturo(){
    const {saldo, transferindo} = estado;
    return saldo - transferindo;
}

function validaValorTransferencia(){
    const {saldo, transferindo} = estado;
    return saldo >= transferindo;


}

function cadastraNome(){
    if(estado.nomeAInserir.length >= 3){
        estado.nomes.push(estado.nomeAInserir)
    }else{
        alert('Nome Invalido')
    }

}

</script>

<template>

<h1>Olá</h1>
<h2>{{ nome }}</h2>
<h2>{{ estado.filme }}</h2>
<h2>{{ dizOi() }}</h2>

<img :src="img" alt="">
<br>
<hr>

{{ estado.contador }}
<button @click="incrementar">+</button>
<button @click="decrementar">-</button>

<br>
<hr>


<input type="email" @keyup="alteraEmail">
{{ estado.email }}

<br>
<hr>

<div class="container">
    <h3>Saldo: {{ estado.saldo }}</h3>
    <h3>Tranferindo: {{ estado.transferindo }}</h3>
    <h3>Saldo depois da transferência: {{ mostraSaldoFuturo(1000) }}</h3>
    <input class="campo" :class="{ invalido : !validaValorTransferencia() }" @keyup="evento  => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferência">
    <button v-if="validaValorTransferencia()">Tranferir</button>
    <span v-else>Valor Maior que o saldo</span>

    <br>
    <hr>

    <ul>
        <li v-for="nome in estado.nomes">
        {{nome}}
    </li>
    </ul>
    <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um nome">
    <button @click="cadastraNome()" type="button">Cadastrar Nome</button>

    <br>

    <h3 v-for="nome in estado.nomes"> {{ nome }}</h3>
</div>

</template>

<style scoped>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}
.invalido{
    outline-color: red;
    border-color: red;
}

.campo{
    border:  2px solid #000;
}

h1{
    text-align: center;
    
}

img{
    margin: 16px 16px;
    width: 300px;
    border-radius: 8px;
    opacity: .7;
}

button{
    width: 100px;
    margin: 8px 16px;
    
}

.container{
    display: flex;
    justify-content: center;
    flex-direction: column;
    padding: 12px;
    margin: 18px;
}


</style>
