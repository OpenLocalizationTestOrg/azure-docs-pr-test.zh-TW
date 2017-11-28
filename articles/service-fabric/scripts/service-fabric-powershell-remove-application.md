---
title: "Azure PowerShell 指令碼範例 - 從叢集移除應用程式 | Microsoft Docs"
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
ms.openlocfilehash: 05851132c7e5e5877884d29f04bce6c0717ce411
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="610ff-103">從 Service Fabric 叢集移除應用程式</span><span class="sxs-lookup"><span data-stu-id="610ff-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="610ff-104">這個範例指令碼刪除執行中的 Service Fabric 應用程式執行個體、從叢集取消註冊應用程式類型和版本，並刪除叢集映像存放區中的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="610ff-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster, and deletes the application package from the cluster image store.</span></span>  <span data-ttu-id="610ff-105">刪除應用程式執行個體也會刪除應用程式相關聯的所有執行中服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="610ff-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="610ff-106">視需要自訂參數。</span><span class="sxs-lookup"><span data-stu-id="610ff-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="610ff-107">如有需要，可隨同 [Service Fabric SDK](../service-fabric-get-started.md) 一起安裝 Service Fabric PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="610ff-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="610ff-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="610ff-108">Sample script</span></span>

<span data-ttu-id="610ff-109">[!code-powershell[主要](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "從叢集移除應用程式")]</span><span class="sxs-lookup"><span data-stu-id="610ff-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="610ff-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="610ff-110">Script explanation</span></span>

<span data-ttu-id="610ff-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="610ff-111">This script uses the following commands.</span></span> <span data-ttu-id="610ff-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="610ff-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="610ff-113">命令</span><span class="sxs-lookup"><span data-stu-id="610ff-113">Command</span></span> | <span data-ttu-id="610ff-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="610ff-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="610ff-115">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="610ff-115">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="610ff-116">從叢集移除執行中的 Service Fabric 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="610ff-116">Removes a running Service Fabric application instance from the cluster.</span></span>  |
| [<span data-ttu-id="610ff-117">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="610ff-117">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="610ff-118">從叢集取消註冊 Service Fabric 應用程式類型和版本。</span><span class="sxs-lookup"><span data-stu-id="610ff-118">Unregisters a Service Fabric application type and version from the cluster.</span></span> |
| [<span data-ttu-id="610ff-119">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="610ff-119">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="610ff-120">從映像存放區移除 Service Fabric 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="610ff-120">Removes a Service Fabric application package from the image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="610ff-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="610ff-121">Next steps</span></span>

<span data-ttu-id="610ff-122">如需有關 Service Fabric PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="610ff-122">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="610ff-123">您可以在 [PowerShell 範例](../service-fabric-powershell-samples.md)中找到適用於 Azure Service Fabric 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="610ff-123">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
