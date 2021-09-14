<template>
	<div v-if="!calcula">
		<h1><p align="center">Calculadora de conversión</p></h1>
		<h3><p align="center">Introduce cualquier numero decimal, hexadecimal o binario y se calculará automáticamente al resto de unidades. (ej: de binario a decimal)</p></h3> 
		<input type="text" v-model="number" >
		<button @click="calcula = true">calcula</button>
	</div>
	<div v-else>
		<h2><p>Origen binario:</p></h2>
		<p>El numero {{ number }} en decimal es {{ number }}</p>
		<p>El numero {{ number }} en Hexadecimal es {{ number }}</p>

		<h2><p>Origen decimal:</p></h2>
		<p>El numero {{ number }} en binario es {{ number }}</p>
		<p>El numero {{ number }} en Hexadecimal es {{ number }}</p>

		<h2><p>Origen hexadecimal:</p></h2>
		<p>El numero {{ number }} en Binario es {{ number }}</p>
		<p>El numero {{ number }} en Decimal es {{ number }}</p>
		<button @click="calcula = false, number = undefined">Atrás</button>
	</div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data:function(){
		return {
			add: 0,
			var2: "",
			number: undefined,
			calcula: false,
		}
	},
  methods: {
	caracter: function(number) {
		for(; number[this.add]!=='' ; this.add++)	{
			//hola
		}

		return this.add;
	},
	//1.1 - Decimal a binario
	deciabin: function(number) {
		let resultado = '';
		while(number > 0) {
			let resto = number%2;
			number = Math.floor(number, 2);
			resultado = resto + resultado;
		}

		return resultado;
	},
	//1.2 - Binario a decimal
	binadeci: function(number) {
		let bin = "0";
		for(let fn="0", i = this.caracter(number)-1,i2 = fn; i >= fn; i--, i2++) {
			bin = bin + number[i2] * Math.pow(2, i);
		}

		return bin;
	},
	//1.3 - Binario a hexadecimal
	binahexa: function(number) {
		let resto;
		let hexa = 0;
		let cont = 0;
		for(let cifra = 0; number>=10;cont++) {
			cifra = number%10;
			if(cifra > 0)
			{
				hexa += Math.pow(2, cont);
			}
			number = Math.floor(number, 10);
		}
		if(number > 0)
		{
			hexa += Math.pow(2,cont);
		}
		let resultado = "";
		while(hexa > 0)
		{
			resto = hexa%16;
			hexa = Math.floor(hexa, 16);
			if(resto == "0" || resto == "1" || resto == "2" || resto == "3" || resto == "4" || resto == "5" || resto == "6" || resto == "7" || resto == "8" || resto == "9"){
				resultado = resto + resultado;
			} else if(resto == "10") {
				resultado="A" + resultado;
			} else if(resto=="11")	{
				resultado="B" + resultado;
			} else if(resto=="12")	{
				resultado="C" + resultado;
			} else if(resto=="13")	{
				resultado="D" + resultado;
			} else if(resto=="14")	{
				resultado="E" + resultado;
			} else if(resto=="15") {
				resultado="F" + resultado;
			}
		}
		return resultado;
	},
	//1.4 - Decimal a hexadecimal
	decihexa: function(number) {
		let resultado = "";
		while(number > 0) {
			let resto = number%16;
			number = Math.floor(number,16);
			if(resto == "0" || resto == "1" || resto == "2" || resto == "3" || resto == "4" || resto == "5" || resto == "6" || resto == "7" || resto == "8" || resto == "9") {
				resultado = resto + resultado;
			} else if(resto == "10") {
				resultado = "A" + resultado;
			} else if(resto == "11") {
				resultado="B" + resultado;
			} else if(resto == "12") {
				resultado="C" + resultado;
			} else if(resto == "13") {
				resultado = "D" + resultado;
			} else if(resto == "14") {
				resultado = "E" + resultado;
			} else if(resto == "15") {
				resultado = "F" + resultado;
			}
		}
		return resultado;
	},
	//1.5 - Hexadecimal a binario
	hexabin: function(number) {
		let binario = "";
		for(let i = 0; i < this.caracter(number); i++)
		{
			if(number[i]=="0") {
				binario = binario + "0000";
			} else if(number[i] == "1"){
				binario = binario + "0001";
			} else if(number[i] == "2")	{
				binario = binario + "0010";
			} else if(number[i] == "3")	{
				binario = binario + "0011";
			} else if(number[i] == "4")	{
				binario = binario + "0100";
			} else if(number[i] == "5")	{
				binario = binario + "0101";
			} else if(number[i] == "6")	{
				binario = binario + "0110";
			} else if(number[i] == "7")	{
				binario = binario + "0111";
			} else if(number[i] == "8"){
				binario = binario + "1000";
			} else if(number[i] == "9")	{
				binario = binario + "1001";
			} else if(number[i] == "A" || number[i] == "a")	{
				binario = binario + "1010";
			} else if(number[i] == "B" || number[i] == "b")	{
				binario = binario + "1011";
			} else if(number[i] == "C" || number[i] == "c")	{
				binario = binario + "1100";
			} else if(number[i] == "D" || number[i] == "d")	{
				binario = binario + "1101";
			} else if(number[i] == "E" || number[i] == "e")	{
				binario = binario + "1110";
			} else if(number[i] == "F" || number[i] == "f")	{
				binario = binario + "1111";
			}
		}
		return binario;
	},
	//1.6 - Hexadecimal a decimal
	hexadeci: function(number)
	{
		let dec = "0";
		let valor;
		for(let fn = "0", i = this.caracter(number)-1, i2 = fn; i >= fn; i--, i2++)
		{
			//let values = [{'A': '10'}, {'B': '11'}, {'C': '12'}, {'D': '13'}, {'E': '14'}, {'F': '15'}, {'0': '0'}, {'1': '1'}, {'2': '2'}, {'3': '3'}, {'4': '4'}, {'5': '5'}, {'6': '6'}, {'7': '7'}, {'8': '8'}, {'9': '9'}];
			//let tempValue = number[i2].toUpperCase()
			//let valor = values[tempValue];

			if(number[i2] == "0" || number[i2] == "1" || number[i2] == "2" || number[i2] =="3" || number[i2] == "4" || number[i2] == "5" || number[i2] == "6" || number[i2] == "7" || number[i2] == "8" || number[i2] == "9") {
				valor = number[i2];
			} else if(number[i2] == "A" || number[i2] == "a") {
				valor="10";
			} else if(number[i2] == "B" || number[i2] == "b") {
				valor="11";
			} else if(number[i2] == "C" || number[i2] == "c") {
				valor="12";
			} else if(number[i2] == "D" || number[i2] == "d") {
				valor="13";
			} else if(number[i2] == "E" || number[i2] == "e") {
				valor="14";
			} else if(number[i2] == "F" || number[i2] == "f") {
				valor="15";
			}
			dec = dec + valor * Math.pow(16, i);
		}
		return dec;
	},
  },
  mounted:function(){
	//this.number = this.hexadeci('A');
  }
}
</script>

<style></style>
