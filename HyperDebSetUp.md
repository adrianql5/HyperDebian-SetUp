# Tutorial Completo para Configurar Hyprland en Debian 13

Este tutorial te guiará paso a paso sobre cómo instalar y configurar **Hyprland**, un gestor de ventanas dinámico y moderno, en **Debian 13**. Cada comando y procedimiento está explicado para que entiendas exactamente qué hace y por qué es necesario, así no te perderás en ningún momento.

> **¿Eres nuevo en Linux o Git?**  
> Si no tienes experiencia previa con sistemas Linux o Git, te recomiendo consultar alguno de estos recursos antes o durante el proceso:
> 
> - [Pro Git Book (Español)](https://git-scm.com/book/es/v2)
> - [Guía Debian para principiantes](https://wiki.debian.org/es/FrontPage)
> - [Curso básico de Linux - OpenWebinars](https://openwebinars.net/blog/curso-basico-linux/)
> 
> Estos documentos te pueden ayudar a entender conceptos básicos y resolver dudas si te pierdes durante la instalación.

---

## 1. ¿Qué es Hyprland y por qué usarlo con Debian?

### ¿Qué es Hyprland?
Hyprland es un **compositor dinámico para Wayland**, centrado en la personalización, velocidad y efectos visuales modernos. Permite una experiencia gráfica fluida, moderna y altamente configurable, ideal para quienes buscan personalizar su entorno de escritorio.

> **¿Qué es Wayland?**  
> Wayland es un protocolo moderno que reemplaza al tradicional X11 en Linux para la gestión de gráficos. Define cómo los programas se comunican con el servidor gráfico y con el hardware de la computadora, ofreciendo mayor seguridad, mejor rendimiento y soporte para gráficos avanzados.

### Ventajas de usar Hyprland con Debian
- **Debian** es una de las distribuciones más estables y robustas de Linux, ideal tanto para servidores como para escritorios gracias a su fiabilidad.
- Al combinar Debian con Hyprland, obtienes una base sólida y estable junto a una interfaz gráfica moderna, fluida y muy personalizable.
- **Hyprland** aprovecha las tecnologías más recientes del ecosistema Linux, brindando un rendimiento gráfico superior, soporte para múltiples monitores y gestos modernos.

---

## 2. Cómo crear un USB booteable con Debian 13 usando Balena Etcher

### ¿Para qué sirve este paso?

Antes de instalar Debian, necesitas un USB booteable con la imagen de Debian 13 para poder arrancar e instalar el sistema operativo en tu PC o portátil.

### Pasos detallados:

#### 1. Descargar la imagen ISO de Debian 13

* Ve a la [página oficial de descargas de Debian](https://www.debian.org/download).
* Descarga la ISO adecuada para tu arquitectura.

  * Para la mayoría de PCs (Intel/AMD): **`debian-13.0.0-amd64-netinst.iso`**
  * Para procesadores ARM (ej. algunos portátiles o placas): **`arm64`**

> 📌 El archivo más común es el **netinst (Network Installation)**, que ocupa poco espacio y descarga los paquetes durante la instalación.
> Si prefieres, también puedes descargar la ISO completa (DVD) desde la misma página.

#### 2. Descargar e instalar Balena Etcher

* Página oficial: [https://www.balena.io/etcher/](https://www.balena.io/etcher/)
* Descarga el instalador para tu sistema operativo (Windows, macOS o Linux) e instálalo siguiendo los pasos que indica la web.

#### 3. Flashear la ISO en el USB

* Abre **Balena Etcher**.
* Selecciona la imagen ISO de Debian que descargaste.
* Inserta tu USB y selecciónalo en Etcher.
* Haz clic en **“Flash!”** para grabar la imagen en el USB.
  *(Este proceso borrará todo lo que haya en el USB)*

#### 4. Instalar Debian usando el USB booteable

* Reinicia tu PC y entra en el menú de arranque (boot menu).
  *(Suele ser una tecla como F12, F2, ESC o DEL, dependiendo del fabricante. Busca en internet “boot menu + tu marca/modelo” si tienes dudas).*
* Elige arrancar desde el USB.
* Sigue el asistente de instalación guiado de Debian.
  *(El proceso es bastante intuitivo, solo sigue las instrucciones en pantalla y selecciona las opciones recomendadas si tienes dudas).*


## 3. Primeros pasos tras instalar Debian

### a) Cambiar a superusuario (root)

```bash
su -
```
- **¿Para qué sirve?**  
  Cambia al usuario root, que tiene permisos totales en el sistema.

### b) Dar permisos de sudo a tu usuario

```bash
sudo usermod -aG sudo "tu_usuario_debian"
```
Finalmente reiniciamos con ``` reboot``` 

- **¿Para qué sirve?**  
  Agrega tu usuario al grupo `sudo`, permitiéndote ejecutar comandos que requieran de ciertos privilegios.

---

### c) Verificar que tienes configuradas correctamente las fuentes de paquetes
Un paquete es un archivo que contiene todo lo necesario para instalar un programa en Linux: el ejecutable, librerías, documentación y scripts de configuración. Los paquetes suelen tener extensión .deb en Debian y derivados (como Ubuntu).

Los sistemas Linux usan gestores de paquetes para instalar, actualizar o eliminar software de forma sencilla y segura. Estos gestores descargan los paquetes desde servidores llamados "repositorios".

APT (Advanced Package Tool) es el sistema de gestión de paquetes usado en Debian y muchas de sus variantes. Permite buscar, instalar, actualizar y eliminar software automáticamente, resolviendo dependencias entre paquetes.

El archivo /etc/apt/sources.list y los archivos en /etc/apt/sources.list.d/ indican a APT de dónde descargar los paquetes (las “fuentes de paquetes”).
- `sudo apt update` actualiza la lista de paquetes disponibles.
- `sudo apt install nombre_paquete` instala un programa.


1. **Edita el archivo de fuentes de APT**  
   Abre el archivo `/etc/apt/sources.list` con privilegios de superusuario:

   ```bash
   sudo nano /etc/apt/sources.list
   ```

2. **Asegúrate de que contenga las siguientes líneas:**  
   (Reemplaza el contenido si es necesario)

   ```
   deb http://deb.debian.org/debian/ trixie main non-free-firmware
   deb-src http://deb.debian.org/debian/ trixie main non-free-firmware

   deb http://security.debian.org/debian-security trixie-security main non-free-firmware
   deb-src http://security.debian.org/debian-security trixie-security main non-free-firmware

   deb http://deb.debian.org/debian/ trixie-updates main non-free-firmware
   deb-src http://deb.debian.org/debian/ trixie-updates main non-free-firmware
   ```

3. **Guarda y cierra el archivo:**  
   - Presiona `Ctrl + O` para guardar los cambios  
   - Presiona `Enter` para confirmar  
   - Presiona `Ctrl + X` para salir del editor

4. **Actualiza la lista de paquetes:**  
   Ejecuta el siguiente comando para actualizar los repositorios:

   ```bash
   sudo apt update
   ```
   
### d) Instalar Git
Git es un sistema de control de versiones distribuido.
Sirve para gestionar y registrar los cambios que se realizan en archivos y proyectos, especialmente en desarrollo de software.
Permite trabajar en equipo, guardar el historial de modificaciones, recuperar versiones anteriores y colaborar fácilmente entre varias personas, asegurando que los cambios no se pierdan y se puedan combinar de manera ordenada.

```bash
sudo apt install git
```

---

## 4. Instalar Hyprland
``` bash
sudo apt install hyprland
```

Finalmente clonamos este repostitorio: https://github.com/JaKooLit/Debian-Hyprland

```bash
git clone https://github.com/JaKooLit/Debian-Hyprland
```

Esto creará una carpeta llamada Debian-Hyprland en el directorio donde ejecutaste el comando. Accede a la carpeta y ejecuta el instalador:
``` bash
cd Debian-Hyprland
./install.sh
```
Sigue las instrucciones que te muestre el instalador. Por ejemplo, podrías ver una pantalla como esta:
<img width="717" height="437" alt="imagen" src="https://github.com/user-attachments/assets/ea9fef0c-8ec7-4afa-bd0d-484d7fad1989" />

Selecciona las opciones que prefieras según tus necesidades.

Cuando la instalación termine, reinicia tu sistema para aplicar los cambios:
```bash
sudo reboot
```

---

## 5. Consejos y enlaces útiles

- [Wiki oficial de Hyprland](https://wiki.hyprland.org/)
- [Documentación de Debian](https://wiki.debian.org/)
- Puedes personalizar Hyprland editando el archivo de configuración en `~/.config/hypr/hyprland.conf`.

---
