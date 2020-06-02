# ansible-deployment

## Comprobar los hosts y grupos configurados en el inventario usado

ansible-playbook -i <ruta_inventarios> <ruta_playbook> --list-hosts

## Ejecutar playbook

ansible-playbook -i <ruta_inventarios> <ruta_playbook>

## Solucion de problemas

1. Al probar en vagrant con Ubuntu 18 obtenia un error con ssh-copy-id

El problema se debia a que el servidor ssh de la VM tenia desactivado la autenticacion
con password, se arregla entrando a la VM con `vagrant ssh` y editando el archivo
`/etc/ssh/sshd_config` en la linea `PasswordAuthentication no` cambiandola por `PasswordAuthentication yes`:

Al final se ejecutan los siguientes comandos y la conexion por llave publica ya funciona:

```bash 
sudo systemctl restart sshd.service
exit
ssh-keygen -f "$HOME/.ssh/known_hosts" -R "<IP>"
ssh-copy-id -i ~/.ssh/id_rsa vagrant@IP
```
