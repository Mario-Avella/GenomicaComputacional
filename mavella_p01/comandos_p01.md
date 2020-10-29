# Comandos de la Práctica 01
## Mario Alberto Avella Villalobos

# Parte I 

**Respuesta 1:**

* `echo $SHELL`
/bin/bash

* `echo $0`
-bash

**Respuesta 2:**

`mkdir data/ filtered/ raw_data/ meta/ scripts/ figures/ archive/`

**Respuesta 3:**

`mv filtered/ data/ && mv raw_data/ data/`

**Respuesta 4:**

¿A qué se debe el nombre y la organización de los directorios que acabamos de crear? 
Tras visitar éste [repositorio](https://github.com/u-genoma/BioinfinvRepro/blob/master/Unidad2/Unidad2_Organizacion_proyecto_bioinf.md) me queda claro que la organización de los directorios y los nombres responden a un orden que contemple la naturaleza de los datos y procesos, así como los productos del análisis. Sigue una pauta más o menos estándar en la comunidad y en aquellos repositorios de datos, de manera que esto influye mucho con el concepto y problema de reproducibilidad de la ciencia. La autora del repositorio comenta lo siguiente:
> Un proyecto bioinformático consiste en los datos crudos, datos procesados, scripts y documentación necesarios para reproducir los análisis realizados

De manera que se supone una organización que contemple un directorio para los datos (que incluiría aquellos "datos crudos[*raw_data/*]" y aquellos sometidos a un filtro "[*filtered/*]") que en nuestro caso serían de genomas. Igualmente se contemplarían directorios para los scripts realizados y utilizados en los análisis (*scripts/*), separando aquellos que exclusivamente se utilizarían para generar figuras en su propio directorio (*figures/*). Idealmente también se contempla un directorio para almacenar información referente a las muestras, documentos para procesar los datos y los metadatos (*meta/*), éste directorio suele ponerse a parte o incluirse en el de "datos". Por último, se puede incluir un directorio que sirviese de "archivo" (*archive/*), donde se depositen los scripts que no *sirvieron* pero que no queremos borrar. En el repositorio nos dicen que este directorio NO se sube pero es bueno tenerlo. 
De todas formas, la lógica de la ordenación que se realice de los directorios y los datos debe ir explicada a detalle en un archivo **README**.

# Parte II

`cd scripts/ && touch delay.sh && nano delay.sh`
Se introdujeron las siguientes líneas de código:
```
#!/bin/bash
echo "Después de la Parte I. necesito un descanso de exactamente 30 segundos."
```
**Respuesta 1:**

`chmod 777 delay.sh`

**Respuesta 2:**

`ls -lth delay.sh && ./delay.sh` 

_Por pasos:_

Se escribió el comando `ls -lth delay.sh` obteniéndose:
```
-rwxrwxrwx  1 marioavella  staff   128B Oct 27 12:56 delay.sh
```
Se puede ver que, en efecto, el script ahora posee todos los permisos. Posteriormente se ejecutó el script mediante `./delay.sh`

**Respuesta 3:**

El comando `sleep` (suspende la ejecución por un intervalo de tiempo en segundos) se añadió a la tercera línea de código del script "delay.sh"
```
#!/bin/bash
echo "Después de la Parte I. necesito un descanso de exactamente 30 segundos."
sleep 30
echo "Ya puedo continuar!"
```

**Respuesta 4:**

Imaginemos que en lugar de 30 segundos le pusimos 300, y luego lo corremos en "_backround_":
```
#!/bin/bash
echo "Después de la Parte I. necesito un descanso de exactamente 30 segundos."
sleep 300
echo "Ya puedo continuar!"
```
Al correrlo mediante `./delay.sh &` para que fuese en _backround_, se obtuvo a su vez el PID del proceso (la serie numérica después de [1]):
```
[1] 54745
Después de la Parte I. necesito un descanso de exactamente 30 segundos.
```
Como no queremos esperar 300 segundos, _cancelamos_ el proceso utilizando su PID mediante `kill -9 54745`, obteniéndose:
```
[1]+  Killed: 9               ./delay.sh
```

# Parte III

**Respuesta 1:**

Partimos de Home y nos movemos al directorio **meta/**
`cd GenomicaComputacional/ && cd mavella_p01/ && cd meta/ && touch SarsCov-2.txt`
Con lo anterior generamos el archivo de texto **SarsCov-2.txt** el cual, a continuación, con `nano SarsCov-2.txt` procedemos a escribir el resumen de la [conferencia](https://www.youtube.com/watch?v=I0AbpnFP1g8) acerca de la estructura molecular del SARS-Cov-2, apoyándome también en una [lectura](https://www.nytimes.com/interactive/2020/04/03/science/coronavirus-genome-bad-news-wrapped-in-protein.html) complementaria.

Para fines prácticos el resumen del archivo *SarsCov-2.txt* se reproduce a continuación:
> El virus SARS-CoV-2 (familia Coronaviridae), presenta un tamaño de entre 50-200 nm y su estructura consiste en una cadena de RNA sencilla positiva de 27-32 kb envuelta por una nucleocápside y ésta a su vez rodeada por una capa de glicoproteínas de membrana. De ellas sobresalen las "spike proteins" que son proteínas glicosiladas a las que se les atribuye el mecanismo de patogenicidad. Dicha proteína está formada por un ectodominio: un trímero de dominio S1 (que se une al receptor en las células de vías respiratorias y gastrointestinales: ACE2, provocando una cascada de señalización) unido a un tallo trimérico S2 (encargado de transmitir el péptido de fusión, estirando y fusionando las membranas celulares para permitir que penetre el material genético).

Comprobamos mediante `wc -w SarsCov-2.txt` que la extensión del texto en el archivo **SarsCov-2.txt** no supere las 120 palabras, obteniéndose:
```
     120 SarsCov-2.txt
```
Con 120 palabras en una línea, se da por concluída esta sección.

**Respuesta 2:**

..1. Cambiamos el nombre de los archivos descargados de [NCBI](https://www.ncbi.nlm.nih.gov/) situándonos primero en Home con `cd` y de ahí mediante `cd Downloads/`nos situamos en el directorio donde se descargaron los dos archivos **sequence.fasta** y **sequence.gff3** del genoma de referencia completo del SARS-CoV-2. Renombramos los archivos descargados con la siguiente línea de comandos:
```
 mv sequence.fasta sarscov2_genome.fasta && mv sequence.gff3 sarscov2_genome.gff3
```

..2. Posteriormente del mismo sitio descargamos 3 secuencias de aminoácidos de la proteína _Spike_ del SARS-CoV-2 (correspondientes a Chain C, SARS-CoV-2 spike glycoprotein; Chain B, SARS-CoV-2 spike glycoprotein y Chain A, SARS-CoV-2 spike glycoprotein), obteniéndose:
....a) sequence.fasta
....b) sequence(1).fasta
....c) sequence(2).fasta
Se les renombró con el siguiente comando:
```
mv sequence.fasta splike_c.faa && mv 'sequence(1).fasta' splike_b.faa && mv 'sequence(2).fasta' splike_a.faa
```

..3. De Github se descargaron 3 comprimidos: **SRR10971381_R1.fastq.gz**, **SRR10971381_R2.fastq.gz** y **sarscov2_assembly.fasta.gz**
Todos los archivos renombrados y descargados se movieron al directorio `data\raw_data`mediante la siguiente línea de comandos:

Downloads marioavella$ `mv splike_c.faa splike_b.faa splike_a.faa sarscov2_genome.fasta sarscov2_genome.gff3 SRR10971381_R1.fastq.gz SRR10971381_R2.fastq.gz sarscov2_assembly.fasta.gz ~/GenomicaComputacional/mavella_p01/data/raw_data/`

..4. Se creó a su vez un archivo de texto **SarsCov-2_Spike.txt** en el directorio `/meta` en donde se describió a grandes rasgos cuál es la función de la "SARS-CoV-2 spike ectodomain structure" basándonos en ésta [publicación](https://www.annualreviews.org/doi/abs/10.1146/annurev-virology-110615-042301).
Se proporciona el resumen a continuación:
>**Función de la proteína**: La proteína espícula (Spike protein) es la parte de la maquinaria vírica que regula la entrada del coronavirus en las células del hospedero. Se conforma por dos dominios principalmente, entre los que se encuentran el dominio S1 N-terminal (S1-NTD) y el dominio C terminal (S1-CTD). Los S1-NTD son responsables para unir azúcar y el S1-CTD son responsables de reconocer los receptores proteicos de ACE2, APN y DPP4. Una vez que el virus entra al cuerpo del hospedero y reconoce los receptores celulares a los que invade, las proteasas hacen un corte que activan el mecanismo, en el que la subunidad S1 en su conformación de prefusión se une a la membrana de la célula hospedera y tira de la membrana celular para fusionarse con la membrana vírica; en este momento el RNA vírico ingresa a la célula y las proteínas espícula pasan a su conformación de profusión. 

# Parte IV

**Respuesta 1:**

Desde el directorio mavella_p01 se escribe `cd data/filtered/` para situarnos en el directorio de `filtered/` donde se crearon las tres ligas simbólicas suaves de los archivos splike_c.faa, splike_b.faa y splike_a.faa, como se muestra a continuación:
```
ln -s ~/../raw_data/splike_c.faa && ln -s ~/../raw_data/splike_b.faa && ln -s ~/../raw_data/splike_a.faa
```

**Respuesta 2:**

Desde el mismo directorio en el que estamos de la respuesta anterior se ejecuta el siguiente comando: `touch glycoproteins.faa`

**Respuesta 3:**

Desde el directorio mavella_p01 se ejecutan los siguientes comandos `cd data/raw_data && head -n1 splike_c.faa splike_b.faa splike_a.faa` y se reporta la primera línea de los archivos splike_*.faa:

head -n1 splike_c.faa
> pdb|6VXX|C Chain C, SARS-CoV-2 spike glycoprotein
head -n1 splike_b.faa
> pdb|6VXX|B Chain B, SARS-CoV-2 spike glycoprotein
head -n1 splike_a.faa
> pdb|6VXX|A Chain A, SARS-CoV-2 spike glycoprotein

**Respuesta 4:**

`less splike_*.faa >> ../filtered/glycoproteins.faa`

**Respuesta 5:**

`mv data/raw_data/splike_*.faa ~/GenomicaComputacional/mavella_p01/archive/`

* ¿Qué pasó con las ligas simbólicas suaves? 
> Estas se rompieron: si cambias la ubicación de los documentos, al abrir la liga simbólica aparece que no existe el archivo original.

**Respuesta 6:**

`cd mavella_p01/data/raw_data/`

..a) Lectura y exploración de los archivos:

`less sarscov2_genome.fasta`

`zless sarscov2_assembly.fasta.gz`

> Se descomprimió posteriormente con `gunzip sarscov2_assembly.fasta.gz`

..b) Las primeras 3 líneas de los archivos
* Con `head -n3 sarscov2_genome.fasta` se obtuvo:
```
>NC_045512.2 Severe acute respiratory syndrome coronavirus 2 isolate Wuhan-Hu-1, complete genome
ATTAAAGGTTTATACCTTCCCAGGTAACAAACCAACCAACTTTCGATCTCTTGTAGATCTGTTCTCTAAA
CGAACTTTAAAATCTGTGTGGCTGTCACTCGGCTGCATGCTTAGTGCACTCACGCAGTATAATTAATAAC
```
* Con `zless sarscov2_assembly.fasta.gz | head -n3` se obtuvo:
```
>NODE_1_length_264_cov_161.042781
CACAAATCTTAACACTCTTCCCTACACGACGCTCTTCCGATCTACGCCGGGCCATTCGTA
CGAACCGATACCTGTGGTAAAGGGTCCTACTGTATGGTGGTACACGAGTAGTAGCAAATG
```
..c) ¿Cómo explicas la diferencia entre el número de lecturas de los archivos `.fasta`?
El archivo **sarscov2_assembly.fasta.gz** es un archivo comprimido que contiene un ensamblaje de secuencias (las secuencias aparecen divididas por "nodos"), por lo que naturalmente contiene un mayor número de lecturas cortas que en realidad son fragmentos de secuencia del DNA resultado al posible tratamiento para facilitar su secuenciación, que posteriormente se pretende reconstruir. Por otra parte, el archivo `.fasta` (**sarscov2_genome.fasta**) ya es la secuencia completa y "ensamblada", por lo que es una sola lectura corrida.

**Respuesta 7:**

`grep '>' sarscov2_genome.fasta | wc -l`

Respuesta: 1

El comando original sería `zless sarscov2_assembly.fasta.gz | grep '>' | wc -l`

Respuesta: 35

> Como se descomprimió se trató como `grep '>' sarscov2_assembly.fasta | wc -l` obteniéndose el mismo resultado.

**Respuesta 8:**

`zless SRR10971381_R2.fastq.gz | head -n12`

Reporte de las primeras 12 líneas:
```
@SRR10971381.512_2
CGTGGAGTATGGCTACATACTACTTATTTGATGAGTCTGGTGAGTTTAAAGTGGCTTCACATATGTATTGTTCTTTCTACCCTCCAGATGAGGATGAAGAAGAAGGTGATTGTGAAGAAGAAGAGTTTGAGCCATCAACTCAATATGAGT
+
/FFFA/A/FFFF66FFFFFF/FF/FFFFFFFFFFFFF/AFFF6FFFA6FFFFF/FFFFFFFFFFFFFFFFFF/FF/FFFFFA/FFF/FFF/A/AFA/FFFFF/=F/F/F/AFAFF//A/AFF//FFAF/FFF=FFAFFFA/A/6=///==
@SRR10971381.556_2
TTTGTAAAAATAAAATAAAAAAAATAAAAATAATATATTAAAAAAAGATAAATAAAAAAATGAACAATTAATAAAAAAAAAAAAAAAAAAAAATTAAAAAAAAAAAAAAAAAAAATAAAAAAAAAAAAAAATAAAAAAAAAATTATAAAA
+
6AFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF/FFFAFFFFFF/FFA/FF=F//=FF/FFFFFFFFFFFFFA/FFFF/FF/FA//F/FFFFFFA/=FFFFF/FFFF/F=FFFAFF///FFFFA/FF/6//////=/
@SRR10971381.1428_2
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
+
FFFFFFFFFFFFAFFFAFFFFFF6A//F//FFF
```
Observando este patrón, identificamos al "@" como el candidato para hacer el conteo de secuencias. De igual manera podría usarse `@SRR10971381`dado que también se repite.

`zless SRR10971381_R2.fastq.gz | grep '@' | wc -l` Respuesta:	  130022

`zless SRR10971381_R2.fastq.gz | grep '@SRR10971381' | wc -l` Respuesta:	130022

> Vemos que serían 130022 secuencias.

**Respuesta 9:**

Explica la diferencia entre los siguientes formatos: 

`.faa`
> Secuencias de aminoácidos, hacen referencia a proteínas.

`.fastqc` 
> Es un formato basado en texto para almacenar tanto una secuencia biológica (de nucleótidos por lo general) y sus puntuaciones de calidad correspondientes en formato PHRED. Estas son letras acompañadas de otros símbolos que nos indica la calidad del genoma, es decir, la probabilidad de que el nucléotido mostrado en la secuencia sea el correcto (según [esta fuente](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjCnevZ4tjsAhWEqp4KHanjCPoQFjABegQIBRAC&url=http%3A%2F%2Fcongresos.nnb.unam.mx%2FTIB2014%2Fsites%2Fdefault%2Ffiles%2FTIB2014%2Fvjimenez-ManejodeDatosNGSv4.pdf&usg=AOvVaw1CSPrkK1v65EtJHc1go7zb), a partir de un valor Q).

`fasta`
> Secuencias de nucleótidos

* En el formato FASTA (al que hacen referencia los `.fasta` y `.faa`) una secuencia comienza con una línea de cabecera con '>' que indica el ID de secuencia (identificadores) y una breve descripción, seguida por líneas de datos de secuencia. No debería existir espacio entre el '>' y la primera letra del identificador. En el formato FASTA se recomienda que todas las líneas de texto sean menores de 80 caracteres, mientras que en [FASTQ](https://en.wikipedia.org/wiki/FASTQ_format) la secuencia y los puntajes de calidad generalmente se colocan en una sola línea cada uno. Un archivo FASTQ normalmente usa cuatro líneas por secuencia.
..a) La línea 1 comienza con un carácter '@' y va seguida de un identificador de secuencia y una descripción opcional (como una línea de título FASTA).
..b) La línea 2 son las letras de secuencia sin formato.
..c) La línea 3 comienza con un carácter '+' y opcionalmente va seguida de nuevo por el mismo identificador de secuencia (y cualquier descripción).
..d) La línea 4 codifica los valores de calidad para la secuencia en la línea 2 y debe contener el mismo número de símbolos que letras en la secuencia.

**Respuesta 10:**

Al abrir el archivo con `less sarscov2_genomee.gff3`, la información se presenta por líneas. En cambio, `less -S sarscov2_genome.gff3` comprime los espacios consecutivos en blanco (hace que las líneas más largas que el ancho de la pantalla se corten o trunquen en lugar de ajustarlas) y por lo mismo se ve más organizado el texto porque no se muestra la parte de una línea larga que no cabe en el ancho de la pantalla. A diferencia de otros comandos similares (como `more`), `less` permite una completa navegación por el contenido del archivo, ya que pone los espacios y "sobrantes" de la información, en este caso sobre la secuencia, en la siguienta línea.

**Respuesta 11:**
`grep 'gene' sarscov2_genome.gff3 | sort -k3 | cut -f3 | uniq -c`

13 CDS
**11 gene** #Tiene 11 genes el archivo#
4 stem_loop

> El campo tres corresponde a las regiones del gen.

> La diferencia entre `gene` y `CDS` es que "[CDS](https://en.wikipedia.org/wiki/Coding_region)" (proveniente de "coding sequence") es la región codificante del gen o el conjunto de exones, o sea la región que se traduce a proteína, y "gene" representaría todo el gen, incluyendo intrones y exones.

# **Ejercicio Extra**

**Respuesta 1:**

Desde el Home: `cd GenomicaComputacional/mavella_p01/figures/`

`ln -s ~/../raw_data/sarscov2_genome.gff3`

