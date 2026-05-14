# Instalación y Configuración de Hyper-V y Laboratorio Windows Server 2022

Objetivo

En esta práctica se instalará Hyper-V en Windows 11, se configurará una red NAT para las máquinas virtuales y se implementarán dos servidores Windows Server 2022:

TAILWIND-DC1 → Controlador de dominio.

TAILWIND-MBR1 → Servidor miembro del dominio.

# Parte 1. Instalación de Hyper-V

# 1. Iniciar sesión

Inicie sesión en Windows 11 con una cuenta que tenga privilegios de administrador local.

# 2. Habilitar Hyper-V
   
Abra el menú Inicio.

Seleccione Configuración.

Entre en Sistema.

Desplácese hasta Funciones opcionales y selecciónelo.

En la parte inferior, pulse Más características de Windows.

En la ventana de características de Windows:

Marque la casilla Hyper-V.

Pulse Aceptar.

Windows instalará los componentes necesarios.

<img width="937" height="830" alt="Screenshot_20260514_110237" src="https://github.com/user-attachments/assets/26f89ecb-0718-410c-ac68-900051189ad6" />

# 3. Reiniciar el equipo

Cuando finalice la instalación:

Pulse Reiniciar ahora.

Espere a que el sistema se reinicie.

Vuelva a iniciar sesión con la misma cuenta de administrador.

<img width="931" height="761" alt="Screenshot_20260514_110409" src="https://github.com/user-attachments/assets/6abe65ac-c151-44b6-9622-cd4598e91628" />

# Parte 2. Configuración inicial de Hyper-V

# 1. Abrir el Administrador de Hyper-V

Abra el menú Inicio.

Busque:

Administrador de Hyper-V

Abra la aplicación.

Opcionalmente:

Haga clic derecho sobre el icono y seleccione Anclar a la barra de tareas.

# 2. Configurar rutas predeterminadas

En el panel izquierdo del Administrador de Hyper-V:

Haga clic derecho sobre el nombre del equipo.

Seleccione:

Configuración de Hyper-V.

Configurar carpeta de máquinas virtuales

En la sección Servidor, seleccione:

Máquinas virtuales

Establezca la siguiente ruta:

C:\VirtualMachines

Configurar carpeta de discos virtuales

Seleccione:

Discos duros virtuales

Configure la siguiente ruta:

C:\VirtualMachines\VHDs

Pulse Aceptar.

<img width="826" height="616" alt="Screenshot_20260514_110910" src="https://github.com/user-attachments/assets/1e535e2c-3564-4007-9e58-ab0b4638388e" />

# Parte 3. Configuración de la red NAT

# 1. Abrir PowerShell como administrador
   
Abra el menú Inicio.

Busque:

PowerShell

Haga clic derecho y seleccione:

Ejecutar como administrador

<img width="901" height="848" alt="Screenshot_20260514_111026" src="https://github.com/user-attachments/assets/9206dd8a-735a-4655-80d9-95351f298d26" />
<img width="952" height="967" alt="Screenshot_20260514_111110" src="https://github.com/user-attachments/assets/0c1eda57-aa81-43fa-b674-ebe7b1de1bc6" />

# 4. Crear el conmutador NAT

Ejecute los siguientes comandos uno por uno:

New-VMSwitch -SwitchName "NATSwitch" -SwitchType Internal

New-NetIPAddress -IPAddress 10.10.10.1 -PrefixLength 24 -InterfaceAlias "vEthernet (NATSwitch)"

New-NetNat -Name "NATNetwork" -InternalIPInterfaceAddressPrefix "10.10.10.0/24"

Cierre PowerShell.

Parte 4. Descarga de la ISO de Windows Server 2022

Descargue la ISO oficial desde:

Microsoft Evaluation Center — Windows Server 2022

Guardar la ISO

Cree la carpeta:

C:\ISOs

Guarde el archivo ISO descargado dentro de esa carpeta.

# Parte 5. Creación del controlador de dominio (TAILWIND-DC1)

# 1. Crear la máquina virtual
   
En el Administrador de Hyper-V:

Seleccione Acción → Nuevo → Máquina virtual.

En el asistente:

Pulse Siguiente.

# 4. Configuración de la máquina virtual
   
Nombre

Introduzca:

TAILWIND-DC1

Pulse Siguiente.

Generación

Seleccione:

Generación 2

Pulse Siguiente.

Memoria

Configure:

4096 MB

Mantenga activada la opción:

Usar memoria dinámica para esta máquina virtual

Pulse Siguiente.

Red

Seleccione:

NATSwitch

Pulse Siguiente.

Disco duro virtual

Deje la configuración predeterminada y pulse Siguiente.

Archivo ISO

Seleccione:

Instalar un sistema operativo desde un archivo de imagen de arranque

Pulse Examinar.

Seleccione la ISO almacenada en:

C:\ISOs

Pulse Siguiente y luego Finalizar.

Parte 6. Desactivar puntos de control automáticos

Haga clic derecho sobre:

TAILWIND-DC1

Seleccione:

Configuración

Entre en:

Puntos de control

Desmarque:

Usar puntos de control automáticos

Pulse Aceptar.

# Parte 7. Instalación de Windows Server 2022

# 1. Iniciar la máquina virtual

Haga doble clic sobre:

TAILWIND-DC1

Pulse:

Iniciar

# 2. Arrancar desde la ISO

Cuando aparezca el mensaje:

Press any key to boot from CD or DVD

Pulse la barra espaciadora.

# 3. Instalar Windows Server
   
