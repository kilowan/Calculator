<template>
		<div id="page-wrap">		
			<img src="./images/foto.jpg" alt="Photo of juan" id="pic" />		
			<div id="contact-info" class="vcard">			
				<!-- Microformats! -->	
				<h1 class="fn">{{ inputData.name }} {{ inputData.surname }}</h1>
				<p>
					Teléfono: <span class="tel">{{ inputData.phone }}</span><br />
					Email: <a class="email" :href="'mailto:'+ inputData.email">{{ inputData.email }}</a>
				</p>
			</div>					
			<div id="objective">
				<p>{{ inputData.description }}</p>
			</div>			
			<div class="clear"></div>		
			<dl>
				<dd class="clear"></dd>				
				<dt class="formacion">Formación académica</dt>
				<dd>
					<ul>
						<li v-for="(academicTraining, index) in inputData.academicTraining" v-bind:key="index">
							<h2><strong>{{ academicTraining.name }}</strong></h2>
							<ul>
								<li><strong>Centro/ Lugar: </strong>{{ academicTraining.place }}</li>
								<li v-if="academicTraining.graduationDate"><strong>Graduación: </strong>{{ academicTraining.graduationDate }}</li>
								<li v-if="academicTraining.initDate"><strong>Fecha inicio: </strong>{{ academicTraining.initDate }}</li>
								<li v-if="academicTraining.endDate"><strong>Fecha Fin: </strong>{{ academicTraining.endDate }}</li>
								<li v-if="academicTraining.content">Contenido:
									<ul>
										<li v-for="(content, contentIndex) in academicTraining.content" v-bind:key="contentIndex">{{ content }}</li>
									</ul>
								</li>
							</ul>
						</li>
					</ul>
				</dd>
				<dd class="clear"></dd>
				<dt class="formacion2">Formación complementaria</dt>
				<dd>
					<ul>
						<li v-for="(complementaryTraining, firstindex) in inputData.complementaryTraining" v-bind:key="firstindex">
							<h2>{{ complementaryTraining.name }}</h2>
							<ul>
								<li v-for="(content, secondindex) in complementaryTraining.content" v-bind:key="secondindex">
									<h5>{{ content.key }}</h5>
									<ul>
										<li v-for="(data, thirdindex) in content.values" v-bind:key="thirdindex">{{ data }}</li>
									</ul>
								</li>
							</ul>
						</li>
					</ul>
				</dd>
				<dd class="clear"></dd>
				<dt class="experiencia">Experiencia profesional</dt>
				<dd>
					<ul>
						<li v-for="(professionalExperience, firstindex) in inputData.professionalExperience" v-bind:key="firstindex">
							<h2>{{ professionalExperience.name }}</h2>
							<ul>
								<li v-for="(contract, firstindex) in professionalExperience.contracts" v-bind:key="firstindex">{{ contract.name }}
									<ul>
										<li>Lugar: {{ contract.place }}</li>
										<li>Fecha de inicio/ Fin: {{ contract.date }}</li>
									</ul>
								</li>
							</ul>
						</li>
					</ul>
				</dd>					
				<dd class="clear"></dd>
				<dt class="idiomas">Idiomas</dt>
				<dd>
					<ul>
						<li v-for="(languages, index) in inputData.languages" v-bind:key="index"><strong>{{ languages.name }}:</strong> {{ languages.level }}</li>
					</ul>
				</dd>				
				<dd class="clear"></dd>					
				<dt class="otros">Otros datos</dt>
				<dd>
					<ul>
						<li>Disponibilidad horaria</li>
						<li>Puntualidad, responsabilidad y constancia</li>
						<li>Incorporación inmediata</li>
						<li>Disponibilidad de cambio de domicilio</li>
					</ul>
				</dd>					
				<dd class="clear"></dd>
			</dl>
			<dd class="clear"></dd>
		</div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data:function(){
		return {
			page: 'select',
			selected: undefined,
			inputData: {
				name:"Juan Francisco",
				surname:"Navarro Ramiro",
				phone:"656995114",
				email:"kilowan2@gmail.com",
				description:"Busco perfeccionar mis habilidades y si es posible adquirir nuevas y a su vez perfeccionarlas también, además de aumentar a mi experiencia tanto como se pueda, mi estilo es colaborativo más que competitivo pero si hay que competir se compite.",
				academicTraining:[
					{
						name:"Bachillerato científico-técnico",
						place:"I.E.S Carrús",
						graduationDate:"2017"
					},
					{
						name:"Administración de Sistemas Informáticos en Red",
						place:"I.E.S. Severo Ochoa",
						graduationDate:"2018"
					},
					{
						name:"Beca Everis",
						place:"San Juan (Alicante)",
						initDate:"01/2019",
						endDate: "03/2019",
						content: [
							".net Framework",
							"GitHub",
							"Sharepoint",
						]
					},
				],
				complementaryTraining:[
					{
						name:"Programación",
						content:[
							{
								key: "Lenguajes",
								values: [
									"Javascript",
									"Typescript",
									"C# (.net Framework, .net Core)",
									"PHP",
								],
							},
							{
								key: "Conocimiento en Frameworks",
								values: [
									"Vue.js",
									"jquery",
									"bootstrap",
								],
							},
							{
								key: "Tecnologías de microsoft",
								values: [
									"WCF",
									"WPF",
									"Azure Web services",
								],
							},
							{
								key: "Bases de datos",
								values: [
									"MySql",
									"Postgres",
									"Sql Server",
								],
							}
						],
					},
				],
				professionalExperience:[
					{
						name: "Grupo oesía",
						contracts: [
							{
								name:"Desarrollo Backend de webservices .net en c#",
								place: "Murcia",
								date: "09/2019-09/2020",
							},
							{
								name:"Desarrollo Frontend en Vue.js",
								place: "Murcia",
								date: "09/2010-Actualidad",
							},
						],
					}
				],
				languages: [
					{
						name:"Inglés",
						level:"Equivalente a B1",
					},
					{
						name:"Valenciano",
						level:"Equialente a A2",
					},
					{
						name:"Español",
						level:"Nativo",
					}
				]
			},
			height: 500,
		}
	},
  methods: {},
  mounted:function(){}
}
</script>

