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

- Ve a la [página oficial de descargas de Debian](https://www.debian.org/).
- Haz clic en **Otras Descargas**:
  ![imagen1](https://github.com/user-attachments/assets/f863ec4e-d266-40df-9cf5-ae2dab24f902)
- Luego, selecciona **Imágenes ISO de Debian «en pruebas» («testing»)**:
  ![imagen2](https://github.com/user-attachments/assets/1b0375ae-86bf-4483-b3ed-b2b8b65b23bd)
- Descarga el archivo `.iso` apropiado para tu arquitectura:
    - Para la mayoría de PCs (Intel/AMD): selecciona `amd64`
    - Para equipos con procesadores tipo Mac M1/M2: selecciona `arm64`
  ![imagen3](https://github.com/user-attachments/assets/c97127eb-536f-48ab-b6ba-f060b54fa225)
- [Enlace directo a las imágenes de instalación](https://www.debian.org/devel/debian-installer/)

#### 2. Descargar e instalar Balena Etcher

- Página oficial: [https://www.balena.io/etcher/](https://www.balena.io/etcher/)
- Descarga el instalador para tu sistema operativo (Windows, macOS o Linux) e instálalo siguiendo los pasos que indica la web.

#### 3. Flashear la ISO en el USB

- Abre **Balena Etcher**.
- Selecciona la imagen ISO de Debian que descargaste.
- Inserta tu USB y selecciónalo en Etcher.
- Haz clic en **“Flash!”** para grabar la imagen en el USB.  
  *(Este proceso borrará todo lo que haya en el USB)*

#### 4. Instalar Debian usando el USB booteable

- Reinicia tu PC y entra en el menú de arranque (boot menu).  
  *(Suele ser una tecla como F12, F2, ESC, o DEL, dependiendo del fabricante. Busca en internet “boot menu + tu marca/modelo” si tienes dudas)*
- Elige arrancar desde el USB.
- Sigue el asistente de instalación guiado de Debian.  
  *(El proceso es bastante intuitivo, solo sigue las instrucciones en pantalla y selecciona las opciones recomendadas si tienes dudas)*

---

## 3. Primeros pasos tras instalar Debian

### a) Dar permisos de sudo a tu usuario

```bash
sudo usermod -aG sudo "tu_usuario_debian"
```
- **¿Para qué sirve?**  
  Agrega tu usuario al grupo `sudo`, permitiéndote ejecutar comandos que requieran de ciertos privilegios.

### b) Cambiar a superusuario (root)

```bash
su -
```
- **¿Para qué sirve?**  
  Cambia al usuario root, que tiene permisos totales en el sistema.

### c) Editar repositorios de software

```bash
sudo nano /etc/apt/sources.list
```

```
deb http://deb.debian.org/debian trixie main contrib non-free non-free-firmware
deb http://deb.debian.org/debian trixie-updates main contrib non-free non-free->
deb http://security.debian.org/debian-security trixie-security main contrib non>
deb http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware
```



- **¿Para qué sirve?**  
  Abre el archivo donde se listan los repositorios de software. Aquí puedes añadir, quitar o modificar las fuentes desde donde Debian descarga los programas.

### d) Actualizar la lista de paquetes

```bash
sudo apt update
```
- **¿Para qué sirve?**  
  Refresca el listado de paquetes disponibles y sus versiones.

---

## 4. Añadir el repositorio "unstable" para obtener Hyprland

### ¿Por qué es necesario?
Hyprland y algunos paquetes están más actualizados en el repositorio "unstable" de Debian.

```bash
echo 'deb http://deb.debian.org/debian unstable main contrib non-free non-free-firmware' | sudo tee /etc/apt/sources.list.d/unstable.list
sudo apt update
```

- **¿Para qué sirve?**
  - Añade el repositorio "unstable" a tu sistema para acceder a las versiones más recientes de ciertos paquetes.
  - Ten en cuenta que usar "unstable" puede aumentar el riesgo de instalar software menos probado.

### Instalar Hyprland usando el repositorio unstable

```bash
sudo apt -t unstable install hyprland
```
- **¿Para qué sirve?**  
  Instala Hyprland y sus dependencias desde el repositorio "unstable".

---

## 5. Instalar utilidades adicionales

### Instalar GNOME Network Manager (opcional pero recomendado)

```bash
sudo apt install network-manager-gnome
```
- **¿Para qué sirve?**  
  Herramienta gráfica para gestionar conexiones de red fácilmente.

---

## 6. Descargar y ejecutar un script de configuración de Hyprland

### ¿Por qué este paso?
Existen scripts que automatizan la configuración y optimización de Hyprland en Debian, facilitando el proceso especialmente para principiantes.

```bash
git clone --depth=1 https://github.com/JaKooLit/Debian-Hyprland.git ~/Debian-Hyprland
cd ~/Debian-Hyprland
chmod +x install.sh
./install.sh
```
- **¿Para qué sirve cada comando?**
  - `git clone ...`: Descarga el repositorio con los scripts de configuración.
  - `cd ~/Debian-Hyprland`: Entra en la carpeta del repositorio clonado.
  - `chmod +x install.sh`: Da permisos de ejecución al script.
  - `./install.sh`: Ejecuta el script que instalará y configurará Hyprland automáticamente.

---

## 7. Reinicia tu ordenador

Una vez completados los pasos anteriores, reinicia tu PC para empezar a utilizar Hyprland.

---

## 8. Consejos y enlaces útiles

- [Wiki oficial de Hyprland](https://wiki.hyprland.org/)
- [Documentación de Debian](https://wiki.debian.org/)
- Puedes personalizar Hyprland editando el archivo de configuración en `~/.config/hypr/hyprland.conf`.

---
