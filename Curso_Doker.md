# 🚀 Curso de Docker: Do Básico à Orquestração

Bem-vindo ao repositório de estudo do curso de Docker! Este guia foi criado para acompanhar sua jornada de aprendizado, cobrindo desde os fundamentos dos containers até a orquestração com Docker Compose, Docker Swarm e uma introdução ao Kubernetes.

O conteúdo deste curso segue a grade apresentada no mapa mental, garantindo uma progressão lógica e abrangente.

## 🗺️ Estrutura do Curso

Abaixo está a estrutura do curso, com os principais tópicos e exemplos de comandos para cada fase.

---

### 1. Introdução

Nesta seção, você entenderá o que é Docker, por que ele é revolucionário para o desenvolvimento de software e quais são os conceitos fundamentais como imagens, containers e Docker Hub.

* **O que aprender:**
    * Definição e importância do Docker.
    * Diferença entre VMs e Containers.
    * Componentes da arquitetura Docker.
    * Conceitos de Imagem, Container e Volume.

* **Comandos Essenciais (Exemplos):**

    * **Verificar a instalação do Docker:**
        ```bash
        docker --version
        docker info
        ```

    * **Executar seu primeiro container "Hello World":**
        ```bash
        docker run hello-world
        ```
        *Este comando baixa a imagem `hello-world` do Docker Hub (se não tiver localmente) e executa um container que imprime uma mensagem de saudação.*

---

### 2. Trabalhando com Containers

Aqui, você aprenderá a gerenciar o ciclo de vida dos containers, desde a execução até a remoção.

* **O que aprender:**
    * Comandos para iniciar, parar, reiniciar e remover containers.
    * Execução de containers em segundo plano (detached mode).
    * Mapeamento de portas entre o host e o container.

* **Comandos Essenciais (Exemplos):**

    * **Executar um container Nginx em segundo plano, mapeando a porta 80 do container para a porta 8080 do host:**
        ```bash
        docker run -d -p 8080:80 --name meu-nginx nginx:latest
        ```
        * `-d`: detached mode (executa em segundo plano).
        * `-p 8080:80`: mapeia a porta 8080 do host para a porta 80 do container.
        * `--name meu-nginx`: atribui um nome amigável ao container.
        * `nginx:latest`: imagem a ser utilizada.
        *Após a execução, acesse `http://localhost:8080` no seu navegador.*

    * **Listar containers em execução:**
        ```bash
        docker ps
        ```

    * **Listar todos os containers (incluindo parados):**
        ```bash
        docker ps -a
        ```

    * **Parar um container (pelo nome ou ID):**
        ```bash
        docker stop meu-nginx
        ```

    * **Iniciar um container parado:**
        ```bash
        docker start meu-nginx
        ```

    * **Reiniciar um container:**
        ```bash
        docker restart meu-nginx
        ```

    * **Remover um container (deve estar parado):**
        ```bash
        docker rm meu-nginx
        ```
        *Para remover um container em execução, use `docker rm -f meu-nginx` (forçado).*

    * **Visualizar os logs de um container:**
        ```bash
        docker logs meu-nginx
        ```

    * **Acessar o terminal de um container em execução (interativo):**
        ```bash
        docker exec -it meu-nginx bash
        # Você estará dentro do container. Digite 'exit' para sair.
        ```
        * `-it`: modo interativo e pseudo-TTY.

---

### 3. Imagens e Avançando em Containers

Esta seção aborda a criação de imagens personalizadas usando Dockerfiles e o gerenciamento de imagens.

* **O que aprender:**
    * Estrutura e instruções de um Dockerfile (`FROM`, `RUN`, `COPY`, `CMD`, `EXPOSE`, etc.).
    * Processo de construção de imagens (`docker build`).
    * Publicação de imagens no Docker Hub (`docker push`).
    * Melhores práticas para otimização de imagens.

