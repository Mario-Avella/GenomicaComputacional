
# Comandos de la Práctica 02
## Equipo 01 
### Integrante 1: Astrid Austria López
### Integrante 2: Xochitl Vanessa Conde Alonzo 
### Integrante 3: Mario Alberto Avella Villalobos

# Parte I. 

**Respuesta 1**

Tabla

| Plataforma/ compañía      | Longitud de reads (pb) | # reads x run   | Tiempo      | Costo x 10^6 bases | Error (%) | Química                 |                                                 |
|---------------------------|------------------------|-----------------|-------------|--------------------|-----------|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------
|Primera Generación         |                        |                 |             |                    |           |                         | 
| Sanger/Life technologies  | 800                    | 1               | 2 hrs       | $2400              | 0.3       | Dideoxy terminator      |
| Método de Maxam y Gilbert | 400 - 900 pb           | 96              | 2 hrs       | $500 (0.5 $ x 1kb) | 0.3       | Secuenciación por degradación química|

|Segunda Generación         |                        |                 |             |                    |           |                         |                                 
| Illumina/ HiSeq           | 50 - 250               | 5x10^9          | 27-240 hrs  | ~$0.10             | 0.8       |Revesible terminators    |
| Roche/ 454                | 700                    | 1000000         | 1 - 2 día   | $10                | 1         |Pyrosequencing           |
|Tercera generación         |                        |                 |             |                    |           |                         |
| PACBio/ SMRT              | 2900                   |1x10^6           |<2 hrs       | $2                 | 12.9      |Real-time SMS            | 
| Nanopore/ Oxford          | >5000                  | 6x10^4          | 3 días      | <1                 | 34        |Real-time SMS            |
| Heliscopio/ Helicos       | 35                     | 7x10^9          |8 días       | $0,01              | 0.2       |Real-timw SMS            |

Referencias: 
[1] Kulski, J. (2016). Next-Generation Sequencing — An Overview of the History, Tools, and “Omic” Applications. Next Generation Sequencing–Advances, Applications and Challenges, 3-60. https://www.intechopen.com/books/next-generation-sequencing-advances-applications-and-challenges/next-generation-sequencing-an-overview-of-the-history-tools-and-omic-applications (Consultada el 10 de Diciembre del 2020)
[2] Wikipedia contributors. (2020). Maxam–Gilbert sequencing. In Wikipedia, The Free Encyclopedia. Recuperado el 10 de Diciembre del 2020 de https://en.wikipedia.org/w/index.php?title=Maxam%E2%80%93Gilbert_sequencing&oldid=996250084 

# Parte II

**Respuesta 1**

1) Repositorio donde están las secuencias: https://www.ebi.ac.uk/ena/browser/view/PRJEB5172

2) El archivo comprimido se bajó y movió a la carpeta de trabajo, descromprimiéndose con la siguiente secuencia:

```
 para descomprimir:

 unzip ena_files.zip
 
 gunzip ERR486827_1.fastq.gz

 gunzip ERR486827_2.fastq.gz
 ```

3) Convertir el archivo de `fastq` a `fasta`

```
 awk '{if (NR% 4 == 1) {printf (">% s \ n", substr ($ 0,2));} else if (NR% 4 == 2) print;}' ERR486827_1.fastq > secuencia1.fa

 awk '{if (NR% 4 == 1) {printf (">% s \ n", substr ($ 0,2));} else if (NR% 4 == 2) print;}' ERR486827_2.fastq > secuancia2.fa
```

**Respuesta 2** 

¿Ambos archivos fasta tienen la misma cantidad de secuencias?

> Sí, demostrándose con lo siguiente:

```
grep -c "^>" ~/secuencia1.fa
 
> 398824

grep -c "^>" ~/secuancia2.fa

> 398824
```

# Parte III

**Respuesta 1** 

para descomprimir:

 unzip FastQC-0.11.9.zip

para dar permisos de ejecución:

chmod +x fastqc 

#/Users/uliaus/Desktop/FastQC-0.11.9

 para el enlace simbólico: sudo ln -s /Users/uliaus/Desktop/FastQC-0.11.9/fastqc /usr/local/bin/fastqc

Para hacerlo ejecutable:
 
export PATH=$PATH:/Users/uliaus/desktop/FastQC

