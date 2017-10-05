---
title: "Service Fabric 叢集安全性：用戶端角色 |Microsoft Docs"
description: "本文說明兩個用戶端角色及提供給這些角色的權限。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 85935e60bba4b27972282700e2e9c9a22b403bdb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a><span data-ttu-id="260fc-103">角色型存取控制 (適用於 Service Fabric 用戶端)</span><span class="sxs-lookup"><span data-stu-id="260fc-103">Role-based access control for Service Fabric clients</span></span>
<span data-ttu-id="260fc-104">Azure Service Fabric 針對連線到 Service Fabric 叢集的用戶端，支援兩種不同的存取控制類型：系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="260fc-104">Azure Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="260fc-105">存取控制可讓叢集系統管理員針對不同的使用者群組限制特定叢集作業的存取權，讓叢集更加安全。</span><span class="sxs-lookup"><span data-stu-id="260fc-105">Access control allows the cluster administrator to limit access to certain cluster operations for different groups of users, making the cluster more secure.</span></span>  

<span data-ttu-id="260fc-106">**系統管理員**可以完整存取管理功能 (包括讀取/寫入功能)。</span><span class="sxs-lookup"><span data-stu-id="260fc-106">**Administrators** have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="260fc-107">**使用者**預設只具有管理功能的讀取存取權 (例如查詢功能)，以及解析應用程式和服務的能力。</span><span class="sxs-lookup"><span data-stu-id="260fc-107">By default, **users** only have read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>

<span data-ttu-id="260fc-108">您可在建立叢集時為每個角色提供個別的憑證，以指定兩個用戶端角色 (系統管理員和用戶端)。</span><span class="sxs-lookup"><span data-stu-id="260fc-108">You specify the two client roles (administrator and client) at the time of cluster creation by providing separate certificates for each.</span></span> <span data-ttu-id="260fc-109">如需有關設定安全 Service Fabric 叢集的詳細資訊，請參閱 [Service Fabric 叢集安全性](service-fabric-cluster-security.md) 。</span><span class="sxs-lookup"><span data-stu-id="260fc-109">See [Service Fabric cluster security](service-fabric-cluster-security.md) for details on setting up a secure Service Fabric cluster.</span></span>

## <a name="default-access-control-settings"></a><span data-ttu-id="260fc-110">預設存取控制設定</span><span class="sxs-lookup"><span data-stu-id="260fc-110">Default access control settings</span></span>
<span data-ttu-id="260fc-111">系統管理員存取控制類型可以完整存取所有的 FabricClient API。</span><span class="sxs-lookup"><span data-stu-id="260fc-111">The administrator access control type has full access to all the FabricClient APIs.</span></span> <span data-ttu-id="260fc-112">它可以在 Service Fabric 叢集上執行任何讀取和寫入，包括下列作業：</span><span class="sxs-lookup"><span data-stu-id="260fc-112">It can perform any reads and writes on the Service Fabric cluster, including the following operations:</span></span>

