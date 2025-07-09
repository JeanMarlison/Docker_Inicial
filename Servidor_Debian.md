# 📘 Curso de Servidor Debian: Do Básico ao Avançado

Este curso foi cuidadosamente elaborado para fornecer uma compreensão aprofundada da administração de servidores Debian, desde os conceitos fundamentais até tópicos avançados de segurança, automação e virtualização.  
Se você busca dominar a arte de gerenciar sistemas Linux estáveis e seguros, este é o lugar certo.

---

## 📚 Conteúdo Programático

O curso está dividido em **quatro módulos principais**, com complexidade crescente:

---

### 🧱 Módulo 1: Fundamentos do Debian e Linux

#### 🧭 Introdução ao Linux e Software Livre

- Filosofia do Software Livre
- Instalação do Debian (particionamento com LVM, configuração inicial)

#### 🖥️ Primeiros Passos no Terminal

```bash
# Navegação
ls -l       # Lista com detalhes
ls -a       # Lista arquivos ocultos
cd ..       # Volta um diretório
cd ~        # Vai para o home
pwd         # Mostra o caminho atual

# Manipulação de Arquivos
cp arquivo.txt /tmp/
cp -r pasta/ /backup/
mv nome.txt novo_nome.txt
rm arquivo.txt
rm -rf pasta/
mkdir novo_diretorio
```

#### 📦 Gerenciamento de Pacotes com APT

```bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove htop
apt search firewall
```

#### 🔐 Permissões de Arquivos

```bash
chmod 755 script.sh
chmod +x script.sh
sudo chown usuario:grupo arquivo.txt
```

#### 👥 Gerenciamento de Usuários e Grupos

```bash
sudo useradd -m joao
sudo passwd joao
sudo usermod -aG sudo joao
```

---

### 🧰 Módulo 2: Administração de Sistema

#### ⚙️ Processos e Serviços (systemd)

```bash
ps aux | grep nginx
top
htop
kill 12345
sudo systemctl start apache2
sudo systemctl stop apache2
sudo systemctl restart apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

#### 💽 Gerenciamento de Discos e Sistemas de Arquivos

```bash
df -h
du -sh /var/log
lsblk
```

#### ⏰ Agendamento de Tarefas com Cron

```bash
crontab -e
# Exemplo:
# 0 2 * * * apt update && apt upgrade -y
```

#### 📊 Monitoramento de Recursos

```bash
free -h
```

#### 🌐 Rede Básica

```bash
ip a
ping google.com
ss -tunl
```

#### 💾 Backup e Restauração

```bash
rsync -avz /var/www/ /mnt/backup/web/
tar -czvf backup.tar.gz /home/usuario/
```

---

### 🔐 Módulo 3: Segurança e Serviços Essenciais

#### 🔒 Segurança do Servidor

- Boas práticas
- SSH Hardening

#### 🔥 Firewall (UFW/Iptables)

```bash
sudo ufw enable
sudo ufw allow 22/tcp
sudo ufw status
```

#### 🔑 Servidor SSH com Autenticação por Chave

```bash
ssh-keygen -t rsa -b 4096
ssh-copy-id usuario@IP_DO_SERVIDOR
```

#### 🌐 Servidor Web (Apache/Nginx)

```bash
sudo apt install apache2
sudo apt install nginx
```

#### 🛢️ Banco de Dados (MariaDB/PostgreSQL)

```bash
sudo apt install mariadb-server
```

#### 📂 Compartilhamento de Arquivos (Samba/NFS)

```bash
sudo apt install samba
```

---

### 🚀 Módulo 4: Tópicos Avançados e Automação

#### 🧩 Virtualização (KVM/QEMU)

```bash
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
```

#### 📦 Contêineres com Docker

```bash
# Instalação (resumida)
sudo apt update
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl status docker
```

```bash
# Comandos Docker
docker run hello-world
docker ps
docker images
```

#### 🧠 Automação com Shell Script

```bash
#!/bin/bash
echo "Olá do meu script Debian!"
df -h
```

#### ⚙️ Ferramentas de Gerenciamento (Ansible, Puppet, Chef)

```bash
sudo apt install ansible
```

#### 📈 Monitoramento Avançado

- Conceitos de Prometheus e Grafana

#### 🧪 Troubleshooting Avançado

---

## 🎓 Metodologia de Ensino

- Aulas expositivas com demonstrações práticas
- Laboratórios em ambiente virtual
- Estudos de caso e desafios
- Material de apoio (roteiros, scripts, documentação)
- Suporte via fórum e canais de discussão

---

## ✅ Pré-requisitos

- Conhecimentos básicos de linha de comando
- Uma máquina com suporte a virtualização (VirtualBox ou VMware)
- Vontade de aprender e colocar a mão na massa 💪

---

## 📎 Licença

Este material é de uso educacional. Sinta-se livre para estudar, adaptar e compartilhar com colegas.  
Créditos ao autor original do curso.

---
