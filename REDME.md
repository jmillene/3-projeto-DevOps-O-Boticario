# 3º Projeto Prático - DevOps: Implementação de Microsserviços com Kubernetes (K8s) na AWS

## Estrutura de Diretórios

# Projeto de DevOps: Implementação de Microsserviços com Kubernetes na AWS (EKS)

Este projeto tem como objetivo demonstrar a implementação de microsserviços utilizando Kubernetes na AWS (EKS). Inclui a configuração de serviços com Nginx, a criação de Dockerfiles, a utilização de Docker Compose, e a configuração de monitoramento com Prometheus.

## Índice
1. [Pré-requisitos](#pré-requisitos)
2. [Estrutura do Projeto](#estrutura-do-projeto)
3. [Configuração do Docker](#configuração-do-docker)
4. [Configuração do Kubernetes](#configuração-do-kubernetes)
5. [Monitoramento com Prometheus](#monitoramento-com-prometheus)
6. [Automatização de Deployments](#automatização-de-deployments)
7. [Escalabilidade](#escalabilidade)
8. [Conclusão](#conclusão)

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes itens instalados e configurados:

- Docker
- Docker Compose
- kubectl
- Um cluster Kubernetes (Minikube ou AWS EKS)
- Acesso ao Docker Hub ou um registro Docker privado

## Estrutura do Projeto

A estrutura do projeto está organizada da seguinte maneira:

C:.
│   .gitignore
│   REDME.md
│
├───ecommerce-project
│   ├───.github
│   │   └───workflows
│   │           ci-cd-pipeline.yml
│   │
│   ├───order-service
│   │   │   docker-compose.yml
│   │   │   Dockerfile
│   │   │
│   │   ├───dist
│   │   │       healthz.html
│   │   │       index.html
│   │   │       readiness.html
│   │   │
│   │   ├───nginx
│   │   │       nginx.conf
│   │   │
│   │   └───src
│   └───product-service
│       │   docker-compose.yml
│       │   Dockerfile
│       │
│       ├───dist
│       │       healthz.html
│       │       index.html
│       │       readiness.html
│       │
│       ├───nginx
│       │       nginx.conf
│       │
│       └───src
└───kubernetes
        grafana-service.yml
        nginx-configmap.yml
        order-service-claim0-persistentvolumeclaim.yaml
        order-service-deployment.yaml
        order-service-hpa.yml
        order-service-service.yaml
        product-service-claim0-persistentvolumeclaim.yaml
        product-service-deployment.yaml
        product-service-hpa.yml
        product-service-service.yaml
        prometheus-config.yml
        prometheus-configmap.yml
        prometheus-deployment.yml
        prometheus-service.yml

## Configuração do Docker

### Criação dos Dockerfiles

Crie um Dockerfile para cada serviço (`order-service` e `product-service`). Aqui estão os links para os Dockerfiles:

- [Dockerfile para order-service](./order-service/Dockerfile)
- [Dockerfile para product-service](./product-service/Dockerfile)

#### O que o Dockerfile faz:
- **FROM nginx:alpine**: Utiliza a imagem base do Nginx.
- **COPY ./dist /usr/share/nginx/html**: Copia os arquivos estáticos para o diretório do Nginx.
- **EXPOSE 80**: Expõe a porta 80 para acesso ao serviço.

### Configuração do Docker Compose

Crie um arquivo `docker-compose.yml` para cada serviço. Aqui estão os links para os arquivos:

- [docker-compose.yml para order-service](./order-service/docker-compose.yml)
- [docker-compose.yml para product-service](./product-service/docker-compose.yml)

#### O que o docker-compose.yml faz:
- Define os serviços (`order-service` e `product-service`).
- Configura a construção da imagem Docker a partir do Dockerfile.
- Mapeia as portas do contêiner para a máquina host.
- Monta volumes para persistir dados e configurar Nginx.
- Define limites e reservas de recursos para os contêineres.

## Configuração do Kubernetes

### Subir os Pods com Kubernetes

Para criar e gerenciar os Pods no Kubernetes, siga os passos abaixo:

1. **Criação do Deployment para `order-service`**:
   - [order-service-deployment.yml](./kubernetes/order-service-deployment.yml)

2. **Criação do Deployment para `product-service`**:
   - [product-service-deployment.yml](./kubernetes/product-service-deployment.yml)

3. **Aplicar os Deployments**:
   ```sh
   kubectl apply -f kubernetes/order-service-deployment.yml
   kubectl apply -f kubernetes/product-service-deployment.yml

## Verificar os Pods:
   ```sh

kubectl get pods

```
# Conceitos e Ferramentas Utilizadas

## Pods

### O que são:
Em Kubernetes, um pod é a menor unidade de computação que pode ser criada e gerenciada. Um pod pode conter um ou mais containers que compartilham o mesmo armazenamento, rede e informações sobre como rodar os containers. Os pods são usados para executar aplicações e serviços dentro do cluster Kubernetes.

### Por que são utilizados:
Pods são usados para isolar e gerenciar aplicações e serviços. Eles fornecem uma maneira de agrupar containers que precisam trabalhar juntos e facilitam a escalabilidade e a gestão dos recursos da aplicação.

## Prometheus

### O que é:
Prometheus é uma ferramenta de monitoramento e alertas para sistemas e serviços. Ele coleta e armazena métricas em tempo real e permite consultar essas métricas para gerar gráficos e alertas.

### Por que foi utilizado:
No projeto, Prometheus foi utilizado para monitorar a performance e a saúde dos serviços e pods em seu cluster Kubernetes. Ele coleta dados como uso de CPU, memória e latência, ajudando a identificar problemas e a garantir que a aplicação esteja funcionando corretamente.

## Grafana

### O que é:
Grafana é uma ferramenta de visualização de dados que se integra com várias fontes de dados, incluindo o Prometheus. Ele permite criar dashboards e gráficos interativos para visualizar as métricas coletadas.

### Por que foi utilizado:
Grafana foi utilizado para criar visualizações e dashboards das métricas coletadas pelo Prometheus. Isso facilita a análise das métricas e a identificação de tendências e problemas no desempenho da aplicação, ajudando na tomada de decisões informadas para a gestão e otimização do sistema.

# Utilização no Projeto

- **Pod**: Usado para executar os serviços e garantir que eles estejam operando conforme o especificado.
- **Prometheus e Grafana**: Utilizados juntos para monitorar e visualizar o desempenho dos serviços e pods no Kubernetes, permitindo uma gestão eficaz e a resolução proativa de problemas.

# Monitoramento com Prometheus

## Arquivos de Configuração

- **prometheus-configmap.yml**: Define um ConfigMap que armazena a configuração do Prometheus.
- **prometheus-deployment.yml**: Cria um Deployment para o Prometheus com as configurações necessárias. Define volumes e volume mounts para configurar Prometheus.
- **prometheus-service.yml**: Define um Service para expor o Prometheus. Configura o Service para usar a porta 9090 e mapeia para uma NodePort.


## Aplicar as Configurações

Aplique os recursos criados:

```sh
kubectl apply -f kubernetes/prometheus-configmap.yml
kubectl apply -f kubernetes/prometheus-deployment.yml
kubectl apply -f kubernetes/prometheus-service.yml
```

# Automatização de Deployments

Para automatizar os deployments, recomendamos configurar pipelines de CI/CD usando ferramentas como Jenkins, GitLab CI ou GitHub Actions. Um exemplo de pipeline pode incluir etapas como build da imagem Docker, push para o Docker Hub e aplicação das configurações Kubernetes. Nesse projeto foi utilizado o Github.

## Exemplo de Pipeline

```yaml
# Pipeline de CI/CD exemplo para GitHub Actions
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout código
        uses: actions/checkout@v2

      - name: Configurar Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Build da imagem Docker
        run: docker build -t docker-user/kubernets:latest .

      - name: Login no Docker Hub
        run: echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin

      - name: Push da imagem para o Docker Hub
        run: docker push docker-user/kubernets:latest

      - name: Aplicar configurações Kubernetes
        run: kubectl apply -f kubernetes/

    ```yaml
    spec:
  replicas: 3

## Escalabilidade
Teste a escalabilidade dos serviços aumentando o número de réplicas nos deployments. Por exemplo, para aumentar o número de réplicas do order-service, edite o campo replicas no arquivo order-service-deployment.yml:

Aplique a configuração atualizada:

```sh

kubectl apply -f kubernetes/order-service-deployment.yml

```