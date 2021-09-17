<template>
	<div>
		<h1><p style="text-align: center;">Calculadora de conversión</p></h1>
		<h3><p style="text-align: center;">Introduce cualquier numero decimal, hexadecimal o binario y se calculará automáticamente al resto de unidades. (ej: de binario a decimal)</p></h3> 
		<div style="text-align: center;">
			<div v-if="calcula">
				<div v-if="result.includes('binario')">
					<h2><p>Origen binario:</p></h2>
					<p>El numero {{ number }} en decimal es {{ all? number : parseInt(number, 2) }}</p>
					<p>El numero {{ number }} en Hexadecimal es {{ all? number : decihexa(parseInt(number, 2)) }}</p>
				</div>
				<div v-if="result.includes('decimal')">
					<h2><p>Origen decimal:</p></h2>
					<p>El numero {{ number }} en binario es {{ all? number : deciabin(number) }}</p>
					<p>El numero {{ number }} en Hexadecimal es {{ all? number : decihexa(parseInt(number, 10)) }}</p>
				</div>
				<div v-if="result.includes('hexadecimal')">
					<h2><p>Origen hexadecimal:</p></h2>
					<p>El numero {{ number }} en Binario es {{ all? number : deciabin(parseInt(number, 16)) }}</p>
					<p>El numero {{ number }} en Decimal es {{ all? number : parseInt(number, 16) }}</p>
				</div>
				<div v-if="result.length == 0">
					<h2><p>Carácter incorrecto</p></h2>
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
			binValues: ['0', '1'],
			decValues: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
			HexValues: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'],
			decHexValues: {0: '0', 1: '1', 2: '2', 3: '3', 4: '4', 5: '5', 6: '6', 7: '7', 8: '8', 9: '9', 'A': '10', 'B': '11', 'C': '12', 'D': '13', 'E': '14', 'F': '15'},
			hexValues: {0: '0', 1: '1', 2: '2', 3: '3', 4: '4', 5: '5', 6: '6', 7: '7', 8: '8', 9: '9', 10: 'A', 11: 'B', 12: 'C', 13: 'D', 14: 'E', 15: 'F'},
			hexaBinValues: {'0': '0000', '1': '0001', '2': '0010', '3': '0011', '4': '0100', '5': '0101', '6':'0110', '7':'0111', '8':'1000', '9':'1001', 'A':'1010', 'B':'1011', 'C':'1100', 'D':'1101', 'E':'1110', 'F':'1111'},
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
		if(this.binValues.includes(number)) {
			this.result.push('binario', 'decimal', 'hexadecimal');
			this.all = true;
		} else if(number != "0") {
			//Binario
			let data = this.characherVerifier(number, this.binValues);
			if(data.toString().length == number.toString().length)	this.result.push('binario');
			//Decimal
			data = this.characherVerifier(number, this.decValues);
			if(data.toString().length == number.toString().length) this.result.push('decimal');
			//Hexadecimal
			data = this.characherVerifier(number.toUpperCase(), this.HexValues);
			if(data.toString().length == number.toString().length) this.result.push('hexadecimal');
		} else this.error += number;
	},
	characherVerifier(number, array) {
		let data = '';
		for(let i = "0"; i <= number.toString().length-1; i++)	{
			if(array.includes(number[i])) data = data + "*";
		}
		return data;
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
	//1.4 - Decimal a hexadecimal
	decihexa: function(number) {
		let resultado = "";
		while(number > 0) {
			let resto = number%16;
			number = Math.trunc(number/16);
			resultado = this.hexValues[resto] + resultado;
		}
		return resultado;
	},
  },
  mounted:function(){}
}
</script>
<style></style>
