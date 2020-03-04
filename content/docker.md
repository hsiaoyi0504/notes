# Docker

## FAQ

- Enter detached container (for example, a development server)

  ``` shell

    docker run -d -p 8888:8888 python:3.5 python -m http.server 8888 --name python_http
    docker exec -it python_http /bin/bash
  
  ```

- Mount the data to the container

  `docker run -ti -v "$PWD":/work_dir ubuntu:14.04 /bin/bash`

- Remove the <none> images

  `docker images -f "dangling=true" -q`

- Rename the image
  ``` shell

    docker tag <old_name> <new_name>
    docker rmi <old_name>

  ```
