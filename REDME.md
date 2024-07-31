# 3º Projeto Prático - DevOps: Implementação de Microsserviços com Kubernetes (K8s) na AWS

## Desafio
Projete e implemente uma aplicação utilizando arquitetura de microsserviços no Kubernetes (K8s) no provedor de nuvem da AWS (EKS).

## Estrutura de Diretórios

```plaintext
ecommerce-project/
│
├── product-service/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   ├── nginx/
│   │   └── nginx.conf
│   ├── src/
│   │   └── # Código fonte do product-service
│   └── html/
│       └── # Arquivos estáticos do product-service
│
├── order-service/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   ├── nginx/
│   │   └── nginx.conf
│   ├── src/
│   │   └── # Código fonte do order-service
│   └── html/
│       └── # Arquivos estáticos do order-service
│
├── kubernetes/
│   ├── product-service-deployment.yml
│   ├── product-service-service.yml
│   ├── order-service-deployment.yml
│   ├── order-service-service.yml
│   └── ingress.yml
│
└── README.md
