---
title: "使用 Windows 安全性保護在 Windows 上執行的叢集 | Microsoft Docs"
description: "了解如何使用 Windows 安全性在 Windows 上執行的獨立叢集上設定節點對節點和用戶端對節點安全性。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: e093a631b0cf81195981a8e3d345504ebce02723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="f6d13-103">使用 Windows 安全性保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="f6d13-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="f6d13-104">為避免有人未經授權存取 Service Fabric 叢集，您必須保護叢集。</span><span class="sxs-lookup"><span data-stu-id="f6d13-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="f6d13-105">當叢集執行生產工作負載時，安全性尤其重要。</span><span class="sxs-lookup"><span data-stu-id="f6d13-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="f6d13-106">本文說明如何在 *ClusterConfig.JSON* 檔案中使用 Windows 安全性，設定節點對節點和用戶端對節點的安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="f6d13-107">此程序會對應[建立在 Windows 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)的設定安全性步驟。</span><span class="sxs-lookup"><span data-stu-id="f6d13-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="f6d13-108">如需有關 Service Fabric 如何使用 Windows 安全性的詳細資訊，請參閱[叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f6d13-109">請仔細考慮選擇節點對節點安全性，因為您無法選擇將叢集從某種安全性升級到另一種安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="f6d13-110">若要變更安全性選擇，您必須重建完整叢集。</span><span class="sxs-lookup"><span data-stu-id="f6d13-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="f6d13-111">使用 gMSA 設定 Windows 安全性</span><span class="sxs-lookup"><span data-stu-id="f6d13-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="f6d13-112">隨著 [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) 獨立叢集封裝下載的範例 *ClusterConfig.gMSA.Windows.MultiMachine.JSON* 組態檔，包含可供使用[群組受管理服務帳戶 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) 來設定 Windows 安全性的範本：</span><span class="sxs-lookup"><span data-stu-id="f6d13-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="f6d13-113">**組態設定**</span><span class="sxs-lookup"><span data-stu-id="f6d13-113">**Configuration Setting**</span></span> | <span data-ttu-id="f6d13-114">**說明**</span><span class="sxs-lookup"><span data-stu-id="f6d13-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="f6d13-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="f6d13-115">WindowsIdentities</span></span> |<span data-ttu-id="f6d13-116">包含叢集和用戶端身分識別。</span><span class="sxs-lookup"><span data-stu-id="f6d13-116">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="f6d13-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="f6d13-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="f6d13-118">設定節點對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-118">Configures node-to-node security.</span></span> <span data-ttu-id="f6d13-119">群組受管理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6d13-119">A group managed service account.</span></span> |  
| <span data-ttu-id="f6d13-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="f6d13-120">ClusterSPN</span></span> |<span data-ttu-id="f6d13-121">gMSA 帳戶的完整網域名稱 SPN</span><span class="sxs-lookup"><span data-stu-id="f6d13-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="f6d13-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="f6d13-122">ClientIdentities</span></span> |<span data-ttu-id="f6d13-123">設定用戶端對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-123">Configures client-to-node security.</span></span> <span data-ttu-id="f6d13-124">用戶端使用者帳戶的陣列。</span><span class="sxs-lookup"><span data-stu-id="f6d13-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="f6d13-125">身分識別</span><span class="sxs-lookup"><span data-stu-id="f6d13-125">Identity</span></span> |<span data-ttu-id="f6d13-126">用戶端身分識別，即網域使用者。</span><span class="sxs-lookup"><span data-stu-id="f6d13-126">The client identity, a domain user.</span></span> |  
| <span data-ttu-id="f6d13-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="f6d13-127">IsAdmin</span></span> |<span data-ttu-id="f6d13-128">True 表示網域使用者具有系統管理員用戶端存取，False 表示具有使用者用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="f6d13-128">True specifies that the domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="f6d13-129">需要在 gMSA 下執行 Service Fabric 時，可透過 **ClustergMSAIdentity** 來設定[節點對節點安全性](service-fabric-cluster-security.md#node-to-node-security)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="f6d13-130">為了建置節點之間的信任關係，它們必須注意彼此。</span><span class="sxs-lookup"><span data-stu-id="f6d13-130">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="f6d13-131">有兩種不同的方式可達成此目的︰指定群組受管理服務帳戶 (其中包含叢集中的所有節點)，或指定包含叢集中所有節點的網域電腦群組。</span><span class="sxs-lookup"><span data-stu-id="f6d13-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="f6d13-132">強烈建議使用 [群組受管理服務帳戶 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) 方法，特別適合於較大型的叢集 (超過 10 個節點) 或可能會擴大或縮小的叢集。</span><span class="sxs-lookup"><span data-stu-id="f6d13-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="f6d13-133">此方法不需要建立叢集系統管理員已獲得存取權限的網域群組，即可加入和移除成員。</span><span class="sxs-lookup"><span data-stu-id="f6d13-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="f6d13-134">進行自動密碼管理時，這些帳戶也很有用。</span><span class="sxs-lookup"><span data-stu-id="f6d13-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="f6d13-135">如需詳細資訊，請參閱 [開始使用群組受管理的服務帳戶](http://technet.microsoft.com/library/jj128431.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="f6d13-136">[ClientIdentities](service-fabric-cluster-security.md#client-to-node-security) 可設定 **ClientIdentities**的設定安全性步驟。</span><span class="sxs-lookup"><span data-stu-id="f6d13-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="f6d13-137">若要建立用戶端與叢集之間的信任，您必須設定叢集才能知道用戶端可以信任的身分識別。</span><span class="sxs-lookup"><span data-stu-id="f6d13-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="f6d13-138">有兩種不同的方式可達成此目的︰指定可以連線的網域群組使用者，或指定可以連線的網域節點使用者。</span><span class="sxs-lookup"><span data-stu-id="f6d13-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="f6d13-139">Service Fabric 針對連線到 Service Fabric 叢集的用戶端，支援兩種不同的存取控制類型：系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="f6d13-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="f6d13-140">存取控制可讓叢集系統管理員針對不同的使用者群組限制特定類型的叢集作業的存取權，讓叢集更加安全。</span><span class="sxs-lookup"><span data-stu-id="f6d13-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="f6d13-141">系統管理員可以完整存取管理功能 (包括讀取/寫入功能)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-141">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="f6d13-142">使用者預設只具有管理功能的讀取存取權 (例如查詢功能)，以及解析應用程式和服務的能力。</span><span class="sxs-lookup"><span data-stu-id="f6d13-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="f6d13-143">如需存取控制的詳細資訊，請參閱[角色型存取控制 (適用於 Service Fabric 用戶端)](service-fabric-cluster-security-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="f6d13-144">下列範例 **security** 區段可使用 gMSA 設定 Windows 安全性，並指定 *ServiceFabric.clusterA.contoso.com* gMSA 中的電腦隸屬於叢集，而 *CONTOSO\usera* 具有系統管理員用戶端存取權︰</span><span class="sxs-lookup"><span data-stu-id="f6d13-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="f6d13-145">使用電腦群組設定 Windows 安全性</span><span class="sxs-lookup"><span data-stu-id="f6d13-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="f6d13-146">隨著 [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) 獨立叢集封裝下載的範例 *ClusterConfig.Windows.MultiMachine.JSON* 組態檔包含可供設定 Windows 安全性的範本。</span><span class="sxs-lookup"><span data-stu-id="f6d13-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="f6d13-147">Windows 安全性於 **Properties** 區段中設定︰</span><span class="sxs-lookup"><span data-stu-id="f6d13-147">Windows security is configured in the **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="f6d13-148">**組態設定**</span><span class="sxs-lookup"><span data-stu-id="f6d13-148">**Configuration setting**</span></span> | <span data-ttu-id="f6d13-149">**說明**</span><span class="sxs-lookup"><span data-stu-id="f6d13-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f6d13-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="f6d13-150">ClusterCredentialType</span></span> |<span data-ttu-id="f6d13-151">如果 ClusterIdentity 指定 Active Directory 電腦群組名稱，則 **ClusterCredentialType** 會設定為 *Windows*。</span><span class="sxs-lookup"><span data-stu-id="f6d13-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="f6d13-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="f6d13-152">ServerCredentialType</span></span> |<span data-ttu-id="f6d13-153">設定為 [Windows] 可為用戶端啟用 Windows 安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-153">Set to *Windows* to enable Windows security for clients.</span></span><br /><br /><span data-ttu-id="f6d13-154">這表示叢集的用戶端和叢集本身都在 Active Directory 網域內執行。</span><span class="sxs-lookup"><span data-stu-id="f6d13-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="f6d13-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="f6d13-155">WindowsIdentities</span></span> |<span data-ttu-id="f6d13-156">包含叢集和用戶端身分識別。</span><span class="sxs-lookup"><span data-stu-id="f6d13-156">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="f6d13-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="f6d13-157">ClusterIdentity</span></span> |<span data-ttu-id="f6d13-158">使用電腦群組名稱 (domain\machinegroup) 來設定節點對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="f6d13-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="f6d13-159">ClientIdentities</span></span> |<span data-ttu-id="f6d13-160">設定用戶端對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="f6d13-160">Configures client-to-node security.</span></span> <span data-ttu-id="f6d13-161">用戶端使用者帳戶的陣列。</span><span class="sxs-lookup"><span data-stu-id="f6d13-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="f6d13-162">身分識別</span><span class="sxs-lookup"><span data-stu-id="f6d13-162">Identity</span></span> |<span data-ttu-id="f6d13-163">新增網域使用者 (domain\username) 以做為用戶端身分識別。</span><span class="sxs-lookup"><span data-stu-id="f6d13-163">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="f6d13-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="f6d13-164">IsAdmin</span></span> |<span data-ttu-id="f6d13-165">設定為 true 可指定網域使用者具有系統管理員用戶端存取權，設定為 false 則具有使用者用戶端存取權。</span><span class="sxs-lookup"><span data-stu-id="f6d13-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="f6d13-166">如果您想要使用 Active Directory 網域內的電腦群組，可使用 **ClusterIdentity** 來設定[節點對節點安全性](service-fabric-cluster-security.md#node-to-node-security)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="f6d13-167">如需詳細資訊，請參閱[在 Active Directory 中建立電腦群組 (Create a Machine Group in Active Directory)](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="f6d13-168">[用戶端對節點安全性](service-fabric-cluster-security.md#client-to-node-security)是使用 **ClientIdentities** 來設定的。</span><span class="sxs-lookup"><span data-stu-id="f6d13-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="f6d13-169">若要在用戶端與叢集之間建立信任，您必須設定叢集，讓叢集知道它可以信任的用戶端身分識別。</span><span class="sxs-lookup"><span data-stu-id="f6d13-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="f6d13-170">您可以透過兩種不同方式建立信任︰</span><span class="sxs-lookup"><span data-stu-id="f6d13-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="f6d13-171">指定可以連線的網域群組使用者。</span><span class="sxs-lookup"><span data-stu-id="f6d13-171">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="f6d13-172">指定可以連線的網域節點使用者。</span><span class="sxs-lookup"><span data-stu-id="f6d13-172">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="f6d13-173">Service Fabric 針對連線到 Service Fabric 叢集的用戶端，支援兩種不同的存取控制類型：系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="f6d13-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="f6d13-174">存取控制可讓叢集系統管理員針對不同的使用者群組限制特定類型的叢集作業的存取權，讓叢集更加安全。</span><span class="sxs-lookup"><span data-stu-id="f6d13-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="f6d13-175">系統管理員可以完整存取管理功能 (包括讀取/寫入功能)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-175">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="f6d13-176">使用者預設只具有管理功能的讀取存取權 (例如查詢功能)，以及解析應用程式和服務的能力。</span><span class="sxs-lookup"><span data-stu-id="f6d13-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="f6d13-177">下列範例 **security** 區段可設定 Windows 安全性，指定 ServiceFabric/clusterA.contoso.com 中的電腦隸屬於叢集，並指定 CONTOSO\usera 具有系統管理員用戶端存取權︰</span><span class="sxs-lookup"><span data-stu-id="f6d13-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="f6d13-178">不應在網域控制站上部署 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="f6d13-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="f6d13-179">請確定在使用電腦群組或群組受管理服務帳戶 (gMSA) 時，ClusterConfig.json 不會包含網域控制站的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f6d13-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f6d13-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6d13-180">Next steps</span></span>
<span data-ttu-id="f6d13-181">在 *ClusterConfig.JSON* 檔案中設定 Windows 安全性之後，繼續進行 [建立在 Windows 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)中的叢集建立程序。</span><span class="sxs-lookup"><span data-stu-id="f6d13-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="f6d13-182">如需有關節點對節點安全性、用戶端對節點安全性和角色型存取控制的詳細資訊，請參閱[叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="f6d13-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="f6d13-183">如需使用 PowerShell 或 FabricClient 來連線的範例，請參閱[連線到安全的叢集](service-fabric-connect-to-secure-cluster.md) 。</span><span class="sxs-lookup"><span data-stu-id="f6d13-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