* **Comandos Essenciais (Exemplos):**

    * **Exemplo de um Dockerfile simples (ex: `Dockerfile` na raiz do seu projeto):**
        ```dockerfile
        # Use uma imagem base do Node.js
        FROM node:18-alpine

        # Crie um diretório de trabalho
        WORKDIR /app

        # Copie os arquivos de dependência e instale-os
        COPY package*.json ./
        RUN npm install

        # Copie o restante da aplicação
        COPY . .

        # Exponha a porta que a aplicação vai usar
        EXPOSE 3000

        # Comando para iniciar a aplicação
        CMD ["node", "app.js"]
        ```

    * **Construir uma imagem a partir de um Dockerfile (na pasta onde o Dockerfile está):**
        ```bash
        docker build -t minha-app-node:1.0 .
        ```
        * `-t minha-app-node:1.0`: nome e tag da imagem.
        * `.`: contexto da construção (diretório atual).

    * **Listar imagens locais:**
        ```bash
        docker images
        ```

    * **Remover uma imagem (deve não estar em uso por containers):**
        ```bash
        docker rmi minha-app-node:1.0
        ```

    * **Fazer login no Docker Hub:**
        ```bash
        docker login
        # Digite seu usuário e senha do Docker Hub
        ```

    * **Publicar uma imagem no Docker Hub (primeiro, tag com seu usuário):**
        ```bash
        docker tag minha-app-node:1.0 seu_usuario/minha-app-node:1.0
        docker push seu_usuario/minha-app-node:1.0
        ```
        *Substitua `seu_usuario` pelo seu nome de usuário do Docker Hub.*

---

### 4. Introduzindo Volumes aos Containers

Aprenda a persistir dados em containers, garantindo que suas informações não sejam perdidas ao reiniciar ou remover containers.

* **O que aprender:**
    * Necessidade de persistência de dados.
    * Tipos de volumes: Bind Mounts e Named Volumes.
    * Gerenciamento de volumes.

* **Comandos Essenciais (Exemplos):**

    * **Criar um container Nginx com um Bind Mount (compartilhando uma pasta local com o container):**
        ```bash
        mkdir -p /caminho/para/seu/html # Crie esta pasta e coloque um index.html dentro
        docker run -d -p 8081:80 --name meu-nginx-com-volume -v /caminho/para/seu/html:/usr/share/nginx/html nginx:latest
        ```
        * `-v /caminho/para/seu/html:/usr/share/nginx/html`: mapeia o diretório local para o diretório de arquivos do Nginx dentro do container.

    * **Criar um Named Volume:**
        ```bash
        docker volume create dados-app-db
        ```

    * **Usar um Named Volume em um container (ex: PostgreSQL):**
        ```bash
        docker run -d -p 5432:5432 --name meu-postgres -e POSTGRES_PASSWORD=mysecretpassword -v dados-app-db:/var/lib/postgresql/data postgres:latest
        ```
        * `-v dados-app-db:/var/lib/postgresql/data`: anexa o volume nomeado para persistir os dados do PostgreSQL.

    * **Listar volumes:**
        ```bash
        docker volume ls
        ```

    * **Remover um volume (deve não estar em uso):**
        ```bash
        docker volume rm dados-app-db
        ```

---

### 5. Conectando Containers em Networks

Entenda como containers podem se comunicar entre si de forma isolada e eficiente.

* **O que aprender:**
    * Tipos de redes Docker (bridge, host, none, overlay).
    * Criação de redes customizadas.
    * Conectividade entre containers na mesma rede.
    * Descoberta de serviço.

* **Comandos Essenciais (Exemplos):**

    * **Criar uma rede customizada:**
        ```bash
        docker network create minha-rede-app
        ```

    * **Rodar um container de banco de dados na rede customizada:**
        ```bash
        docker run -d --name meu-mongo --network minha-rede-app mongo:latest
        ```

    * **Rodar um container de aplicação na mesma rede, conectando-se ao banco de dados pelo nome do serviço:**
        ```bash
        # Supondo que você tenha um Dockerfile para sua aplicação Node.js que se conecta a 'meu-mongo'
        docker run -d -p 3000:3000 --name minha-app --network minha-rede-app minha-app-node:1.0
        ```
        *Dentro da sua aplicação, você se conectaria ao banco de dados usando o hostname `meu-mongo`.*

    * **Listar redes:**
        ```bash
        docker network ls
        ```

    * **Inspecionar uma rede (para ver os containers conectados):**
        ```bash
        docker network inspect minha-rede-app
        ```

    * **Remover uma rede (deve não ter containers conectados):**
        ```bash
        docker network rm minha-rede-app
        ```

