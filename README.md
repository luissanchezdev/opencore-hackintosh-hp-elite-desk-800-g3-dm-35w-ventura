# TUTORIAL HACKINTOSH VENTURA HP ELITE DESK 800 G3 DM MINI 35W

Instalación de MACOSX Ventura con el método online


Especificaciones del PC:
- Intel i5 6500t
- Intel HD Graphics 530
- RAM DE 16GB

## Preparación 

### BIOS

Las imágenes de la configuración se encuentran en la carpeta 'bios'

- Security:
	- Deshabilitar:
		- Physical Presence Interface
		- Intel Software Guard Extensions (SGX)
		- TPM Embedded Security:
			- TPM Device: Hidden
			- TPM State: uncheck

- Advanced -> Boot Options:
	- Deshabilitar solamente:
		- Fast Boot
		- CD-ROM Boot
		- Network (PXE) Boot
		- Prompt on Fixed Storage Change
		- Audio Alerts During Boot: Es opcional sí lo quiere desactivar
		- NumLock on at boot
	- After Power Loss : Power Off

- Advanced -> Secure Boot Configuration:
	- Configure Legacy Support and Secure Boot: Legacy Support Enable and Secure Boot Disable
	- Enable MS UEFI CA Key: check
	- El resto de las opciones deshabilitarlas

- Advanced -> System Options:
	- Deshabilitar solamente:
		- Configure Storage Controller for Intel Optane
		- Virtualization Technology (VTx)
		- Allow PCIe/PCI SERR# Interrupt

- Advanced -> Built-In Device Options:
	- Deshabilitar:
		- Wake On LAN: Disabled
		- LAN / WLAN Auto Switching
		- Wake on WLAN

- Advanced -> Port Options: Todas habilitadas

- Advanced -> Power Managment Options:
	- Deshabilitar solamente:
		- S5 Maximum Power Savings

- Advanced -> Remote Managment Options:
	- Active Management (AMT): check
	- USB Key Provisioning Support: uncheck
	- USB Redirection Support: check
	- Unconfigure AMT on next boot: Do Not Apply
	- SQL Terminal Emulation Mode: ANSI
	- Show Unconfigure ME Confirmation Prompt: check
	- Verbose Boot Messages: uncheck
	- Watchdog Timer: uncheck
	- CIRA Timeout (min.) : 1min


### EFI para la instalación

- EFI con un SMBios para iMac18,1

**NOTA**: Realmente se podría usar la versión final de la EFI( versión que se usa cuando está instalado ya el sistema), pero voy ha mostrar como llegó a funcionarme la instalación, por eso incluyo el paso a paso con el cual me funcionó. Ahora esta claro que podemos y es el lo normal, usar una sola EFI durante todo el proceso, y solo agregar cambios para agregar más soporte al Hadware o quitar el debug.


### USB
- Memoria USB formateada en FAT32
- Colocar el contenido de la carpeta "USB para instalación"
- Crear una nueva carpeta en la raiz de la memoria USB con el nombre "com.apple.recovery.boot"
- Descargar los archivos "BaseSystem.chunklist" y "BaseSystem.dmg" del siguiente enlace: https://drive.google.com/drive/folders/1x1M4ZQmHdIYPU3-Xfr7BPC8GLRLmQINN
- Ubicar los dos archivos descargados dentro de la carpeta "com.apple.recovery.boot"


## Instalación

- Bootear desde la USB
- Formatear el disco escogido para MAC. Es importante asegurarse de que sea el disco de MAC y no el de otro sistema operativo.
- Instalar
**NOTA**: Durante el proceso no desconectar la red, ni realizar un corte forzoso de energía. Activar Apple ID después.

## Post Instalación

- Copiar la carpeta EFI final en la partición EFI del disco de mac, para así evitar usar el arranque desde el USB

**NOTA SOBRE LA EFI**: Como indique anteriormente, es posible usar una sola EFI en todo el proceso, para realizar esto sencillamente usa la versión que yo llamo "version final" en todo el proceso. En mi caso muestro el registro de como me funcionó, ya que no he tenido que reinstalar, pero debido a tantos intentos no tengo duda de que funcionará.

**NOTA RECOMENDACIÓN**: Evitar estár cambiando de tipo de dispositivo usado, además de serial. Esto evitar problemas incomodos desde loguearse de nuevo en los servicios o en activar la sincronización móvil, hasta problemas de incompatibilidad. 

### Aceleración gráfica

- Antes de iniciar el sistema, es necesario conectar el display port al puerto principal
- Cuándo inicie, se queda sin video, en ese momento cambiar el display por al segundo puerto para reactivar el video con aceleración gráfica.

