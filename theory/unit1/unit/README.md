# LECTURE THEORY

##### Name: Pallavi Singh
##### Sap Id: 500119176
##### Batch: 02 [CCVT]
##### Roll Number: R2142230249

---
# Docker Commands & Flags – HandsOn Notes
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




# Preserving Changes Inside a Docker Container (Java Lab)

## Objective

Install Java inside a container, create an app, then convert the container into a reusable image for sharing and reuse.

We will learn:

- Container → Image conversion
- Save / Load images
- Export / Import difference
- Best practices

---

## Scenario Overview

You will:

1. Start Ubuntu container
2. Install Java compiler
3. Create Java app in `/home/app`
4. Convert container → image
5. Reuse & share image

---

## 1. Run Base Ubuntu Container

```bash
docker run -it --name java_lab ubuntu:22.04 bash
```
You are now inside the container.

---

## 2. Install Java Compiler (Inside Container)

```bash
apt update
apt install -y openjdk-17-jdk
```

Verify installation:

```bash
javac --version
```
![Uploading Screenshot 2026-02-06 at 12.01.07 PM.png…]()
<img width="1440" height="854" alt="Screenshot 2026-02-06 at 12 04 58 PM" src="https://github.com/user-attachments/assets/d82b4c37-c1cb-45d5-a729-fd86c71ebbc6" />
<img width="1436" height="868" alt="Screenshot 2026-02-06 at 12 05 09 PM" src="https://github.com/user-attachments/assets/b8388bc0-0c75-4770-8bb5-d7cfa8ab8e55" />
<img width="1439" height="829" alt="Screenshot 2026-02-06 at 12 05 17 PM" src="https://github.com/user-attachments/assets/20706514-1af0-4627-832d-cc0169a2bd9b" />
<img width="1440" height="869" alt="Screenshot 2026-02-06 at 12 05 39 PM" src="https://github.com/user-attachments/assets/990c7655-e8f0-489f-86dd-cb7b2a92b93b" />
<img width="1440" height="837" alt="Screenshot 2026-02-06 at 12 07 22 PM" src="https://github.com/user-attachments/assets/08a4a6a8-9470-4c06-a37e-47d73f7ae9f9" />

---

## 3. Create Java App in /home/app

```bash
mkdir -p /home/app
cd /home/app
nano Hello.java
```
<img width="493" height="43" alt="Screenshot 2026-02-06 at 12 15 10 PM" src="https://github.com/user-attachments/assets/112cb312-c997-4658-85da-423dee2ab00c" />
<img width="513" height="145" alt="Screenshot 2026-02-06 at 12 15 18 PM" src="https://github.com/user-attachments/assets/c1410e39-b9f6-4cb8-beb0-fbc572326f02" />


Java code:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello from Docker container!");
    }
}
```
<img width="746" height="450" alt="Screenshot 2026-02-06 at 12 15 50 PM" src="https://github.com/user-attachments/assets/c392e09f-2ea5-4ade-9222-bd55939a3ca6" />

Compile and run:

```bash
javac Hello.java
java Hello
```
<img width="440" height="42" alt="Screenshot 2026-02-06 at 12 16 53 PM" src="https://github.com/user-attachments/assets/df0918c3-3c6b-45aa-b8f5-28bb59edb4ff" />

Now the container contains:

- Java installed
- Java source file
- Compiled program
---

## 4. Exit Container

```bash
exit
```
<img width="486" height="165" alt="Screenshot 2026-02-06 at 12 15 23 PM" src="https://github.com/user-attachments/assets/1945eceb-6156-47b7-9e66-8c3279c5d69d" />

Container stops, but changes remain saved in that container.

---

## 5. Convert Container → Image

This captures the container snapshot.

```bash
docker commit java_lab myrepo/java-app:1.0
```
<img width="567" height="115" alt="Screenshot 2026-02-06 at 12 18 18 PM" src="https://github.com/user-attachments/assets/dee2837c-fe7f-4e13-91dd-c45d0156fbaa" />

Verify:

```bash
docker images
```
<img width="563" height="183" alt="Screenshot 2026-02-06 at 12 18 38 PM" src="https://github.com/user-attachments/assets/0382ab4d-24cb-4bbb-8ee1-75d6e8e7c9de" />

A new reusable image now exists.

---

## 6. Reuse the Image

```bash
docker run -it myrepo/java-app:1.0 bash
```
Test:

```bash
cd /home/app
java Hello
```
<img width="558" height="127" alt="Screenshot 2026-02-06 at 12 19 53 PM" src="https://github.com/user-attachments/assets/f7711224-cb9b-446c-a15d-dbba1907fea0" />

Java and program already exist 🎉

---

## 7. Save / Load (Offline Transfer)

### Save image to file

```bash
docker save -o java-app.tar myrepo/java-app:1.0
```
<img width="564" height="32" alt="Screenshot 2026-02-06 at 12 22 06 PM" src="https://github.com/user-attachments/assets/a35b019c-b044-4955-8b8e-f5baceb3c5cf" />

Transfer the `.tar` file anywhere.

### Load image

```bash

