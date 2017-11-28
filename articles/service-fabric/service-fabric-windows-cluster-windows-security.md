---
title: "叢集執行於 Windows 上使用 Windows 安全性 aaaSecure |Microsoft 文件"
description: "了解如何在獨立的 tooconfigure 節點對節點和用戶端對節點安全性叢集執行於 Windows 上使用 Windows 安全性。"
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
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="18314-103">使用 Windows 安全性保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="18314-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="18314-104">tooprevent 未經授權存取 tooa Service Fabric 叢集，您必須保護 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="18314-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="18314-105">Hello 叢集中執行生產工作負載時，安全性是特別重要。</span><span class="sxs-lookup"><span data-stu-id="18314-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="18314-106">本文說明如何在 hello 中使用 Windows 安全性的 tooconfigure 節點對節點和用戶端對節點安全性*追蹤*檔案。</span><span class="sxs-lookup"><span data-stu-id="18314-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="18314-107">hello 程序對應 toohello 設定的安全性步驟[建立在 Windows 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="18314-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="18314-108">如需有關 Service Fabric 如何使用 Windows 安全性的詳細資訊，請參閱[叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="18314-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="18314-109">因為沒有從一個安全性選擇 tooanother 含叢集升級，您應該仔細思考 hello 選取的節點到節點的安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="18314-110">toochange hello 安全性選取項目，您有 toorebuild hello 完整的叢集。</span><span class="sxs-lookup"><span data-stu-id="18314-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="18314-111">使用 gMSA 設定 Windows 安全性</span><span class="sxs-lookup"><span data-stu-id="18314-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="18314-112">hello 範例*ClusterConfig.gMSA.Windows.MultiMachine.JSON*下載組態檔，以 hello [Microsoft.Azure.ServiceFabric.WindowsServer。<version>。zip](http://go.microsoft.com/fwlink/?LinkId=730690)獨立叢集封裝包含的範本設定使用 Windows 安全性[群組受管理服務帳戶 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="18314-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

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
  
| <span data-ttu-id="18314-113">**組態設定**</span><span class="sxs-lookup"><span data-stu-id="18314-113">**Configuration Setting**</span></span> | <span data-ttu-id="18314-114">**說明**</span><span class="sxs-lookup"><span data-stu-id="18314-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="18314-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="18314-115">WindowsIdentities</span></span> |<span data-ttu-id="18314-116">包含 hello 叢集和用戶端識別。</span><span class="sxs-lookup"><span data-stu-id="18314-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="18314-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="18314-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="18314-118">設定節點對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-118">Configures node-to-node security.</span></span> <span data-ttu-id="18314-119">群組受管理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="18314-119">A group managed service account.</span></span> |  
| <span data-ttu-id="18314-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="18314-120">ClusterSPN</span></span> |<span data-ttu-id="18314-121">gMSA 帳戶的完整網域名稱 SPN</span><span class="sxs-lookup"><span data-stu-id="18314-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="18314-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="18314-122">ClientIdentities</span></span> |<span data-ttu-id="18314-123">設定用戶端對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-123">Configures client-to-node security.</span></span> <span data-ttu-id="18314-124">用戶端使用者帳戶的陣列。</span><span class="sxs-lookup"><span data-stu-id="18314-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="18314-125">身分識別</span><span class="sxs-lookup"><span data-stu-id="18314-125">Identity</span></span> |<span data-ttu-id="18314-126">hello 用戶端身分識別，網域使用者。</span><span class="sxs-lookup"><span data-stu-id="18314-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="18314-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="18314-127">IsAdmin</span></span> |<span data-ttu-id="18314-128">True 會指定該 hello 網域使用者具有系統管理員用戶端存取，讓使用者用戶端存取，則為 false。</span><span class="sxs-lookup"><span data-stu-id="18314-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="18314-129">[節點 toonode 安全性](service-fabric-cluster-security.md#node-to-node-security)蒻謔設定**ClustergMSAIdentity**當 service fabric 需要 toorun 下 gMSA。</span><span class="sxs-lookup"><span data-stu-id="18314-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="18314-130">在訂單 toobuild 節點之間的信任關係，他們必須撰寫知道彼此的存在。</span><span class="sxs-lookup"><span data-stu-id="18314-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="18314-131">即可達成這兩個不同的方式： 指定 hello 群組受管理的服務帳戶，其中包含 hello 叢集中的所有節點，或指定都包含 hello 叢集中的所有節點的 hello 網域電腦群組。</span><span class="sxs-lookup"><span data-stu-id="18314-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="18314-132">我們強烈建議使用 hello[群組受管理服務帳戶 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)方法，特別是針對較大叢集 （10 個以上的節點），或可能 toogrow 或縮小叢集。</span><span class="sxs-lookup"><span data-stu-id="18314-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="18314-133">這個方法不需要 hello 建立網域群組的叢集系統管理員已授與存取權限 tooadd 和移除成員。</span><span class="sxs-lookup"><span data-stu-id="18314-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="18314-134">進行自動密碼管理時，這些帳戶也很有用。</span><span class="sxs-lookup"><span data-stu-id="18314-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="18314-135">如需詳細資訊，請參閱 [開始使用群組受管理的服務帳戶](http://technet.microsoft.com/library/jj128431.aspx)。</span><span class="sxs-lookup"><span data-stu-id="18314-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="18314-136">[用戶端 toonode 安全性](service-fabric-cluster-security.md#client-to-node-security)已設定為使用**ClientIdentities**。</span><span class="sxs-lookup"><span data-stu-id="18314-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="18314-137">在用戶端與 hello 叢集之間的順序 tooestablish 信任，您必須設定 hello 叢集 tooknow 可以信任哪些用戶端身分識別。</span><span class="sxs-lookup"><span data-stu-id="18314-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="18314-138">這可以在兩個不同的方式完成： 指定 hello 網域群組使用者可以連接，或指定 hello 網域節點使用者可以連線。</span><span class="sxs-lookup"><span data-stu-id="18314-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="18314-139">Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa Service Fabric 叢集： 系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="18314-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="18314-140">存取控制提供 hello hello 能力叢集系統管理員 toolimit 存取 toocertain 類型的使用者，使 hello 叢集更安全的不同群組的叢集操作。</span><span class="sxs-lookup"><span data-stu-id="18314-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="18314-141">系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。</span><span class="sxs-lookup"><span data-stu-id="18314-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="18314-142">使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="18314-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="18314-143">如需存取控制的詳細資訊，請參閱[角色型存取控制 (適用於 Service Fabric 用戶端)](service-fabric-cluster-security-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="18314-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="18314-144">下列範例 hello**安全性**區段設定使用 gMSA 的 Windows 安全性，並指定該 hello 機器中*ServiceFabric.clusterA.contoso.com* gMSA 屬於 hello 叢集，*CONTOSO\usera*具有系統管理員用戶端存取權：</span><span class="sxs-lookup"><span data-stu-id="18314-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
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
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="18314-145">使用電腦群組設定 Windows 安全性</span><span class="sxs-lookup"><span data-stu-id="18314-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="18314-146">hello 範例*ClusterConfig.Windows.MultiMachine.JSON*下載組態檔，以 hello [Microsoft.Azure.ServiceFabric.WindowsServer。<version>。zip](http://go.microsoft.com/fwlink/?LinkId=730690)獨立叢集封裝包含的範本設定 Windows 安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="18314-147">Windows 安全性設定中 hello**屬性**> 一節：</span><span class="sxs-lookup"><span data-stu-id="18314-147">Windows security is configured in hello **Properties** section:</span></span> 

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

| <span data-ttu-id="18314-148">**組態設定**</span><span class="sxs-lookup"><span data-stu-id="18314-148">**Configuration setting**</span></span> | <span data-ttu-id="18314-149">**說明**</span><span class="sxs-lookup"><span data-stu-id="18314-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="18314-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="18314-150">ClusterCredentialType</span></span> |<span data-ttu-id="18314-151">**ClusterCredentialType**設定得*Windows*如果 ClusterIdentity 指定 Active Directory 電腦群組名稱。</span><span class="sxs-lookup"><span data-stu-id="18314-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="18314-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="18314-152">ServerCredentialType</span></span> |<span data-ttu-id="18314-153">設定得*Windows* tooenable 用戶端的 Windows 安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="18314-154">這表示 hello hello 叢集和 hello 叢集本身的用戶端正在執行 Active Directory 網域內。</span><span class="sxs-lookup"><span data-stu-id="18314-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="18314-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="18314-155">WindowsIdentities</span></span> |<span data-ttu-id="18314-156">包含 hello 叢集和用戶端識別。</span><span class="sxs-lookup"><span data-stu-id="18314-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="18314-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="18314-157">ClusterIdentity</span></span> |<span data-ttu-id="18314-158">使用電腦群組名稱、 domain\machinegroup、 tooconfigure 節點對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="18314-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="18314-159">ClientIdentities</span></span> |<span data-ttu-id="18314-160">設定用戶端對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="18314-160">Configures client-to-node security.</span></span> <span data-ttu-id="18314-161">用戶端使用者帳戶的陣列。</span><span class="sxs-lookup"><span data-stu-id="18314-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="18314-162">身分識別</span><span class="sxs-lookup"><span data-stu-id="18314-162">Identity</span></span> |<span data-ttu-id="18314-163">加入 hello 網域使用者，網域 \ 使用者名稱，如 hello 用戶端身分識別。</span><span class="sxs-lookup"><span data-stu-id="18314-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="18314-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="18314-164">IsAdmin</span></span> |<span data-ttu-id="18314-165">Hello 網域使用者的設定 tootrue toospecify 具有系統管理員用戶端存取權或 false，供使用者用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="18314-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="18314-166">[節點 toonode 安全性](service-fabric-cluster-security.md#node-to-node-security)已設定使用**ClusterIdentity**如果您想 toouse Active Directory 網域內的電腦群組。</span><span class="sxs-lookup"><span data-stu-id="18314-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="18314-167">如需詳細資訊，請參閱[在 Active Directory 中建立電腦群組 (Create a Machine Group in Active Directory)](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx)。</span><span class="sxs-lookup"><span data-stu-id="18314-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="18314-168">[用戶端對節點安全性](service-fabric-cluster-security.md#client-to-node-security)是使用 **ClientIdentities** 來設定的。</span><span class="sxs-lookup"><span data-stu-id="18314-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="18314-169">tooestablish 之間的信任的用戶端與 hello 叢集中，您必須設定 hello 叢集 tooknow hello 用戶端 hello 叢集的身分識別可以信任。</span><span class="sxs-lookup"><span data-stu-id="18314-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="18314-170">您可以透過兩種不同方式建立信任︰</span><span class="sxs-lookup"><span data-stu-id="18314-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="18314-171">指定可以連接的 hello 網域群組使用者。</span><span class="sxs-lookup"><span data-stu-id="18314-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="18314-172">指定可以連接的 hello 網域節點使用者。</span><span class="sxs-lookup"><span data-stu-id="18314-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="18314-173">Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa Service Fabric 叢集： 系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="18314-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="18314-174">存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 類型的叢集操作的不同使用者群組，這會讓 hello 叢集更安全。</span><span class="sxs-lookup"><span data-stu-id="18314-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="18314-175">系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。</span><span class="sxs-lookup"><span data-stu-id="18314-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="18314-176">使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="18314-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="18314-177">下列範例 hello**安全性**區段設定 Windows 安全性，以指定該 hello 機器*ServiceFabric/clusterA.contoso.com*是 hello 叢集的一部分，並指定該*CONTOSO\usera*具有系統管理員用戶端存取權：</span><span class="sxs-lookup"><span data-stu-id="18314-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

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
> <span data-ttu-id="18314-178">不應在網域控制站上部署 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="18314-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="18314-179">請確定追蹤不會不使用電腦群組時，包含 hello hello 網域控制站的 IP 位址或群組受管理的服務帳戶 (gMSA)。</span><span class="sxs-lookup"><span data-stu-id="18314-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="18314-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18314-180">Next steps</span></span>
<span data-ttu-id="18314-181">在 hello 中設定 Windows 安全性之後*追蹤*檔案時，請繼續 hello 叢集建立程序中的[建立在 Windows 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="18314-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="18314-182">如需有關節點對節點安全性、用戶端對節點安全性和角色型存取控制的詳細資訊，請參閱[叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="18314-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="18314-183">請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)如需使用 PowerShell 或 FabricClient 連接的範例。</span><span class="sxs-lookup"><span data-stu-id="18314-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
