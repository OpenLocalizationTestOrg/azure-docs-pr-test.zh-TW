---
title: "PowerShell 指令碼範例-aaaAzure 升級 Service Fabric 應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 升級 Service Fabric 應用程式。"
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="c131a-103">升級 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="c131a-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="c131a-104">這個範例指令碼升級執行 Service Fabric 應用程式執行個體 tooversion 1.3.0。</span><span class="sxs-lookup"><span data-stu-id="c131a-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="c131a-105">hello 指令碼複製 hello 新應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型、 開始進行監視的升級，和 hello 升級完成或回復之前會持續檢查 hello 升級狀態。</span><span class="sxs-lookup"><span data-stu-id="c131a-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="c131a-106">視需要自訂 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="c131a-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="c131a-107">如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c131a-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c131a-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c131a-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="c131a-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c131a-109">Script explanation</span></span>

<span data-ttu-id="c131a-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="c131a-110">This script uses hello following commands.</span></span> <span data-ttu-id="c131a-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c131a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c131a-112">命令</span><span class="sxs-lookup"><span data-stu-id="c131a-112">Command</span></span> | <span data-ttu-id="c131a-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="c131a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c131a-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="c131a-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="c131a-115">取得 hello Service Fabric 叢集中的所有 hello 應用程式或特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="c131a-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="c131a-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="c131a-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="c131a-117">取得 hello Service Fabric 應用程式升級狀態。</span><span class="sxs-lookup"><span data-stu-id="c131a-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="c131a-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c131a-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="c131a-119">取得 hello 註冊 hello Service Fabric 叢集上的 Service Fabric 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="c131a-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="c131a-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c131a-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="c131a-121">取消註冊 Service Fabric 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="c131a-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="c131a-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="c131a-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="c131a-123">複製 Service Fabric 應用程式套件 toohello 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="c131a-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="c131a-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c131a-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="c131a-125">註冊 Service Fabric 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="c131a-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="c131a-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="c131a-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="c131a-127">升級 Service Fabric 應用程式 toohello 指定的應用程式類型版本。</span><span class="sxs-lookup"><span data-stu-id="c131a-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c131a-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c131a-128">Next steps</span></span>

<span data-ttu-id="c131a-129">如需有關 hello Service Fabric PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="c131a-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="c131a-130">可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c131a-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