<img width="546" height="48" alt="Screenshot 2026-02-06 at 12 22 16 PM" src="https://github.com/user-attachments/assets/b7ba5030-df5a-46bc-83da-878ff3af67ed" />

docker load -i java-app.tar
```

Check:

```bash
docker images
```
<img width="566" height="175" alt="Screenshot 2026-02-06 at 12 23 00 PM" src="https://github.com/user-attachments/assets/3133bb97-51c8-475e-99d1-62df7e2e14f6" />


---

## Export vs Save (Important Difference)

### docker export

```bash
docker export java_lab > container.tar
```

Exports raw filesystem only.

You lose:

- image name
- layers
- metadata
- CMD / ENTRYPOINT
<img width="567" height="73" alt="Screenshot 2026-02-06 at 12 24 33 PM" src="https://github.com/user-attachments/assets/30d8e759-5101-4bc2-91c4-9c466727b6d2" />

---

### docker save (Recommended)

```bash
docker save -o image.tar myrepo/java-app:1.0
```
<img width="565" height="186" alt="Screenshot 2026-02-06 at 12 26 17 PM" src="https://github.com/user-attachments/assets/6d0b32d9-9f66-4eaa-b0d6-b4133f473fa1" />

Keeps full image structure.

---

## Command Summary

| Command | Purpose |
|---------|---------|
| docker commit | Container → Image |
| docker save | Image → File |
| docker load | File → Image |
| docker push/pull | Registry sharing |
| docker export/import | Raw filesystem only |

---

## Best Practice (Real Projects)

Use Dockerfile instead of commit:

```Dockerfile
FROM ubuntu:22.04
RUN apt update && apt install -y openjdk-17-jdk
WORKDIR /home/app
COPY Hello.java .
RUN javac Hello.java
CMD ["java", "Hello"]
```

Build image:

```bash
docker build -t java-app:2.0 .
```
<img width="1354" height="876" alt="Screenshot 2026-02-06 at 12 30 19 PM" src="https://github.com/user-attachments/assets/5351b98d-e819-4b46-a686-deb4e096643f" />
<img width="1321" height="197" alt="Screenshot 2026-02-06 at 12 30 26 PM" src="https://github.com/user-attachments/assets/4b1f1c3a-37d5-46f2-8f99-5f86c061c7c4" />

---

# ASSIGNMENT
## Create a director for C and then make an image and a iontainer on Docker using GCC form Docker Hub.
<img width="863" height="872" alt="Screenshot 2026-02-06 at 12 56 20 PM" src="https://github.com/user-attachments/assets/2aa0a2ab-ccd7-4d3c-aaec-4703a0244f7c" />
<img width="893" height="282" alt="Screenshot 2026-02-06 at 12 56 32 PM" src="https://github.com/user-attachments/assets/264c55dd-ec34-4727-bce5-3170b1146c4f" />
<img width="955" height="42" alt="Screenshot 2026-02-06 at 12 57 15 PM" src="https://github.com/user-attachments/assets/a4cc0de4-f5b5-4a95-baad-995039e9a7ac" />
<img width="938" height="40" alt="Screenshot 2026-02-06 at 12 57 30 PM" src="https://github.com/user-attachments/assets/5bf248e5-8151-40ba-acdb-6a112679a8f9" />

---


