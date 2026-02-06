# LECTURE THEORY

## 1. Docker Basics

### Check Docker version
```bash
docker version
```
Shows client + server version and confirms Docker daemon connectivity.
<img width="1439" height="534" alt="Screenshot 2026-02-06 at 11 06 41 AM" src="https://github.com/user-attachments/assets/dfe58166-f974-4730-921b-0393d7abe953" />

### System information
```bash
docker info
```
Displays system-wide Docker info:
- storage driver
- cgroups
- images
- containers
<img width="1439" height="534" alt="Screenshot 2026-02-06 at 11 06 41 AM" src="https://github.com/user-attachments/assets/418ab45e-44bf-49e0-8f6c-355cb3708b2c" />

---

## 2. Image Management

### List local images
```bash
docker images
```
<img width="562" height="228" alt="Screenshot 2026-02-06 at 11 18 08 AM" src="https://github.com/user-attachments/assets/2dd592cd-22f3-4056-b02b-87488d3c6f36" />

Flags:
- `-a` → show all images (including intermediate layers)
- `-q` → only image IDs

---

### Pull image from registry
```bash
docker pull ubuntu
docker pull ubuntu:22.04
```
<img width="568" height="283" alt="Screenshot 2026-02-06 at 11 19 01 AM" src="https://github.com/user-attachments/assets/f294f2e4-5606-4d77-a1fd-0381ac348525" />

Downloads image from Docker Hub.  
`:tag` specifies version.

---

### Remove image

```bash
docker rmi ubuntu
```

Flags:
- `-f` → force removal
- `-a` → remove all unused images
<img width="566" height="329" alt="Screenshot 2026-02-06 at 11 44 19 AM" src="https://github.com/user-attachments/assets/8bc595ca-7f82-40f7-81c3-049b9e79d785" />

---

## 3. Container Lifecycle

### Run a container
```bash
docker run ubuntu
```
<img width="569" height="113" alt="Screenshot 2026-02-06 at 11 45 07 AM" src="https://github.com/user-attachments/assets/095ffd70-8d3d-436d-b996-18cb47a4316b" />

Common flags:
- `-it` → interactive + terminal
- `--name mycontainer` → custom container name
- `-d` → detached (background)
- `--rm` → auto-remove after exit

Example:
```bash
docker run -it --name test ubuntu bash
```

---

### List containers
```bash
docker ps
```

Flags:
- `-a` → all containers
- `-q` → only container IDs
<img width="568" height="114" alt="Screenshot 2026-02-06 at 11 45 31 AM" src="https://github.com/user-attachments/assets/6f16fe85-6ddd-45db-b9f8-54b9fd03f826" />

---

### Start / Stop / Restart
```bash
docker start container_name
docker stop container_name
docker restart container_name
```

---

### Remove container
```bash
docker rm container_name
```

Flags:
- `-f` → force remove
- prune all stopped:
```bash
docker container prune
```

---

## 4. Execute Commands Inside Containers

### Attach terminal
```bash
docker attach container_name
```

### Execute command
```bash
docker exec -it container_name bash
```

Flags:
- `-i` → interactive
- `-t` → terminal

---

## 5. Networking & Ports

### Port mapping
```bash
docker run -d -p 8080:80 nginx
```

Explanation:
- host port → 8080
- container port → 80

Flags:
- `-p host:container`
- `-P` → random host ports
<img width="566" height="133" alt="Screenshot 2026-02-06 at 11 48 20 AM" src="https://github.com/user-attachments/assets/7b84e00a-73af-46aa-bb5d-6ace4b001cd2" />

---

### List networks
```bash
docker network ls
```
<img width="510" height="127" alt="Screenshot 2026-02-06 at 11 48 41 AM" src="https://github.com/user-attachments/assets/09d6c054-2a63-47f2-81f4-1642f44856ea" />

### Create network
```bash
docker network create mynet
```
<img width="538" height="49" alt="Screenshot 2026-02-06 at 11 49 00 AM" src="https://github.com/user-attachments/assets/2301d0f0-686a-471a-8c14-072df502dc14" />

Attach container:
```bash
docker run -d --network=mynet nginx
```

---


## 6. Volumes & Data Persistence

### Create volume
```bash
docker volume create mydata
```
<img width="535" height="48" alt="Screenshot 2026-02-06 at 11 49 28 AM" src="https://github.com/user-attachments/assets/089531f8-3b13-497a-a962-0142e2f04963" />
### Mount volume
```bash
docker run -v mydata:/data ubuntu
```

Bind mount:
```bash
docker run -v /host/path:/container/path ubuntu
```

Read-only:
```bash
docker run -v mydata:/data:ro ubuntu
```
<img width="571" height="143" alt="Screenshot 2026-02-06 at 11 50 06 AM" src="https://github.com/user-attachments/assets/d1fd301e-a1d1-41ee-ae2a-b52f5198061d" />

---

## 7. Logs & Monitoring

### View logs
```bash
docker logs container_name
```

Flags:
- `-f` → follow live logs
- `--tail 50`
- `--since 10m`
<img width="541" height="35" alt="Screenshot 2026-02-06 at 11 50 29 AM" src="https://github.com/user-attachments/assets/247e39fd-a900-42a9-9fc0-eff28b839cb1" />
---

### Resource usage
```bash
docker stats
```

Shows:
- CPU
- Memory
- Network I/O
- Disk I/O
<img width="568" height="217" alt="Screenshot 2026-02-06 at 11 51 02 AM" src="https://github.com/user-attachments/assets/599c4aa6-2c56-48ad-8457-3ac08076a378" />

---

## 8. Inspect & Metadata

### Inspect container
```bash
docker inspect container_name
```

Returns JSON with:
- IP address
- mounts
- environment variables
- network config

---

## 9. Docker Build (Images)

### Build image
```bash
docker build -t myapp .
```

Flags:
- `-t` → tag image
- `-f Dockerfile.dev`
- `--no-cache`

---

### Example Dockerfile

```Dockerfile
FROM ubuntu:22.04
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

---

## 10. Cleanup Commands

Remove unused containers:
```bash
docker container prune
```

Remove unused images:
```bash
docker image prune
```

Remove everything unused:
```bash
docker system prune
```

Flags:
- `-a`
- `--volumes`
<img width="1025" height="796" alt="Screenshot 2026-02-06 at 11 08 07 AM" src="https://github.com/user-attachments/assets/8a803169-0041-40c3-942b-9c197bb536c6" />

---

## 11. Docker Compose (Overview)

Start services:
```bash
docker compose up
```

Flags:
- `-d`
- `--build`

Stop services:
```bash
docker compose down
```

---

## 12. Important Run Flags (Quick Reference)

| Flag | Meaning |
|------|---------|
| -it | Interactive terminal |
| -d | Detached mode |
| --rm | Auto-remove |
| --name | Container name |
| -p | Port mapping |
| -v | Volume mount |
| -e | Environment variable |
| --network | Custom network |
| --restart=always | Auto restart |

---

## 13. Minimal Lab Example (Ubuntu + Nginx)

```bash
docker pull nginx
docker run -d --name web -p 8080:80 nginx
docker ps
docker logs web
docker stop web
docker rm web
```
<img width="1439" height="432" alt="Screenshot 2026-02-06 at 11 09 40 AM" src="https://github.com/user-attachments/assets/4124f45c-6fa9-4823-ba6a-70923460b0b2" />

---
->By:
Pallavi Singh

