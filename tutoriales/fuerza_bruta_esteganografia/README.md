# Ataque de fuerza bruta a Estegranografia

Tenemos una imagen a la cual se le han empotrado archivos de texto. Desconocemos la contraseña, por lo que vamos a iniciar un ataque de fuerza bruta basada en diccionario para recuperar la contraseña y poder encontrar el Payload.

## Fueza bruta basada en diccionario, con Bash

Primero debemos encontrar una técnica apropiada para poder probar las contraseñas, para lo que se recomienda el lenguaje de scripting de Bash. Vamos a iniciar con listar las primeras 10 contraseñas del diccionario rockyou.txt

```bash
for clave in $(head rockyou.txt)
do
  echo $i
  sleep 1s
done
```

Utilizando ``for`` y ejecución anidada, logramos imprimir las 10 primeras contraseñas de rockyou.txt. De forma similar vamos a integrar las herramientas de esteganografía a nuestro ataque.

```bash
sudo apt install steghide
for clave in $(head -n 1000 rockyou.txt)
do
  steghide info -p $clave imagen.jpg
done
```

Para resolver el ejercicio debe indicar la contraseña con la que fue cifrado el archivo empotrado, o definir el contenido del archivo empotrado.
