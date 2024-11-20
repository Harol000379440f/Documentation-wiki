# Transer Technical Documentation

Wiki para documentar los aspectos tecnicos o de ingenieria relacionados a las areas de trabajo, aplicaciones o proyectos en transer.

## Quick Start

Requisitos: 

- [Docker](https://docs.docker.com/engine/install/)
- [Git](https://git-scm.com/downloads)

Clonar el proyecto desde el repositorio

```
git clone https://pragmatranser.visualstudio.com/Transer/_git/transer-wiki && cd transer-wiki/
```

Construir instantanea mkdocs-material para transer

```
docker build . -t mkdocs-transer
```

Inicialize un servidor para previsualizar la doc en el navegador (modo desarrollador)

```
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs mkdocs-transer
```

Ahora puede ver el en [http://localhost:8000](http://localhost:8000) 

El servidor auto-recarga el sitio web un vez que detecte cualquier cambio en los archivos fuentes. 

## ¿Como contribuir?

Puede empezar escribiendo archivos en formato markdown en la respectiva carpeta según el área de trabajo que se relaciona con el contenido de la documentación que desea agregar. Vaya a la [Guía de Contribución](./docs/contributing-guide.md)