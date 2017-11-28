---
title: "Azure PowerShell 指令碼範例 - 升級 Service Fabric 應用程式 | Microsoft Docs"
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
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="50d5f-103">升級 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="50d5f-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="50d5f-104">這個範例指令碼會將執行中的 Service Fabric 應用程式執行個體升級到 1.3.0 版。</span><span class="sxs-lookup"><span data-stu-id="50d5f-104">This sample script upgrades a running Service Fabric application instance to version 1.3.0.</span></span> <span data-ttu-id="50d5f-105">指令碼會將新的應用程式套件複製到叢集映像存放區，註冊應用程式類型，開始進行監視的升級，並會持續檢查升級狀態，直到升級完成或復原為止。</span><span class="sxs-lookup"><span data-stu-id="50d5f-105">The script copies the new application package to the cluster image store, registers the application type, starts a monitored upgrade, and continuously checks the upgrade status until the upgrade completes or rolls back.</span></span> <span data-ttu-id="50d5f-106">視需要自訂參數。</span><span class="sxs-lookup"><span data-stu-id="50d5f-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="50d5f-107">如有需要，可隨同 [Service Fabric SDK](../service-fabric-get-started.md) 一起安裝 Service Fabric PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="50d5f-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="50d5f-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="50d5f-108">Sample script</span></span>

<span data-ttu-id="50d5f-109">[!code-powershell[主要](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "升級應用程式")]</span><span class="sxs-lookup"><span data-stu-id="50d5f-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="50d5f-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="50d5f-110">Script explanation</span></span>

<span data-ttu-id="50d5f-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="50d5f-111">This script uses the following commands.</span></span> <span data-ttu-id="50d5f-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="50d5f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="50d5f-113">命令</span><span class="sxs-lookup"><span data-stu-id="50d5f-113">Command</span></span> | <span data-ttu-id="50d5f-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="50d5f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50d5f-115">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="50d5f-115">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="50d5f-116">取得 Service Fabric 叢集或特定應用程式中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="50d5f-116">Gets all the applications in the Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="50d5f-117">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="50d5f-117">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="50d5f-118">取得 Service Fabric 應用程式升級的狀態。</span><span class="sxs-lookup"><span data-stu-id="50d5f-118">Gets the status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="50d5f-119">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="50d5f-119">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="50d5f-120">取得已在 Service Fabric 叢集上註冊的 Service Fabric 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="50d5f-120">Gets the Service Fabric application types registered on the Service Fabric cluster.</span></span> |
| [<span data-ttu-id="50d5f-121">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="50d5f-121">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="50d5f-122">取消註冊 Service Fabric 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="50d5f-122">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="50d5f-123">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="50d5f-123">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="50d5f-124">將 Service Fabric 應用程式套件複製到映像存放區。</span><span class="sxs-lookup"><span data-stu-id="50d5f-124">Copies a Service Fabric application package to the image store.</span></span>  |
| [<span data-ttu-id="50d5f-125">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="50d5f-125">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="50d5f-126">註冊 Service Fabric 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="50d5f-126">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="50d5f-127">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="50d5f-127">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="50d5f-128">將 Service Fabric 應用程式升級至指定的應用程式類型版本。</span><span class="sxs-lookup"><span data-stu-id="50d5f-128">Upgrades a Service Fabric application to the specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="50d5f-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50d5f-129">Next steps</span></span>

<span data-ttu-id="50d5f-130">如需有關 Service Fabric PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="50d5f-130">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="50d5f-131">您可以在 [PowerShell 範例](../service-fabric-powershell-samples.md)中找到適用於 Azure Service Fabric 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="50d5f-131">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