### Está trabajando:
	- Aceleración
	- Sonido
	- Wifi
	- Las aplicaciones que uso de Apple funcionan bien:
		- Xcode
		- App Store
		- Mail
### Qué no està trabajando:
	- Hibernación
	- Microfono

### Errores descubiertos:
	- Cuándo el sistema se suspende da problemas, es decir, da problemas con los tiempos prolongados de inactividad. Se aplicó Fixed Slepp según la guía de Dortania.
	- Consultar sí se descubren más errores este repositorio o el repositorio original

El proyecto en el cual me base fue: https://github.com/toshinori8/HP-ProDesk-600-G3-DM

De antemano gracias a Toshinori8

## Enlaces importantes para entender el proceso y solucionar problemas:

https://dortania.github.io/OpenCore-Install-Guide/config.plist/skylake.html#nvram | Desktop Skylake | OpenCore Install Guide
https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/intel-gpu.html | Intel GPUs | GPU Buyers Guide
https://github.com/randyzhong/OS-X-HP-EliteDesk-800-G3-DM-Clover | randyzhong/OS-X-HP-EliteDesk-800-G3-DM-Clover: Files needed for installing Mac OSX on HP EliteDesk 800 G3 Desktop Mini Business PC 65W/35W. Feel free to contribute!
https://github.com/lqph1994/OpenCore-Hackintosh-HP-EliteDesk-800-G3 | lqph1994/OpenCore-Hackintosh-HP-EliteDesk-800-G3: Self project making my Intel PC running latest macOS
https://www.tonymacx86.com/threads/hd530-igpu-on-ventura-woes.325717/page-2 | HD530 iGPU on Ventura woes | Page 2 | tonymacx86.com
https://www.google.com/search?q=whatevergreen+configure+framebuffer+skylake+intel+hd+530&rlz=1C5CHFA_enCO1086CO1086&oq=whatevergreen+configure+framebuffer+skylake+intel+hd+530&gs_lcrp=EgZjaHJvbWUyBggAEEUYOdIBCTI1MjQ3ajBqN6gCALACAA&sourceid=chrome&ie=UTF-8 | whatevergreen configure framebuffer skylake intel hd 530 - Buscar con Google
https://github.com/dortania/clover-laptop-guide/blob/master/prepare-install-macos/display-configuration.md | clover-laptop-guide/prepare-install-macos/display-configuration.md at master · dortania/clover-laptop-guide
https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md#intel-uhd-graphics-610-650-kaby-lake-and-amber-lake-y-processors | WhateverGreen/Manual/FAQ.IntelHD.en.md at master · acidanthera/WhateverGreen
https://www.tonymacx86.com/threads/guide-general-framebuffer-patching-guide-hdmi-black-screen-problem.269149/page-121#post-2141095 | [GUIDE] General Framebuffer Patching Guide (HDMI Black Screen Problem) | Page 121 | tonymacx86.com
https://www.tonymacx86.com/threads/guide-catalina-on-hp-elitedesk-800-g4-g5-mini-the-perfect-macmini8-1-hackintosh-clover-oc.298530/#post-2127547 | [GUIDE] Catalina on HP EliteDesk 800 G4/G5 Mini - The Perfect MacMini8,1 Hackintosh - CLOVER & OC | tonymacx86.com
https://www.tonymacx86.com/threads/guide-general-framebuffer-patching-guide-hdmi-black-screen-problem.269149/page-145#post-2169249 | [GUIDE] General Framebuffer Patching Guide (HDMI Black Screen Problem) | Page 145 | tonymacx86.com
https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#preparations | Fixing Sleep | OpenCore Post-Install


## CHANGELOG

Solucion para fixear el sleep en mac, ya que no vuelve a dar video. Ejecutar los siguientes comandos:

	sudo pmset autopoweroff 0
	sudo pmset powernap 0
	sudo pmset standby 0
	sudo pmset proximitywake 0
	sudo pmset tcpkeepalive 0

Agregar los siguientes cambios en el config.plis: 

- Misc -> Boot -> HibernateMode -> None
We're gonna avoid the black magic that is S4 for this guide
- NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> boot-args
keepsyms=1 - Makes sure that if a kernel panic does happen during sleep, that we get all the important bits from it
swd_panic=1 - Avoids issue where going to sleep results in a reboot, this should instead give us a kernel panic log

Y en la bios:

Wake on LAN: disabled
TPM: Optional
Wake on USB: enable
Wake on Bluetooth: disabled

Para más clarida ir al original


*Fuente*: https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#preparations

**BY LUISSDEV**
