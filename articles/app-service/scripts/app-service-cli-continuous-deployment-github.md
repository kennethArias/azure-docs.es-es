---
title: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación continua desde GitHub | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación continua desde GitHub | Microsoft Docs"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: bbfc66a2913c4459bfe8c80770b170ae1b2bc356
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>Creación de una aplicación web con implementación continua desde GitHub

Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, configura la implementación continua desde un repositorio de GitHub. Para la implementación de GitHub sin una implementación continua, consulte [Creación de una aplicación web e implementación de código desde GitHub](app-service-cli-deploy-github.md). Para este ejemplo, se necesita:

* Un repositorio de GitHub con código de aplicación, para el cual deberá tener permisos administrativos.
* Un [token de acceso personal (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para su cuenta de GitHub.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si decide instalar y usar la CLI localmente, necesitará la CLI de Azure versión 2.0 o posterior. Para encontrar la versión, ejecute `az --version`. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos. Cada comando de la tabla crea un vínculo a documentación específica del comando.

| Comando | Notas |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az_group_create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az_appservice_plan_create) | Crea un plan de App Service, |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) | Crea una aplicación web de Azure. |
| [`az webapp deployment source config`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az_webapp_deployment_source_config) | Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial. |

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).

Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).
