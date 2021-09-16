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
			binValues: ['0', '1'],
			decValues: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
			hexDecValues: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'],
			hexValues: {0: '0', 1: '1', 2: '2', 3: '3', 4: '4', 5: '5', 6: '6', 7: '7', 8: '8', 9: '9', A: '10', B: '11', C: '12', D: '13', E: '14', F: '15'},
			hexaBinValues: {0: '0000', 1: '0001', 2: '0010', 3: '0011', 4: '0100', 5: '0101', 6:'0110', 7:'0111', 8:'1000', 9:'1001', A:'1010', B:'1011', C:'1100', D:'1101', E:'1110', F:'1111'},
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
			let data = "";
			//Binario
			for(let i = "0"; i <= number.toString().length-1; i++)	{
				if(this.binValues.includes(number[i]))	data = data + "*";
			}
			if(data.toString().length == number.toString().length)	this.result.push('binario');
			//Decimal
			data = "";
			for(let i = "0"; i <= number.toString().length-1; i++)	{
				if(this.decValues.includes(number[i])) data = data + "*";
			}
			if(data.toString().length == number.toString().length) this.result.push('decimal');
			//Hexadecimal
			data = "";
			for(let i = "0"; i <= number.toString().length-1; i++)	{
				let tmpValue = number[i].toUpperCase();
				
				if(this.hexDecValues.includes(tmpValue)) data = data + "*";	
				else this.error += number[i];
			}
			if(data.toString().length == number.toString().length) this.result.push('hexadecimal');
		} else this.error += number;
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
		let bin = '0';
		for(let fn = '0', i = (number.toString().length-1).toString(), i2 = fn; i >= fn; i--, i2++) {
			bin = bin + number[i2] * Math.pow(2, i);
		}

		return bin.toString();
	},
	//1.3 - Binario a hexadecimal
	binahexa: function(number) {
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
		if(number > 0)	hexa += Math.pow(2,cont);
		return this.decihexa(hexa);
	},
	//1.4 - Decimal a hexadecimal
	decihexa: function(number) {
		let resultado = "";
		while(number > 0) {
			let resto = number%16;
			number = Math.trunc(number/16);
			if(this.hexValues[resto]) resultado = this.hexValues[resto] + resultado;
		}
		return resultado;
	},
	//1.5 - Hexadecimal a binario
	hexabin: function(number) {
		let binario = "";
		for(let i = 0; i < number.toString().length; i++)
		{
			let tmpValue = number[i].toUpperCase();
			binario += this.hexaBinValues[tmpValue];
		}
		return binario;
	},
	//1.6 - Hexadecimal a decimal
	hexadeci: function(number)
	{
		let dec = 0;
		let valor;
		for(let fn = 0, i = number.toString().length-1, i2 = fn; i >= fn; i--, i2++) {
			let tempValue = number[i2].toUpperCase();
			valor = this.hexDecValues.indexOf(tempValue);
			dec += (parseInt(valor) * Math.pow(16, i));
		}
		return dec;
	},
  },
  mounted:function(){}
}
</script>
<style></style>
