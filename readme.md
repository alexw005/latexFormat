To simplify running texlive/texlive with Docker Compose, here’s a docker-compose.yml file. This file will allow you to run the LaTeX compilation with a single docker-compose up command.
docker-compose.yml

yaml

version: '3.8'

services:
  latex:
    image: texlive/texlive
    working_dir: /workdir
    volumes:
      - .:/workdir
    entrypoint: ["pdflatex", "yourfile.tex"]

Explanation

    version: '3.8': Specifies the version of Docker Compose syntax.
    services: Defines the latex service.
        image: Specifies the Docker image to use, in this case, texlive/texlive.
        working_dir: Sets the working directory inside the container.
        volumes: Mounts the current directory to /workdir inside the container, so the .tex files and output files are accessible from your local machine.
        entrypoint: Defines the command to run when the container starts. Replace yourfile.tex with the name of your .tex file.

Running the Docker Compose File

Once you have the docker-compose.yml file ready, navigate to its directory and run:

bash

`docker-compose up`

This will run pdflatex yourfile.tex in the texlive/texlive container. The compiled output (e.g., yourfile.pdf) will be saved in the same directory as your .tex file.
Customizing Commands

If you need to run other commands (e.g., xelatex, bibtex), modify the entrypoint line accordingly. You could also pass different commands using docker-compose run:

bash

`docker-compose run latex xelatex yourfile.tex`

This setup keeps the Docker Compose file flexible, allowing you to easily switch LaTeX engines or files.
