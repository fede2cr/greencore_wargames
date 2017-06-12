# Fuerza Bruta a XOR

Encontrando la contraseña de un cifrado con XOR, con ataque de fuerza bruta

## Descripción

Tenemos un texto que ha sido cifrado con XOR. Queremos ejecutar un ataque para encontrar la contraseña.

## Preparación de laboratorio

Se recomienda en equipo con Kali Linux, o Debian/Ubuntu

```bash
sudo apt install python-pip
sudo pip install docopt
git clone https://github.com/hellman/xortool
cd xortool
chmod +x setup.py
sudo ./setup.py install
```

## Ataque

Por ser XOR un algoritmo *aditivo*, cuando se usa una palabra como "greencore" para cifrar un texto, la secuencia de caracteres se va a repetir, en este caso cada 9 letras.

Para este ejercicio, no conocemos la longitud de la contraseña usada, por lo que iniciamos por solicitar que detecte la frecuencia.

```bash
xortool cifrado.txt
```

En este caso se nos sugiere que la contraseña puede ser de 8 caracteres, para lo cual se recomienda probar con dicha longitud, agregando ataque de fuerza bruta.

```bash
xortoll -l 8 -b cifrado.txt
```

En el nuevo directorio creado de xortool, revise el contenido de los archivos CSV para encontrar la contraseña correcta, así como compruebe que el archivo .out correspondiente a la llave ha sido decifrado correctamente.
