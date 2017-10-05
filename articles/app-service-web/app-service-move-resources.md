---
title: "將 Web App 資源移動到另一個資源群組"
description: "描述您可以將 Web Apps 與 App Service 從一個資源群組移至另一個的案例。"
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="16482-103">支援的移動組態</span><span class="sxs-lookup"><span data-stu-id="16482-103">Supported Move Configurations</span></span>
<span data-ttu-id="16482-104">您可以使用 [Resource Manager 移動資源 API](../azure-resource-manager/resource-group-move-resources.md) 來移動 Azure Web 應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="16482-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="16482-105">Azure Web Apps 目前支援下列移動案例：</span><span class="sxs-lookup"><span data-stu-id="16482-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="16482-106">將整個資源群組內容 (Web 應用程式、App Service 方案及憑證) 移到另一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="16482-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="16482-107">在此案例中，目的地資源群組不能包含任何 Microsoft.Web 資源。</span><span class="sxs-lookup"><span data-stu-id="16482-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="16482-108">將個別 Web 應用程式移到不同的資源群組，但同時仍將它們裝載在其目前的 App Service 方案中 (App Service 方案會保留在舊的資源群組中)。</span><span class="sxs-lookup"><span data-stu-id="16482-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


