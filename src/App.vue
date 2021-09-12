<template>
		<form v-if="page == 'select'" action="curriculum.php" method="post" >
			<label>Tipo</label>
			<input v-model="selected" name="tipo" type="text" id="tipo" required>
			<input @click="page='main'" type="submit" name="Submit" value="LOGIN">
		</form>
		<div v-else id="page-wrap">		
			<img src="./images/foto.jpg" alt="Photo of juan" id="pic" />		
			<div id="contact-info" class="vcard">			
				<!-- Microformats! -->			
				<h1 class="fn">Juan Francisco Navarro Ramiro</h1>			
				<p>
					Teléfono: <span class="tel">656995114</span><br />
					Email: <a class="email" href="mailto:kilowan2@gmail.com">kilowan2@gmail.com</a>
				</p>
			</div>					
			<div id="objective">
				<p>
					Busco perfeccionar mis habilidades y si es posible adquirir nuevas y a su vez perfeccionarlas también, además de aumentar a mi experiencia tanto como se pueda, mi estilo es colaborativo más que competitivo pero si hay que competir se compite.
				</p>
			</div>			
			<div class="clear"></div>			
			<dl>
				<dd class="clear"></dd>				
				<dt class="formacion">Formación académica</dt>
				<dd>
					<ul>
						<li>
							<h2><strong>Bachillerato científico-técnico</strong></h2>
							<ul>
								<li><strong>Centro:</strong> I.E.S Carrús</li>
								<li><strong>Graduación:</strong> 2017</li>
							</ul>
						</li>
						<li v-if="selected == 'TIC'">
							<h2><strong>Administración de Sistemas Informáticos en Red</strong></h2>
							<ul>
								<li><strong>Centro:</strong> I.E.S. Severo Ochoa</li>
								<li><strong>Graduación:</strong> 2018</li>
							</ul>
						</li>
						<li v-if="selected == 'TIC'">
							<h2>Beca Everis</h2>
							<ul>
								<li>Lugar: San Juan (Alicante)</li>
								<li>Fecha inicio: 01/2019</li>
								<li>Fecha Fin: 03/2019</li>
								<li>Contenido:
									<ul>
										<li><h5>.net Framework</h5></li>
										<li><h5>GitHub</h5></li>
										<li><h5>Sharepoint</h5></li>
									</ul>
								</li>
							</ul>
						</li>
					</ul>
				</dd>
				<dd class="clear"></dd>
				<dt class="formacion2" v-if="selected == 'TIC'">Formación complementaria</dt>
				<dd v-if="selected == 'TIC'">
					<h2>Programación</h2>
					<ul>
						<li><h5>Lenguajes</h5>
							<ul>
								<li>Javascript</li>
								<li>Typescript</li>
								<li>C# (.net Framework, .net Core)</li>
								<li>PHP</li>
							</ul>
						</li>
						<li><h5>Conocimiento en Frameworks</h5>
							<ul>
								<li>Vue.js</li>
								<li>jquery</li>
								<li>bootstrap</li>
							</ul>
						</li>
						<li><h5>Tecnologías de microsoft</h5>
							<ul>
								<li>WCF</li>
								<li>WPF</li>
								<li>Azure Web services</li>
							</ul>
						</li>
						<li>
							<h5>Bases de datos</h5>
							<ul>
								<li>MySql</li>
								<li>Postgres</li>
								<li>Sql Server</li>
							</ul>
						</li>
					</ul>
				</dd>
				<dd v-if="selected == 'Electrónica'">
					<h2>Electrónica</h2>
					<p>Reparación mantenimiento y sustitución de partes dañadas de dispositivos moviles, videoconsolas y otros elementos electrónicos</p>
						
					<h2>Telecomunicaciones</h2>
					<p>Instalación y mantenimiento de infraestructuras de TV, internet y teléfono</p>
				</dd>
				<dd class="clear"></dd>
				<dt class="experiencia">Experiencia profesional</dt>
				<dd>
					<ul>
						<li v-if="selected == 'TIC'">
							<h2>Grupo oesía </h2>
							<ul>
								<li>Desarrollo Backend de webservices .net en c#
									<ul>
										<li>Lugar: Murcia</li>
										<li>Fecha de inicio/ Fin: 09/2019-09/2020</li>
									</ul>
								</li>
								<li>Desarrollo Frontend en Vue.js
									<ul>
										<li>Lugar: Murcia</li>
										<li>Fecha de inicio/ Fin: 09/2010-Actualidad</li>
									</ul>
								</li>
							</ul>
						</li>
						<li v-if="selected == 'Carga y descarga'">
							<h2>Hijos de Tomás Pascual</h2>
							<ul>
								<li>Cargo: Mozo</li>
								<li>Lugar: Elche</li>
								<li>Fecha de inicio/ Fin: 2007-2015</li>
								<li>Tareas:
									<ul>
										<li>Descarga/ carga camiones de pollos/ pavos</li>
										<li>Envío de pedidos a los clientes</li>
										<li>Encargado del reciclaje</li>
									</ul>
								</li>
							</ul>
							<h2>Ángel</h2>
							<ul>
								<li>Cargo: Mozo</li>
								<li>Lugar: Mercado plaza de Madrid - Elche</li>
								<li>Fecha de inicio/ Fin: 2014-2015</li>
								<li>Tareas:
									<ul>
										<li>Descarga de camion pescado</li>
										<li>Encargado de limpieza</li>
									</ul>
								</li>
							</ul>
						</li>
						<li v-if="selected == 'Hostelería'">
							<h2>Cafetería Maryant <span>Encargado de terraza - Elche, Alicante - 2016-Actualidad</span></h2>
							<ul>Tareas:
								<li>Recoger terraza</li>
								<li>Limpiar terraza</li>
							</ul>
						</li>
					</ul>
				</dd>					
				<dd class="clear"></dd>
				<dt class="idiomas">Idiomas</dt>
				<dd>
					<ul>
						<li><strong>Inglés:</strong> equivalente a B1</li>
						<li><strong>Valenciano:</strong> equialente a A2</li>
						<li><strong>Español:</strong> Nativo</li>
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