### <a name="application-and-service-operations"></a><span data-ttu-id="260fc-113">應用程式和服務作業</span><span class="sxs-lookup"><span data-stu-id="260fc-113">Application and service operations</span></span>
* <span data-ttu-id="260fc-114">**CreateService**：建立服務</span><span class="sxs-lookup"><span data-stu-id="260fc-114">**CreateService**: service creation</span></span>                             
* <span data-ttu-id="260fc-115">**CreateServiceFromTemplate**：從範本建立服務</span><span class="sxs-lookup"><span data-stu-id="260fc-115">**CreateServiceFromTemplate**: service creation from template</span></span>                             
* <span data-ttu-id="260fc-116">**UpdateService**：更新服務</span><span class="sxs-lookup"><span data-stu-id="260fc-116">**UpdateService**: service updates</span></span>                             
* <span data-ttu-id="260fc-117">**DeleteService**：刪除服務</span><span class="sxs-lookup"><span data-stu-id="260fc-117">**DeleteService**: service deletion</span></span>                             
* <span data-ttu-id="260fc-118">**ProvisionApplicationType**：佈建應用程式類型</span><span class="sxs-lookup"><span data-stu-id="260fc-118">**ProvisionApplicationType**: application type provisioning</span></span>                             
* <span data-ttu-id="260fc-119">**CreateApplication**：建立應用程式</span><span class="sxs-lookup"><span data-stu-id="260fc-119">**CreateApplication**: application creation</span></span>                               
* <span data-ttu-id="260fc-120">**DeleteApplication**：刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="260fc-120">**DeleteApplication**: application deletion</span></span>                             
* <span data-ttu-id="260fc-121">**UpgradeApplication**：啟動或中斷應用程式升級</span><span class="sxs-lookup"><span data-stu-id="260fc-121">**UpgradeApplication**: starting or interrupting application upgrades</span></span>                             
* <span data-ttu-id="260fc-122">**UnprovisionApplicationType**：解除應用程式類型佈建</span><span class="sxs-lookup"><span data-stu-id="260fc-122">**UnprovisionApplicationType**: application type unprovisioning</span></span>                             
* <span data-ttu-id="260fc-123">**MoveNextUpgradeDomain**：以明確的更新網域繼續進行應用程式升級</span><span class="sxs-lookup"><span data-stu-id="260fc-123">**MoveNextUpgradeDomain**: resuming application upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="260fc-124">**ReportUpgradeHealth**：以目前的升級進度繼續進行應用程式升級</span><span class="sxs-lookup"><span data-stu-id="260fc-124">**ReportUpgradeHealth**: resuming application upgrades with the current upgrade progress</span></span>                             
* <span data-ttu-id="260fc-125">**ReportHealth**：回報健康狀態</span><span class="sxs-lookup"><span data-stu-id="260fc-125">**ReportHealth**: reporting health</span></span>                             
* <span data-ttu-id="260fc-126">**PredeployPackageToNode**：預先佈署 API</span><span class="sxs-lookup"><span data-stu-id="260fc-126">**PredeployPackageToNode**: predeployment API</span></span>                            
* <span data-ttu-id="260fc-127">**CodePackageControl**：重新啟動程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="260fc-127">**CodePackageControl**: restarting code packages</span></span>                             
* <span data-ttu-id="260fc-128">**RecoverPartition**：復原某個資料分割</span><span class="sxs-lookup"><span data-stu-id="260fc-128">**RecoverPartition**: recovering a partition</span></span>                             
* <span data-ttu-id="260fc-129">**RecoverPartitions**：復原多個資料分割</span><span class="sxs-lookup"><span data-stu-id="260fc-129">**RecoverPartitions**: recovering partitions</span></span>                             
* <span data-ttu-id="260fc-130">**RecoverServicePartitions**：復原服務分割</span><span class="sxs-lookup"><span data-stu-id="260fc-130">**RecoverServicePartitions**: recovering service partitions</span></span>                             
* <span data-ttu-id="260fc-131">**RecoverSystemPartitions**：復原系統服務分割</span><span class="sxs-lookup"><span data-stu-id="260fc-131">**RecoverSystemPartitions**: recovering system service partitions</span></span>                             