---

### 6. Introdução ao YAML

Preparação para Docker Compose e Kubernetes, focando na sintaxe do YAML.

* **O que aprender:**
    * Sintaxe básica do YAML (indentação, listas, mapas).
    * Importância do YAML em arquivos de configuração Docker e Kubernetes.

* **Exemplo de estrutura YAML:**

    ```yaml
    # Exemplo de arquivo YAML
    servicos:
      web:
        imagem: nginx:latest
        portas:
          - "80:80"
      banco_dados:
        imagem: postgres:13
        ambiente:
          SENHA_DB: "minhasenha"
        volumes:
          - dados:/var/lib/postgresql/data

    volumes:
      dados: {}
    ```

---

### 7. Docker Compose

Orquestre múltiplos serviços Docker com um único arquivo de configuração (`docker-compose.yml`).

* **O que aprender:**
    * Estrutura de um `docker-compose.yml` (`services`, `volumes`, `networks`).
    * Comandos para gerenciar aplicações multi-container.

* **Comandos Essenciais (Exemplos):**

    * **Exemplo de `docker-compose.yml`:**
        ```yaml
        version: '3.8'

        services:
          web:
            build: . # Constrói a imagem a partir do Dockerfile no diretório atual
            ports:
              - "3000:3000"
            volumes:
              - .:/app # Mapeia o código-fonte para recarga automática em desenvolvimento
            depends_on:
              - db
            networks:
              - app-network

          db:
            image: mongo:latest
            volumes:
              - db-data:/data/db
            networks:
              - app-network

        volumes:
          db-data:

        networks:
          app-network:
            driver: bridge
        ```

    * **Iniciar todos os serviços definidos no `docker-compose.yml` (na pasta do arquivo):**
        ```bash
        docker-compose up -d
        ```
        * `-d`: executa em segundo plano.

    * **Parar e remover todos os serviços, redes e volumes criados pelo Compose:**
        ```bash
        docker-compose down
        ```

    * **Listar os serviços em execução gerenciados pelo Compose:**
        ```bash
        docker-compose ps
        ```

    * **Visualizar os logs de todos os serviços ou de um serviço específico:**
        ```bash
        docker-compose logs
        docker-compose logs web
        ```

    * **Executar um comando dentro de um serviço:**
        ```bash
        docker-compose exec web bash
        ```

---

### 8. Docker Swarm

Explore a orquestração de containers em cluster, ideal para produção em escala menor.

* **O que aprender:**
    * Conceitos de Swarm (manager, worker, service, task).
    * Inicialização e gerenciamento de um cluster Swarm.
    * Deploy e escalabilidade de serviços no Swarm.

* **Comandos Essenciais (Exemplos):**

    * **Inicializar um Swarm (no nó manager):**
        ```bash
        docker swarm init --advertise-addr <IP_DO_MANAGER>
        ```
        * `<IP_DO_MANAGER>`: Endereço IP da máquina que será o manager.

    * **Juntar um nó worker ao Swarm (no nó worker, usando o token gerado pelo `swarm init`):**
        ```bash
        docker swarm join --token <TOKEN> <IP_DO_MANAGER>:2377
        ```

    * **Listar os nós do Swarm (no manager):**
        ```bash
        docker node ls
        ```

    * **Deploy de um serviço no Swarm (usando a sintaxe de `docker-compose.yml` com `stack deploy`):**
        ```bash
        docker stack deploy -c docker-compose.yml minha-stack
        ```

    * **Listar serviços no Swarm:**
        ```bash
        docker service ls
        ```

    * **Escalar um serviço:**
        ```bash
        docker service scale minha-stack_web=3
        ```
        *Aumenta o número de réplicas do serviço `web` para 3.*

    * **Remover uma stack do Swarm:**
        ```bash
        docker stack rm minha-stack
        ```

---

### 9. Kubernetes

Introdução ao Kubernetes, o orquestrador de containers mais popular e robusto do mercado.

