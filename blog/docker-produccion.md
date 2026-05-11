---
title: Docker para Entornos de Producción: Guía Práctica
category: DevOps
readtime: 15 min lectura
date: 2024-03-18
tags: [Docker, CI/CD, GitHub Actions, Producción]
---

## Introducción

Docker ha revolucionado la forma en que desplegamos aplicaciones. Pero pasar del desarrollo a producción requiere más que solo containerizar tu app. En esta guía aprenderás las mejores prácticas para usar Docker en entornos de producción.

## ¿Por qué Docker en Producción?

- **Consistencia** - Same environment from dev to prod
- **Aislamiento** - Apps no se pelean entre sí
- **Escalabilidad** - Scale up/down containers easily
- **Rapidez** - Deploy en segundos no minutos

## Dockerfile Optimizado

```dockerfile
# Usa imagen base ligera
FROM node:20-alpine AS builder

WORKDIR /app

# Copiar solo dependencias primero (mejor caché)
COPY package*.json ./
RUN npm ci --only=production

# Copiar código fuente
COPY . .

# Build de producción
RUN npm run build

# Imagen final optimizada
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## Docker Compose para Producción

```yaml
version: '3.8'
services:
  app:
    image: tu-app:latest
    restart: always
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=db
    depends_on:
      - db
    networks:
      - app-network

  db:
    image: postgres:15-alpine
    restart: always
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=${DB_PASSWORD}
    networks:
      - app-network

volumes:
  pgdata:

networks:
  app-network:
    driver: bridge
```

## GitHub Actions CI/CD

```yaml
name: Deploy to Docker

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Build Docker image
        run: |
          docker build -t tu-app:${{ github.sha }} .
          
      - name: Push to Registry
        run: |
          echo "${{ secrets.REGISTRY_TOKEN }}" | docker login ghcr.io -u ${{ github.actor }} --password-stdin
          docker push ghcr.io/${{ github.repository }}:${{ github.sha }}
      
      - name: Deploy
        run: |
          ssh ${{ secrets.SERVER_HOST }} "docker pull ghcr.io/${{ github.repository }}:${{ github.sha }}"
```

## Monitoreo con Prometheus + Grafana

```yaml
services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3001:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=${GRAFANA_PASSWORD}
```

## Checklist para Producción

- [ ] Multi-stage build para imágenes pequeñas
- [ ] No usar root dentro del contenedor
- [ ] Health checks definidos
- [ ] Logs centralizados
- [ ] Redes aisladas entre servicios
- [ ] Secrets manejados fuera del contenedor
- [ ] Backups de volúmenes configurados

## Conclusión

Docker en producción requiere planificación. Aplica estas prácticas desde el inicio y tendrás una infraestructura robusta y mantenible.

---

*¿Quieres ver más sobre Kubernetes? Sígueme para el próximo tutorial.*