---
title: "Azure Service Fabric CLI 指令碼移除範例"
description: "使用 Azure Service Fabric CLI 將應用程式從 Azure Service Fabric 叢集中移除"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="44d50-103">從 Service Fabric 叢集移除應用程式</span><span class="sxs-lookup"><span data-stu-id="44d50-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="44d50-104">這個範例指令碼會刪除執行中的 Service Fabric 應用程式執行個體，並從叢集取消註冊應用程式類型和版本。</span><span class="sxs-lookup"><span data-stu-id="44d50-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="44d50-105">刪除應用程式執行個體也會刪除應用程式相關聯的所有執行中服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="44d50-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="44d50-106">接下來，系統會從映像存放區刪除應用程式檔案。</span><span class="sxs-lookup"><span data-stu-id="44d50-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="44d50-107">如有需要，請安裝[ Service Fabric SDK](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="44d50-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="44d50-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="44d50-108">Sample script</span></span>

<span data-ttu-id="44d50-109">[!code-sh[主要](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "從叢集移除應用程式")]</span><span class="sxs-lookup"><span data-stu-id="44d50-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="44d50-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44d50-110">Next steps</span></span>

<span data-ttu-id="44d50-111">如需詳細資訊，請參閱 [Service Fabric CLI 文件](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="44d50-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="44d50-112">您可以在 [Service Fabric CLI 範例](../samples-cli.md)中找到適用於 Azure Service Fabric 的其他 Service Fabric CLI 範例。</span><span class="sxs-lookup"><span data-stu-id="44d50-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
