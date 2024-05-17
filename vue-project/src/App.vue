<script setup>
import { reactive } from 'vue';

const nome = "Bruno"
const meuObjeto = {
  nome: "Bruno",
  filmeFavorito: "Spiderman"
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

const enderecoImagemDoBatman = "https://conteudo.imguol.com.br/c/entretenimento/04/2022/02/25/batman-1645790799911_v2_1x1.jpg";
const imagemSuperman = "https://i.pinimg.com/474x/a5/4a/64/a54a640e1472797500d0c1cf2c34a711.jpg"

const botaoEstaDesabilidado = true

const gostaDoBatman = true
const gostaDoSuperman = true

const estaAutorizado = false

// let contador = 0

const estado = reactive({
  contador:0,
  email: "",
  saldo: 5000,
  transferindo: 0,
  nomes:['gian', 'paulo', 'luisa', 'monica'],
  nomeAInserir: '',
})

function incrementar () {
  estado.contador ++
}

function decrementar () {
  estado.contador --
}

function alteraEmail(evento) {
  estado.email = (evento.target.value)
}

function mostraSaldoFuturo() {
  const {saldo, transferindo} = estado;
  return saldo - transferindo;
}

function validaValorTransferencia () {
  const {saldo, transferindo} = estado;
  return saldo >=transferindo
}

function cadastraNome () {
  if (estado.nomeAInserir.length >=3) {
    estado.nomes.push(estado.nomeAInserir)
  }else{
    alert("Digite mais caracteres")
  }
}



</script>

<template>
  <h1>{{ dizOla("Júlio") }}</h1>
  <img v-if="gostaDoBatman" :src="enderecoImagemDoBatman" alt="">
  <img v-else-if="gostaDoSuperman" :src="imagemSuperman" alt="">
  <h2 v-else>Não gosta de heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem Vindo</h1>
  <h1 v-else>Não possui acesso</h1>
  <button :disabled="botaoEstaDesabilidado" >Enviar mensagem</button>

  <br/>
  <hr/>

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br/>
  <hr/>

  {{  estado.email }}
  <input type="email" @keyup="alteraEmail">


  <br/>
  <hr/>
  saldo: {{ estado.saldo }} <br/>
  Transferindo: {{ estado.transferindo }} <br/>
  Saldo depois da transferência: {{ mostraSaldoFuturo() }} <br/>
  <input :class="{invalid: !validaValorTransferencia()}" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir"/>
  <button v-if="validaValorTransferencia()">transferir</button>
  <span v-else >Valor maior que o saldo</span>

  <br/>
  <hr/>

  <ul>
    <li v-for="nome in estado.nomes">
    {{ nome }}
    </li>
  </ul>

  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastraNome" type="button">Cadastrar nome</button>

</template>

<style scoped>
img {
  max-width: 200px
}

.invalid {
  outline-color: red;
  border-color: red;
}
</style>
