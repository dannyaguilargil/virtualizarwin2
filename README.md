# virtualizarwin2
Virtualizacion de windows 10 en kali linux usando como host MacOS

Como virtualizar windows en kali linux usando QEMU/KVM como gestor de maquinas virtuales, en los siguientes pasos:


*abrimos la terminal y digitamos los siguientes comando pero antes de eso debemos actualizar los repositorios:

NOTA:  SE UTILIZARAN // PARA  COMENTARIOS

-sudo apt-get update  

1) Instalamos los drivers, dependiendo de la tarjeta:

-sudo apt install intel-microcode       //para tarjeta intel
-sudo apt install amd64-microcode         // para tarjeta amd

2)Instalamos qemu y kvm:
-sudo apt install -y qemu qemu-kvm
-sudo  apt install -y qemu-kvm libvirt0 virt-manager bridge-utils

3)Creamos la carpeta en el cual guardaremos el sistema operativo, en este caso windows


-mkdir -p ~/qemu/windows

Ahora nos posicionamos dentro de la carpeta
cd ~/qemu/windows

4)Descargamos el iso, dependiendo de la version de windows que quereremos instalar, en este caso usamos windows 10

https://www.microsoft.com/es-es/software-download/windows10ISO

5)Creamos la imagen QEMU
- qemu-img create -f qcow2 windows.img17G   
// podemos cambiar windows por el nombre que deseemos y cambiar 17g por la cantidad de almacenamiento que queremos solo hay que tener en cuenta los requisitos minimos de instalacion en el momento de asignar el espacio.


6) Pocedemos a la configuracion para la instalacion
 -nano install.sh
Agregamos las siguientes lineas
 kvm -hda windows.img \
         -cdrom nombredeliso.iso \
         -m 1024 // pueden cambiar 1024 por la cantidad de ram que deseen
         -net nic \
         -soundhw all
Control+x, digitamos y, luego presionamos enter
 -chmod+x install.sh
 -./install.sh

Procedemos a la instalacion del sistema operativo
-Seguir manual de instalacion dependiendo del s.o


7)Una vez instalado el s.o creamos el lanzador

-nano start.sh
 kvm -hda windows.img \
         -cdrom nombredeliso.iso \
         -m 1024 // pueden cambiar 1024 por la cantidad de ram que deseen
         -net nic \
         -soundhw all
-chmod +x start.sh
-./start.sh

luego agregamos estas lineas y las guardamos con ctrl+x y presionamos enter

aqui ya podemos apagar la maquina y cada ves que deseemos iniciar nuestra maquina virtual es necesario posicionarse en la carpeta y ejecutar el comando start, aqui el ejemplo:

-cd ~/qemu/windows
-./start.sh

//PARA MAS INFORMACION PUEDES CONSULTAR 
//http://danyasolucionesinformaticas.blogspot.com/
