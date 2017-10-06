---
title: "aaaAzure 服務網狀架構 CLI 指令碼中移除的範例"
description: "從使用 Azure Service Fabric CLI hello Azure Service Fabric 叢集中移除應用程式"
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="cf812-103">從 Service Fabric 叢集移除應用程式</span><span class="sxs-lookup"><span data-stu-id="cf812-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="cf812-104">這個範例指令碼執行的 Service Fabric 應用程式執行個體中刪除、 取消登錄的應用程式類型和從 hello 叢集的版本。</span><span class="sxs-lookup"><span data-stu-id="cf812-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="cf812-105">正在刪除 hello 應用程式執行個體也會刪除所有 hello 執行該應用程式相關聯的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="cf812-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="cf812-106">接下來，就會從 hello 映像存放區刪除 hello 應用程式檔案。</span><span class="sxs-lookup"><span data-stu-id="cf812-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="cf812-107">如有需要安裝 hello[服務網狀架構 CLI](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="cf812-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="cf812-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="cf812-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="cf812-109">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf812-109">Next steps</span></span>

<span data-ttu-id="cf812-110">如需詳細資訊，請參閱 hello[服務網狀架構 CLI 文件](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="cf812-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="cf812-111">適用於 Azure Service Fabric 的其他服務網狀架構 CLI 範例可以在 hello[服務網狀架構 CLI 範例](../samples-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="cf812-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
