# Nivel de ataque de frecuencia

Tenemos un texto corto, escrito **en Español** que ha sido cifrado con algún algoritmo de subtitución, y debemos ejecutar un ataque de frecuencia para conocer la substitución.

## ¿Que es un ataque de frecuencia?

Para cada idioma escrito, existe alguna letra del alfabeto que va a ser la más utilizada, otra que va a ser la segunda más utilizada, etc. Como en este caso que ya conocemos el idioma, podemos utilizar un texto en el mismo idioma para crear una frecuencia de letras, y luego utilizar esta frecuencia como **base** para tratar de abrir el texto.

Esta técnica fue creada por el polímata Al-Kindi, siendo la primera técnica de criptoanálisis conocida, capaz de romper algoritmos de substitución, con una mayor eficiencia entre más texto se tenga que haya cifrado de la misma forma.

### Creando **nuestra** lista de frecuencia

Para crear nuestra lista de frecuencia vamos a descargar una obra de Miguel de Cervantes Saavedra y una de Rubén Darío.

Descargamos el archivo, usamos ``sort`` y ``uniq`` para contar letras.

```bash
wget -O quijote.txt https://www.gutenberg.org/ebooks/2000.txt.utf-8
grep -o . quijote.txt | sort | uniq -ci | sort -n
```
Esto nos va a entregar una tabla de frecuencia para el Quijote, donde la letra E es la más frecuente, seguido de la A, O, S, N, R, L y D.

```bash
wget -O cuentos_y_cronicas.txt https://www.gutenberg.org/files/51627/51627-0.txt
grep -o . cuentos_y_cronicas.txt | sort | uniq -ci | sort -n
```

Para los Cuentos y Crónicas de Darío, la frecuencia es: E, A, O, S, N, R, L, I, D.

Nótese que la letra I es más frecuente que la D en este libro en particular. Por ello vamos a utilizar la frecuencia no como una regla, sino como una probabilidad, donde podemos jugar con los valores de algunos caracteres hasta encontrar texto que tenga sentido.

### Iniciando el criptoanálisis del archivo.

El archivo se encuentra escrito en mayúsculas, pero con espacios para mejor legibilidad. Vamos a hacer una tabla de frecuencia para este texto cifrado, e ir reemplazando las letras una por una, tratando encontrar palabras conocidas en el texto.

Cuando vayamos reemplazando caracteres, vamos a pasar de mayúscula a minúscula para que se entienda mejor las partes del texto que ya hemos descifrado.

```bash
grep -o . cifrado.txt | sort | uniq -ci | sort -n
```

Según el criptoanálisis para el archivo ``cifrado.txt`` la frecuencia es: R, N, B, F, E, V, e.g.

Con la herramienta sed vamos a ir probando combinaciones, una por una, de mayor frecuencia a menor frecuencia, usándo las frecuencias de Cervantes y Daría solo como una guía.

Iniciamos reemplazando la ``R`` por una ``e``.

Letra cifrada | Sustitucion
--------------|-------
R             | e

```bash
sed 's/R/e/g' cifrado.txt
```

Podemos notar que aparecen varias letras ``e`` en el texto, pero todavía es muy temprano para encontrar palabras, por lo que probamos con otras letras, reconociendo que podemos cometer errores por lo que hay que estar listo para probar con otra letra de la frecuencia.

Letra cifrada | Sustitucion
--------------|-------
R             | e
N             | a

```bash
sed 's/R/e/g ; s/N/a/g' cifrado.txt
```

Un último ejemplo con más reemplazos. Ahora debes jugar con la reemplazos y frecuencias hasta poder leer el archivo completo.

Letra cifrada | Sustitucion
--------------|-------
R             | e
N             | a
B             | o 
F             | s
E             | g

```bash
sed 's/R/e/g ; s/N/a/g ; s/B/o/g ; s/F/s/g ; s/E/r/g' cifrado.txt
```

Para completar el ejercicio, debe entregar la tabla de sustitución completa, o el comando de sed completo.
