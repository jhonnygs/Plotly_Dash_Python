# Plotly_Dash_Python
En el siguiente documento se observa un dash que explica la Contaminación del medio ambiente causado por nuevos vehiculos en UK en el año 2016, esta es una forma de como a través de python podemos utilizar la librería plotly para realizar gráficos interactivos y combinar otros atribultos como HTLM, inputs y outputs.



	
	#pip install dash
	#pip install chart_studio
	#pip install cufflinks
	#pip install plotlyimport matplotlib.pyplot as plt
	#pip install hvplot
	#pip install dash-mantine-components
	# pip install dash-bootstrap-components
	import matplotlib as mpl
	import matplotlib.ticker as plticker
	import seaborn as sns
	import pandas as pd
	import numpy as npb
	import seaborn as sns
	import pandas as pd
	import numpy as np
	import plotnine 
	import dash_mantine_components as dmc 
	import chart_studio.plotly as py
	import plotly.express as px
	%matplotlib inline
	import plotly.offline as pyo
	from plotnine import *
	from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
	init_notebook_mode(connected=True)
	import cufflinks as cf
	cf.go_offline()
	cf.set_config_file(offline=False, world_readable=True)
	import dash
	from dash import Dash,html, dcc, Output, Input  
	import dash_bootstrap_components as dbc    
	import plotly.express as px     
	import plotly.graph_objects as go
	from plotly.subplots import make_subplots

	# incorporate data into app
	df= pd.read_csv("https://raw.githubusercontent.com/jhonnygs/ucm_master_2023_PYTHON/main/vehiculos_UK_2016.csv",sep = "|")
	df = df.fillna(0)
	#tratamiento de los datos
	para_treemap = df[["Manufacturer", 
										 "Tipo"]].value_counts()
	para_treemap
	para_tree2 = para_treemap.reset_index(name = "count")
	para_tree2

	para_treemap1 = df[["Manufacturer", 
											'Tipo','CO2gkm']].value_counts()
	para_tree21 = para_treemap1.reset_index(name = "count")


	# Construción de componentes
	app = Dash(__name__, title= "JGS",  external_stylesheets=[dbc.themes.LUX])
	mytitle = html.H1("Contaminación del medio ambiente causado por nuevos vehiculos en UK en el 2016",
													 style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'})

	mytext= html.Div(dcc.Markdown( "El medio ambiente se ve afectado por diversos contaminantes ya sean cotaminantes de tipo"+
										" atmosferico, hidrico o subterraneos. En este estudio nos centraremos en la producción"+
									 " de contaminantes atmosfericos producidos por nuevos vehiculos en el año 2016 en la region de UK. "+
									 "Primeramente debemos definir conceptos de lo que se va a estudiar:" ,
													 style={'fontSize':15, 'textAlign':'center', 'fontFamily': 'Roboto'}))

	mytext1= html.Div("La contaminación atmosférica es la presencia que existe en el aire de pequeñas partículas o productos "+ 
										"secundarios gaseosos que pueden implicar riesgo, daño o molestia para las personas, plantas y animales "+
										"que se encuentran expuestas a dicho ambiente. "+
										"Los principales medios por los cuales se produce contaminación atmosférica se concentran en los procesos "+
										"industriales en donde se realiza combustión, así como por fuentes móviles tales como los automóviles." ,
													 style={'fontSize':15, 'textAlign':'center', 'fontFamily': 'Roboto'})

	mytext2= html.H2("Cantidad de tipos de automóviles por modelo",
													 style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'})

	mytext3= html.Div('''En el siguiente mapa de arbol se puede observar los modelos nuevos de autos clasificandos por tres 
											 tipos de carburante, observamos que los modelos de BMW tienen mayor cantidad tanto en Disel como en 
											 Gasolina, por otra parte se observan otros tipos de combustibles que se han agrupado debido a su baja 
											 producción de contaminantes llamada HEV en la cual el modelo más contaminante es Lexus. 
											''',
													 style={'fontSize':15, 'textAlign':'center', 'fontFamily': 'Roboto'})

	mytext4= html.Div(dcc.Markdown( '''El propósito del estudio a continuación es ayudar a los consumidores a tomar una decisión informada al 
									comprar un automóvil nuevo, permitiéndoles identificar fácilmente los modelos que podrían ahorrarles dinero 
									en costos de combustible y reducir el impacto en el medio ambiente. La guía enumera las cifras de rendimiento 
									de consumo de combustible, dióxido de carbono (CO2) y otras emisiones de los automóviles NUEVOS, actualmente 
									en el mercado en el Reino Unido. También busca asesorar sobre temas ambientales clave, así como brindar 
									orientación sobre formas de reducir el impacto de los automóviles en el medio ambiente. Las cifras que se 
									muestran se obtienen de las pruebas oficiales, que se requieren antes de que un modelo de automóvil pueda 
									ofrecerse a la venta. Las cifras se enumeran para la mayoría de los automóviles nuevos de gasolina y diésel 
									a la venta en el Reino Unido, así como para algunos automóviles propulsados por combustibles alternativos 
									(gas licuado de petróleo o Gas natural comprimido). También se enumeran las cifras de algunos vehículos 
									híbridos, que utilizan tanto motores eléctricos como de combustión interna, y de coches eléctricos puros.''',

																 style={'fontSize':15, 'textAlign':'center', 'fontFamily': 'Roboto'}))

	mytext5= html.Div( '''El cambio climático, a menudo denominado calentamiento global (que es un aspecto del cambio climático), se 
									considera una de las mayores amenazas ambientales que enfrenta el mundo en la actualidad. Cuando los 
									hidrocarburos (HC) (gasolina, diésel y la mayoría de los combustibles alternativos) se queman para obtener 
									energía en un motor de combustión interna, los principales subproductos son agua y dióxido de carbono (CO2),
									junto con otras emisiones. Aunque no es directamente dañino para la salud humana, el CO2 es el más 
									importante de los gases de efecto invernadero que contribuyen al cambio climático. En 2013, las emisiones 
									del transporte nacional representaron alrededor de una quinta parte de todas las emisiones de gases de 
									efecto invernadero (GEI) del Reino Unido, y el transporte por carretera contribuyó con alrededor del 93 % 
									de las emisiones de GEI del transporte. El transporte por carretera es también una de las principales 
									fuentes de contaminantes de la calidad del aire que son perjudiciales para la salud humana, especialmente 
									en las zonas urbanas.''' ,
													 style={'fontSize':15, 'textAlign':'center', 'fontFamily': 'Roboto'})

	mytext6 = html.Div([
					dcc.Markdown('''
					## Medidas para reducir las emisiones de CO2 de los automóviles
					'''),
					dcc.Markdown('''
					En **1998**, la Comisión Europea y las asociaciones industriales de los principales fabricantes de vehículos de motor acordaron 
					reducir las emisiones medias de CO2 de los coches nuevos. Este acuerdo voluntario pretendía reducir las emisiones medias de 
					CO2 de los coches nuevos en más del 25 % para 2008/2009 a 140 g CO2/km y, como resultado, ver una mejora del 25 % en el consumo 
					medio de combustible.
					'''),
					dcc.Markdown('''
					En 2009 entró en vigor un Reglamento europeo que establece objetivos vinculantes para reducir las emisiones de CO2 de los coches nuevos 
					(Reglamento CE nº 443/2009). Las principales características del Reglamento son las siguientes:
					* El objetivo es una media global de la flota europea de 130 g/km de emisiones de CO2 a partir de 2015 (a partir de 2012);
					* Para cumplir con este promedio, los fabricantes establecen un objetivo de emisiones específico, en función de los tipos de vehículos que realmente venden en un año determinado, en lugar de exigir que cada vehículo individual tenga menos de 130 g de CO2/km. Esto permite que una amplia gama de vehículos permanezca a la venta y los fabricantes decidan dónde realizar mejoras para garantizar el cumplimiento;
					* El 'tipo' de vehículo está actualmente determinado por su masa. Los fabricantes que venden predominantemente autos más pesados tendrán un objetivo de gramos de CO2/km más alto;
					* Existen diferentes arreglos para los fabricantes que producen cantidades muy pequeñas de automóviles en cualquier año, a fin de proteger la diversidad del mercado;
					* Existe otro objetivo de mejora a partir de 2021, fijado en 95 g CO2/km (95 % de la flota en fase de incorporación a partir de 2020).
					'''),

					dcc.Markdown('''
					 [Soporte de datos](https://carfueldata.vehicle-certification-agency.gov.uk/downloads/download.aspx?rg=aug2016).
					'''),
			dcc.Markdown('''
					No obstante se puede observar un promedio de producción de CO2 en base al frabricante observando el siguiente grafico:
					''')
					], style={'fontSize':15, 'fontFamily': 'Roboto'})




	# fig.update_layout( ... )
	mypic= html.Img(src="https://png.pngtree.com/thumb_back/fw800/background/20190830/pngtree-background-of-planet-earth-contaminated-by-oil-image_309840.jpg",
											style="color: green; background:transparent" ,
													 className= "banner")

	mypic1= html.Img(src="https://climate.selectra.com/sites/climate.selectra.com/files/styles/_default/public/autres/efecto-invernadero-750.png?itok=uvfb5uQ4",
									 className= "banner", style={'width': '45%', 'height': '35%'})



	mygraph = dcc.Graph(figure={})

	mygraph1 = dcc.Graph(figure={})

	mygraph3 = dcc.Graph(figure={})

	mygraph6 = dcc.Graph(figure={})

	fig2 = px.treemap(para_tree2, 
									 path = ["Tipo", 'Manufacturer'],
									 values = 'count',
									 color='count',
									 color_continuous_scale='RdPu')
	fig4 = px.treemap(para_tree21, 
									 path = ['Tipo', 'Manufacturer'],
									 values = 'CO2gkm',
									 color='CO2gkm',
									 color_continuous_scale='deep')

	mygraph2 = dcc.Graph(figure=fig2)
	mygraph4 = dcc.Graph(figure=fig4)

	dropdown = dcc.Dropdown(options=[{'label': 'CO', 'value': 'EmissionsCOmgkm'},
																	{'label': 'NOx', 'value': 'EmissionsNOxmgkm'},
																	 {'label': 'CO2', 'value': 'CO2gkm'},
																 {'label': 'THC', 'value': 'THCEmissionsmgkm'},       
																	 {'label': 'No Particulas', 'value': 'ParticulatesNo_mgkm'},                                 
																	 ],
													value='CO2gkm',  # Primera carga de visualización 
													clearable=False)

	reference= html.Div([
			html.Label(["Fuente: ",
							html.A('vehiculos_UK_2016.csv',
											href='https://raw.githubusercontent.com/jhonnygs/ucm_master_2023_PYTHON/main/vehiculos_UK_2016.csv'),
													". Acceso en 02/03/2023"
										 ]),
			html.Div(html.Label([
					html.P(["  Desarollado por Jhonny González Sánchez (jhonnygs01@gmail.com)"])
			]))
					], style={'textAlign': 'center',
											'fontFamily' : "Roboto",
											'paddingTop': 15
											}
			)

	#co2           
	mycont = html.Div([dcc.Markdown(children='')])


	# Customize your own Layout Aquí se ponen todas nuestras salidas visuales
	app.layout = dbc.Container([

			dbc.Row([
					dbc.Col([mytitle]) #titulo principal
			]),

			dbc.Row([
					dbc.Col([mytext]) #texto principal 
			]),

			dbc.Row([
					dbc.Col([mytext1]) #texto que siguie 
			]),

			dbc.Row([
					dbc.Col(html.H3([mypic1],style={'textAlign': 'center'})) #imagen 
			]),

			dbc.Row([
					dbc.Col([mytext4]) #texto que siguie 
			]),

			dbc.Row([
					dbc.Col([mytext5] ,style={'textAlign': 'center'}) #texto que siguie 
			]),    

			html.Hr(), #barra espaciadora ############################################

			dbc.Row([
					dbc.Col([mytext2]) #Titulo del treemap
			]), 

			dbc.Row([dbc.Col([mytext3]) #texto de treemap
			]),

			dbc.Row([
					 dbc.Col([mygraph2])  #grafico de treemap    
			]),

			dbc.Row([dbc.Col([mytext6]) #texto de treemap
			]),

			dbc.Row([
					 dbc.Col([mygraph4])  #grafico de treemap    
			]),

			html.Hr(), ######################################################

			dbc.Row([
					dbc.Col([dropdown], width=3) #Despliegue de lo que queremos ver en la tercera parte de la web
			]),

			html.Div(id='tabs-content-classes-2', children={}), #cambio en base a lo que se elija explicando cada texto

			dbc.Row([

							 dbc.Col([mygraph1]),
							dbc.Col([mygraph6]), 
							 dbc.Row([dbc.Col([mygraph]),
												dbc.Col([mygraph3])
											 ]) #dash con todos los graficos 
			]),

			dbc.Row([
					dbc.Col([reference]) #referencias 
			])

	], fluid=True)


	@app.callback(
			Output(mygraph, component_property='figure'),
			Output(mygraph1, component_property='figure'),
			Output(mygraph3, component_property='figure'),
			Output(mygraph6, component_property='figure'),
			Input(dropdown, component_property='value')
	)
	def update_graph(user_input):  # function arguments come from the component property of the Input
			if user_input == 'EmissionsCOmgkm':              

					fig = go.Figure(data=[go.Pie(labels=df["Tipo"], values=df['EmissionsCOmgkm'], hole=.3)])

					fig.update_traces(hole=.4, hoverinfo="label+percent+value")

					fig.update_layout(
									title_text="Porcentaje de monoxidos de carbono por combustible",
									# Add annotations in the center of the donut pies.
									annotations=[dict(text='CO', x=0.50, y=0.5, font_size=20, showarrow=False)]) 

					fig1 = px.scatter(df, x='EngineCapacity', 
											 y='FuelCost12000Miles',
											 trendline="ols", 
											 color='EmissionsCOmgkm', 
											 size='EmissionsCOmgkm', 
											 color_continuous_scale="PuBu",
											 labels={
															 "EngineCapacity": "Capacidad del motor",
															 'FuelCost12000Miles': "Costo de Combustible por 12000Millas" 
															 })     

					fig3 = px.bar(df, x=['MetricUrbanCold', "MetricExtraUrban", "MetricCombined"], 
												y='EmissionsCOmgkm')

					fig6 = px.box(df, x="Tipo", y="EmissionsCOmgkm", points="all", color="Tipo") 

			elif user_input == "EmissionsNOxmgkm":

					fig = go.Figure(data=[go.Pie(labels=df["Tipo"], values=df["EmissionsNOxmgkm"], hole=.3)])

					fig.update_traces(hole=.4, hoverinfo="label+percent+value")

					fig.update_layout(
									title_text="Porcentaje de oxidos nitrosos por combustible",
									# Add annotations in the center of the donut pies.
									annotations=[dict(text='NOx', x=0.50, y=0.5, font_size=20, showarrow=False)])         

					fig1 = px.scatter(df, x='EngineCapacity', 
											 y='FuelCost12000Miles',
											 trendline="ols", 
											 color="EmissionsNOxmgkm", 
											 size="EmissionsNOxmgkm", 
											 color_continuous_scale="PuBu",
											 labels={
															 "EngineCapacity": "Capacidad del motor",
															 'FuelCost12000Miles': "Costo de Combustible por 12000Millas" 
															 })  

					fig3 = px.bar(df, x=['MetricUrbanCold', "MetricExtraUrban", "MetricCombined"], 
												y="EmissionsNOxmgkm") 

					fig6 = px.box(df, x="Tipo", y="EmissionsCOmgkm", points="all", color="Tipo")

			elif user_input == "THCEmissionsmgkm":

					fig = go.Figure(data=[go.Pie(labels=df["Tipo"], values=df["THCEmissionsmgkm"], hole=.3)])

					fig.update_traces(hole=.4, hoverinfo="label+percent+value")

					fig.update_layout(
									title_text="Porcentaje de THC por combustible",
									# Add annotations in the center of the donut pies.
									annotations=[dict(text='THC', x=0.50, y=0.5, font_size=20, showarrow=False)])        


					fig1 = px.scatter(df, x='EngineCapacity', 
											 y='FuelCost12000Miles',
											 trendline="ols", 
											 color="THCEmissionsmgkm", 
											 size="THCEmissionsmgkm", 
											 color_continuous_scale="PuBu",
											 labels={
															 "EngineCapacity": "Capacidad del motor",
															 'FuelCost12000Miles': "Costo de Combustible por 12000Millas" 
															 }) 

					fig3 = px.bar(df, x=['MetricUrbanCold', "MetricExtraUrban", "MetricCombined"], 
														y="THCEmissionsmgkm")

					fig6 = px.box(df, x="Tipo", y="EmissionsCOmgkm", points="all", color="Tipo") 

			elif user_input == "ParticulatesNo_mgkm":

					fig = go.Figure(data=[go.Pie(labels=df["Tipo"], values=df["ParticulatesNo_mgkm"], hole=.3)])

					fig.update_traces(hole=.4, hoverinfo="label+percent+value")

					fig.update_layout(
									title_text="Porcentaje de Emisión de Número de particulas",
									# Add annotations in the center of the donut pies.
									annotations=[dict(text='No P', x=0.50, y=0.5, font_size=20, showarrow=False)])

					fig1 = px.scatter(df, x='EngineCapacity', 
											 y='FuelCost12000Miles',
											 trendline="ols", 
											 color="ParticulatesNo_mgkm", 
											 size="ParticulatesNo_mgkm", 
											 color_continuous_scale="PuBu",
											 labels={
															 "EngineCapacity": "Capacidad del motor",
															 'FuelCost12000Miles': "Costo de Combustible por 12000Millas" 
															 })

					fig3 = px.bar(df, x=['MetricUrbanCold', "MetricExtraUrban", "MetricCombined"], 
												y="ParticulatesNo_mgkm")

					fig6 = px.box(df, x="Tipo", y="EmissionsCOmgkm", points="all", color="Tipo") 

			elif user_input == 'CO2gkm':

					fig = go.Figure(data=[go.Pie(labels=df["Tipo"], values=df['CO2gkm'], hole=.3)])

					fig.update_traces(hole=.4, hoverinfo="label+percent+value")

					fig.update_layout(
									title_text="Porcentaje de producción de dioxido de carbono en base al tipo de combustible",
									# Add annotations in the center of the donut pies.
									annotations=[dict(text='CO2', x=0.50, y=0.5, font_size=20, showarrow=False)])

					fig1 = px.scatter(df, x='EngineCapacity', 
											 y='FuelCost12000Miles',
											 trendline="ols", 
											 color='CO2gkm', 
											 size='CO2gkm', 
											 color_continuous_scale="PuBu",
											 labels={
															 "EngineCapacity": "Capacidad del motor",
															 'FuelCost12000Miles': "Costo de Combustible por 12000Millas" 
															 })

					fig3 = px.bar(df, x=['MetricUrbanCold', "MetricExtraUrban", "MetricCombined"], 
												y='CO2gkm') 

					fig6 = px.box(df, x="Tipo", y="EmissionsCOmgkm", points="all", color="Tipo")

			return fig, fig1, fig3, fig6
											# returned objects are assigned to the component property of the Output

	@app.callback(Output('tabs-content-classes-2', 'children'),
								Input(dropdown, component_property='value'))

	def render_content(user_input):
			if user_input == 'EmissionsCOmgkm':
					return html.Div([
							html.H3('Monóxido de Carbono (CO)', 
											style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'}),
							html.Div('''El monóxido de carbono es un gas producido a partir de la combustión incompleta, es decir,
											la combustión en baja concentración de oxígeno. Este puede generarse de forma natural cuando se 
											pxida el metano producido por la descomposición de la materia. No obstante, la gran mayoría está 
											producida por la emisiones de los automóviles, la industria y la quema de distintos productos.
											A pesar de que es muy raro que las concentraciones de monóxido de carbono lleguen a ser los suficiente 
											altas para poner en peligro nuestra salud, el hecho de que compita con el oxígeno en el torrente 
											sanguíneo, hace que las personas con problemas de corazón puedan ver afectadas sus capacidades 
											cardíacas.''', 
											style={'fontSize':15, 'textAlign':'center','fontFamily': 'Roboto'})     
					])
			elif user_input == "EmissionsNOxmgkm":
					return html.Div([
							html.H3('Compuestos provenientes del oxidos de nitrogeno (NOx)', 
											style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'}),
					html.Div('''Dióxido de nitrógeno: Aunque en realidad el dióxido de nitrógeno forma parte de las partículas 
											en suspensión que justo acabamos de explicar, encontramos necesario mencionarlo aparte por el papel 
											que cumplen en la contaminación del aire. El NO2, el dióxido de carbono, se forma en la combustión 
											de los motores, siendo los diésel los que mayor cantidad de NO2 producen.
											Como hemos explicado, es emite principalmente por los motores, esta es la razón por la cual se 
											encuentra en cantidades tan elevadas en las ciudades, sitios donde se acumulan los vehículos y 
											donde no hay ventilación posible. Esta no es una cuestión cualquiera, puesto que, como ya se 
											sospechaba y han demostrado estudios de la OMS, hay una correlación entre las concentraciones 
											de NO2 y la pérdida de funciones pulmonares.''', 
											style={'fontSize':15, 'textAlign':'center','fontFamily': 'Roboto'})
					])
			elif user_input == "THCEmissionsmgkm":
					return html.Div([
							html.H3('Total de hidrocarburos no quemados(THC)', 
											style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'}),
							html.Div('''Los HC son restos de combustible que quedan sin quemar y vapores de aceite, que se generan por una mala ignición, 
													un pobre encendido, pérdida de compresión en el motor o un desgaste excesivo del mismo. Se pueden encontrar en 
													vehículos de diésel o gasolina por igual. 

													Aunque no son mortales para las personas, una concentración alta de estos compuestos en el aire 
													provoca irritación en los ojos, la piel y el sistema respiratorio, por lo que son molestos y pueden 
													agravar enfermedades relacionadas con los pulmones.''', 
											style={'fontSize':15, 'textAlign':'center','fontFamily': 'Roboto'})
					])
			elif user_input == "ParticulatesNo_mgkm":
					return html.Div([
							html.H3('Número de Particulas (No)', 
											style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'}),
							html.Div('''Cuando hablamos de partículas nos referimos a la materia de tamaño microscópico que se encuentra 
													suspendida en el aire. Una forma de verlas, por ejemplo, es en las fachadas ennegrecidas de los 
													edificios de las ciudades, que se vuelven de este color como consecuencia de estas partículas.
													Los estudios que se han hecho en Europa han demostrado que las partículas son consideradas como 
													el agente contaminante más dañino para la salud humana. Pero, ¿de dónde proceden las partículas? La 
													realidad es que no todas son iguales ni tienen el mismo origen. De forma genérica, se pueden separar 
													entre las partículas gruesas y las partículas finas. Las PM 10, es decir, de diámetro menor a las 10 
													micras, básicamente procede como resultado de los procesos mecánicos que se dan en actividades humanas 
													como la construcción. Por otro lado, las PM 2,5, es decir, de diámetro menor a las 2,5 micras, que son 
													resultado de la combustión de carburantes o maderas.

													Son precisamente estas partículas de menor tamaño las que resultan más dañinas para la salud, puesto que 
													tienen la capacidad de penetrar en las vías respiratorias o incluso en la sangre. Entre los problemas de 
													salud que puede acarrear están los problemas respiratorios como las alergias, asma o EPOC, hasta el cáncer 
													o problemas cardiovasculares.''', 
											style={'fontSize':15, 'textAlign':'center','fontFamily': 'Roboto'})
					])

			elif user_input == 'CO2gkm':
					return html.Div([
							html.H3('Dioxido de carbono (CO2)', 
											style={'fontSize':40, 'textAlign':'center','fontFamily': 'Roboto'}),
							dcc.Markdown('''El dióxido de carbono se trata de una molécula que se compone por la unión de dos átomos de oxígeno 
													por uno de carbono CO2. El dióxido de carbono está presente naturalmente en la atmósfera, aunque sus
													niveles de concentración han ido variando a través de la historia de nuestro planeta. Este es uno de 
													los gases de efecto invernadero, lo que lo convierte en indispensable a la hora de mantener la temperatura 
													de la Tierra. De hecho, si no existiera sería imposible la vida en nuestro planeta. Sin embargo, así como una 
													concentración baja sería problemática también lo son las concentraciones altas, que pueden retener demasiado el 
													calor y subir la temperatura como esta sucediendo en la actualidad.''', 
											style={'fontSize':15, 'textAlign':'center','fontFamily': 'Roboto'}),
							dcc.Markdown('''
							* para el gráfico de Scatter se observa un aumento directamente proporcional a nivel, capacidad de motor, costo de combustible
							y producción de dióxido de carbono.

							* En el gráfico circular no hay una diferencia notable entre producción de dióxido de carbono para los dos tipos de 
								combustible HEV. (Esto puede deberse al poco tamaño muestral que tenemos de este tipo de vehículos o a que los combustibles
								no emiten una mayor concentración de CO2.).

							* Hay mayor producción de CO2 en Metric Extra Urban de valor bajo y a su vez observamos que la Metric cold urban se comporta 
							de una manera similar, pero con valores más bajos y con una cola más alargada hacia la derecha.
											''', 
											style={'fontSize':15,'fontFamily': 'Roboto'})
					])


			# Run app
	if __name__=='__main__':
			app.run_server(port=8049)
