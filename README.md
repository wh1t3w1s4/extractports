# Extractports
Extractports es una herramienta escrita en Python3 que filtra el output de un escaneo de puertos de nmap. 
Muy útil para CTFs o máquinas de HTB que requieran un escaneo exhaustivo (-sCV) de determinados puertos, agilizando el proceso de reconocimiento.

## Ejemplo:
### Output de escaneo inicial (-sS): 
```
Nmap scan report for 10.129.XX.XX
Host is up, received user-set (0.074s latency).
Scanned at 2026-11-08 19:26:26 CET for 14s
Not shown: 65486 closed tcp ports (reset), 38 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE      REASON
135/tcp   open  msrpc        syn-ack ttl 127
139/tcp   open  netbios-ssn  syn-ack ttl 127
445/tcp   open  microsoft-ds syn-ack ttl 127
5985/tcp  open  wsman        syn-ack ttl 127
47001/tcp open  winrm        syn-ack ttl 127
49664/tcp open  unknown      syn-ack ttl 127
49665/tcp open  unknown      syn-ack ttl 127
49666/tcp open  unknown      syn-ack ttl 127
49667/tcp open  unknown      syn-ack ttl 127
49668/tcp open  unknown      syn-ack ttl 127
49669/tcp open  unknown      syn-ack ttl 127

```
lanzamos extractports en la terminal y pegamos desde 
```
PORT      STATE SERVICE      REASON
```
hasta el último puerto, en este caso 
```
49669/tcp open  unknown      syn-ack ttl 127
```
tras pulsar enter una o dos veces la herramienta nos devolverá lo siguiente:
```
Discovered open ports: 135,139,445,5985,47001,49664,49665,49666,49667,49668,49669
```
ahora podemos copiar esos puertos fácilmente y realizar un escaneo exhaustivo de los mismos.


## Integración en el PATH
para su correcta ejecución, debemos seguir los siguientes pasos:
1. Dar permisos de ejecución al script tras clonar el repositorio
```
chmod +x extractports
```
2. ver nuestro PATH en nuestra máquina Linux con el comando `echo $PATH`. Veremos algo como esto:
```
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```
3. Seleccionamos una ruta del PATH cualquiera, recomiendo /usr/local/bin ya que suele estar siempre en los sistemas linux y es una ruta adecuada para binarios personalizados.

4. Movemos el script a esa ruta con privilegios de root
```
sudo mv extractports /usr/local/bin
```
5. Reiniciamos la configuración de la terminal (bash -> ~/.bashrc | zsh -> ~/.zshrc)
```
source ~/.bahrc
```
6. Ya podemos llamar al script de forma relativa desde cualquier ruta de nuestro sistema usando `extractports`
