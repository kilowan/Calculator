<template>
	<div>
		<h1><p style="text-align: center;">Conversor de unidades</p></h1>
		<h3><p style="text-align: center;">Introduce cualquier número {{ decimal }}, {{ hexadecimal }} o {{ binario }} y se calculará automáticamente al resto de unidades. (ej: de {{ binario }} a {{ decimal }})</p></h3> 
		<div style="text-align: center;">
			<div v-if="calcula">
				<div v-if="result.includes(binario)">
					<h2><p>Origen {{ binario }}:</p></h2>
					<p>El número {{ number }} en {{ decimal }} es {{ all? number : parseInt(number, 2) }}</p>
					<p>El número {{ number }} en {{ hexadecimal }} es {{ all? number : decihexa(parseInt(number, 2)) }}</p>
				</div>
				<div v-if="result.includes(decimal)">
					<h2><p>Origen {{ decimal }}:</p></h2>
					<p>El número {{ number }} en {{ binario }} es {{ all? number : deciabin(number) }}</p>
					<p>El número {{ number }} en {{ hexadecimal }} es {{ all? number : decihexa(parseInt(number, 10)) }}</p>
				</div>
				<div v-if="result.includes(hexadecimal)">
					<h2><p>Origen hexadecimal:</p></h2>
					<p>El número {{ number }} en {{ binario }} es {{ all? number : deciabin(parseInt(number, 16)) }}</p>
					<p>El número {{ number }} en {{ decimal }} es {{ all? number : parseInt(number, 16) }}</p>
				</div>
				<div v-if="result.length === 0">
					<p v-if="number !== undefined">Carácter incorrecto {{ error.toLowerCase() }}</p>
					<p v-else>Campo vacío</p>
				</div>
			</div>
			<input @input="reset()" type="text" v-model="number"/>
			<button @click="reset(), calcula = true, checkNumber(number)">calcula</button>
		</div>
	</div>
</template>

<script>
const hexadecimal = 'hexadecimal';
const decimal = 'decimal';
const binario = 'binario';

export default {
  name: 'App',
  components: {},
  data:function(){
		return {
			number: undefined,
			calcula: false,
			result: [],
			error: '',
			all: false,
			values: {},
			hexadecimal: hexadecimal,
			decimal: decimal,
			binario: binario,
		}
	},
  methods: {
	reset: function() {
			this.calcula = false;
			this.result = [];
			this.error = undefined;
			this.all = false;
	},
	checkNumber: function(number) {
		//2 - Comprobaciones
		if(this.values[binario].includes(number)) {
			this.result.push(binario, decimal, hexadecimal);
			this.all = true;
		} else if(number != "0") {
			//Binario
			this.checkNumberTypes(number, binario);
			//Decimal
			this.checkNumberTypes(number, decimal);
			//Hexadecimal
			this.checkNumberTypes(number.toUpperCase(), hexadecimal, true);
		} else this.error += number;
	},
	checkNumberTypes: function(number, type, last = false) {
		let length = 0;
		for(let i = 0; i <= number.toString().length-1; i++)	{
			this.values[type].includes(number[i]) ? length++ : last? this.error += number[i] : this.error = '';
		}

		if(length == number.toString().length) this.result.push(type);
	},
	//changeBase dec to hexa/bin
	changeBase: function(number, type) {
		let base = {binario: 2, hexadecimal: 16};
		let resultado = "";
		while(number > 0) {
			let resto = number%base[type];
			number = Math.trunc(number/base[type]);
			resultado = this.values[type][resto] + resultado;
		}

		return resultado.toString();
	},
	//1.1 - Decimal a binario
	deciabin: function(number) { return this.changeBase(number, binario);	},
	//1.4 - Decimal a hexadecimal
	decihexa: function(number) { return this.changeBase(number, hexadecimal); },
  },
  mounted:function(){
	this.values[binario] = ['0', '1'];
	this.values[decimal] = this.values[binario].concat(['2', '3', '4', '5', '6', '7', '8', '9']);
	this.values[hexadecimal] = this.values[decimal].concat(['A', 'B', 'C', 'D', 'E', 'F']);
  }
}
</script>
<style></style>
