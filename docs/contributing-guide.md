---
  hide:
  - navigation  

  title: Guia de contribución
  author: Santiago Villegas <santiago.villegas@pragma.com.co>
---

# Guia de contribución

## Introducción

A largo plazo las organizaciones que quieren mantener su rendimiento necesitan una documentación que ayude a entender, operar y evolucionar su tecnología. 
Nuestra misión principal es tener una buena documentación útil tanto para los colaboradores nuevos como existentes. 

Tips para una excelente documentación:

- Revise los documentos con un par, antes de publicar. 
- Piense en su yo del futuro cuando escriba documentos, lo agredecerá.
- Aplique un estándar consistente en todos los documentos relacionados, para facilitar la lectura.
- Mantenga la documentación actualizada (y sin errores) con las versiones actuales.

## Empezando

Requisitos: 

- [Docker](https://docs.docker.com/engine/install/)
- [Git](https://git-scm.com/downloads)

### Inicializar Modo escritor

Clonar el proyecto desde el repositorio

```
git clone https://pragmatranser.visualstudio.com/Transer/_git/transer-wiki && cd transer-wiki/
```

Construir instantanea mkdocs-material para transer

```
docker build . -t mkdocs-transer
```

Luego, inicialice un servidor para pre-visualizar la doc en el navegador (modo escritor)

```
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs mkdocs-transer
```

Ahora puede ver el sitio de la doc en [http://localhost:8000](http://localhost:8000) 

El servidor auto-recarga el sitio web un vez que detecte cualquier cambio en los archivos fuentes. 

### Estructura del proyecto 

Como contribuidor solamente debe escribir archivos .md dentro de las carpetas de las secciónes principales respectivamente segun el area de trabajo que se relaciona con el contenido de la documentación que desea agregar.

```
.
├── css
│   └── extra.css
├── images
│   └── favicon.png
├── backend
├── process
├── infraestr
├── security
├── observability
├── web
├── index.md
├── template.md
...
```

**Consideraciones:**

- Cada sección principal tiene una carpeta en el directorio de docs/ y una referencia directa en el archivo '.pages'.
- Los documentos no relacionados a una sección principal pueden ir sobre el directorio 'docs/'.
- No modificar la estructura actual, ni eliminar contenido de otros autores. 
- Cualquier modificación significativa sobre el proyecto debe ser aprobada por el arquitecto del proyecto y el DevOps.

!!! Note
    Para comprender las secciones y navegación recomendamos leer la [Guía de exploración](explorer-guide.md) antes de avanzar.

## Contribuir

En general toda documentación es buena pero puede ser mejor asi que alentamos a que recuerde los tips para una excelente documentación. 

Existen varias formas de contribuir, puede empezar con las siguientes preguntas: 

- ¿Encontraste algo que faltaba? 
- ¿Has encontrado un error? 
- ¿Cómo crear un documento propio?
- ¿Cómo arreglar las cosas aquí? 

Aunque no vamos a cubrir todas los casos puede seguir los mismos pasos a continuacíon para cualquier tipo de contribución.

!!! Info
    Tenga en cuenta que la guía esta pensada para ejecutarse sobre línea de comando, 
    pero puede realizar los mismos pasos con su herramienta favorita.

A continuación encuentra el paso a paso para contribuir a la documentación.

### Agregar una nuevo documento

Como caso práctico vamos a escribir un documento para la sección de 'Proceso'

!!! Tip
    Puedes seguir el mismo paso a paso para agregar un documento a una sección diferente, de acuerdo a su interés.

Cree una nueva rama con el prefijo de `doc/` ejemplo: `doc/cicd-process-for-mobile`

```
git checkout -b doc/cicd-process-for-mobile
```

Vaya a la carpeta de `/process` y cree un nuevo documento utilizando como base el template.

```
cp docs/template.md docs/process && cd docs/process
```

Ahora renombre el archivo con el título del documento en pocas palabras (no más de 4)

```
mv template.md cicd-process-mobile.md
```

Luego, abrir el archivo `cicd-process-mobile.md` en su editor de código y reemplazar los meta-datos del documento, ejemplo:

```
---
title: CI-CD Mobile
author: Santiago Villegas <santiago.villegas@pragma.com.co>
contributors: Juanito Pérez
---
```

Ahora en el sitio local [http://localhost:8000](http://localhost:8000) deberías ver en la sección de 'Proceso'
un nuevo item con el título en el menú secundario ubicado al costado izquierdo de la página.

En este punto puedes escribir en el archivo toda la documentación que veas relevante, 

!!! Tip
    Mientras escribe el documento puede ir pre-visualizando en el sitio http://localhost:8000

Una vez completado y en buena forma, debes enviar tus cambios al repositorio para una posterior publicación.

Ejecute los comandos a continuación:

Agregue el nuevo archivo, reemplazar `FILE_NAME` por `cicd-process-mobile.md`

```
git add FILE_NAME
```

Confirmar los cambios
```
git commit -m "Add doc ci-cd for mobile" 
```

Enviar los cambios en la rama al repositorio central en Bitbucket
```
git push origin doc/cicd-process-for-mobile
```

[Vaya a Bitbucket en el repositorio de la documentación](https://pragmatranser.visualstudio.com/Transer/_git/transer-wiki/pullrequests?_a=mine) 
y cree un nuevo Pull Request de su respectiva rama a master, recuerde agregar a uno de sus compañeros como revisor.

!!! Info
    En ocasiones no es necesario agregar un revisor, por ejemplo, cuando esta realizando correcciones que usted mismo rectifica.

Espere a que el PR fuese revisado y una vez aprobado por el equipo de DevOps puede hacer merge.

!Felicitaciones has publicado tu primer documento! :cowboy:

### Agregar una nueva sección principal

Como caso práctico de ejemplo vamos a crear una nueva sección llamada 'Onboarding', 
Recuerda que puedes crear una sección diferente a la de esta guía.

!!! Note
    Solo puede agregar secciones principales con la aprobación del equipo de DevOps vía PR.

Cree una nueva rama con el prefijo de `doc/` ejemplo, `doc/new-section-onboarding`

```
git checkout -b doc/new-section-onboarding
```

Ahora, desde el directorio raíz del proyecto vaya a crear una nueva caperta
```
mkdir docs/onboarding
```

Y agregue un documento overview en la carpeta `docs/onboarding`

```sh
cp docs/template.md docs/onboarding/overview.md && cd docs/onboarding
```

Luego agregue un nuevo item al menú principal en el archivo `.pages`
```
echo '\n    - Onboarding: onboarding' >> ../.pages
```

!!! Tip
    El archivo .pages contiene la definición de los items del menú principal, una vez agregué un nuevo item
    y su carpeta, MKDocs actualiza el menú y sub-menú con sus respectivas páginas .md como items.

Ahora para comprobar que la nueva sección aparece en el menú principal y redirige a la página de overview.
Vaya al sitio local [http://localhost:8000](http://localhost:8000) 

Luego de verificar que la sección se agregó correctamente, y enviar tus cambios al repositorio para una posterior publicación.

Ejecute los comandos a continuación:

Agregue el nuevo archivo, reemplazar `FILE_NAME` por `overview.md`

```
git add FILE_NAME
```

```
git commit -m "Add new section Onboarding" 
```

```
git push origin doc/new-section-onboarding
```

[Vaya a Azure Repos en el repositorio de la documentación](https://pragmatranser.visualstudio.com/Transer/_git/transer-wiki/pullrequests?_a=mine) 
y cree un nuevo Pull Request de su respectiva rama a master, recuerde agregar a uno de sus compañeros como revisor.

Espere a que el PR fuese revisado y una vez aprobado por el equipo de DevOps puede hacer merge.

!Felicitaciones has publicado tu primer sección principal! :cowboy: