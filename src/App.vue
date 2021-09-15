<template>
	<div>
		<h1><p style="text-align: center;">Calculadora de conversión</p></h1>
		<h3><p style="text-align: center;">Introduce cualquier numero decimal, hexadecimal o binario y se calculará automáticamente al resto de unidades. (ej: de binario a decimal)</p></h3> 
		<div style="text-align: center;">
			<div v-if="calcula">
				<div v-if="result.includes('binario')">
					<h2><p>Origen binario:</p></h2>
					<p>El numero {{ number }} en decimal es {{ all? number : binadeci(number) }}</p>
					<p>El numero {{ number }} en Hexadecimal es {{ all? number : binahexa(number) }}</p>
				</div>
				<div v-if="result.includes('decimal')">
					<h2><p>Origen decimal:</p></h2>
					<p>El numero {{ number }} en binario es {{ all? number : deciabin(number) }}</p>
					<p>El numero {{ number }} en Hexadecimal es {{ all? number : decihexa(number) }}</p>
				</div>
				<div v-if="result.includes('hexadecimal')">
					<h2><p>Origen hexadecimal:</p></h2>
					<p>El numero {{ number }} en Binario es {{ all? number : hexabin(number) }}</p>
					<p>El numero {{ number }} en Decimal es {{ all? number : hexadeci(number) }}</p>
				</div>
			</div>
			<input @input="reset()" type="text" required v-model="number"/>
			<button @click="reset(), calcula = true, checkNumber(number)">calcula</button>
		</div>
	</div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data:function(){
		return {
			add: 0,
			number: undefined,
			calcula: false,
			result: [],
			error: undefined,
			all: false,
			hexDecValues: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'],
			decValues: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
		}
	},
  methods: {
	reset: function() {
			this.add = 0;
			this.calcula = false;
			this.result = [];
			this.error = undefined;
			this.all = false;
	},
	checkNumber: function(number) {
		//2 - Comprobaciones
		if(number == "0" || number == "1") {
			this.result.push('binario', 'decimal', 'hexadecimal');
			this.all = true;
		} else if(number != "0") {
			let data = "";
			//Binario
			for(let i = "0"; i <= number.toString().length-1; i++)	{
				if(number[i] == "0" || number[i] == "1")
				{
					data = data + "*";
				}
			}
			if(data.toString().length == number.toString().length)	{
				this.result.push('binario');
			}
			//Decimal
			data = "";
			for(let i = "0"; i <= number.toString().length-1; i++)	{
				
				if(this.decValues.includes(number[i])) {
					data = data + "*";
				}
			}
			if(data.toString().length == number.toString().length) {
				this.result.push('decimal');
			}
			//Hexadecimal
			data = "";
			for(let i = "0"; i <= number.toString().length-1; i++)	{
				let tmpValue = number[i].toUpperCase();
				
				if(this.hexDecValues.includes(tmpValue)) {
					data = data + "*";
				}
				else
				{
					this.error += number[i];
				}
			}
			if(data.toString().length == number.toString().length) {
				this.result.push('hexadecimal');
			}
		}
	},
	//1.1 - Decimal a binario
	deciabin: function(number) {
		let resultado = '';
		while(number > 0) {
			let resto = number%2;
			number = Math.trunc(number/2);
			resultado = resto + resultado;
		}

		return resultado;
	},
	//1.2 - Binario a decimal
	binadeci: function(number) {
		let bin = 0;
		for(let fn = 0, i = number.toString().length-1, i2 = fn; i >= fn; i--, i2++) {
			bin = bin + number[i2] * Math.pow(2, i);
		}

		return bin.toString();
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
			number = Math.trunc(number/10);
		}
		if(number > 0)
		{
			hexa += Math.pow(2,cont);
		}
		let resultado = "";
		while(hexa > 0)
		{
			resto = hexa%16;
			hexa = Math.trunc(hexa/16);
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
			number = Math.trunc(number/16);
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
		for(let i = 0; i < number.toString().length; i++)
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
		let dec = '0';
		let valor;
		for(let fn = '0', i = number.toString().length-1, i2 = fn; i >= fn; i--, i2++)
		{
			let tempValue = number[i2].toUpperCase();
			valor = this.hexDecValues.indexOf(tempValue);
			dec = dec + valor * Math.pow(16, i);
		}
		return parseInt(dec);
	},

  },
  mounted:function(){}
}
</script>

<style></style>