**Respuesta 2**

Creación de script (el archivo se encuentra en la carpeta Equipo01_p03)

**Respuesta 3**

Archivo html (se encuentra dentro de la carpeta en formato pdf y html)

file:///Users/uliaus/pruebanueva/ERR486827_1_fastqc.html
file:///Users/uliaus/pruebanueva/ERR486827_2_fastqc.html

####Descripcion de lecturas 

La calidad de ambas secuenciaciones es muy buena, porque las secuencias se encuentran entre los valores de calidad de 30-40 phreds, lo que significa que la probabilidad de que los pares de bases sean correctas está en un rango del 99.9% al 99.99%. El comportamient1o de la gráfica de calidad es bastante estable a lo largo de todas las lecturas.

**Respuesta 4**

cobertura= (150*398824)/580000 = 103.1441


# Parte IV

**Respueta 1**

Secuencias crudas de Saccharomyces (_Saccharomyces cerevisiae_)

Saccharomyces cerevisiae tiene un genoma pequeño, un tiempo de duplicación relativamente corto y se puede analizar genéticamente, muchos de los avances que se han hecho en biología molecular han utilizado esta levadura como herramienta de investigación. Este organismo tiene importantes usos industriales para la producción de cerveza, pan, vino, péptidos y proteínas recombinantes. Saccharomyces cerevisiae también se aísla de productos lácteos que incluyen leche, yogures y quesos, verduras fermentadas y productos vegetales mínimamente procesados, aunque la importancia de esta especie en el deterioro de estos productos no está claramente definida. La transformación de la levadura generalmente se realiza de dos maneras: ya sea mediante la formación de esferoplastos, incluida la eliminación de la pared celular, o mediante un tratamiento más rápido de células intactas con cationes alcalinos como organismo hospedador para la expresión de ADN extraño, introducido en forma de vectores de ADN plasmídico , ha sido una parte importante de los avances actuales que se han producido en la tecnología del ADN recombinante.

 Secuencias obtenidas de: https://www.ebi.ac.uk/ena/browser/view/PRJNA33187

**Respuesta 2**

Se utilizó el método Sanger para la secuenciación del genoma

Es una técnica de secuenciación dirigida que utiliza cebadores de oligonucleótidos para buscar regiones de ADN específicas. En primer lugar se lleva a cabo la desnaturalización del ADN de doble hebra, teniendo una sola hebra de ADN se hibrida on cebadores de oligonucleótidos y se alarga usando una mezcla de dNTP que otorgan los nucleótidos de arginina, citosina, tirosina y guanina necesarios para contruir la nueva estructura de doble hebra. Se agregara tambien una cantidad de ddNTP para cada nucleótido. Las probabilidades de que dNTP y ddNTP de unirse a la secuencia es la misma. Los ddNTP incluyen iuna marcador florescente que al unirse a la secuencia de alargamiento, la base emite flourescencia segun el nucleótido que se asocia. Las lecturas son registradas de a cuendo a la intensidad flourescente.

Fuentes

https://www.sanger.ac.uk/research/projects/genomeinformatics/sgrp.html

**Respuesta 3**

cobertura = (1280 * 1254)/12156677 = 1.3239

**Respuesta 4**

*FastQC
*.html (se muestra en la carpeta Equipo01_p02 en formato pdf)

Las secuenciaciones de 1-9 indican una mala calidad debido a que las lecturas se encuentran en un rango de 0-10 phreds mientras que las secuencias de 100-649 marcan 
una calidad media a buena en un rango de 22-56 phreds. La gráfica vuelve a bajar en las secuencias 850-1049 las cuales se encuentran de 6-40, las lecturas no se 
mantienen estables a lo largo de la gráfica lo que indica alguna falla durante la secuenciacion o antes de la misma.

**Respuesta 5**

valores de phred de 10-32 dando un resultado fallido indicado por el mismo programa.

**Respuesta 6** 

Se propone un corte de las secuencias en la parte de inicio que tienen valores de phred de 0-10 y en la parte final con valores de 6-40 phreds. El corte de 
secuencias se llevaría a cabo acabo utilizando ERNE-filter ya que con este programa se pueden recortar las lecturas al eliminar las bases de baja calidad en los 
extremos de estas y filtrar aquellas que están contaminadas.
