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
				<div v-if="result.length === 0">
					<h2><p>Carácter incorrecto {{ error }}</p></h2>
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
			number: undefined,
			calcula: false,
			result: [],
			error: '',
			all: false,
			binValues: [],
			decValues: [],
			HexValues: [],
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
		if(this.binValues.includes(number)) {
			this.result.push('binario', 'decimal', 'hexadecimal');
			this.all = true;
		} else if(number != "0") {
			//Binario
			this.checkNumberTypes(number, this.binValues, 'binario');
			//Decimal
			this.checkNumberTypes(number, this.decValues, 'decimal');
			//Hexadecimal
			this.checkNumberTypes(number.toUpperCase(), this.HexValues, 'hexadecimal', true);
		} else this.error += number;
	},
	checkNumberTypes: function(number, array, type, last = false) {
		let length = 0;
		for(let i = 0; i <= number.toString().length-1; i++)	{
			array.includes(number[i]) ? length++ : last? this.error += number[i] : this.error = '';
		}
		if(length == number.toString().length) this.result.push(type);
	},
	//changeBase dec to hexa/bin
	changeBase: function(number, array, base) {
		let resultado = "";
		while(number > 0) {
			let resto = number%base;
			number = Math.trunc(number/base);
			resultado = array[resto] + resultado;
		}

		return resultado.toString();
	},
	//1.1 - Decimal a binario
	deciabin: function(number) { return this.changeBase(number, this.binValues, 2);	},
	//1.4 - Decimal a hexadecimal
	decihexa: function(number) { return this.changeBase(number, this.HexValues, 16); },
  },
  mounted:function(){
	this.binValues = ['0', '1'];
	this.decValues = this.binValues.concat(['2', '3', '4', '5', '6', '7', '8', '9']);
	this.HexValues = this.decValues.concat(['A', 'B', 'C', 'D', 'E', 'F']);
  }
}
</script>
<style></style>
