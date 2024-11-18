<template>
  <q-page class="flex flex-center">
    <q-card class="q-pa-md">
      <div class="row">
        <div class="col">
          <q-input dense outlined rounded v-model="tela_Calculadora"></q-input>
        </div>
      </div>
      <div class="row q-mt-md q-col-gutter-x-sm">
        <div class="col">
          <q-btn label="%" @click="adicionarNaTela('%')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="CE" @click="adicionarNaTela('CE')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="C" @click="adicionarNaTela('C')"></q-btn>
        </div>
        <div class="col">
          <q-btn
            outline
            color="red-7"
            icon="arrow_back"
            @click="deletarValorAnterior('delete')"
          ></q-btn>
        </div>
      </div>
      <div class="row q-mt-sm q-col-gutter-x-lg">
        <div class="col">
          <q-btn label="+" @click="adicionarNaTela('+')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="-" @click="adicionarNaTela('-')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="*" @click="adicionarNaTela('*')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="/" @click="adicionarNaTela('/')"></q-btn>
        </div>
      </div>
      <div class="row q-ml-md q-mt-md q-col-gutter-x-sm">
        <div class="col">
          <q-btn label="7" @click="adicionarNaTela('7')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="8" @click="adicionarNaTela('8')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="9" @click="adicionarNaTela('9')"></q-btn>
        </div>
      </div>
      <div class="row q-ml-md q-mt-md q-col-gutter-x-sm">
        <div class="col">
          <q-btn label="4" @click="adicionarNaTela('4')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="5" @click="adicionarNaTela('5')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="6" @click="adicionarNaTela('6')"></q-btn>
        </div>
      </div>
      <div class="row q-ml-md q-mt-md q-col-gutter-x-sm">
        <div class="col">
          <q-btn label="1" @click="adicionarNaTela('1')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="2" @click="adicionarNaTela('2')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="3" @click="adicionarNaTela('3')"></q-btn>
        </div>
      </div>
      <div class="row q-ml-md q-mt-md q-col-gutter-x-sm">
        <div class="col">
          <q-btn color="blue-7" label="." @click="adicionarNaTela('.')"></q-btn>
        </div>
        <div class="col">
          <q-btn label="0" @click="adicionarNaTela('0')"></q-btn>
        </div>
        <div class="col">
          <q-btn color="orange-7" label="=" @click="resultado()"></q-btn>
        </div>
      </div>
    </q-card>
  </q-page>
</template>

<script setup>
import { defineComponent, ref, onMounted } from "vue";
defineOptions({
  name: "IndexPage",
});

const tela_Calculadora = ref("");

const adicionarNaTela = (valor) => {
  if (
    tela_Calculadora.value.indexOf("+") != -1 ||
    tela_Calculadora.value.indexOf("-") != -1 ||
    tela_Calculadora.value.indexOf("*") != -1 ||
    tela_Calculadora.value.indexOf("/") != -1 ||
    tela_Calculadora.value.indexOf("%") != -1
  ) {
    if (
      valor == "+" ||
      valor == "-" ||
      valor == "*" ||
      valor == "/" ||
      valor == "%"
    )
      return;
  }

  if (valor == "CE" || valor == "C" || valor == "delete") {
    tela_Calculadora.value = "";
    return;
  }
  tela_Calculadora.value += valor;
};

const somar = (valor) => {
  let valores = valor.split("+");
  let resultado = 0;

  if (valores.length == 2) {
    resultado = parseFloat(valores[0]) + parseFloat(valores[1]);
  }

  return resultado;
};
const subtrair = (valor) => {
  let valores = valor.split("-");
  let resultado = 0;

  if (valores.length == 2) {
    resultado = parseFloat(valores[0]) - parseFloat(valores[1]);
  }

  return resultado;
};

const multiplicar = (valor) => {
  let valores = valor.split("*");
  let resultado = 0;

  if (valores.length == 2) {
    resultado = parseFloat(valores[0]) * parseFloat(valores[1]);
  }

  return resultado;
};

const dividir = (valor) => {
  let valores = valor.split("/");
  let resultado = 0;

  if (valores.length == 2) {
    resultado = parseFloat(valores[0]) / parseFloat(valores[1]);
  }

  return resultado;
};

const porcentagem = (valor) => {
  let valores = valor.split("%");
  let resultado = 0;

  if (valores.length == 2) {
    resultado = parseFloat(valores[0]) % parseFloat(valores[1]);
  }

  return resultado;
};

const resultado = () => {
  let resultado_fim = "";
  if (tela_Calculadora.value.indexOf("+") != -1)
    resultado_fim = somar(tela_Calculadora.value);
  if (tela_Calculadora.value.indexOf("-") != -1)
    resultado_fim = subtrair(tela_Calculadora.value);
  if (tela_Calculadora.value.indexOf("*") != -1)
    resultado_fim = multiplicar(tela_Calculadora.value);
  if (tela_Calculadora.value.indexOf("/") != -1)
    resultado_fim = dividir(tela_Calculadora.value);
  if (tela_Calculadora.value.indexOf("%") != -1)
    resultado_fim = porcentagem(tela_Calculadora.value);

  if (resultado_fim) {
    tela_Calculadora.value = resultado_fim.toString();
  }
};

const deletarValorAnterior = () => {
  if (tela_Calculadora.value.length > 0) {
    const aux = tela_Calculadora.value.length;
    const alt = tela_Calculadora.value.substring(0, aux - 1);
    tela_Calculadora.value = alt;
  }
};
</script>
