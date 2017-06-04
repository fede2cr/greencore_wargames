# Ataque de fuerza bruta a Caesar

Tenemos un texto que ha sido cifrado usando sustitución, específicamente Caesar.Para abrir un Caesar es necesario saber cuantos caracteres fueron movidos, para moverlos en la otra dirección y obtener el texto original. En este ejercicio desconocemos dicho número.

## ¿Que es un ataque de fuerza bruta?

Es un ataque donde nos aprovechamos que la cantidad de posibilidades, ya sea de una contraseña, de un espacio de llaves o en este caso de posiciones de rotación, es lo suficientemente pequeño para poder probar todas las posibilidades.

Para el cifrado de Caesar tenemos solamente 26 posiblidades, la cantidad de caracteres en el alfabeto latín, desde la A hasta la Z.

Este es un ejemplo donde la labor necesaria para completar las posibilidades es poca, pero puede ser utilizado también para contraseñas sencillas.

## Fuerza bruta con Bash

Bash, el shell usado por la mayoría de las distribuciones de GNU/Linux tiene capacidades interesantes para ayudar con programación de scripts y de trucos en la línea de comando de una sola línea. Nosotros usaremos tanto expansión como for.

Para expandir una lista de caracteres o números usamos corchetes, de esta forma:

```bash
$ echo {1..3}
1 2 3
```

También podemos mezclarlo con el comando for para procesarlos de forma individual de esta manera:

```bash
$ for numero in {1..3}
do
   echo $numero
done
1
2
3
```

## Integrando con Caesar

Iniciamos por cifrar un pequeño texto de ejemplo, usando cualquier número como el argumento que le indica la cantidad de posiciones a rotar el texto. Para este ejemplo, el número 1.

```bash
$ sudo apt-get install bsdgames
$ echo abc greencore | caesar 1
bcd hsffodpsf
```

Imaginemos que se nos comparte este texto pero no se nos indica el número que debemos usar con la herramienta ``caesar``. Ahora utilizaremos la expanción y for para probar todas las combinaciones. Este ejemplo agrega la herramienta ``nl`` para numerar líneas para que sea un poco más claro la posición de rotación.

```bash
$ for rotacion in {1..26}
do
   echo bcd hsffodpsf | /usr/games/caesar $rotacion
done | nl
     1	cde itggpeqtg
     2	def juhhqfruh
     3	efg kviirgsvi
     4	fgh lwjjshtwj
     5	ghi mxkktiuxk
     6	hij nyllujvyl
     7	ijk ozmmvkwzm
     8	jkl pannwlxan
     9	klm qbooxmybo
    10	lmn rcppynzcp
    11	mno sdqqzoadq
    12	nop terrapber
    13	opq ufssbqcfs
    14	pqr vgttcrdgt
    15	qrs whuudsehu
    16	rst xivvetfiv
    17	stu yjwwfugjw
    18	tuv zkxxgvhkx
    19	uvw alyyhwily
    20	vwx bmzzixjmz
    21	wxy cnaajykna
    22	xyz dobbkzlob
    23	yza epcclampc
    24	zab fqddmbnqd
    25	abc greencore
    26	bcd hsffodpsf

```

