# Sesión IV - Expresiones regulares: grep, sed y awk

Herramientas computacionales para bioinformática: UNIX, expresiones regulares y shell script

Edita esta plantilla en formato markdown [Guía aquí](https://guides.github.com/features/mastering-markdown/) como se pide en el guión. 
Cuando hayas acabado, haz un commit de tus cambios y súbelos al repositorio antes de la fecha de entrega señalada. 

======================================

**Añade por favor capturas de pantalla y el código de tus pipelines.**


## Ejercicio 1
Usando el fichero `aquella_voluntad.txt`, identifica usando grep:

1. El número de líneas que terminan por `o`. 
2. El número de líneas que terminan por `o` o por `a`. 
3. El número de líneas pares que terminan por `o` o por `a`
4. Todas las palabras que empiezan y acaban por `s` (ordenadas alfabéticamente)
5. Todas las palabras que no empiezan por t y acaban por `s`. (ordenadas por número de línea)
6. Todas las palabras que empiezan y acaban por la misma letra (volver a este punto al acabar toda la lección). 

### Respuesta ejercicio 1

**1.1 Número de líneas que terminan por `o`.**

En la siguiente imagen se ve un ejemplo de como hemos realizado el ejercicio y los comandos usados.

![palabras que terminan en o 2021-11-10 a las 15 27 09](https://user-images.githubusercontent.com/92113168/141133273-fe2d300b-7018-42f7-a04a-a7a6674e7e74.png)

Para que cuente las líneas le añado la c y elimino el comando --color
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -cE o$ aquella_voluntad.txt 
60
```


**1.2 Numero de lineas que terminan por `o` o por `a`.**

En la siguiente imagen se ve un ejemplo de como hemos realizado el ejercicio y los comandos usados.

![palabras en o O a 2021-11-10 a las 15 31 40](https://user-images.githubusercontent.com/92113168/141134537-8e236003-bfd5-4f5d-97be-e62189b33380.png)

Como en el ejercicio anterior, ahora que sé que está bien elimino el --color y añado la c
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -cE 'o$|a$' aquella_voluntad.txt 
119
```



**1.3 Numero de lineas pares que terminan por `o` o por `a`.**
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -n [oa]$ aquella_voluntad.txt | grep -c "[02468]:"
61

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -nE 'o$|a$' aquella_voluntad.txt | grep -c "[02468]:"
61
```

![Captura de pantalla de 2021-11-17 14-32-34](https://user-images.githubusercontent.com/91688843/142210592-b55ad6a3-b3ea-438c-b712-e70c697bc67d.png)





**1.4 palabras que empiezan y acaban por `s` (ordenadas alfabéticamente)**

Nos ha costado un montón pero al final lo hemos conseguido. Hemos buscado ayuda en el cheetseat de expresiones regulares y luego probando en la consola. 

```
i-mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E '\bs' --color aquella_voluntad.txt
Esta orden nos daba las palabras que empezaban con -s pero no reconoce la palabra solo la s al inicio de cada palabra

ii-mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E '\bs\w*' --color aquella_voluntad.txt
OR
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E '\bs\w+' --color aquella_voluntad.txt

con \* Estamos diciendo que reconozca las palabras que empiezan por s seguidos de 0 o más caracteres
con \+ con 1 o más caracteres (tiene más sentido para este texto)


iii-mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -oi '\bs\w+s\b' --color aquella_voluntad.txt 
sentidos
sauces
sus
sus
sus
sus
sendos
sembradas
silvestres
selvas
sombras
sus
selvas
sus
salvajes
sus
sauces
sabemos


RESPUESTA
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -oi '\bs\w*s\b' aquella_voluntad.txt |sort |uniq -c
OR
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -oi '\bs\w+s\b' -aquella_voluntad.txt | sort | uniq -c
      1 sabemos
      1 salvajes
      2 sauces
      2 selvas
      1 sembradas
      1 sendos
      1 sentidos
      1 silvestres
      1 sombras
      7 sus
```

**1.5 Todas las palabras que no empiezan por `t` y acaban por `s`. (ordenadas por número de línea)**
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -oi '^[^(t)]\w+s\b' aquella_voluntad.txt
                                                                      OR
                                                                       grep -E -oi '^[^(t)]\w*s\b' aquella_voluntad.txt
                                                                      
mas
pues
mas
Las
los
las
las
después
los
las
antes
entretejidas
cestillos
las
antes
mas
las
claras
las
los
los
dos
las
mancebos
más
más
mas
las
sabemos
mas
juntas
las
```
**1.6 Todas las palabras que empiezan y acaban por la misma letra**

```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -Eowi "([a-z])\w+\1" aquella_voluntad.txt | head -5
Aquella
Aquella
otro
alma
acompañada
```
![Captura de pantalla de 2021-11-17 15-03-20](https://user-images.githubusercontent.com/91688843/142215205-9378995b-9ec4-4b9f-8d3f-230d9cc59d10.png)

### Comentarios: Muy bien, todo correcto. 
### Nota: 2.5/2.5

## Ejercicio 2
¿Cuántos gene_ids existen con varios ceros seguidos en los dos gtfs (Humano y Drosophila)?. ¿Cuáles son? ¿Cuántas veces aparece cada uno en el .gtf dado?
Explora el fichero de anotaciones para ver si existen otros gene_ids con muchos números seguidos iguales.

### Respuesta ejercicio 2

**Drosophila**
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*(0{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | head -n5
gene_id "FBgn0037232"; transcript_id "FBtr0273009"
gene_id "FBgn0037232"; transcript_id "FBtr0273009"
gene_id "FBgn0037232"; transcript_id "FBtr0273009"
gene_id "FBgn0037232"; transcript_id "FBtr0273009"
gene_id "FBgn0037232"; transcript_id "FBtr0273009"

NO ENTIENDO PORQUE DA EL TRANSCRITO Y NO PARA EN LA SEGUNDA COMILLA : "FBgn0037232"

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -cE 'gene_id ".*(0{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf 
17435
```
```
CUALES SON Y CUANTAS VECES APARECEN
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*(0{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | grep -E -o 'gene_name "\w+"' | uniq -c
     35 gene_name "smash"
      8 gene_name "CG12007"
      4 gene_name "CG1161"
     27 gene_name "CG11000"
      3 gene_name "CG18744"
      1 gene_name "CG44227"
     18 gene_name "ScsbetaA"
     17 gene_name "Csk"
     12 gene_name "Lk6"
      9 gene_name "prd1"
     19 gene_name "Sbf"
     27 gene_name "CG10005"
      2 gene_name "CG14384"
    104 gene_name "CG6006"
     31 gene_name "CG4009"
      5 gene_name "naz"
      7 gene_name "WRNexo"
      7 gene_name "gl"
      7 gene_name "CG7675"
      3 gene_name "CG14309"
     23 gene_name "CG6005"
     12 gene_name "CG34008"
     12 gene_name "CG4000"
     12 gene_name "CG7009"
      6 gene_name "AdipoR"
     15 gene_name "CG6000"
      4 gene_name "CG17782"
      3 gene_name "CG17781"
      9 gene_name "CG17780"
      3 gene_name "CG13615"
      3 gene_name "CG13616"
      8 gene_name "nAChRalpha1"
     10 gene_name "CG7006"
      1 gene_name "CG14245"
      8 gene_name "Tsp97E"
      
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -cE 'gene_id ".*(0{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | grep -E -o 'gene_name "\w+"' | uniq -c | wc -l
326
```
```
OTROS GENES MUCHOS NUMEROS SEGUIDOS 

cuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*([1-9]{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | head -n5
gene_id "FBgn0267431"; gene_name "Myo81F"
gene_id "FBgn0267431"; transcript_id "FBtr0392909"; gene_name "Myo81F"
gene_id "FBgn0267431"; transcript_id "FBtr0392909"; exon_number "1"; gene_name "Myo81F"
gene_id "FBgn0267431"; transcript_id "FBtr0392909"; exon_number "2"; gene_name "Myo81F"
gene_id "FBgn0267431"; transcript_id "FBtr0392909"; exon_number "2"; gene_name "Myo81F"; gene_source "FlyBase"; gene_biotype "protein_coding"; transcript_source "FlyBase"; transcript_biotype "protein_coding"; protein_id "FBpp0352251"


mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*([1-9]{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | tail -n10
gene_id "FBgn0085506"; transcript_id "FBtr0302344"; exon_number "1"; gene_name "CG40635"; gene_source "FlyBase"; gene_biotype "protein_coding"; transcript_source "FlyBase"; transcript_biotype "protein_coding"; protein_id "FBpp0291548"
gene_id "FBgn0085506"; transcript_id "FBtr0302344"; exon_number "1"; gene_name "CG40635"
gene_id "FBgn0085506"; transcript_id "FBtr0302344"; exon_number "2"; gene_name "CG40635"
gene_id "FBgn0085506"; transcript_id "FBtr0302344"; exon_number "2"; gene_name "CG40635"; gene_source "FlyBase"; gene_biotype "protein_coding"; transcript_source "FlyBase"; transcript_biotype "protein_coding"; protein_id "FBpp0291548"
gene_id "FBgn0259870"; gene_name "Su(Ste):CR42439"
gene_id "FBgn0259870"; transcript_id "FBtr0300167"; gene_name "Su(Ste):CR42439"
gene_id "FBgn0259870"; transcript_id "FBtr0300167"; exon_number "1"; gene_name "Su(Ste):CR42439"
gene_id "FBgn0085511"; gene_name "lncRNA:CR40719"
gene_id "FBgn0085511"; transcript_id "FBtr0304147"; gene_name "lncRNA:CR40719"
gene_id "FBgn0085511"; transcript_id "FBtr0304147"; exon_number "1"; gene_name "lncRNA:CR40719"


mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*([1-9]{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | grep -E -o 'gene_name "\w+"' | sort | uniq -c | head -n10
      4 gene_name "140up"
      8 gene_name "18w"
      4 gene_name "2mit"
     23 gene_name "312"
     25 gene_name "5PtaseI"
      4 gene_name "7B2"
     28 gene_name "a"
      2 gene_name "a5"
      3 gene_name "a6"
      3 gene_name "AANAT1"

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*([1-9]{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | grep -E -o 'gene_name "\w+"' | sort | uniq -c | tail -10
     14 gene_name "ZnT86D"
    105 gene_name "zormin"
      6 gene_name "zpg"
      2 gene_name "Zpr1"
     10 gene_name "Zw"
      2 gene_name "Zw10"
      4 gene_name "Zwilch"
     49 gene_name "zyd"
      3 gene_name "zye"
     34 gene_name "Zyx"
     
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ grep -E -o 'gene_id ".*([1-9]{2})[^"]"' Drosophila_melanogaster.BDGP6.28.102.gtf | grep -E -o 'gene_name "\w+"' | sort | uniq -c | wc -l
12345
```

**HOMO.GTF**
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*(0{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz | head -n5
gene_id "ENSG00000238009"
gene_id "ENSG00000238009"
gene_id "ENSG00000238009"
gene_id "ENSG00000238009"
gene_id "ENSG00000238009"

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*(0{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz | tail -n5
gene_id "ENSG00000275063"; gene_version "1"; transcript_id "ENST00000618003"
gene_id "ENSG00000275063"; gene_version "1"; transcript_id "ENST00000618003"
gene_id "ENSG00000271254"; gene_version "6"; transcript_id "ENST00000614336"; transcript_version "4"; exon_number "11"; gene_name "AC240274.1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "AC240274.1-201"; transcript_source "ensembl"; transcript_biotype "protein_coding"; exon_id "ENSE00003717009"
gene_id "ENSG00000271254"; gene_version "6"; transcript_id "ENST00000612640"; transcript_version "4"; exon_number "11"; gene_name "AC240274.1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "AC240274.1-202"; transcript_source "ensembl"; transcript_biotype "protein_coding"; exon_id "ENSE00003717009"
gene_id "ENSG00000271254"; gene_version "6"; transcript_id "ENST00000616361"; transcript_version "1"; exon_number "15"; gene_name "AC240274.1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "AC240274.1-204"; transcript_source "ensembl"; transcript_biotype "protein_coding"; exon_id "ENSE00003717009"

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*(0{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz |wc -l
87593
```
```
CUALES SON Y CUANTAS VECES APARECEN

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*(0{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz |grep -E -o 'gene_name "\w+"' | sort | uniq -c | head -n10
      1 gene_name "A1BG"
      1 gene_name "A2M"
      1 gene_name "A4GALT"
      1 gene_name "AAAS"
      1 gene_name "AACSP1"
      1 gene_name "AADACP1"
      1 gene_name "AAGAB"
      1 gene_name "AAMDC"
     20 gene_name "AARS1"
      1 gene_name "AARSD1"

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*(0{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz |grep -E -o 'gene_name "\w+"' | sort | uniq -c | wc -l
5896
```

```
OTROS GENES MUCHOS NUMEROS SEGUIDOS

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*([1-9]{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz |grep -E -o 'gene_name "\w+"' | sort | uniq -c
   7 gene_name "ZXDA"
      7 gene_name "ZXDB"
     56 gene_name "ZXDC"
     98 gene_name "ZYG11A"
      1 gene_name "ZYG11AP1"
     67 gene_name "ZYG11B"
     92 gene_name "ZYX"
      1 gene_name "ZYXP1"
    143 gene_name "ZZEF1"
    119 gene_name "ZZZ3"

mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion/gtfs$ zgrep -E -o 'gene_id ".*([1-9]{2})[^"]"' Homo_sapiens.GRCh38.102.gtf.gz |grep -E -o 'gene_name "\w+"' | sort | uniq -c | wc -l
32897
```

### Comentarios: No seleccionáis exclusivamente los gene ID, esto se debe a que en vuestra expresión regular (`gene_id ".*(0{2})[^"]"`) estáis indicando con el primer `.*` que seleccione cualquer caracter, incluyendo las comillas, lo correcto para que no seleccione las palabras con comilla es indicar `gene_id "[^"]*"` para indicar que seleccione cualquier palabra con cero o más caracteres que no sean comillas y después utilizar `gene_id ".*0{2,}.*"` para que seleccione los ID con 2 o más ceros, de tal manera que el comando correcto sería `grep -Eo 'gene_id "[^"]*"' Drosophila_melanogaster.BDGP6.28.102.gtf | grep -Eoc 'gene_id ".*0{2,}.*"'`.
### Nota: 1.5/2.5

## Ejercicio 3

Crea un pipeline que convierta un fichero fasta con secuencias partidas en múltiples líneas en otro sin saltos de línea. 
Al final, para cada secuencia, imprimirá su nombre y el número de caracteres que tenga. 

### Respuesta ejercicio 3

**ME RINDO, NO SABEMOS HACERLO**
```
mcuadrado@cpg3:~$ awk 'S0 == /[AGCT]/' covid.fasta | tr -d \n | tee covid-copy.fasta | awk 'S0 == ">*"' {print $1} covid-copy.fasta | wc -l este no me da el nº de caracteres de la seq pero es que no lo sé hacer
awk: fatal: cannot open file `{print' for reading: No existe el fichero o el directorio
```
### Comentario: Este era muy difícil, lamento que no os haya salido.
### Nota: 0.5/2.5

## Ejercicio 4
En la sección 3.1., convertimos la cadena `chr1:3214482-3216968` a un formato tabular con `sed`. Sin embargo, existen otras maneras en las que podríamos haber obtenido el mismo resultado final. ¿Se te ocurren algunas? Recuerda que puedes usar el flag `g`, o puedes encadenar distintas llamadas a `sed` con tuberías si ves que meterlo todo en una única expresión regular se te antoja complicado. 

### Respuesta ejercicio 4
```
mcuadrado@cpg3:~$ echo chr1:3214482-3216968 | sed -E 's/[:-]/\t/g'
chr1	3214482	3216968
```
### Comentarios: Muy bien, todo correcto.
### Nota: 2.5/2.5

## Nota final: 7.0/10
