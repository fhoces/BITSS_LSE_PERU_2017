<!--YAML HEADER
---
title : Introduccion a Git utilizando Github Desktop
part of : BITSS PUC-Chile
time : 3 hours
author: Garret Christensen
affiliation: UC Berkeley
---
-->

Taller de Git & GitHub Desktop
==============================
BITSS PUC-Chile 2017
------------------------------
Fernando Hoces de la Guardia

Gracias a [Garret Christensen](http://www.ocf.berkeley.edu/~garret) por proveer el material original para este entrenamiento.

Básicamente, estamos tratando de evitar una situación como esta:
![http://www.phdcomics.com/comics/archive/phd101212s.gif](http://www.phdcomics.com/comics/archive/phd101212s.gif)

Y acercarnos un poco a esto:

![Git xkcd comic](https://imgs.xkcd.com/comics/git.png)


### Contexto:

A un nivel fundamental, el problema es que rara vez creamos productos perfectos en el primer intento. Añadimos, borramos y revisamos constantemente. En el caso de tareas de procesar texto, como en el ejemplo de PhD Comics, las consecuencias son menores, como el tiempo que te toma en encontrar el archivo correcto, o la vergüenza de enviar la versión incorrecta a un colega.

Cuando trabajas con tus datos, sea en recolección, limpieza, transformaciones, o análisis, puede que ya trabajes de una forma que es auto-documentante. Esto ocurre cuando estas escribiendo código y no ocupando herramientas de 'point & click' (GUI  - Graphical User Interface). La ventaja de esto es que es reproducible, la desventaja es que si tienes la versión incorrecta toda linea de producción de tu estudio se estanca.

Una forma relativamente común de definir tu flujo de trabajo se puede encontrar [aqui](https://bids.github.io/2017-01-12-ucb/lessons/R/reproducible_workflow.html). Si hacen clases en pre-grado, miren el protocolo del [Project TIER](http://www.projecttier.org/).  

La meta aspiracional es que yo debería ser capaz de entrar en tu laboratorio en la noche, borrar todos tus archivos excepto tu código y datos originales, y tu deberías ser capaz de ejecutar un solo comando para regenerar TODO, incluyendo todos los resultados, tablas y figuras en su forma final. Esto es lo que se entiende por 'flujo de trabajo de un-click'.


En el otro extremo, cuando no puedes encontrar la versión correcta de tu procesacimento o análisis de datos, pierdes la habilidad de recrear cualquier resultado que fue generado en el pasado. Si tus resultados no son reproducibles, también adolecen de los siguientes problemas:

1. No son verificables
2. Son mas difíciles de explicar
3. No son extendibles


Por esta razón, necesitamos saber cual es la versión exacta que estamos utilizando y que ha cambiado con respecto a la versión previa. Hay muchas soluciones en este espacio. Algunos mantienen diferentes revisiones manualmente, separando todo en una serie de carpetas. Otros ocupan software que registra cada acción tomada (STATA o SPPS 'logs'). También hay quienes utilizan alguna función del tipo 'control de cambios' en su GUI (Graphical User Interface).


Todas estas soluciones adolecen del mismo problema, en tanto obligan al usuario a pensar que es una versión y como se deben manejar cambios a través de versiones. Por ejemplo si estas documentando tu flujo de trabajo en logs (SPSS o STATA) y quieres saber de donde salió ese resultado que generaste la semana pasada, tienes que manualmente buscar en el log de el día en cuestión, más todos los logs que potencialmente te pudieron llevado a generar ese resultado.

Git, or `git`, es un software que elimina ese problema. Es un programa de control de versiones que te ayuda, de manera muy precisa, a registrar *todos* los cambios en archivos de texto, con o sin colaboradores. Noten que `.txt, .do, .R, .md, .tex`, y muchos otros formatos son archivos de texto. Otros formatos como `.doc, .docx, .xls, .xlsx, .pdf, .dta` no son archivos de texto (`.csv` es complicado, pero la respuesta corta es no). De esta forma hay un alto valor en utilizar Git o Gihub en archivos con codigo (.do), pero no hay mucho valor en usarlo en archivos con datos (.dta). La mayor barrera para la adopción masiva de Git en la comunidad científica (publicado por primera vez en el 2005) es que no es particularmente intuitivo. Sus desventajas son:

1. Difícil de entender
2. Difícil de usar correctamente

Y sus ventajas son:

1. Nunca mas vas a borrar o perder un archivo de manera accidental.
2. Siempre vas a ser capaz de volver a la versión anterior en tu flujo de trabajo.
3. Fácil descubrir que ha cambiado (i.e. origen del problema), y cuando

Afortunadamente para nosotros, Github y otras compañías han creado aplicaciones que apuntan a proveer acceso a git de manera amigable para el usuario. Usuarios con mas experiencia usan Git en la linea de comandos (Terminal en Mac y Git Shell/Bash en Windows). Pero estas aplicaciones pueden llevar a cabo las principales funciones de Git, lo cual es suficiente para nuestras necesidades.

Puede que necesitemos utilizar la linea de comandos para hacer algunas cosas. [Aquí](http://swcarpentry.github.io/shell-novice/02-filedir/) hay algo de ayuda, y no dudes en preguntar.

### Antes de empezar:

* Asegurence de tener un editor de texto en su computador.
  * **Windows:** Notepad
  * **Mac:** Textedit -  cambien los defaults como se indica [aqui](http://www.iphonehacks.com/2017/06/plain-text-mode-textedit-mac.html). O instalen un editor.
Como [Atom](http://atom.io), Sublime o Notepad++ (el editor de do-files de Stata también funciona).

* Descargar e instalar el [GitHub Desktop app](http://desktop.github.com).

* [Crear](https://github.com/join?source=header-home) una cuenta en Github.com.

## Forking

Vamos a ocupar nuestra nueva cuenta de Github para hacer *fork* `fork`<sup>1</sup> de un respositorio -- el mismo repositorio en el cual fue creado este taller!

* Vayan a [https://github.com/fhoces/BITSS_PUC_CHILE_2017](https://github.com/fhoces/BITSS_PUC_CHILE_2017)

* Busquen el botón que dice 'fork' en la esquina superior derecha y hagan click

Este repositorio va a ser copiado a tu cuenta (pero **no** a tu computador), permitiendo modificarlo como lo desees. Dado que el 'fork' vive en los servidores de Github, cualquier cambio que se hagan a esos servidores ya van a estar respaldados para ti.

* Para evitar confusiones, cambien el nombre del repositorio a algo así como `GitTaller` en la seccion de settings.

### Clonando, Creando y Modificando
Las opciones en la app de Github (desktop) bajo el botón '+' son: añadir, crear o clonar un repositorio. *Añadir* busca un repositorio en tu computador y le dice a la app que lo añada al listado de repositorio que esta siguiendo. *Crear* crea un nuevo repositorio: una carpeta en tu computador y lo añade automáticamente al listado de repositorios a seguir. *Clonar* copia un repositorio de tu cuenta en github.com en tu computador.  

Para clonar un repositorio publico que no te pertenece, haz click en el botón de descarga que esta justo a la izquierda del botón 'Download ZIP' en la pagina del repositorio en GitHub.com.

* Clonen el fork que hicieron del repositorio de este taller. Luego naveguen en su computador para verificar que esta ahí.

* Qué archivos ven ahí? Hay algún archivo que no saben lo que es (`.gitignore`)? Si no, prueben esto: [[Mac](http://www.macworld.co.uk/how-to/mac-software/how-show-hidden-files-in-mac-os-x-finder-funter-macos-sierra-3520878/)][[Windows](https://support.microsoft.com/en-us/help/14201/windows-show-hidden-files)]
Si ven estos archivos escondidos, *nunca jamas* los deben tocar (aquí es donde git guarda todo el historial de cambios).

Felicitaciones! han clonado exitosamente su primer repositorio. Ahora vamos a *crear* un repositorio nuevo.

* Creen un nuevo repositorio. Denle un nombre como `primer_repo_tunombre` *Qué archivos ven ahí?*

* Creen un archivo y nombrenlo `README.md` ocupando el editor de texto.  

> Primera linea en su programa

> Segunda linea del programa

> Tercera linea del programa

* Guarden el archivo en la carpeta `primer_repo_tunombre`

Qué ha cambiado en el app de Github?

* Abran el archivo `README.md` en Github Desktop.

Git guarda archivos en tres areas. El area de trabajo, el area de posicionamiento (staging), y el repositorio.
![SWC Git areas](https://swcarpentry.github.io/git-novice/fig/git-staging-area.svg)

Github Desktop automáticamente añade los archivos al área de posicionamiento. Eso es lo que significa el check al lado de cada nombre.

* Quiten y vuelvan a añadir el check al archivo `README.md`.

* Hagan commit, o archiven de manera permante, el archivo `README.md` añadiendo un preve descripción como `README creado`. Luego hagan click in `Commit to master`.

* Creen un segundo archivo ocupando el editor de do-files de Stata y llamenlo `regressions.do`. Escriban estas lineas:

`clear all`

`set more off`

`sysuse auto`

`reg price mpg`

* Guarden el archivo .do

* Añadan una cuarta linea al texto de `README.md` y guarden.

> Cuarta linea del programa

* Quiten el check de `regressions.do` y hagan commit de *solamente* el archivo`README.md` con el mensaje `cuarta linea agregada a README`.

* Vuelvan a checkear `regressions.do` y hagan commit con el mensaje `agregamos regressions.do`.

* Añadan una quinta linea a `README.md`:
> Quinta linea del programa

* Hagan commit.

* Agregen otra linea al archivo `README.md`:
> La sexta! linea de este creativo programa

* Hagan commit de este cambio.


#### Deshacer
Hay varias formas de deshacer en git, no todas de ellas son posibles en Github Desktop. Los métodos de GH son:

1. Click derecho sobre el archivo deseado y seleccione 'Discard changes'.

2. Click en algún cambio en la sección 'History' y luego click en 'revert'.

3. Click en Undo inmediatamente después de un commit.

* Reviertan el commit que agregó la quinta linea en `README.md`.

* Reviertan la reversion de forma tal que vuevan a tener las 6 lineas completas en `README.md`.

<!--
We'll try one quick command in the command line. (See the SWC lesson [here](https://swcarpentry.github.io/git-novice/05-history/).)
* Open Git Shell (Windows) or Terminal (Mac).
* Navigate (using `cd`) to inside the folder that is the repository.
* Enter `git status` to make sure you're in your repository.
* Enter `git log` to see the record of your changes.
* Enter `git checkout <hash> <filename.txt>` where `<hash>` is the unique letter and number string refering to the place you want to jump back to and filename is the specific file.
* Verify that the file has changed back to the point you want.
* To get the latest version back, type `git checkout HEAD <filename.txt>` or `git checkout master` which will send you to the tip of the `master` branch. (I know, we haven't talked about branches yet! So let's do that now.)

Atlassian has a great [explanation](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting) of the differences between revert, reset, and checkout.  
-->

### Branching:
Git utiliza ramas (branches) para que puedas experimentar con ideas nuevas o corregir errores de codigo.

* Crea, nombra y sincroniza una nueva rama de nombre `experimental` haciendo click en 'create new branch'.

* Cambien el archivo `regressions.do` haciendo la regresion robusta a heterocedasticidad, guarden y hagan commit a la rama `experimental`.


* Emergencia! Imagina que algo ocurrió y tienes que volver a la rama maestra.

* Cambia una parte diferente de `regressions.do`. Agrega la linea al final: `summ length`

* Unan la rama experimental a la rama maestra. In Github Desktop esto se hace mediante un click en `Branch/Update from`. Es importante asegurarse de estar **en** la rama maestra y hacer update **desde** la rama experimental.

### Publicando en la web (pushing y pulling):

Todo el contenido rastreado por git (y más) puede ser almacenado online en GitHub.com (o cualquier otro servidor con Git instalado), lo que te va a permitir trabajar en multiples computadores.

Git hace uso frequente de comandos llamados `push`ing (enviar) y `pull`ing (recivir). Github Desktop simplifica ambas en una operacion llamada "Sync".

Para publicar tu repositorio en la web.
* Simplemente has click en el botón 'Publish'.

<!--Now we want to make sure that we can make changes online via GitHub.com, and then sync them to your computer (pulling).

* Go back and forth between making a local change, committing, and pushing it to the web, and making remote (online) changes (click the pencil button to edit, then commit at the bottom of the screen), being sure to sync between each commit. Eventually you'll screw up and not sync enough. (That is, change a file online and commit it. Don't sync. Make a contradictory change locally and commit it. Try and sync. *What happens?*)
-->

<!--Aside: This tutorial is written in Markdown. If you want something *not* to render markdown, comment it out like this. Same as HTML.-->

<!--
#### Conflictos
Between the experimental branch and the main branch, make and commit some conflicting changes (that is, changes to the same lines of the same file). Then try and merge. *What happens?*
* Change the regression line to read `reg price mpg weight` in master. Save and commit to master.
* Change the regression line to read `reg price mpg length, robust` in experimental. Save and commit to experimental.
* Try and merge.
* View the conflict (`<<<<<<<` `=======` and `>>>>>>>`), resolve the conflict by editing the weird part out of the file yourself, saving, and committing.

There's a conflict tutorial [here](https://bids.github.io/2017-01-12-ucb/lessons/git/).

### Collaborating:
Thus far we've been working solo. Now we'll collaborate. GitHub is built for this. Thousands of people contribute code to large open source coding projects without ever meeting in person. It's also great for just a few people to collaborate on simpler coding projects.

There are two ways to collaborate:

1. Make everyone you trust a collaborator. For small projects with trusted collaborators only.
2. Pull requests. For big projects--let anyone make suggestions (called pull requests) and the owner gets to choose whether to accept.

We'll probably only have time for #1.

1. Pair up with a neighbor. One of you be A and one be B for this exercise.
2. In the settings tab for A's repository on Github.com (that A published above), add B as a collaborator.
3. B accept the invitation, and clone A's repository so you have it on your own computer.
4. B make a change, commit, and sync (push) the change.
5. A sync (pull) B's changes, make your own changes, commit, and push.
6. After handing off back and forth successfully, make simultaneous conflicting changes. *How do you resolve the conflicts?*
7. Switch roles between A & B and repeat.

If we have time for Pull Request collaboration, or you have questions, we will follow Github's [guide](https://help.github.com/desktop/guides/).

### Additional Git Topics:

#### Pull Requests:
This is how you suggest changes to repositories to which you aren't a full fledged collaborator. Try this with a partner if you have time. Clone a repo you don't own, make a change, submit a pull request, and ask the owner to merge the pull request. Switch roles.

#### Command Line:
Many, if not most, experienced users will use Git via the command line. (Terminal on a Mac, the Git Shell that came with the Desktop app, Windows PowerShell, there are a lot of options. They're all where you type commands for your computer to execute.) You can read why [here](http://programmers.stackexchange.com/questions/173297/why-learn-git-when-there-are-gui-apps-for-github). Basically, it's more powerful.
-->

Hay muchos tutoriales sobre git en la web. Un recurso que recomiendo mucho es [Software Carpentry](http://swcarpentry.github.io/git-novice/) y también [Atlassian](https://www.atlassian.com/git/tutorials/). Lo mas básico esta muy bien resumido en una pagina [aquí](http://rogerdudler.github.io/git-guide/) in a single page.


**1.** Para más información sobre forking, ver [https://help.github.com/articles/fork-a-repo/](https://help.github.com/articles/fork-a-repo/)