Pulse Siguiente.

Seleccione:

Instalar ahora

<img width="952" height="967" alt="Screenshot_20260514_111110" src="https://github.com/user-attachments/assets/8fa9d823-90ff-4664-8b15-9667be2bf4a9" />
<img width="899" height="884" alt="Screenshot_20260514_111159" src="https://github.com/user-attachments/assets/7abe8768-4a0f-4ec4-b5be-f5fbc3a17d21" />

Elija:

Windows Server 2022 Standard Evaluation (Desktop Experience)

Pulse Siguiente.

Acepte los términos de licencia.

Seleccione:

Personalizada

Seleccione la unidad 0.

Pulse Siguiente.

La instalación comenzará automáticamente.

# Parte 8. Configuración inicial del servidor

# 1. Contraseña del administrador

Introduzca la contraseña:

Pa55w.rdPa55w.rd

Pulse Finalizar.

# 2. Configuración de red

Abra:

Configuración de red → Cambiar opciones del adaptador.

Entre en las propiedades de:

<img width="899" height="884" alt="Screenshot_20260514_111159" src="https://github.com/user-attachments/assets/5ccc8f25-4f1a-42d6-b7dc-a66f25e17e56" />
<img width="912" height="726" alt="Screenshot_20260514_111248" src="https://github.com/user-attachments/assets/997b4f27-0ecc-467b-b094-a9a0550d0e1e" />

IPv4

Configure:

Parámetro	Valor

Dirección IP	10.10.10.10

Máscara	255.255.255.0

Puerta de enlace	10.10.10.1

DNS preferido	1.1.1.1

DNS alternativo	8.8.8.8

Pulse Aceptar y cierre las ventanas.

# Parte 9. Cambiar nombre del servidor

Abra:

Administrador del servidor → Servidor local

Pulse sobre:

Nombre del equipo

Seleccione:

Cambiar

Introduzca:

TAILWIND-DC1

Reinicie el servidor.

# Parte 10. Instalar Active Directory

# 1. Agregar roles

Abra:

Administrador del servidor

Seleccione:

Administrar → Agregar roles y características

# 2. Tipo de instalación

Seleccione:

Instalación basada en roles o características

Pulse Siguiente.

# 3. Seleccionar roles

Marque:

Servicios de dominio de Active Directory

Pulse:

Agregar características

<img width="912" height="726" alt="Screenshot_20260514_111248" src="https://github.com/user-attachments/assets/209642f5-bdac-405e-8b2b-8cc11da393ae" />
<img width="919" height="740" alt="Screenshot_20260514_111632" src="https://github.com/user-attachments/assets/4ade55a5-a69f-4359-b3fd-ce1d210bf093" />

Continúe pulsando Siguiente hasta llegar a:

Instalar

Espere a que finalice la instalación.

Parte 11. Promover el servidor a controlador de dominio

1. Configuración del dominio
2. 
En el Administrador del servidor:

Pulse el icono de notificación.

Seleccione:

Promover este servidor a controlador de dominio

# 4. Crear bosque

Seleccione:

Agregar un nuevo bosque

Dominio raíz:

tailwindtraders.internal

Pulse Siguiente.

<img width="919" height="740" alt="Screenshot_20260514_111632" src="https://github.com/user-attachments/assets/56a192eb-13d0-4835-9271-0c7f752c6c43" />

NO ME DEJA SEGUIR LA PRACTICA

# 3. Contraseña DSRM

Configure:

Pa55w.rdPa55w.rd

Continúe pulsando Siguiente hasta llegar a:

Instalar

El servidor se reiniciará automáticamente.

# Parte 12. Inicio de sesión en el dominio

Después del reinicio:

Usuario:

tailwindtraders\administrator

Contraseña:

Pa55w.rdPa55w.rd

# Parte 13. Creación del servidor miembro (TAILWIND-MBR1)

Repita el mismo procedimiento utilizado para crear el controlador de dominio, con las siguientes diferencias:

Configuración	Valor

Nombre de la VM	TAILWIND-MBR1

Dirección IP	10.10.10.20

Máscara	255.255.255.0

Puerta de enlace	10.10.10.1

DNS preferido	10.10.10.10

DNS alternativo	8.8.8.8

Parte 14. Unir el servidor al dominio

# 1. Cambiar nombre del equipo

Configure el nombre:

TAILWIND-MBR1

Reinicie el servidor.

<img width="841" height="650" alt="Screenshot_20260514_111820" src="https://github.com/user-attachments/assets/d28e6378-ab37-409a-96e8-abffab637d76" />

# 2. Unir al dominio

Abra:

Propiedades del sistema

Pulse:

Cambiar

Seleccione:

Dominio

Introduzca:

TAILWINDTRADERS

ERROR AL UNIR DOMINIO

# 3. Introducir credenciales

Usuario:

TAILWINDTRADERS\Administrador

Contraseña:

Pa55w.rdPa55w.rd

# 4. Reiniciar

Cuando aparezca el mensaje de bienvenida al dominio:

Pulse Aceptar.

Reinicie el servidor.

Resultado final del laboratorio

Equipo	Dirección IP	Función

TAILWIND-DC1	10.10.10.10	Controlador de dominio

TAILWIND-MBR1	10.10.10.20	Servidor miembro

Dominio configurado:

tailwindtraders.internal

Red NAT:

10.10.10.0/24
<img width="937" height="830" alt="Screenshot_20260514_110237" src="https://github.com/user-attachments/assets/7cb6c4e0-0a14-4baf-9d0e-848aa1d7341c" />