* **O que aprender:**
    * Arquitetura do Kubernetes (Master/Control Plane, Nodes).
    * Objetos essenciais: Pods, Deployments, Services, ConfigMaps, Secrets, Volumes.
    * YAML para Kubernetes e uso do `kubectl`.

* **Comandos Essenciais (Exemplos):**

    * **Instalar Minikube (Kubernetes local):**
        * Siga as instruções oficiais: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)

    * **Iniciar o Minikube:**
        ```bash
        minikube start
        ```

    * **Verificar o status do Minikube:**
        ```bash
        minikube status
        ```

    * **Exemplo de `pod.yaml`:**
        ```yaml
        apiVersion: v1
        kind: Pod
        metadata:
          name: meu-primeiro-pod
        spec:
          containers:
          - name: nginx-container
            image: nginx:latest
            ports:
            - containerPort: 80
        ```

    * **Aplicar um arquivo YAML no Kubernetes:**
        ```bash
        kubectl apply -f pod.yaml
        ```

    * **Listar Pods:**
        ```bash
        kubectl get pods
        ```

    * **Verificar logs de um Pod:**
        ```bash
        kubectl logs meu-primeiro-pod
        ```

    * **Remover um Pod:**
        ```bash
        kubectl delete -f pod.yaml
        # Ou:
        kubectl delete pod meu-primeiro-pod
        ```

    * **Exemplo de `deployment.yaml` (maneira mais comum de rodar apps):**
        ```yaml
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: nginx-deployment
        spec:
          replicas: 3 # Roda 3 instâncias do Pod
          selector:
            matchLabels:
              app: nginx
          template:
            metadata:
              labels:
                app: nginx
            spec:
              containers:
              - name: nginx
                image: nginx:latest
                ports:
                - containerPort: 80
        ```

    * **Aplicar um Deployment:**
        ```bash
        kubectl apply -f deployment.yaml
        ```

    * **Listar Deployments:**
        ```bash
        kubectl get deployments
        ```

    * **Exemplo de `service.yaml` (para expor o Deployment):**
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: nginx-service
        spec:
          selector:
            app: nginx
          ports:
            - protocol: TCP
              port: 80
              targetPort: 80
          type: NodePort # Ou LoadBalancer, ClusterIP
        ```

    * **Aplicar um Service:**
        ```bash
        kubectl apply -f service.yaml
        ```

    * **Listar Services:**
        ```bash
        kubectl get services
        ```

    * **Parar o Minikube:**
        ```bash
        minikube stop
        ```

---

### Extras: Terminal e Shell Essencial

A familiaridade com o terminal é crucial para trabalhar com Docker e outras ferramentas de linha de comando.

* **O que aprender:**
    * Comandos básicos de navegação, manipulação de arquivos e diretórios.
    * Redirecionamento de entrada/saída, pipes.
    * Variáveis de ambiente.

* **Comandos Essenciais (Exemplos):**

    * **Listar conteúdo de um diretório:**
        ```bash
        ls -l
        ```

    * **Navegar para um diretório:**
        ```bash
        cd meu_projeto
        ```

    * **Criar um diretório:**
        ```bash
        mkdir nova_pasta
        ```

    * **Criar um arquivo vazio:**
        ```bash
        touch meu_arquivo.txt
        ```

    * **Copiar um arquivo:**
        ```bash
        cp arquivo_origem.txt arquivo_destino.txt
        ```

    * **Mover/Renomear um arquivo:**
        ```bash
        mv arquivo_antigo.txt arquivo_novo.txt
        ```

    * **Remover um arquivo/diretório:**
        ```bash
        rm meu_arquivo.txt
        rm -rf meu_diretorio/ # Cuidado: remove recursivamente e força
        ```

---

### Atualizações!

O mundo do Docker e dos containers está em constante evolução. Mantenha-se atualizado!

* **O que fazer:**
    * Acompanhe as documentações oficiais do Docker e Kubernetes.
    * Siga blogs e comunidades relevantes.
    * Participe de fóruns e grupos de discussão.

---

## 🤝 Contribuição

Sinta-se à vontade para sugerir melhorias, correções ou adicionar mais exemplos. Sua contribuição é muito bem-vinda!

## 📜 Licença

Este projeto é de código aberto e está disponível sob a licença [MIT License](LICENSE).

---