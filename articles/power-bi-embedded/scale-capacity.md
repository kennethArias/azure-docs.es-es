---
title: Escalado de la capacidad de Power BI Embedded | Microsoft Docs
description: "Este artículo lo guía por el proceso de escalado de una capacidad de Power BI Embedded en Microsoft Azure."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 09/28/2017
ms.author: asaxton
ms.openlocfilehash: e1ab6a2f52fa56f1e04c6c327796587daf43596e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="scale-your-power-bi-embedded-capacity"></a>Escalado de la capacidad de Power BI Embedded

Este artículo lo guía por el proceso de escalado de una capacidad de Power BI Embedded en Microsoft Azure. El escalado permite aumentar o disminuir el tamaño de la capacidad.

Se da por hecho que ha creado una capacidad de Power BI Embedded. Si no lo ha hecho, consulte [Creación de una capacidad de Power BI Embedded en Azure Portal](create-capacity.md) para empezar a trabajar.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="scale-a-capacity"></a>Escalado de una capacidad

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).

2. Seleccione **Más servicios** > **Power BI Embedded** para ver sus capacidades.

    ![Opción Más servicios de Azure Portal](media/scale-capacity/azure-portal-more-services.png)

3. Seleccione la capacidad que desea escalar.

    ![Lista de capacidades de Power BI Embedded en Azure Portal](media/scale-capacity/azure-portal-capacity-list.png)

4. Seleccione **Plan de tarifa** en **Escala** en su capacidad.

    ![Opción Plan de tarifa en Escala](media/scale-capacity/azure-portal-scale-pricing-tier.png)

    El plan de tarifa actual se muestra en azul.

    ![Plan de tarifa actual mostrado en azul](media/scale-capacity/azure-portal-current-tier.png)

5. Para escalar o reducir verticalmente, seleccione el nuevo nivel al que desplazarse. Si se selecciona un nuevo nivel, se muestra un borde azul discontinuo alrededor de la selección. Seleccione **Seleccionar** para escalar al nuevo nivel.

    ![Selección del nuevo nivel](media/scale-capacity/azure-portal-select-new-tier.png)

    El escalado de la capacidad puede tardar un minuto o dos en completarse.

6. Confirme el nivel en la pestaña Información general. Se muestra el plan de tarifa actual.

    ![Confirmación del plan actual](media/scale-capacity/azure-portal-confirm-tier.png)

## <a name="next-steps"></a>Pasos siguientes

Para hacer una pausa en la capacidad, o iniciarla, consulte [Pausado e inicio de la capacidad de Power BI Embedded en Azure Portal](pause-start.md).

Para empezar a insertar contenido de Power BI en una aplicación, consulte [Inserción de paneles, informes e iconos de Power BI](https://powerbi.microsoft.com/documentation/powerbi-developer-embedding-content/).

¿Tiene más preguntas? [Pruebe a plantearlas en la Comunidad de Power BI](http://community.powerbi.com/)