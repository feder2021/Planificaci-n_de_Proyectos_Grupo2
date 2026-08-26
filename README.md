# tdse-tp0_01-stm32_project
FIUBA - Electrónica - Taller de Sistemas Embebidos - Trabajo Práctico Nº 0 

===========================================================================
               APUNTES DE GIT - SISTEMAS EMBEBIDOS (FIUBA)
===========================================================================

---------------------------------------------------------------------------
0. CONFIGURACIÓN INICIAL DE LA PC (Se hace una sola vez)
---------------------------------------------------------------------------
Establece tu identidad para todos los repositorios de esta máquina:
git config --global user.name "Tu Nombre"
git config --global user.email "tu-email@ejemplo.com"
git config --global init.defaultBranch main        # Fuerza que la rama inicial sea siempre 'main' en vez de 'master'

Para revisar los datos cargados:
git config --list

---------------------------------------------------------------------------
1. CASO A: CREAR UN REPOSITORIO PROPIO DESDE CERO
---------------------------------------------------------------------------
Usá este flujo cuando iniciás un TP nuevo en tu PC y querés subirlo a un GitHub vacío.

1. Abrir la terminal de Windows y navegar hasta la carpeta exacta del proyecto:
   cd "C:\Path\A\Tu\tdse-tp0_01-stm32_project"

2. Configurar el archivo de exclusiones (.gitignore):
   Crear un archivo llamado exactamente `.gitignore` en la raíz de la carpeta y escribir:
   Debug/
   Release/
   .settings/
   (Esto evita que se suban archivos generados por el compilador del IDE).

3. Inicializar el sistema de control de versiones local:
   git init

4. Vincular el proyecto local con la URL del repositorio creado en GitHub:
   git remote add origin https://github.com

5. Descargar el README.md inicial que genera GitHub de forma mandatoria:
   git pull origin main --allow-unrelated-histories

6. Indexar y realizar el primer guardado local:
   git add .
   git commit -m "Initial commit: Estructura limpia del proyecto STM32"

7. Subir por primera vez estableciendo el puente permanente (-u):
   git push -u origin main

---------------------------------------------------------------------------
2. CASO B: TRABAJAR SOBRE EL REPOSITORIO DE UN COMPAÑERO
---------------------------------------------------------------------------
Usá este flujo si tu compañero ya creó el repositorio en GitHub y vos necesitás una copia idéntica en tu computadora para trabajar.

1. Abrir la terminal en la carpeta contenedora general (ej. tdse_workspace):
   cd "C:\Users\Fede\Documents\Facultad\Sistemas Embebidos\tdse_workspace"

2. Clonar el repositorio (descarga la carpeta con todo su historial):
   git clone https://github.com

3. Entrar a la carpeta que se acaba de crear de forma automática:
   cd proyecto-stm32

4. Verificar que el origen apunte correctamente al servidor:
   git remote -v
   (A partir de este paso, el puente ya queda configurado y listo para trabajar).

---------------------------------------------------------------------------
3. FLUJO DIARIO: CÓMO SUBIR MODIFICACIONES Y ENVIAR CAMBIOS
---------------------------------------------------------------------------
Cada vez que edites código, agregues funciones o completes un punto del TP:

1. Consultar qué archivos sufrieron modificaciones:
   git status

2. Ver las líneas exactas de código que cambiaste (opcional):
   git diff

3. Pasar los archivos modificados al área de preparación (Staging):
   git add .                        # Agrega absolutamente todos los cambios
   git add "Core/Src/main.c"        # Alternativa: Agrega solo un archivo puntual

   *Nota de auxilio:* Si agregaste un archivo por error al staging, lo quitás con:
   git reset <archivo>

4. Consolidar el cambio en el historial local firmándolo con un mensaje descriptivo:
   git commit -m "Core: Se programa la inicialización del temporizador del TP0"

5. Descargar cambios que haya subido tu compañero para evitar conflictos:
   git pull origin main

6. Subir tus commits definitivos a la nube de GitHub:
   git push

