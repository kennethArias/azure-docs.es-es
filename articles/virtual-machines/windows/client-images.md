---
title: "Uso de imágenes de cliente de Windows en Azure | Microsoft Docs"
description: "Cómo usar las ventajas para la suscripción de Visual Studio a fin de implementar Windows 7, Windows 8 o Windows 10 en Azure para escenarios de desarrollo/pruebas"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/15/2017
ms.author: iainfou
ms.openlocfilehash: 6db900981daa2139a0d2e951f41fc48d5c291074
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/16/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Uso del cliente Windows en Azure para escenarios de desarrollo y pruebas
Puede usar Windows 7, Windows 8 o Windows 10 en Azure para escenarios de desarrollo y pruebas siempre que tenga una suscripción adecuada a Visual Studio (anteriormente MSDN). En este artículo se describen los requisitos de idoneidad para ejecutar el cliente Windows en Azure y usar las imágenes de la galería de Azure.

## <a name="subscription-eligibility"></a>Idoneidad de la suscripción
Los suscriptores activos de Visual Studio (es decir, las personas que adquirieron una licencia de suscripción de Visual Studio) pueden usar el cliente Windows para desarrollo y pruebas. El cliente Windows se puede usar en su propio hardware y en máquinas virtuales de Azure que se ejecutan en cualquier tipo de suscripción de Azure. El cliente Windows no se puede implementar ni usar en Azure para un uso de producción normal. Tampoco lo pueden usar quienes no son suscriptores activos de Visual Studio.

Para su comodidad, ciertas imágenes de Windows 10 están disponibles en la galería de Azure dentro de las [ofertas de desarrollo y pruebas a las que tiene acceso](#eligible-offers). Los suscriptores de Visual Studio dentro de cualquier tipo de oferta también pueden [preparar y crear apropiadamente](prepare-for-upload-vhd-image.md) una imagen de Windows 7, Windows 8 o Windows 10 de 64 bits y, luego, [cargarla en Azure](upload-generalized-managed.md). El uso sigue limitado a desarrollo y pruebas por parte de los suscriptores activos de Visual Studio.

## <a name="eligible-offers"></a>Ofertas a las que se puede tener acceso
La tabla siguiente muestra los detalles de los id. de oferta idóneos para implementar Windows 10 a través de la galería de Azure. Las imágenes de Windows 10 solo son visibles para las ofertas siguientes. Los suscriptores de Visual Studio que deban ejecutar el cliente Windows en un tipo de oferta distinto necesitan que [prepare y cree apropiadamente](prepare-for-upload-vhd-image.md) una imagen de Windows 7, Windows 8 o Windows 10 de 64 bits y, [luego, la cargue en Azure](upload-generalized-managed.md).

| Nombre de la oferta | Número de la oferta | Imágenes de cliente disponibles |
|:--- |:---:|:---:|
| [Desarrollo/pruebas - Pago por uso](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Suscriptores de Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Suscriptores de Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Suscriptores de Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium con MSDN (ventaja)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Suscriptores de Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Suscriptores de Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Desarrollo/pruebas - Enterprise](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Compruebe la suscripción a Azure
Si no conoce el identificador de su oferta, puede obtenerlo en Azure Portal de una de estas dos formas:  

- En la ventana *Suscripciones*:

  ![Detalles del id. de oferta desde el Portal de Azure](./media/client-images/offer-id-azure-portal.png) 

- O bien, haga clic en **Facturación** y, a continuación, haga clic en el identificador de suscripción. El identificador de oferta aparece en la ventana de *facturación*.

También puede ver el id. de la oferta en la pestaña ["Suscripciones"](http://account.windowsazure.com/Subscriptions) del portal de la cuenta de Azure:

![Detalles del id. de oferta desde el portal de la cuenta de Azure](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>pasos siguientes
Ahora puede implementar las máquinas virtuales con [PowerShell](quick-create-powershell.md), [plantillas de Resource Manager](ps-template.md) o [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

