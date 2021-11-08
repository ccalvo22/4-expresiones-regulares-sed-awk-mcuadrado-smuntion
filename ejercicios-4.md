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

**1.1: Terminar en o**

```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E o$ --color aquella_voluntad.txt 
celebrándose irá, y aquel sonido
De cuatro ninfas que del Tajo amado
el agua baña el prado con sonido
   Con tanta mansedumbre el cristalino
que pudieran los ojos el camino
la cabeza sacó, y el prado ameno
Las aves en el fresco apartamiento
Secaba entonces el terreno aliento
y en mirando de fuera, vieron luego
El agua clara con lascivo juego
para seguir el delicado estilo
de los colores que antes le habían dado
llamada la mayor, con diestra mano
a perder otra vez, y del tirano
   Dinámene no menos artificio
pintando a Apolo en el robusto oficio
Mudar luego le hace el ejercicio
que hizo a Apolo consumirse en lloro
por áspero camino, tan sin tiento
El va siguiendo, y ella huye como
el oro y las colores matizando
estaba los colmillos aguzando
   Tras esto el puerco allí se vía herido
```
Para que cuente las líneas le añado la c y elimino el comando --color

```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -cE o$ aquella_voluntad.txt 
60
```

**2.2 --->  o OR a**

```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -E 'o$|a$' --color aquella_voluntad.txt 
Aquella voluntad honesta y pura (Ga
a despecho y pesar de la ventura
   Y aún no se me figura que me toca
mas con la lengua muerta y fría en la boca
Libre mi alma de su estrecha roca
celebrándose irá, y aquel sonido
y lo que siento más es que la carta
De cuatro ninfas que del Tajo amado
   Cerca del Tajo en soledad amena
el agua baña el prado con sonido
   Con tanta mansedumbre el cristalino
que pudieran los ojos el camino
una ninfa del agua do moraba
la cabeza sacó, y el prado ameno
Las aves en el fresco apartamiento
Secaba entonces el terreno aliento
```
Como en el ejercicio anterior ahora que sé que está bien elimino el --color y añado la c
```
mcuadrado@cpg3:~/4-expresiones-regulares-sed-awk-mcuadrado-smuntion$ grep -cE 'o$|a$' aquella_voluntad.txt 
119
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

