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


**2.2 Numero de lineas que terminan por `o` o por `a`.**

En la siguiente imagen se ve un ejemplo de como hemos realizado el ejercicio y los comandos usados.

![palabras en o O a 2021-11-10 a las 15 31 40](https://user-images.githubusercontent.com/92113168/141134537-8e236003-bfd5-4f5d-97be-e62189b33380.png)

Como en el ejercicio anterior, ahora que sé que está bien elimino el --color y añado la c
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -cE 'o$|a$' aquella_voluntad.txt 
119
```



**2.3 Numero de lineas pares que terminan por `o` o por `a`.**

No sabemos hacer este ejercicio -por ahora-




**2.4 palabras que empiezan y acaban por `s` (ordenadas alfabéticamente)**

Nos ha costado un montón pero al final lo hemos conseguido. Hemos buscado ayuda en el cheetseat de expresiones regulares y luego probando en la consola. 

```
i-mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E '\bs' --color aquella_voluntad.txt
Esta orden nos daba las palabras que empezaban con -s pero no reconoce la palabra solo la s al inicio de cada palabra

ii-mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E '\bs\w*' --color aquella_voluntad.txt
OR
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E '\bs\w+' --color aquella_voluntad.txt

con \* Estamos diciendo que reconozca las palabras que empiezan por s seguidos de 0 o más caracteres
con \+ con 1 o más caracteres (tiene más sentido para este texto)


iii-mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -o '\bs\w+s\b' --color aquella_voluntad.txt 
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
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -o '\bs\w*s\b' aquella_voluntad.txt |sort |uniq -c
OR
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -o '\bs\w+s\b' -aquella_voluntad.txt | sort | uniq -c
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
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E -o '^[^(t)]\w+s\b' aquella_voluntad.txt
                                                                      OR
                                                                       grep -E -o '^[^(t)]\w*s\b' aquella_voluntad.txt
                                                                      
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
**1.6 Todas las palabras que empiezan y acaban por la misma letra

```

```

## Ejercicio 2
¿Cuántos gene_ids existen con varios ceros seguidos en los dos gtfs (Humano y Drosophila)?. ¿Cuáles son? ¿Cuántas veces aparece cada uno en el .gtf dado?
Explora el fichero de anotaciones para ver si existen otros gene_ids con muchos números seguidos iguales.

### Respuesta ejercicio 2


## Ejercicio 3

Crea un pipeline que convierta un fichero fasta con secuencias partidas en múltiples líneas en otro sin saltos de línea. 
Al final, para cada secuencia, imprimirá su nombre y el número de caracteres que tenga. 

### Respuesta ejercicio 3


## Ejercicio 4
En la sección 3.1., convertimos la cadena `chr1:3214482-3216968` a un formato tabular con `sed`. Sin embargo, existen otras maneras en las que podríamos haber obtenido el mismo resultado final. ¿Se te ocurren algunas? Recuerda que puedes usar el flag `g`, o puedes encadenar distintas llamadas a `sed` con tuberías si ves que meterlo todo en una única expresión regular se te antoja complicado. 

### Respuesta ejercicio 4

