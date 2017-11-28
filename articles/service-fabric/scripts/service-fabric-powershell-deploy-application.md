---
title: "aaaAzure PowerShell 指令碼範例-將部署應用程式 tooa 叢集 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-部署應用程式 tooa Service Fabric 叢集。"
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="4ea45-103">部署應用程式 tooa Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="4ea45-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="4ea45-104">這個範例指令碼複製應用程式封裝 tooa 叢集映像存放區、 hello 叢集中註冊 hello 應用程式類型和建立應用程式執行個體從 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="4ea45-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="4ea45-105">如果任何預設的服務定義 hello hello 目標應用程式類型應用程式資訊清單中，此時會建立這些服務。</span><span class="sxs-lookup"><span data-stu-id="4ea45-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="4ea45-106">視需要自訂 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="4ea45-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="4ea45-107">如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4ea45-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4ea45-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4ea45-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4ea45-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="4ea45-109">Clean up deployment</span></span> 

<span data-ttu-id="4ea45-110">Hello 指令碼範例執行後，hello 中的指令碼[移除應用程式](service-fabric-powershell-remove-application.md)可以是使用的 tooremove hello 應用程式執行個體、 取消註冊 hello 應用程式類型，並從 hello 映像存放區刪除 hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="4ea45-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="4ea45-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4ea45-111">Script explanation</span></span>

<span data-ttu-id="4ea45-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4ea45-112">This script uses hello following commands.</span></span> <span data-ttu-id="4ea45-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="4ea45-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4ea45-114">命令</span><span class="sxs-lookup"><span data-stu-id="4ea45-114">Command</span></span> | <span data-ttu-id="4ea45-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="4ea45-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ea45-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="4ea45-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="4ea45-117">複製應用程式封裝 toohello 叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="4ea45-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="4ea45-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="4ea45-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="4ea45-119">註冊應用程式類型和 hello 叢集上的版本。</span><span class="sxs-lookup"><span data-stu-id="4ea45-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="4ea45-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4ea45-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="4ea45-121">從註冊的應用程式類型建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ea45-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4ea45-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ea45-122">Next steps</span></span>

<span data-ttu-id="4ea45-123">如需有關 hello Service Fabric PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="4ea45-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="4ea45-124">可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4ea45-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
