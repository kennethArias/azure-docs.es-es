---
title: "Implementación en Azure Container Instances desde Azure Container Registry"
description: "Implementación de Azure Container Instances desde Azure Container Registry"
services: container-instances
author: seanmck
manager: timlt
ms.service: container-instances
ms.topic: article
ms.date: 01/02/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 4205b47dc67920021812c1e573a98de64ad198ec
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a>Implementación en Azure Container Instances desde Azure Container Registry

Azure Container Registry es un registro privado basado en Azure para imágenes de contenedor de Docker. En este artículo se describe cómo implementar imágenes de contenedor almacenadas en Azure Container Registry en Azure Container Instances.

## <a name="deploy-with-azure-cli"></a>Implementación con la CLI de Azure

La CLI de Azure incluye comandos para crear y administrar contenedores en Azure Container Instances. Si especifica una imagen privada en el comando [az container create][az-container-create], también puede especificar la contraseña del registro de imagen que se requiere para autenticarse con el registro de contenedor.

```azurecli-interactive
az container create --resource-group myResourceGroup --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword
```

El comando [az container create][az-container-create] también admite la especificación de `--registry-login-server` y `--registry-username`. Sin embargo, el servidor de inicio de sesión de Azure Container Registry siempre es *NombreDeRegistro*.azurecr.io y el nombre de usuario predeterminado es *NombreDeRegistro*, por lo que estos valores se infieren del nombre de la imagen si no se proporcionan de forma explícita.

## <a name="deploy-with-azure-resource-manager-template"></a>Implementación con plantillas de Azure Resource Manager

Puede especificar las propiedades de Azure Container Registry en una plantilla de Azure Resource Manager; para ello, se debe incluir la propiedad `imageRegistryCredentials` en la definición del grupo de contenedores:

```JSON
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

Para evitar almacenar la contraseña del registro de contenedor directamente en la plantilla, se recomienda que la almacene como un secreto en [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) y que haga referencia a ella en la plantilla mediante la [integración nativa entre Azure Resource Manager y Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="deploy-with-azure-portal"></a>Implementación con Azure Portal

Si se mantienen imágenes de contenedor en Azure Container Registry, se puede crear fácilmente un contenedor en Azure Container Instances a través de Azure Portal.

1. En Azure Portal, vaya al registro de contenedor.

2. Seleccione **Repositorios**, elija el repositorio desde el que va a implementar, haga clic con el botón derecho en la etiqueta de la imagen de contenedor que desea implementar y seleccione **Ejecutar instancia**.

    !["Ejecutar instancia" en Azure Container Registry de Azure Portal][acr-runinstance-contextmenu]

3. Escriba un nombre para el contenedor y un nombre para el grupo de recursos. También puede cambiar los valores predeterminados si lo desea.

    ![Menú Crear para Azure Container Instances][acr-create-deeplink]

4. Una vez completada la implementación, puede ir al grupo de contenedores desde el panel de notificaciones para buscar la dirección IP y otras propiedades.

    ![Vista de detalles del grupo de contenedores de Azure Container Instances][aci-detailsview]

## <a name="next-steps"></a>pasos siguientes

Obtenga información sobre cómo crear contenedores, insertarlos en un registro de contenedor privado e implementarlos en Azure Container Instances al [completar el tutorial](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png
[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container?view=azure-cli-latest#az_container_create