<style>
* { margin: 0; padding: 0; }
body { font: 16px Helvetica, Sans-Serif; line-height: 24px; background: url(./images/noise.jpg); }
.clear { clear: both; }
.idiomas { height: 80px; border-right: 1px solid #999; }
.otros { height: 110px; border-right: 1px solid #999; }
#page-wrap { width: 800px; margin: 40px auto 60px; }
#pic { float: right; margin: -30px 0 0 0; height: 100px; }
h1 { margin: 0 0 16px 0; padding: 0 0 16px 0; font-size: 34px; font-weight: bold; letter-spacing: -2px; border-bottom: 1px solid #999; }
h2 { font-size: 20px; margin: 0 0 6px 0; position: relative; }
h2 span { position: absolute; bottom: 0; right: 0; font-style: italic; font-family: Georgia, Serif; font-size: 16px; color: #999; font-weight: normal; }
p { margin: 0 0 16px 0; }
a { color: #999; text-decoration: none; border-bottom: 1px dotted #999; }
a:hover { border-bottom-style: solid; color: black; }
ul { margin: 0 0 32px 17px; }
#objective { width: 500px; float: left; }
#objective p { font-family: Georgia, Serif; font-style: italic; color: #666; }
dt { font-style: italic; font-weight: bold; font-size: 18px; text-align: right; padding: 0 26px 0 0; width: 150px; float: left; height: 100px; border-right: 1px solid #999;  }
dd { width: 600px; float: right; }
dd.clear { float: none; margin: 0; height: 15px; }
.formacion { height: 450px; border-right: 1px solid #999; }
.formacion2 { height: 540px; border-right: 1px solid #999; }
.experiencia{ height: 210px; border-right: 1px solid #999; }
</style>