### <a name="cluster-operations"></a><span data-ttu-id="260fc-132">叢集作業</span><span class="sxs-lookup"><span data-stu-id="260fc-132">Cluster operations</span></span>
* <span data-ttu-id="260fc-133">**ProvisionFabric**：佈建 MSI 和/或叢集資訊清單</span><span class="sxs-lookup"><span data-stu-id="260fc-133">**ProvisionFabric**: MSI and/or cluster manifest provisioning</span></span>                             
* <span data-ttu-id="260fc-134">**UpgradeFabric**：啟動叢集升級</span><span class="sxs-lookup"><span data-stu-id="260fc-134">**UpgradeFabric**: starting cluster upgrades</span></span>                             
* <span data-ttu-id="260fc-135">**UnprovisionFabric**：解除 MSI 和/或叢集資訊清單佈建</span><span class="sxs-lookup"><span data-stu-id="260fc-135">**UnprovisionFabric**: MSI and/or cluster manifest unprovisioning</span></span>                         
* <span data-ttu-id="260fc-136">**MoveNextFabricUpgradeDomain**：以明確的更新網域繼續進行叢集升級</span><span class="sxs-lookup"><span data-stu-id="260fc-136">**MoveNextFabricUpgradeDomain**: resuming cluster upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="260fc-137">**ReportFabricUpgradeHealth**：以目前的升級進度繼續進行叢集升級</span><span class="sxs-lookup"><span data-stu-id="260fc-137">**ReportFabricUpgradeHealth**: resuming cluster upgrades with the current upgrade progress</span></span>                             
* <span data-ttu-id="260fc-138">**StartInfrastructureTask**：啟動基礎結構工作</span><span class="sxs-lookup"><span data-stu-id="260fc-138">**StartInfrastructureTask**: starting infrastructure tasks</span></span>                             
* <span data-ttu-id="260fc-139">**FinishInfrastructureTask**：完成基礎結構工作</span><span class="sxs-lookup"><span data-stu-id="260fc-139">**FinishInfrastructureTask**: finishing infrastructure tasks</span></span>                             
* <span data-ttu-id="260fc-140">**InvokeInfrastructureCommand**：基礎結構工作管理命令</span><span class="sxs-lookup"><span data-stu-id="260fc-140">**InvokeInfrastructureCommand**: infrastructure task management commands</span></span>                              
* <span data-ttu-id="260fc-141">**ActivateNode**：啟用節點</span><span class="sxs-lookup"><span data-stu-id="260fc-141">**ActivateNode**: activating a node</span></span>                             
* <span data-ttu-id="260fc-142">**DeactivateNode**：停用某個節點</span><span class="sxs-lookup"><span data-stu-id="260fc-142">**DeactivateNode**: deactivating a node</span></span>                             
* <span data-ttu-id="260fc-143">**DeactivateNodesBatch**：停用多個節點</span><span class="sxs-lookup"><span data-stu-id="260fc-143">**DeactivateNodesBatch**: deactivating multiple nodes</span></span>                             
* <span data-ttu-id="260fc-144">**RemoveNodeDeactivations**：還原多個節點上的停用</span><span class="sxs-lookup"><span data-stu-id="260fc-144">**RemoveNodeDeactivations**: reverting deactivation on multiple nodes</span></span>                             
* <span data-ttu-id="260fc-145">**GetNodeDeactivationStatus**：檢查停用狀態</span><span class="sxs-lookup"><span data-stu-id="260fc-145">**GetNodeDeactivationStatus**: checking deactivation status</span></span>                             
* <span data-ttu-id="260fc-146">**NodeStateRemoved**：回報已移除的節點狀態</span><span class="sxs-lookup"><span data-stu-id="260fc-146">**NodeStateRemoved**: reporting node state removed</span></span>                             
* <span data-ttu-id="260fc-147">**ReportFault**：回報錯誤</span><span class="sxs-lookup"><span data-stu-id="260fc-147">**ReportFault**: reporting fault</span></span>                             
* <span data-ttu-id="260fc-148">**FileContent**：映像存放區用戶端檔案傳輸 (叢集外部)</span><span class="sxs-lookup"><span data-stu-id="260fc-148">**FileContent**: image store client file transfer (external to cluster)</span></span>                             
* <span data-ttu-id="260fc-149">**FileDownload**：起始映像存放區用戶端檔案下載 (叢集外部)</span><span class="sxs-lookup"><span data-stu-id="260fc-149">**FileDownload**: image store client file download initiation (external to cluster)</span></span>                             
* <span data-ttu-id="260fc-150">**InternalList**：映像存放區用戶端檔案清單作業 (內部)</span><span class="sxs-lookup"><span data-stu-id="260fc-150">**InternalList**: image store client file list operation (internal)</span></span>                             
* <span data-ttu-id="260fc-151">**Delete**：映像存放區用戶端刪除作業</span><span class="sxs-lookup"><span data-stu-id="260fc-151">**Delete**: image store client delete operation</span></span>                              
* <span data-ttu-id="260fc-152">**Upload**：映像存放區用戶端上傳作業</span><span class="sxs-lookup"><span data-stu-id="260fc-152">**Upload**: image store client upload operation</span></span>                             
* <span data-ttu-id="260fc-153">**NodeControl**：啟動、停止及重新啟動節點</span><span class="sxs-lookup"><span data-stu-id="260fc-153">**NodeControl**: starting, stopping, and restarting nodes</span></span>                             
* <span data-ttu-id="260fc-154">**MoveReplicaControl**：將複本從一個節點移至另一個節點</span><span class="sxs-lookup"><span data-stu-id="260fc-154">**MoveReplicaControl**: moving replicas from one node to another</span></span>                             

### <a name="miscellaneous-operations"></a><span data-ttu-id="260fc-155">其他作業</span><span class="sxs-lookup"><span data-stu-id="260fc-155">Miscellaneous operations</span></span>
* <span data-ttu-id="260fc-156">**Ping**：用戶端 Ping</span><span class="sxs-lookup"><span data-stu-id="260fc-156">**Ping**: client pings</span></span>                             
* <span data-ttu-id="260fc-157">**Query**：所有允許的查詢</span><span class="sxs-lookup"><span data-stu-id="260fc-157">**Query**: all queries allowed</span></span>
* <span data-ttu-id="260fc-158">**NameExists**：檢查命名 URI 是否存在</span><span class="sxs-lookup"><span data-stu-id="260fc-158">**NameExists**: naming URI existence checks</span></span>                             

<span data-ttu-id="260fc-159">使用者存取控制類型預設限制為下列作業：</span><span class="sxs-lookup"><span data-stu-id="260fc-159">The user access control type is, by default, limited to the following operations:</span></span> 

