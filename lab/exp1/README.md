# Experiment 1 – VM vs Container Setup on macOS

## Aim
To install and configure virtualization and container tools on macOS, deploy an Ubuntu-based Nginx server using a Virtual Machine and Docker container, and observe the behavior of both environments.

---

## Procedure

### Installing Tools on macOS

1. Install Homebrew (package manager)

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

```

Verify:

```
brew --version
```

2. Install Docker Desktop

Download and install Docker Desktop for Mac.

<img width="1225" height="788" alt="Screenshot 2026-02-02 at 1 49 03 AM" src="https://github.com/user-attachments/assets/7f69d505-ec56-4feb-ad63-9535ea5b6963" />
<img width="1018" height="401" alt="Screenshot 2026-02-02 at 1 49 19 AM" src="https://github.com/user-attachments/assets/e72e4649-5d3f-4794-87ca-619fc507b89c" />
<img width="1261" height="705" alt="Screenshot 2026-02-02 at 1 50 01 AM" src="https://github.com/user-attachments/assets/05b1dd0d-0ed0-443c-8d9f-85a5fbd327ec" />

Verify:

```
docker --version
```

3. Install QEMU (for Apple Silicon virtualization)

```
brew install qemu
qemu-system-aarch64 --version
```

4. Install Vagrant

```
brew install --cask vagrant
vagrant --version
```

5. Install QEMU provider for Vagrant

```
vagrant plugin install vagrant-qemu
```

---

### Virtual Machine using Vagrant (QEMU)

1. Create VM directory

```
mkdir vm-lab
cd vm-lab
```

2. Initialize Ubuntu box

```
vagrant init ubuntu/jammy64
```

3. Edit Vagrantfile and add:

```
config.vm.provider "qemu" do |q|
  q.arch = "aarch64"
  q.memory = 2048
  q.cpus = 2
end
```

4. Start VM

```
vagrant up --provider=qemu
vagrant ssh
```

5. Install Nginx inside VM

```
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
curl localhost
```

6. Stop VM

```
vagrant halt
vagrant destroy
```

7. Install UTM (Virtual Machine for macOS)

Download and install UTM from the official website.

Steps inside UTM:

- Open UTM
- Create New → Virtualize → Linux
- Select Ubuntu ISO image
- Allocate memory and storage
- Start the virtual machine
<img width="781" height="624" alt="Screenshot 2026-02-02 at 2 02 00 AM" src="https://github.com/user-attachments/assets/3c817b2d-09fe-4a19-8a56-f8492adb37b2" />
<img width="1269" height="766" alt="Screenshot 2026-02-02 at 2 02 53 AM" src="https://github.com/user-attachments/assets/fec0380b-4b69-404a-b952-c00934cae8c4" />
<img width="1255" height="778" alt="Screenshot 2026-02-02 at 2 03 05 AM" src="https://github.com/user-attachments/assets/bd8b5bf0-e556-44c5-8a1c-ae2f1680ac0b" />


---

### Container using Docker

1. Pull Nginx image

```
docker pull nginx
```

2. Run container

```
docker run -d -p 8080:80 --name nginx-container nginx
```

3. Verify

```
curl localhost:8080
```

---

## Screenshot
<img width="1439" height="874" alt="Screenshot 2026-02-02 at 1 37 05 AM" src="https://github.com/user-attachments/assets/d62f5f96-872b-48e5-ab84-614005b025cb" />
<img width="1440" height="855" alt="Screenshot 2026-02-02 at 1 37 19 AM" src="https://github.com/user-attachments/assets/ac65bc7a-65ba-4e9e-abd7-7684f2ca032c" />
<img width="1440" height="872" alt="Screenshot 2026-02-02 at 1 37 30 AM" src="https://github.com/user-attachments/assets/e63915e0-7f33-479d-bac8-df956bbed355" />
<img width="1437" height="870" alt="Screenshot 2026-02-02 at 1 37 55 AM" src="https://github.com/user-attachments/assets/307d6992-f8cd-4aaa-a87b-f387681e2264" />
<img width="1440" height="871" alt="Screenshot 2026-02-02 at 1 38 05 AM" src="https://github.com/user-attachments/assets/45e497dc-a128-4d65-8634-cc3b19c53c5c" />
<img width="1440" height="873" alt="Screenshot 2026-02-02 at 1 38 15 AM" src="https://github.com/user-attachments/assets/7e80cb85-b446-47fb-98c4-805db28f69e4" />
<img width="1440" height="870" alt="Screenshot 2026-02-02 at 1 39 54 AM" src="https://github.com/user-attachments/assets/bd10b09e-142c-451d-9648-ddf9e90e6e69" />
<img width="1440" height="868" alt="Screenshot 2026-02-02 at 1 40 02 AM" src="https://github.com/user-attachments/assets/d965d216-bf12-496b-bd07-2efaeaf1f100" />