---------------------------------------------------------------------------
4. COMANDOS ÚTILES DE CONSULTA Y MANTENIMIENTO
---------------------------------------------------------------------------
Historial y Ramas:
git log --oneline                  # Muestra la lista de commits simplificada en una línea
git show <hash_commit>             # Muestra en detalle los cambios de un commit específico
git branch                         # Muestra las ramas locales (la activa tiene un asterisco)

Corregir URLs de servidores erróneos:
Si vinculaste el alias 'origin' a un repositorio equivocado (ej. RedNeuronal), corregilo con:
git remote set-url origin https://github.com/feder2021/tdse-tp0_01-stm32_project

Deshacer metidas de pata:
git checkout -- <archivo>          # Descarta los cambios locales no guardados de un archivo
git reset --soft HEAD~1            # Deshace el último commit local manteniendo el código intacto




===========================================================================
             GUÍA DE STM32CUBEIDE - SISTEMAS EMBEBIDOS (FIUBA)
===========================================================================

---------------------------------------------------------------------------
1. CONFIGURACIÓN, PERSPECTIVAS Y RUTAS
---------------------------------------------------------------------------
• Recuperar ventanas perdidas (Perspectiva rota):
  Si se te cierra una solapa clave o se te desordena el entorno de desarrollo:
  WINDOW -> Perspective -> Reset Perspective... (Restaurar vista por defecto).

• Copiar la ruta exacta del proyecto para la consola de Git:
  En el Project Explorer, hacé Click derecho en tu proyecto -> Properties.
  Andá a Resource (en el menú de la izquierda) y copiá la dirección de 'Location'.

• Encontrar un archivo abierto en el árbol de carpetas:
  Si estás editando un código muy oculto y querés ver dónde está guardado en el 
  explorador, activá el ícono de las dos flechas amarillas cruzadas ("Link with Editor") 
  ubicado arriba en la barra de pestañas del explorador de proyectos.

---------------------------------------------------------------------------
2. ATAJOS DE TECLADO RECOMENDADOS (Shortcuts)
---------------------------------------------------------------------------
Para revisar o modificar todos los atajos del IDE: WINDOW -> Preferences -> General -> Keys

• Compilar el proyecto completo:               Ctrl + B
• Autocompletar código / Sugerir funciones:   Ctrl + Space
• Buscador global en todo el Workspace:        Ctrl + H
• Quick Outline (Ir rápido a una función):     Ctrl + O
• Buscar y abrir cualquier archivo por nombre:  Ctrl + Shift + R
• Buscar y abrir elementos específicos (Tipos): Ctrl + Shift + T

• Selección en bloque (Edición multilínea):    Alt + Shift + A
  (Permite seleccionar un rectángulo de texto y editar varias líneas al mismo tiempo. 
  Por ejemplo: cambiar el tipo de dato de 5 variables consecutivas de un solo tiro).

---------------------------------------------------------------------------
3. FLUJO DE TRABAJO EFICIENTE CON TASK TAGS (Notas de desarrollo)
---------------------------------------------------------------------------
Sirve para dejar recordatorios directamente en el código sin tener que recordar 
los números de línea:

1. Configurar una etiqueta personalizada:
   Andá a WINDOW -> Preferences -> C/C++ -> Property Pages Settings -> Task Tags.
   Hacé clic en 'New...', poné el nombre (Ejemplo: "Revisar") y definí su prioridad.

2. Usarlo en el código:
   Escribí un comentario normal usando tu nueva etiqueta: 
   // Revisar: Validar el valor máximo del contador del temporizador aquí.

3. Monitorear las tareas pendientes:
   Andá a WINDOW -> Show View -> Tasks. Se abrirá una solapa que lista todas tus notas. 
   Haciendo doble clic en la tarea, el IDE te lleva directo a la línea correspondiente.

---------------------------------------------------------------------------
4. INSPECCIÓN Y ANÁLISIS DE DEPENDENCIAS
---------------------------------------------------------------------------
• Ver la red de dependencias de un archivo (.c / .h):
  1. Hacé clic en WINDOW -> Show View -> Include Browser.
  2. Arrastrá tu archivo (por ejemplo, `main.c`) dentro de la nueva solapa abierta.
  3. El IDE te desplegará un árbol detallado con todos los archivos de cabecera y 
     librerías del HAL que están asociados de forma directa o indirecta a tu código.

