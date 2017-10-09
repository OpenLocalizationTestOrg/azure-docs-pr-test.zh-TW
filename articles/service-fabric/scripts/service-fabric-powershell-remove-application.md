---
title: "aaaAzure PowerShell 指令碼範例從叢集移除應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 從 Service Fabric 叢集移除應用程式。"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="e4c81-103">從 Service Fabric 叢集移除應用程式</span><span class="sxs-lookup"><span data-stu-id="e4c81-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="e4c81-104">這個範例指令碼刪除正在執行的 Service Fabric 應用程式執行個體、 取消登錄的應用程式類型和版本從 hello 叢集和從 hello 叢集映像存放區刪除 hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="e4c81-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="e4c81-105">正在刪除 hello 應用程式執行個體也會刪除所有 hello 執行該應用程式相關聯的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e4c81-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="e4c81-106">視需要自訂 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="e4c81-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="e4c81-107">如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e4c81-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e4c81-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e4c81-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="e4c81-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e4c81-109">Script explanation</span></span>

<span data-ttu-id="e4c81-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="e4c81-110">This script uses hello following commands.</span></span> <span data-ttu-id="e4c81-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e4c81-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e4c81-112">命令</span><span class="sxs-lookup"><span data-stu-id="e4c81-112">Command</span></span> | <span data-ttu-id="e4c81-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="e4c81-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4c81-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="e4c81-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="e4c81-115">移除 hello 叢集正在執行的 Service Fabric 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="e4c81-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="e4c81-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="e4c81-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="e4c81-117">取消註冊 Service Fabric 應用程式類型和從 hello 叢集的版本。</span><span class="sxs-lookup"><span data-stu-id="e4c81-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="e4c81-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="e4c81-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="e4c81-119">Service Fabric 應用程式套件移除 hello 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="e4c81-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="e4c81-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4c81-120">Next steps</span></span>

<span data-ttu-id="e4c81-121">如需有關 hello Service Fabric PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="e4c81-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="e4c81-122">可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="e4c81-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