* <span data-ttu-id="260fc-160">**EnumerateSubnames**：列舉命名 URI</span><span class="sxs-lookup"><span data-stu-id="260fc-160">**EnumerateSubnames**: naming URI enumeration</span></span>                             
* <span data-ttu-id="260fc-161">**EnumerateProperties**：列舉命名屬性</span><span class="sxs-lookup"><span data-stu-id="260fc-161">**EnumerateProperties**: naming property enumeration</span></span>                             
* <span data-ttu-id="260fc-162">**PropertyReadBatch**：命名屬性讀取作業</span><span class="sxs-lookup"><span data-stu-id="260fc-162">**PropertyReadBatch**: naming property read operations</span></span>                             
* <span data-ttu-id="260fc-163">**GetServiceDescription**：長時間輪詢服務通知和讀取服務描述</span><span class="sxs-lookup"><span data-stu-id="260fc-163">**GetServiceDescription**: long-poll service notifications and reading service descriptions</span></span>                             
* <span data-ttu-id="260fc-164">**ResolveService**：抱怨型服務解析</span><span class="sxs-lookup"><span data-stu-id="260fc-164">**ResolveService**: complaint-based service resolution</span></span>                             
* <span data-ttu-id="260fc-165">**ResolveNameOwner**：解析命名 URI 擁有者</span><span class="sxs-lookup"><span data-stu-id="260fc-165">**ResolveNameOwner**: resolving naming URI owner</span></span>                             
* <span data-ttu-id="260fc-166">**ResolvePartition**：解析系統服務</span><span class="sxs-lookup"><span data-stu-id="260fc-166">**ResolvePartition**: resolving system services</span></span>                             
* <span data-ttu-id="260fc-167">**ServiceNotifications**：事件型服務通知</span><span class="sxs-lookup"><span data-stu-id="260fc-167">**ServiceNotifications**: event-based service notifications</span></span>                             
* <span data-ttu-id="260fc-168">**GetUpgradeStatus**：輪詢應用程式升級狀態</span><span class="sxs-lookup"><span data-stu-id="260fc-168">**GetUpgradeStatus**: polling application upgrade status</span></span>                             
* <span data-ttu-id="260fc-169">**GetFabricUpgradeStatus**：輪詢叢集升級狀態</span><span class="sxs-lookup"><span data-stu-id="260fc-169">**GetFabricUpgradeStatus**: polling cluster upgrade status</span></span>                             
* <span data-ttu-id="260fc-170">**InvokeInfrastructureQuery**：查詢基礎結構工作</span><span class="sxs-lookup"><span data-stu-id="260fc-170">**InvokeInfrastructureQuery**: querying infrastructure tasks</span></span>                             
* <span data-ttu-id="260fc-171">**List**：映像存放區用戶端檔案清單作業</span><span class="sxs-lookup"><span data-stu-id="260fc-171">**List**: image store client file list operation</span></span>                             
* <span data-ttu-id="260fc-172">**ResetPartitionLoad**：重設容錯移轉單元的載入</span><span class="sxs-lookup"><span data-stu-id="260fc-172">**ResetPartitionLoad**: resetting load for a failover unit</span></span>                             
* <span data-ttu-id="260fc-173">**ToggleVerboseServicePlacementHealthReporting**：切換詳細服務位置健康情況報告</span><span class="sxs-lookup"><span data-stu-id="260fc-173">**ToggleVerboseServicePlacementHealthReporting**: toggling verbose service placement health reporting</span></span>                             

<span data-ttu-id="260fc-174">系統管理員存取控制也可存取上述作業。</span><span class="sxs-lookup"><span data-stu-id="260fc-174">The admin access control also has access to the preceding operations.</span></span>

## <a name="changing-default-settings-for-client-roles"></a><span data-ttu-id="260fc-175">變更用戶端角色的預設設定</span><span class="sxs-lookup"><span data-stu-id="260fc-175">Changing default settings for client roles</span></span>
<span data-ttu-id="260fc-176">在叢集資訊清單檔案中，您可以視需要提供系統管理員功能給用戶端。</span><span class="sxs-lookup"><span data-stu-id="260fc-176">In the cluster manifest file, you can provide admin capabilities to the client if needed.</span></span> <span data-ttu-id="260fc-177">您可以在[建立叢集](service-fabric-cluster-creation-via-portal.md)時，前往 [Fabric 設定] 選項，並在 [名稱]、[系統管理員]、[使用者] 和 [值] 欄位中提供上述設定來變更預設值。</span><span class="sxs-lookup"><span data-stu-id="260fc-177">You can change the defaults by going to the **Fabric Settings** option during [cluster creation](service-fabric-cluster-creation-via-portal.md), and providing the preceding settings in the **name**, **admin**, **user**, and **value** fields.</span></span>

## <a name="next-steps"></a><span data-ttu-id="260fc-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="260fc-178">Next steps</span></span>
[<span data-ttu-id="260fc-179">Service Fabric 叢集安全性</span><span class="sxs-lookup"><span data-stu-id="260fc-179">Service Fabric cluster security</span></span>](service-fabric-cluster-security.md)

[<span data-ttu-id="260fc-180">Service Fabric 叢集建立</span><span class="sxs-lookup"><span data-stu-id="260fc-180">Service Fabric cluster creation</span></span>](service-fabric-cluster-creation-via-portal.md)

