# 🚚 Innovatech Chile - Frontend Web App

Este repositorio contiene la aplicación cliente (Frontend) para la plataforma de gestión logística de Innovatech Chile. Proporciona una interfaz gráfica para que los operadores interactúen con los microservicios de Ventas y Despachos, permitiendo visualizar órdenes de compra, asignar transportes y actualizar los estados de entrega en tiempo real.

## ⚙️ Arquitectura y Despliegue
La aplicación está diseñada para ser empaquetada en una imagen Docker y desplegada en un clúster de Amazon Elastic Kubernetes Service (EKS). El acceso público se expone mediante un **Application Load Balancer (ELB)** configurado nativamente por Kubernetes a través de un objeto tipo `Service`.

## 🚀 Instalación y Ejecución Local

### Prerequisitos
* Node.js (v16 o superior)
* npm o yarn

### Pasos
1. Clonar el repositorio:
   ```bash
   git clone [https://github.com/tu-usuario/tu-repo-frontend.git](https://github.com/tu-usuario/tu-repo-frontend.git)
   
2. Instalar las dependencias:
   ```bash
    npm install

3. Configurar variables de entorno:
Crea un archivo .env en la raíz del proyecto y configura las URLs de los microservicios (en desarrollo apuntan a localhost, en producción a los Load Balancers de AWS):

   ```bash
    VITE_URL_VENTAS=http://localhost:8082
    VITE_URL_DESPACHOS=http://localhost:8081

4. Iniciar el servidor de desarrollo:
   ```bash
    npm run dev

## 🔄 Integración y Despliegue Continuo (CI/CD)
El proyecto cuenta con un flujo de GitHub Actions automatizado. Cada vez que se realiza un git push a la rama principal:

1. Se compila la aplicación React utilizando Node.

2. Se construye la imagen Docker del Frontend.

3. Se publica la imagen en un repositorio privado de Amazon ECR.

4. Se ejecuta kubectl set image para actualizar el objeto Deployment en el clúster EKS de AWS, logrando un despliegue sin interrupciones (Zero-Downtime Deployment). Las credenciales de AWS están protegidas mediante GitHub Secrets.
