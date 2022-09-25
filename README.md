# Detección e identificación de clústeres por afectación de dengue en Colombia: una aproximación desde el Aprendizaje no Supervisado

![Python](https://img.shields.io/badge/python-v3.6+-blue.svg)
[![Build Status](https://travis-ci.org/anfederico/clairvoyant.svg?branch=master)](https://travis-ci.org/freddy120/MIAD_no_supervisado_project)
![Dependencies](https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen.svg)
[![GitHub Issues](https://img.shields.io/github/issues/freddy120/MIAD_no_supervisado_project.svg)](https://github.com/freddy120/MIAD_no_supervisado_project/issues)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Resumen

El dengue es una enfermedad viral transmitida por la picadura de mosquitos infectados que se caracteriza por producir fiebre, dolor corporal, pérdida del apetito y, en casos graves, sangrado de mucosas. La población más vulnerable a esta enfermedad son niños y adultos mayores, sin embargo, puede afectar a cualquier grupo demográfico. Según el Instituto Nacional de Salud (INS), a julio de 2022, en Colombia se han presentado 34.017 casos, dentro de los cuales el 52,4% presentaron signos de alarma o graves (1,2).
Es posible prevenir y controlar su propagación concientizando a la población para evitar la proliferación de mosquitos que transmiten esta enfermedad. Así, a través de un análisis de clústeres se estratificaron 1.120 municipios de Colombia según el riesgo de incidencia de dengue de acuerdo con sus características demográficas (edad, población), socioeconómicas (desempleo, estratos), y climáticas (temperatura, precipitaciones), encontrando que existe un mayor riesgo de tasa de incidencia de dengue en municipios de clima cálido.
Los resultados de este proyecto permitirían dirigir recursos hacia la capacitación y concientización de la población para la prevención y control del dengue eficientemente en aquellas zonas de mayor riesgo de incidencia del dengue.
<br>
<br>
**Palabras clave**: Dengue, Epidemia, Aprendizaje no Supervisado, Clústeres, K-Means, time series.   
<br>
<p align="center"><img width=50% src="https://github.com/freddy120/MIAD_no_supervisado_project/blob/main/images/dengue.png"></p>
<br>

## Archivos de interés:
* [ Jupyter Notebook](https://github.com/freddy120/MIAD_no_supervisado_project/blob/main/notebook/Final_Project.ipynb)
* [ Dataset Dengue en Municipalidades Colombia](https://github.com/freddy120/MIAD_no_supervisado_project/blob/main/data/dengue_data_all_municipalities.csv)
* [ Documento del trabajo realizado](https://github.com/freddy120/MIAD_no_supervisado_project/blob/main/doc/Entrega%20proyecto.pdf)
* [ Video Explicativo](https://github.com/freddy120/MIAD_no_supervisado_project/blob/main/doc/Entrega%20proyecto.pdf)

## Exploración de los datos:

Lectura de los datos
```python
dengue_df = pd.read_csv("../data/dengue_data_all_municipalities.csv")
```

* Casos de Dengue: 
  * Casos de dengue semanales basado en la semana epidemiológica: desde la primera semana epidemiológica del año 2007 a la última semana epidemiológica del año 2019. ***Year/epiweek (Año/Semana epidemiológica)***
  * También se puede encontrar casos anuales de dengue entre 2007 y 2019.
* Datos Sociodemograficos y Socioeconómicos:
  * Identificador único del Municipio. ***Municipality code***
  * Nombre del Municipio. ***Municipality***
  * Población para cada municipio entre el año 2007 y el 2019. ***Population2007, Population2008, …, Population2019***
  * Porcentaje de población que pertenece a una cierta edad. ***Age0-4(%), Age5-14(%), Age15-29(%), Age>30(%)***
  * Porcentaje de población afrocolombiana. ***AfrocolombianPopulation***
  * Porcentaje de población india. ***IndianPopulation***
  * Porcentaje de personas con discapacidades: esta variable describe el grupo de personas que tienen alguna limitación física, psicológica o mental. ***PeoplewithDisabilities***
  * Porcentaje de personas que no pueden leer o escribir. ***Peoplewhocannotreadorwrite***
  * Porcentaje de personas que tiene nivel de educación secundario/superior. ***Secondary/HigherEducation***
  * Porcentaje de población empleada. ***Employedpopulation***
  * Porcentaje de población desempleada. ***Unemployedpopulation***
  * Porcentaje de personas que realizan trabajo doméstico. ***Peopledoinghousework***
  * Porcentaje de personas jubiladas. ***Retiredpeople***
  * Género o población en porcentaje de hombres y mujeres. ***Men(%), Women(%)***
  * Hogares sin acceso a agua. ***Householdswithoutwateraccess***
  * Hogares sin acceso a internet. ***Householdswithoutinternetaccess***
  * Estratificación de las viviendas entre 1 y 6. ***Buildingstratification1(%), Buildingstratification2(%), …, Buildingstratification6(%)***
  * Número de hospitales por Km2. ***NumberofhospitalsperKm2***
  * Número de casas por Km2. ***NumberofhousesperKm2***
* Temperatura y Precipitaciones:
  * Temperatura mensual para cada municipio en Colombia. ***TEMPERATURE_jan_07, …, TEMPERATURE_dec_18***
  * Precipitaciones mensuales para cada municipio en Colombia. ***PRECIPITATION_jan_07, …, PRECIPITATION_dec_18***


Casos en Medellin a lo largo del tiempo, desde 2007 a 2019
![](https://github.com/freddy120/MIAD_no_supervisado_project/blob/main/images/medellin_casos.png)


## Fuentes de datos
* Sistema de Vigilancia en Salud Pública (SIVIGILA) del Insituto Nacional de Salud (INS). Por solicitud se puede acceder a las bases de datos de los casos semanales de dengue por semana epidemiológica desde el 2007. (http://portalsivigila.ins.gov.co/)
* Departamento Administrativo Nacional de Estadística (DANE). Cuenta con bases de datos abiertos sobre la población desde el año 2007, con datos como la edad, género, raza, nivel educativo, ocupación, información sobre el hogar, información geográfica como viviendas y hospitales por Km2. (https://www.dane.gov.co/index.php/en/52-espanol/noticias/noticias/4325-bases-de-datos-anonimizadas-disponibles-en-la-web)
* Datos climáticos. Existen varias fuentes con datos abiertos para su obtención. (https://earthengine.google.com/, https://www.worldclim.org/)
* Comunidades de ciencia de datos. Dado el impacto social en la salud pública de la infección por dengue, existen varias organizaciones que han dispuesto datasets para competencias. (https://www.kaggle.com/datasets/davidrestrepo/dengue, https://www.kaggle.com/datasets/davidrestrepo/stratification-of-dengue-in-cauca-colombia)
* DrivenData (https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/page/80/)

## Resultados



## Referencias:
* Instituto Nacional de Salud. Protocolo de Vigilancia de Dengue [Internet]. INS 2022. [citado el 20 de agosto de 2022. Disponible en: https://www.ins.gov.co/buscadoreventos/Lineamientos/Pro_Dengue.pdf 
* Instituto Nacional de Salud. Informe de Evento Dengue [Internet]. INS 2022. Citado el 20 de agosto de 2022. Disponible en: https://www.ins.gov.co/buscadoreventos/Informesdeevento/DENGUE%20PE%20VII%202022.pdf 
* World Health Organization. Dengue and severe dengue [Internet]. WHO 2022. Citado el 04 de septimebre de 2022. Disponible en: https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue#:~:text=The%20number%20of%20dengue%20cases,affecting%20mostly%20younger%20age%20group. 
* Organización Panamericana de la Salud. Dengue [Internet]. OPS. 2020. Citado el 20 de  agosto de 2022. Disponible en: https://www.paho.org/es/temas/dengue 
* Thomas SJ, Rothman AL. Dengue virus infection: Epidemiology. In: UpToDate, Shefner JM (Ed), UpToDate, Waltham, MA. (Accessed on September 04, 2022.) 
Bhatt S, Gething PW, Brady OJ, et al. The global distribution and burden of dengue. Nature. 2013;496(7446):504-507. doi:10.1038/nature12060 
*Sanna M, Hsieh YH. Ascertaining the impact of public rapid transit system on spread of dengue in urban settings. Sci Total Environ. 2017;598:1151-1159. doi:10.1016/j.scitotenv.2017.04.050 
* G. M. Nandana, S. Mala and A. Rawat, "Hotspot Detection of Dengue Fever Outbreaks Using DBSCAN Algorithm," 2019 9th International Conference on Cloud Computing, Data Science & Engineering (Confluence), 2019, pp. 158-161, doi: 10.1109/CONFLUENCE.2019.8776916. 
* Hoyos W, Aguilar J, Toro M. Dengue models based on machine learning techniques: A systematic literature review. Artif Intell Med. 2021;119:102157. doi:10.1016/j.artmed.2021.102157 
* Delmelle E, Hagenlocher M, Kienberger S, Casas I. A spatial model of socioeconomic and environmental determinants of dengue fever in Cali, Colombia. Acta Trop. 2016;164:169-176. doi:10.1016/j.actatropica.2016.08.028 


## Equipo
* Maria Paula Salamanca Delgado (m.salamancad@uniandes.edu.co)
* William Alexander Romero Bolívar (w.romerob@uniandes.edu.co)
* Jorge Oswaldo Suárez Rodríguez (j.suarez1@uniandes.edu.co)
* Freddy Rodrigo Mendoza Ticona (r.mendozat@uniandes.edu.co)

Feel free to contact us for any doubt.\
Enjoy :smile:!!

## License
MIT License. See LICENSE for details.
