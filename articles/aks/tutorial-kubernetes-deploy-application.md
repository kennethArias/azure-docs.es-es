---
title: "Tutorial de Kubernetes en Azure: implementación de la aplicación"
description: "Tutorial de AKS: implementación de la aplicación"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 4468424a96b4949161218d495dd21f24285430fd
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2017
---
# <a name="run-applications-in-azure-container-service-aks"></a>Ejecutar aplicaciones en Azure Container Service (AKS)

En este tutorial, la cuarta parte de ocho, se implementa una aplicación de ejemplo en un clúster de Kubernetes. Los pasos completados incluyen:

> [!div class="checklist"]
> * Actualización de los archivos de manifiesto de Kubernetes
> * Ejecución de una aplicación en Kubernetes
> * Prueba de la aplicación

En tutoriales posteriores se escala horizontalmente y se actualiza esta aplicación, y se configura Operations Management Suite para supervisar el clúster de Kubernetes.

En este tutorial se da por hecho que tiene unos conocimientos básicos de los conceptos de Kubernetes. Para obtener información más detallada sobre esta aplicación, consulte la [documentación de Kubernetes][kubernetes-documentation].

## <a name="before-you-begin"></a>Antes de empezar

En tutoriales anteriores se empaquetó una aplicación en una imagen de contenedor, se cargó esta imagen en Azure Container Registry y se creó un clúster de Kubernetes. 

Para completar este tutorial, necesita el archivo de manifiesto de Kubernetes `azure-vote-all-in-one-redis.yaml` creado previamente. Este archivo se descargó con el código fuente de la aplicación en un tutorial anterior. Confirme que ha clonado el repositorio y que ha cambiado los directorios en el repositorio clonado.

Si no ha realizado estos pasos, pero desea continuar, vuelva al [tutorial 1: Creación de imágenes de contenedor][aks-tutorial-prepare-app].

## <a name="update-manifest-file"></a>Actualización del archivo de manifiesto

En este tutorial se ha usado Azure Container Registry (ACR) para almacenar una imagen de contenedor. Antes de ejecutar la aplicación, hay que actualizar el nombre del servidor de inicio de sesión de ACR en el archivo de manifiesto de Kubernetes.

El nombre del servidor de inicio de sesión de ACR se obtiene con el comando [az acr list][az-acr-list].

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```
Configure kubernetes to use your ACR

```azurecli
kubectrl create secret docker-registry <SECRET_NAME> --docker-server <REGISTRY_NAME>.azurecr.io --docker-email <YOUR_MAIL> --docker-username=<SERVICE_PRINCIPAL_ID> --docker-password <YOUR_PASSWORD>
```


El archivo de manifiesto se creó previamente con el nombre de servidor de inicio de sesión `microsoft`. Abra el archivo con un editor de texto. En este ejemplo, el archivo se abre con `vi`.

```console
vi azure-vote-all-in-one-redis.yaml
```

Reemplace `microsoft` por el nombre del servidor de inicio de sesión de ACR. Este valor se encuentra en la línea **47** del archivo de manifiesto.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

Guarde y cierre el archivo.

## <a name="deploy-application"></a>Implementación de la aplicación

Use el comando [kubectl create][kubectl-create] para ejecutar la aplicación. Este comando analiza el archivo de manifiesto y crea los objetos de Kubernetes definidos.

```azurecli
kubectl create -f azure-vote-all-in-one-redis.yaml
```

Salida:

```
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Prueba de la aplicación

Se crea un [servicio de Kubernetes][kubernetes-service] que expone la aplicación a Internet. Este proceso puede tardar unos minutos. 

Para supervisar el progreso, utilice el comando [kubectl get service][kubectl-get] con el argumento `--watch`.

```azurecli
kubectl get service azure-vote-front --watch
```

En un primer momento, el parámetro *EXTERNAL-IP* del servicio *azure-vote-front* aparece como *pendiente*.
  
```
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
```

Una vez que la dirección *EXTERNAL-IP* haya cambiado de *pendiente* a una *dirección IP*, use `CTRL-C` para detener el proceso de inspección de kubectl. 

```
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

Para ver la aplicación, navegue hasta la dirección IP externa.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>pasos siguientes

En este tutorial, se ha implementado la aplicación Azure Vote en un clúster de Kubernetes en AKS. Las tareas completadas incluyen:  

> [!div class="checklist"]
> * Descargar archivos de manifiesto de Kubernetes
> * Ejecutar la aplicación en Kubernetes
> * Probar la aplicación

Pase al siguiente tutorial para obtener información acerca de cómo escalar una aplicación Kubernetes y la infraestructura de Kubernetes subyacente. 

> [!div class="nextstepaction"]
> [Escalar infraestructura y aplicación de Kubernetes][aks-tutorial-scale]

<!-- LINKS - external -->
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-documentation]: https://kubernetes.io/docs/home/
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-scale]: ./tutorial-kubernetes-scale.md
[az-acr-list]: /cli/azure/acr#list
