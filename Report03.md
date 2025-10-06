@4723113 ➜ /workspaces/WE-Docker (main) $ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                         NAMES
c520196f20a5   postgres:15    "docker-entrypoint.s…"   16 seconds ago   Up 15 seconds   5432/tcp                                      we-docker-db-1
7e9bc83469c9   c8504c232276   "uvicorn main:app --…"   44 minutes ago   Up 44 minutes   0.0.0.0:8000->8000/tcp, [::]:8000->8000/tcp   my-fastapi-container