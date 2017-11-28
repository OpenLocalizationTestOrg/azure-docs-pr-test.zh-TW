---
title: "aaaCreate Service Fabric 叢集 hello Azure 入口網站 |Microsoft 文件"
description: "本文說明如何在 Azure 中，使用安全的 Service Fabric 叢集 tooset hello Azure 入口網站與 Azure 金鑰保存庫。"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="26901-103">使用 hello Azure 入口網站在 Azure 中建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="26901-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26901-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="26901-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="26901-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="26901-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="26901-106">這是引導您設定安全 Service Fabric 叢集使用 hello Azure 入口網站在 Azure 中的 hello 步驟的逐步指南。</span><span class="sxs-lookup"><span data-stu-id="26901-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="26901-107">本指南會引導您 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="26901-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="26901-108">設定叢集安全性金鑰保存庫 toomanage 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="26901-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="26901-109">在 Azure 中建立受保護的叢集，透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="26901-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="26901-110">使用憑證驗證系統管理員。</span><span class="sxs-lookup"><span data-stu-id="26901-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="26901-111">如需更進階的安全性選項 (例如使用 Azure Active Directory 進行使用者驗證及設定應用程式安全性的憑證)，請參閱[使用 Azure Resource Manager 建立您的叢集][create-cluster-arm]。</span><span class="sxs-lookup"><span data-stu-id="26901-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="26901-112">需要安全的叢集，叢集來防止未經授權的存取 toomanagement 作業，包括部署、 升級和刪除應用程式、 服務和 hello 它們包含的資料。</span><span class="sxs-lookup"><span data-stu-id="26901-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="26901-113">不安全的叢集是叢集的任何人都可以用來連接 tooat 任何時間，並執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="26901-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="26901-114">雖然您可能 toocreate 不安全的叢集，它是**強烈建議安全叢集 toocreate**。</span><span class="sxs-lookup"><span data-stu-id="26901-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="26901-115">不安全的叢集 **無法在事後保護其安全** - 必須建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="26901-116">hello 概念是 hello 相同的 hello 叢集 Linux 叢集或 Windows 叢集是否建立安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="26901-117">如需建立安全 Linux 叢集的詳細資訊和協助程式指令碼，請參閱[在 Linux 上建立安全叢集](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters)。</span><span class="sxs-lookup"><span data-stu-id="26901-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="26901-118">hello hello 所提供的協助程式指令碼所取得的參數可以輸入 hello 入口網站直接在 hello > 一節中所述[hello Azure 入口網站中建立叢集](#create-cluster-portal)。</span><span class="sxs-lookup"><span data-stu-id="26901-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="26901-119">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="26901-119">Log in tooAzure</span></span>
<span data-ttu-id="26901-120">本指南使用 [Azure PowerShell][azure-powershell]。</span><span class="sxs-lookup"><span data-stu-id="26901-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="26901-121">當啟動新的 PowerShell 工作階段時，登入 tooyour Azure 帳戶，然後選取您的訂用帳戶，然後再執行 Azure 的命令。</span><span class="sxs-lookup"><span data-stu-id="26901-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="26901-122">登入 tooyour azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="26901-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="26901-123">選取您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="26901-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="26901-124">設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="26901-124">Set up Key Vault</span></span>
<span data-ttu-id="26901-125">Hello 指南的這個部分會引導您建立金鑰保存庫在 Azure 中的 Service Fabric 叢集和 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="26901-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="26901-126">在金鑰保存庫的完整指南，請參閱 hello[金鑰保存庫快速入門指南][key-vault-get-started]。</span><span class="sxs-lookup"><span data-stu-id="26901-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="26901-127">服務網狀架構會使用 X.509 憑證 toosecure 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="26901-128">Azure 金鑰保存庫是使用的 toomanage 憑證在 Azure 中的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="26901-129">在 Azure 中部署叢集時，hello Azure 資源提供者負責建立 Service Fabric 叢集會提取從金鑰保存庫的憑證，並 hello 叢集 Vm 上進行安裝。</span><span class="sxs-lookup"><span data-stu-id="26901-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="26901-130">hello 下列圖表說明 hello 金鑰保存庫、 Service Fabric 叢集和使用憑證時它會建立叢集儲存在金鑰保存庫中的 hello Azure 資源提供者之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="26901-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![憑證安裝][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="26901-132">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="26901-132">Create a Resource Group</span></span>
<span data-ttu-id="26901-133">hello 第一個步驟是 toocreate 特別針對金鑰保存庫的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="26901-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="26901-134">將金鑰保存庫放入自己的資源群組建議，讓您可以移除-例如 hello 有 Service Fabric 叢集資源群組-運算和存放裝置資源群組，而不會遺失您的金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="26901-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="26901-135">hello 具有您金鑰保存庫的資源群組必須在 hello 與正在使用它的 hello 叢集相同的區域。</span><span class="sxs-lookup"><span data-stu-id="26901-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="26901-136">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="26901-136">Create Key Vault</span></span>
<span data-ttu-id="26901-137">Hello 新資源群組中建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="26901-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="26901-138">金鑰保存庫 hello**必須為部署啟用**tooallow hello Service Fabric 資源提供者從它的 tooget 憑證並安裝在叢集節點上：</span><span class="sxs-lookup"><span data-stu-id="26901-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

<span data-ttu-id="26901-139">如果您有現有金鑰保存庫，可以使用 Azure CLI 將它啟用以用於部署：</span><span class="sxs-lookup"><span data-stu-id="26901-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="26901-140">新增憑證 tooKey 保存庫</span><span class="sxs-lookup"><span data-stu-id="26901-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="26901-141">憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。</span><span class="sxs-lookup"><span data-stu-id="26901-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="26901-142">如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例][service-fabric-cluster-security]。</span><span class="sxs-lookup"><span data-stu-id="26901-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="26901-143">叢集和伺服器憑證 (必要)</span><span class="sxs-lookup"><span data-stu-id="26901-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="26901-144">此憑證是必要的 toosecure 叢集，並防止未經授權的存取 tooit。</span><span class="sxs-lookup"><span data-stu-id="26901-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="26901-145">它會透過幾種方式提供叢集安全性：</span><span class="sxs-lookup"><span data-stu-id="26901-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="26901-146">**叢集驗證：** 驗證叢集同盟的節點對節點通訊。</span><span class="sxs-lookup"><span data-stu-id="26901-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="26901-147">可以證明其身分識別與此憑證的節點可以加入 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="26901-148">**伺服器驗證：** hello 叢集管理端點 tooa 管理會用戶端驗證，以便 hello 管理用戶端會知道它正在交涉 toohello 實際叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="26901-149">此憑證也可提供 SSL hello HTTPS 管理 API 與 Service Fabric 總管透過 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="26901-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="26901-150">這些的考量，hello 憑證必須符合下列需求的 hello tooserve:</span><span class="sxs-lookup"><span data-stu-id="26901-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="26901-151">hello 憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="26901-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="26901-152">金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="26901-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="26901-153">hello 憑證的主體名稱必須符合 hello 用網域 tooaccess hello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="26901-154">這是必要的 tooprovide SSL hello 叢集 HTTPS 管理端點和 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="26901-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="26901-155">您無法從 hello 的憑證授權單位 (CA) 取得 SSL 憑證`.cloudapp.azure.com`網域。</span><span class="sxs-lookup"><span data-stu-id="26901-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="26901-156">為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="26901-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="26901-157">當您要求的憑證，CA hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="26901-158">用戶端驗證憑證</span><span class="sxs-lookup"><span data-stu-id="26901-158">Client authentication certificates</span></span>
<span data-ttu-id="26901-159">其他用戶端憑證會驗證系統管理員以執行叢集管理工作。</span><span class="sxs-lookup"><span data-stu-id="26901-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="26901-160">Service Fabric 有兩個存取層級：[系統管理員] 和 [唯讀使用者]。</span><span class="sxs-lookup"><span data-stu-id="26901-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="26901-161">您至少應使用一個單一憑證以用於進行系統管理存取。</span><span class="sxs-lookup"><span data-stu-id="26901-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="26901-162">若要進行其他使用者層級存取，則必須提供個別憑證。</span><span class="sxs-lookup"><span data-stu-id="26901-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="26901-163">如需存取角色的詳細資訊，請參閱[角色型存取控制 (適用於 Service Fabric 用戶端)][service-fabric-cluster-security-roles]。</span><span class="sxs-lookup"><span data-stu-id="26901-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="26901-164">您不需要 tooupload 用戶端驗證憑證 tooKey 保存庫 toowork 以 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="26901-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="26901-165">這些憑證只需要提供叢集管理已獲授權 toousers toobe。</span><span class="sxs-lookup"><span data-stu-id="26901-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="26901-166">Azure Active Directory 是 hello 建議叢集方式 tooauthenticate 用戶端管理作業。</span><span class="sxs-lookup"><span data-stu-id="26901-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="26901-167">您必須 toouse Azure Active Directory，[使用 Azure Resource Manager 建立叢集][create-cluster-arm]。</span><span class="sxs-lookup"><span data-stu-id="26901-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="26901-168">應用程式憑證 (選用)</span><span class="sxs-lookup"><span data-stu-id="26901-168">Application certificates (optional)</span></span>
<span data-ttu-id="26901-169">您可以針對應用程式安全性目的，在叢集上安裝任何數目的其他憑證。</span><span class="sxs-lookup"><span data-stu-id="26901-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="26901-170">之前建立您的叢集，請考慮需要這類 hello 節點上安裝憑證 toobe hello 應用程式安全性案例：</span><span class="sxs-lookup"><span data-stu-id="26901-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="26901-171">加密和解密應用程式組態值</span><span class="sxs-lookup"><span data-stu-id="26901-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="26901-172">在複寫期間跨節點加密資料</span><span class="sxs-lookup"><span data-stu-id="26901-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="26901-173">建立叢集，以透過 hello Azure 入口網站時，無法設定應用程式憑證。</span><span class="sxs-lookup"><span data-stu-id="26901-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="26901-174">您必須在叢集安裝程式階段 tooconfigure 應用程式憑證，[使用 Azure Resource Manager 建立叢集][create-cluster-arm]。</span><span class="sxs-lookup"><span data-stu-id="26901-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="26901-175">一旦建立後，您也可以新增應用程式憑證 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="26901-176">設定憑證格式以供 Azure 資源提供者使用</span><span class="sxs-lookup"><span data-stu-id="26901-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="26901-177">私密金鑰檔案 (.pfx) 可以直接透過金鑰保存庫來新增及使用。</span><span class="sxs-lookup"><span data-stu-id="26901-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="26901-178">不過，hello Azure 資源提供者需要索引鍵 toobe 儲存在特殊的 JSON 格式，其中包含 hello.pfx 做為 base 64 編碼字串和 hello 私用金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="26901-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="26901-179">這些需求，金鑰必須放在 JSON 字串，並儲存為 tooaccommodate*密碼*金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="26901-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="26901-180">此程序會更容易 toomake，PowerShell 模組是[github][service-fabric-rp-helpers]。</span><span class="sxs-lookup"><span data-stu-id="26901-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="26901-181">請遵循這些步驟 toouse hello 模組：</span><span class="sxs-lookup"><span data-stu-id="26901-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="26901-182">Hello 的 hello 儲存機制的整個內容下載至本機目錄中。</span><span class="sxs-lookup"><span data-stu-id="26901-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="26901-183">匯入您的 PowerShell 視窗中的 hello 模組：</span><span class="sxs-lookup"><span data-stu-id="26901-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="26901-184">hello`Invoke-AddCertToKeyVault`此 PowerShell 模組中的命令自動將憑證的私密金鑰格式化為 JSON 字串，並將它上載 tooKey 保存庫。</span><span class="sxs-lookup"><span data-stu-id="26901-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="26901-185">Tooadd hello 叢集憑證與任何其他應用程式憑證 tooKey 保存庫，請使用它。</span><span class="sxs-lookup"><span data-stu-id="26901-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="26901-186">任何額外的憑證，您要在叢集中的 tooinstall 重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="26901-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="26901-187">這些是所有 hello 金鑰保存庫必要條件設定的節點驗證，管理端點的安全性和驗證，以及任何其他應用程式的安全性憑證會安裝 Service Fabric 叢集資源管理員範本使用 X.509 憑證的功能。</span><span class="sxs-lookup"><span data-stu-id="26901-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="26901-188">此時，您現在應該有下列安裝程式在 Azure 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="26901-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="26901-189">金鑰保存庫資源群組</span><span class="sxs-lookup"><span data-stu-id="26901-189">Key Vault resource group</span></span>
  * <span data-ttu-id="26901-190">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="26901-190">Key Vault</span></span>
    * <span data-ttu-id="26901-191">叢集伺服器驗證憑證</span><span class="sxs-lookup"><span data-stu-id="26901-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="26901-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="26901-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="26901-193">在 hello Azure 入口網站中建立叢集</span><span class="sxs-lookup"><span data-stu-id="26901-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="26901-194">搜尋 hello Service Fabric 叢集資源</span><span class="sxs-lookup"><span data-stu-id="26901-194">Search for hello Service Fabric cluster resource</span></span>
![搜尋 hello Azure 入口網站上的 Service Fabric 叢集範本。][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="26901-196">登入 toohello [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="26901-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="26901-197">按一下**新增**tooadd 新的資源範本。</span><span class="sxs-lookup"><span data-stu-id="26901-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="26901-198">搜尋在 hello hello Service Fabric 叢集範本**Marketplace**下**一切**。</span><span class="sxs-lookup"><span data-stu-id="26901-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="26901-199">選取**Service Fabric 叢集**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="26901-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="26901-200">瀏覽 toohello **Service Fabric 叢集**刀鋒視窗中，按一下 **建立**，</span><span class="sxs-lookup"><span data-stu-id="26901-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="26901-201">hello**建立 Service Fabric 叢集**分頁有四個步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="26901-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="26901-202">1.基本概念</span><span class="sxs-lookup"><span data-stu-id="26901-202">1. Basics</span></span>
![建立新資源群組的螢幕擷取畫面。][CreateRG]

<span data-ttu-id="26901-204">在 hello 基本概念刀鋒視窗中，您會需要 tooprovide hello 基本詳細資料為您的叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="26901-205">輸入 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="26901-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="26901-206">輸入**使用者名**和**密碼**hello Vm 的遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="26901-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="26901-207">請確定 tooselect hello**訂用帳戶**您想部署，您叢集 toobe，特別是如果您有多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26901-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="26901-208">建立 **新的資源群組**。</span><span class="sxs-lookup"><span data-stu-id="26901-208">Create a **new resource group**.</span></span> <span data-ttu-id="26901-209">它是最佳 toogive 它 hello hello 叢集相同的名稱，因為它可協助在更新版本中，找到這些物件，特別是當您嘗試 toomake 變更 tooyour 部署或刪除您的叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26901-210">雖然您可以決定 toouse 現有的資源群組，是很好的作法 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="26901-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="26901-211">這可讓您不需要的簡單 toodelete 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="26901-212">選取 hello**區域**想 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="26901-213">您必須使用您的金鑰保存庫的同一個地區處於的 hello。</span><span class="sxs-lookup"><span data-stu-id="26901-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="26901-214">2.叢集組態</span><span class="sxs-lookup"><span data-stu-id="26901-214">2. Cluster configuration</span></span>
![建立節點類型][CreateNodeType]

<span data-ttu-id="26901-216">設定您的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="26901-216">Configure your cluster nodes.</span></span> <span data-ttu-id="26901-217">節點型別定義 hello VM 大小、 hello 的 Vm，以及它們的屬性。</span><span class="sxs-lookup"><span data-stu-id="26901-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="26901-218">您的叢集可以有一個以上的節點類型，但 hello 主要節點類型 (hello hello 入口網站上定義的第一個) 必須至少五個 Vm，因為這是一個 hello 節點型別放置 Service Fabric 系統服務。</span><span class="sxs-lookup"><span data-stu-id="26901-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="26901-219">請勿設定 [放置屬性]，因為會自動新增 "NodeTypeName" 預設放置屬性。</span><span class="sxs-lookup"><span data-stu-id="26901-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="26901-220">多個節點類型的常見案例是包含前端服務和後端服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="26901-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="26901-221">您想 tooput hello 前端上的服務連接埠開啟 toohello 網際網路，具有較小的 Vm （例如 D2 的 VM 大小），但是您想 tooput hello 後端服務在較大的 Vm (例如 D4、 D6、 D15，以及其他 VM 大小） 上開啟任何網際網路的連接埠。</span><span class="sxs-lookup"><span data-stu-id="26901-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="26901-222">選擇您的節點型別 （1 too12 字元包含字母和數字） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="26901-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="26901-223">最小的 hello**大小**hello 主要節點的 Vm 的類型由 hello 所驅動**持久性**層您選擇 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="26901-224">hello 持久性層的 hello 預設值是青銅卡。</span><span class="sxs-lookup"><span data-stu-id="26901-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="26901-225">如需有關持久性的詳細資訊，請參閱[toochoose hello Service Fabric 叢集化的可靠性和持久性][service-fabric-cluster-capacity]。</span><span class="sxs-lookup"><span data-stu-id="26901-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="26901-226">選取 hello VM 大小與定價層。</span><span class="sxs-lookup"><span data-stu-id="26901-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="26901-227">D 系列 VM 擁有 SSD 磁碟機，且強烈建議用於具狀態應用程式。</span><span class="sxs-lookup"><span data-stu-id="26901-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="26901-228">請勿使用只有部分核心或可用磁碟容量少於 7 GB 的任何 VM SKU。</span><span class="sxs-lookup"><span data-stu-id="26901-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="26901-229">最小的 hello**數目**hello 主要節點的 Vm 的類型由 hello 所驅動**可靠性**層選擇。</span><span class="sxs-lookup"><span data-stu-id="26901-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="26901-230">hello 可靠性層的 hello 預設值為銀級。</span><span class="sxs-lookup"><span data-stu-id="26901-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="26901-231">如需可靠性的詳細資訊，請參閱[toochoose hello Service Fabric 叢集化的可靠性和持久性][service-fabric-cluster-capacity]。</span><span class="sxs-lookup"><span data-stu-id="26901-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="26901-232">選擇 hello Vm 數目 hello 節點型別。</span><span class="sxs-lookup"><span data-stu-id="26901-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="26901-233">您可以在稍後相應增加或減少 Vm 的節點型別中的 hello 數字，但 hello 主要節點類型，最小的 hello 由您所選擇的 hello 可靠性層級所驅動。</span><span class="sxs-lookup"><span data-stu-id="26901-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="26901-234">其他節點類型可以有 1 個 VM 的下限。</span><span class="sxs-lookup"><span data-stu-id="26901-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="26901-235">設定自訂端點。</span><span class="sxs-lookup"><span data-stu-id="26901-235">Configure custom endpoints.</span></span> <span data-ttu-id="26901-236">此欄位可讓您以逗號分隔清單的連接埠，您想要透過 hello Azure 負載平衡器 toohello tooexpose tooenter 公用網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="26901-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="26901-237">例如，如果您計劃 toodeploy web 應用程式 tooyour 叢集時，輸入"80"這裡 tooallow 到您的叢集中的連接埠 80 上的流量。</span><span class="sxs-lookup"><span data-stu-id="26901-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="26901-238">如需端點的詳細資訊，請參閱[與應用程式通訊][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="26901-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="26901-239">設定叢集**診斷**。</span><span class="sxs-lookup"><span data-stu-id="26901-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="26901-240">根據預設，在您的問題進行疑難排解的叢集 tooassist 上啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="26901-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="26901-241">如果您想要 toodisable 診斷變更 hello**狀態**太切換**關閉**。</span><span class="sxs-lookup"><span data-stu-id="26901-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="26901-242">**不**建議將診斷關閉。</span><span class="sxs-lookup"><span data-stu-id="26901-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="26901-243">選取的 hello 網狀架構升級您的叢集設定為您想要的模式。</span><span class="sxs-lookup"><span data-stu-id="26901-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="26901-244">選取**自動**，如果您想 hello 系統 tooautomatically 取用 hello 最新可用版本，然後再次嘗試 tooupgrade 叢集 tooit。</span><span class="sxs-lookup"><span data-stu-id="26901-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="26901-245">將 hello 模式設定為太**手動**，如果您想 toochoose 支援的版本。</span><span class="sxs-lookup"><span data-stu-id="26901-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="26901-246">我們支援的叢集限於執行支援的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="26901-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="26901-247">藉由選取 hello**手動**模式中，您就可以在 hello 責任 tooupgrade 您叢集 tooa 支援版本。</span><span class="sxs-lookup"><span data-stu-id="26901-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="26901-248">如需 hello Fabric 升級模式的詳細資訊，請參閱 hello [service fabric 叢集-升級文件。][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="26901-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="26901-249">3.安全性</span><span class="sxs-lookup"><span data-stu-id="26901-249">3. Security</span></span>
![Azure 入口網站中安全性組態的螢幕擷取畫面。][SecurityConfigs]

<span data-ttu-id="26901-251">hello 最後一個步驟是 tooprovide 憑證資訊 toosecure hello 叢集使用金鑰保存庫 hello 和資訊稍早建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="26901-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="26901-252">Hello 主要憑證欄位中填入取自上載 hello hello 輸出**叢集憑證**tooKey 保存庫使用 hello `Invoke-AddCertToKeyVault` PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="26901-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="26901-253">檢查 hello**設定進階設定**方塊 tooenter 用戶端憑證**管理用戶端**和**唯讀用戶端**。</span><span class="sxs-lookup"><span data-stu-id="26901-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="26901-254">在這些欄位中，輸入 hello 您管理用戶端憑證指紋和 hello 您唯讀使用者用戶端憑證指紋，如果適用的話。</span><span class="sxs-lookup"><span data-stu-id="26901-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="26901-255">當系統管理員嘗試 tooconnect toohello 叢集時，則會授與存取擁有 hello 指紋值相符的指模的憑證時，才可以在此處輸入。</span><span class="sxs-lookup"><span data-stu-id="26901-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="26901-256">4.摘要</span><span class="sxs-lookup"><span data-stu-id="26901-256">4. Summary</span></span>
![<span data-ttu-id="26901-257">螢幕擷取畫面的 hello 開始面板顯示 「 部署 Service Fabric 叢集 」。</span><span class="sxs-lookup"><span data-stu-id="26901-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="26901-258">toocomplete hello 建立叢集，按一下 **摘要**toosee hello 設定，您已提供，或下載 hello Azure Resource Manager 範本，用 toodeploy 您的叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="26901-259">提供 hello 必要設定之後，hello**確定**按鈕會變成綠色，而您可以按一下它，以啟動 hello 叢集建立程序。</span><span class="sxs-lookup"><span data-stu-id="26901-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="26901-260">您可以看到在 hello 通知 hello 建立進度。</span><span class="sxs-lookup"><span data-stu-id="26901-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="26901-261">（按一下 hello 狀態列會在 hello 右上角螢幕附近的 hello"鈴鐺 」 圖示）。如果您按下**Pin tooStartboard**同時建立 hello 叢集，您會看到**部署 Service Fabric 叢集**釘選 toohello**啟動**面板。</span><span class="sxs-lookup"><span data-stu-id="26901-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="26901-262">檢視叢集狀態</span><span class="sxs-lookup"><span data-stu-id="26901-262">View your cluster status</span></span>
![螢幕擷取畫面： hello 儀表板中的叢集詳細資料。][ClusterDashboard]

<span data-ttu-id="26901-264">一旦建立您的叢集，您可以檢查您的叢集 hello 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="26901-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="26901-265">跳過**瀏覽**按一下**服務網狀架構叢集**。</span><span class="sxs-lookup"><span data-stu-id="26901-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="26901-266">找出您的叢集，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="26901-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="26901-267">您現在可以看到您的叢集 hello 儀表板，包括 hello 叢集的公用端點及連結 tooService Fabric 總管中的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="26901-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="26901-268">hello**節點監視**hello 叢集儀表板 刀鋒視窗的區段指出 hello 為狀況良好和狀況不良的 Vm 數目。</span><span class="sxs-lookup"><span data-stu-id="26901-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="26901-269">您可以找到更多詳細 hello 叢集健全狀況在[服務網狀架構健全狀況模型簡介][service-fabric-health-introduction]。</span><span class="sxs-lookup"><span data-stu-id="26901-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="26901-270">Service Fabric 叢集需要一律 toomaintain 可用性節點 toobe 數目，並保留狀態-參照 tooas 「 維持仲裁 」。</span><span class="sxs-lookup"><span data-stu-id="26901-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="26901-271">Therfore，通常是不安全關閉 hello 叢集中的所有機器 tooshut 除非您先執行[狀態的完整備份][service-fabric-reliable-services-backup-restore]。</span><span class="sxs-lookup"><span data-stu-id="26901-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="26901-272">遠端連接 tooa 虛擬機器擴展集的執行個體或叢集節點</span><span class="sxs-lookup"><span data-stu-id="26901-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="26901-273">每個 hello NodeTypes 您指定在虛擬機器規模集中取得安裝您叢集的結果。</span><span class="sxs-lookup"><span data-stu-id="26901-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="26901-274">請參閱[tooa 虛擬機器擴展集的執行個體的遠端連接][ remote-connect-to-a-vm-scale-set]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="26901-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26901-275">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26901-275">Next steps</span></span>
<span data-ttu-id="26901-276">此時，您擁有一個使用憑證來管理驗證的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="26901-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="26901-277">下一步 [tooyour 叢集連線](service-fabric-connect-to-secure-cluster.md)並了解如何太[管理應用程式密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="26901-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="26901-278">同時，了解 [Service Fabric 支援選項](service-fabric-support.md)。</span><span class="sxs-lookup"><span data-stu-id="26901-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
