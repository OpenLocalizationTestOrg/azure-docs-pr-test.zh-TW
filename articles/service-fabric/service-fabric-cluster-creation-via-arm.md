---
title: "從範本的 aaaCreate Azure Service Fabric 叢集 |Microsoft 文件"
description: "本文說明如何 tooset 上安全的 Service Fabric 在 Azure 中使用叢集的 Azure 資源管理員，Azure 金鑰保存庫和 Azure Active Directory (Azure AD) 用戶端驗證。"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="d8bff-103">使用 Azure Resource Manager 來建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="d8bff-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8bff-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8bff-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="d8bff-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d8bff-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="d8bff-106">此逐步指南可逐步引導您使用 Azure Resource Manager 在 Azure 中設定安全的 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="d8bff-107">我們了解 hello 文件長度。</span><span class="sxs-lookup"><span data-stu-id="d8bff-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="d8bff-108">不過，除非您已徹底熟悉 hello 內容，是確定 toofollow 每個步驟謹慎。</span><span class="sxs-lookup"><span data-stu-id="d8bff-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="d8bff-109">hello 指南涵蓋下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="d8bff-110">Azure 金鑰保存庫 tooupload 的憑證叢集和應用程式的安全性設定</span><span class="sxs-lookup"><span data-stu-id="d8bff-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="d8bff-111">使用 Azure Resource Manager 在 Azure 中建立受保護的叢集</span><span class="sxs-lookup"><span data-stu-id="d8bff-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="d8bff-112">使用適用於叢集管理的 Azure Active Directory (Azure AD) 來驗證使用者</span><span class="sxs-lookup"><span data-stu-id="d8bff-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="d8bff-113">需要安全的叢集，叢集來防止未經授權的存取 toomanagement 作業。</span><span class="sxs-lookup"><span data-stu-id="d8bff-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="d8bff-114">這包括部署、 升級，和刪除的應用程式、 服務，以及它們所包含的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d8bff-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="d8bff-115">不安全的叢集是叢集的任何人都可以用來連接 tooat 任何時間，並執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="d8bff-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="d8bff-116">雖然可能 toocreate 不安全的叢集，我們強烈建議您從 hello 一開始建立安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="d8bff-117">由於無法在稍後再針對不安全的叢集進行保護，因此必須建立新叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="d8bff-118">建立安全叢集的 hello 概念是 hello 相同，，不論它們 Linux 或 Windows 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="d8bff-119">如需建立安全 Linux 叢集的詳細資訊和協助程式指令碼，請參閱[在 Linux 上建立安全叢集](#secure-linux-clusters)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="d8bff-120">Azure 帳戶登入 tooyour</span><span class="sxs-lookup"><span data-stu-id="d8bff-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="d8bff-121">本指南使用 [Azure PowerShell][azure-powershell]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="d8bff-122">當您啟動新的 PowerShell 工作階段時，登入 tooyour Azure 帳戶，並選取您的訂用帳戶，然後再執行 Azure 命令。</span><span class="sxs-lookup"><span data-stu-id="d8bff-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="d8bff-123">Azure 帳戶登入 tooyour 中：</span><span class="sxs-lookup"><span data-stu-id="d8bff-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d8bff-124">選取您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="d8bff-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="d8bff-125">設定 Key Vault</span><span class="sxs-lookup"><span data-stu-id="d8bff-125">Set up a key vault</span></span>
<span data-ttu-id="d8bff-126">本節說明如何為 Azure 中的 Service Fabric 叢集和為 Service Fabric 應用程式建立 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="d8bff-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="d8bff-127">完整指南 tooAzure 金鑰保存庫，請參閱 toohello[金鑰保存庫快速入門指南][key-vault-get-started]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="d8bff-128">服務網狀架構會使用 X.509 憑證 toosecure 叢集，並提供應用程式的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="d8bff-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="d8bff-129">您可以使用金鑰保存庫 toomanage 憑證在 Azure 中的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="d8bff-130">在 Azure 中部署叢集時，會負責建立 Service Fabric 叢集的 hello Azure 資源提供者就會從金鑰保存庫提取憑證，並 hello 叢集 Vm 上進行安裝。</span><span class="sxs-lookup"><span data-stu-id="d8bff-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="d8bff-131">hello 下列圖表說明 hello Azure 金鑰保存庫、 Service Fabric 叢集和使用憑證時它會建立叢集儲存在金鑰保存庫中的 hello Azure 資源提供者之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="d8bff-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![憑證安裝圖][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="d8bff-133">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d8bff-133">Create a resource group</span></span>
<span data-ttu-id="d8bff-134">hello 第一個步驟是 toocreate 特別針對金鑰保存庫的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d8bff-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="d8bff-135">我們建議您將 hello 金鑰保存庫放入自己的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d8bff-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="d8bff-136">這個動作可讓您移除 hello 運算和存放裝置資源群組，包括 hello 資源群組包含 Service Fabric 叢集，而不會遺失您的金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="d8bff-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="d8bff-137">包含金鑰保存庫中的 hello 資源群組_hello 必須位於相同區域_為正在使用它的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="d8bff-138">如果您計劃在多個地區 toodeploy 叢集，我們建議您命名 hello 資源群組和 hello 金鑰保存庫中指出其所屬的區域的方式。</span><span class="sxs-lookup"><span data-stu-id="d8bff-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="d8bff-139">hello 輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8bff-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="d8bff-140">在 hello 新資源群組中建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="d8bff-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="d8bff-141">hello 金鑰保存庫_必須為部署啟用_tooallow hello 計算資源提供者從它的 tooget 憑證，並將它安裝在虛擬機器執行個體上：</span><span class="sxs-lookup"><span data-stu-id="d8bff-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="d8bff-142">hello 輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8bff-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="d8bff-143">使用現有的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="d8bff-143">Use an existing key vault</span></span>

<span data-ttu-id="d8bff-144">toouse 現有的金鑰保存庫，您_必須為部署啟用_tooallow hello 計算資源提供者從它的 tooget 憑證，並將它安裝在叢集節點上：</span><span class="sxs-lookup"><span data-stu-id="d8bff-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="d8bff-145">新增憑證 tooyour 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="d8bff-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="d8bff-146">憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。</span><span class="sxs-lookup"><span data-stu-id="d8bff-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="d8bff-147">如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例][service-fabric-cluster-security]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="d8bff-148">叢集和伺服器憑證 (必要)</span><span class="sxs-lookup"><span data-stu-id="d8bff-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="d8bff-149">此憑證是必要的 toosecure 叢集，並防止未經授權的存取 tooit。</span><span class="sxs-lookup"><span data-stu-id="d8bff-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="d8bff-150">它會透過兩種方式提供叢集安全性：</span><span class="sxs-lookup"><span data-stu-id="d8bff-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="d8bff-151">叢集驗證：驗證叢集同盟的節點對節點通訊。</span><span class="sxs-lookup"><span data-stu-id="d8bff-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="d8bff-152">可以證明其身分識別與此憑證的節點可以加入 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="d8bff-153">伺服器驗證： hello 叢集管理端點 tooa 管理會用戶端驗證，以便 hello 管理用戶端會知道它正在交涉 toohello 實際叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="d8bff-154">此憑證也可提供 SSL hello HTTPS 管理 API 與 Service Fabric 總管透過 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d8bff-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="d8bff-155">這些的考量，hello 憑證必須符合下列需求的 hello tooserve:</span><span class="sxs-lookup"><span data-stu-id="d8bff-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="d8bff-156">hello 憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="d8bff-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="d8bff-157">金鑰交換，也就是可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d8bff-158">hello 憑證的主體名稱必須符合您使用 tooaccess hello Service Fabric 叢集 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="d8bff-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="d8bff-159">這項比對是必要的 tooprovide hello 叢集 HTTPS 管理端點的 SSL 和 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="d8bff-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d8bff-160">您無法從 hello 的憑證授權單位 (CA) 取得 SSL 憑證。 cloudapp.azure.com 網域。</span><span class="sxs-lookup"><span data-stu-id="d8bff-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="d8bff-161">您必須為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d8bff-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="d8bff-162">當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="d8bff-163">應用程式憑證 (選用)</span><span class="sxs-lookup"><span data-stu-id="d8bff-163">Application certificates (optional)</span></span>
<span data-ttu-id="d8bff-164">您可以針對應用程式安全性目的，在叢集上安裝任何數目的其他憑證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="d8bff-165">之前建立您的叢集，請考慮需要這類 hello 節點上安裝憑證 toobe hello 應用程式安全性案例：</span><span class="sxs-lookup"><span data-stu-id="d8bff-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="d8bff-166">將應用程式組態值加密和解密。</span><span class="sxs-lookup"><span data-stu-id="d8bff-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="d8bff-167">在複寫期間將資料跨節點加密。</span><span class="sxs-lookup"><span data-stu-id="d8bff-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="d8bff-168">格式化憑證以供 Azure 資源提供者使用</span><span class="sxs-lookup"><span data-stu-id="d8bff-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="d8bff-169">您可以透過 Key Vault 來直接新增和使用私密金鑰檔案 (.pfx)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="d8bff-170">不過，hello Azure 計算資源提供者需要特殊的 JavaScript Object Notation (JSON) 格式儲存的索引鍵 toobe。</span><span class="sxs-lookup"><span data-stu-id="d8bff-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="d8bff-171">hello 格式包括為 base 64 編碼的字串和 hello 私密金鑰密碼的 hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8bff-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="d8bff-172">tooaccommodate 這些需求，機碼必須放置在 JSON 字串和儲存為 「 密碼 」 hello 機碼中的 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="d8bff-173">此程序會更方便地 toomake [PowerShell 模組是 github][service-fabric-rp-helpers]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="d8bff-174">toouse hello 模組中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="d8bff-175">Hello 的 hello 儲存機制的整個內容下載至本機目錄中。</span><span class="sxs-lookup"><span data-stu-id="d8bff-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="d8bff-176">移 toohello 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="d8bff-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="d8bff-177">匯入您的 PowerShell 視窗中的 hello ServiceFabricRPHelpers 模組：</span><span class="sxs-lookup"><span data-stu-id="d8bff-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="d8bff-178">hello`Invoke-AddCertToKeyVault`此 PowerShell 模組中的命令自動將憑證的私密金鑰格式化為 JSON 字串，並將它上載 toohello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="d8bff-179">使用 hello 命令 tooadd hello 叢集憑證和任何其他應用程式憑證 toohello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="d8bff-180">任何額外的憑證，您要在叢集中的 tooinstall 重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="d8bff-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="d8bff-181">上傳現有的憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="d8bff-182">如果您收到錯誤，例如 hello 其中一個在這裡顯示，通常表示您有資源 URL 衝突。</span><span class="sxs-lookup"><span data-stu-id="d8bff-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="d8bff-183">tooresolve hello 衝突，變更 hello 金鑰保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="d8bff-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="d8bff-184">Hello 衝突解決後，hello 輸出看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8bff-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="d8bff-185">您需要 hello 三個上述字串，CertificateThumbprint，CertificateURL，安全 Service Fabric 叢集和 tooobtain tooset SourceVault，您也可以使用應用程式安全性的任何應用程式憑證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="d8bff-186">如果您沒有儲存 hello 字串，可能很難 tooretrieve 稍後它們藉由查詢 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="d8bff-187">建立自我簽署的憑證，並將資料上傳 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="d8bff-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="d8bff-188">如果您已上傳憑證 toohello 金鑰保存庫，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="d8bff-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="d8bff-189">這個步驟是針對產生新的自我簽署的憑證，並將它上傳 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="d8bff-190">您變更 hello 下列指令碼中的 hello 參數，然後執行它之後，您應該會提示輸入憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="d8bff-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="d8bff-191">如果您收到錯誤，例如 hello 其中一個在這裡顯示，通常表示您有資源 URL 衝突。</span><span class="sxs-lookup"><span data-stu-id="d8bff-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="d8bff-192">tooresolve hello 衝突、 變更 hello 金鑰保存庫名稱、 RG 名稱等等。</span><span class="sxs-lookup"><span data-stu-id="d8bff-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="d8bff-193">Hello 衝突解決後，hello 輸出看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8bff-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="d8bff-194">您需要 hello 三個上述字串，CertificateThumbprint，CertificateURL，安全 Service Fabric 叢集和 tooobtain tooset SourceVault，您也可以使用應用程式安全性的任何應用程式憑證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="d8bff-195">如果您沒有儲存 hello 字串，可能很難 tooretrieve 稍後它們藉由查詢 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="d8bff-196">此時，您應該有下列項目就地 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="d8bff-197">hello 金鑰保存庫的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d8bff-197">hello key vault resource group.</span></span>
* <span data-ttu-id="d8bff-198">hello 金鑰保存庫和其 URL （hello 上述 PowerShell 輸出中稱為 SourceVault）。</span><span class="sxs-lookup"><span data-stu-id="d8bff-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="d8bff-199">hello 叢集伺服器驗證憑證與它在 hello 金鑰保存庫的 URL。</span><span class="sxs-lookup"><span data-stu-id="d8bff-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="d8bff-200">hello 應用程式憑證，且其 hello 金鑰保存庫中的 Url。</span><span class="sxs-lookup"><span data-stu-id="d8bff-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="d8bff-201">設定用戶端驗用的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8bff-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="d8bff-202">Azure AD 可讓組織 （也稱為租用戶） toomanage 使用者存取 tooapplications。</span><span class="sxs-lookup"><span data-stu-id="d8bff-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="d8bff-203">應用程式分成具有 Web 型登入 UI 的應用程式，以及具有原生用戶端體驗的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8bff-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="d8bff-204">在本文中，我們假設您已經建立租用戶。</span><span class="sxs-lookup"><span data-stu-id="d8bff-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="d8bff-205">如果您沒有這樣做，先閱讀[tooget Azure Active Directory 的租用戶][active-directory-howto-tenant]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="d8bff-206">Service Fabric 叢集提供數個進入點 tooits 管理功能，包括 web 為基礎的 hello [Service Fabric 總管][ service-fabric-visualizing-your-cluster]和[Visual Studio][service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="d8bff-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="d8bff-207">如此一來，您會建立兩個 Azure AD 應用程式 toocontrol 存取 toohello 叢集、 一個 web 應用程式和一個原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8bff-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="d8bff-208">toosimplify 部分 hello 步驟涉及設定 Azure AD 與 Service Fabric 叢集，我們已經建立一組 Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d8bff-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="d8bff-209">您必須完成下列步驟，才能建立 hello 叢集 hello。</span><span class="sxs-lookup"><span data-stu-id="d8bff-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="d8bff-210">Hello 指令碼預期的叢集名稱和端點，因為 hello 值應該計劃，而且不確定您已經建立的值。</span><span class="sxs-lookup"><span data-stu-id="d8bff-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="d8bff-211">[下載 hello 指令碼][ sf-aad-ps-script-download] tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="d8bff-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="d8bff-212">以滑鼠右鍵按一下 hello zip 檔，請選取**屬性**，選取 hello**解除封鎖**核取方塊，然後**套用**。</span><span class="sxs-lookup"><span data-stu-id="d8bff-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="d8bff-213">Hello zip 檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="d8bff-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="d8bff-214">執行`SetupApplications.ps1`，並提供 hello TenantId，ClusterName 和 WebApplicationReplyUrl 做為參數。</span><span class="sxs-lookup"><span data-stu-id="d8bff-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="d8bff-215">例如：</span><span class="sxs-lookup"><span data-stu-id="d8bff-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="d8bff-216">您可以藉由執行 hello PowerShell 命令來找到您 TenantId `Get-AzureSubscription`。</span><span class="sxs-lookup"><span data-stu-id="d8bff-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="d8bff-217">執行這個命令會顯示每個訂用帳戶的 hello TenantId。</span><span class="sxs-lookup"><span data-stu-id="d8bff-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="d8bff-218">ClusterName 是使用的 tooprefix hello Azure AD 應用程式所建立的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d8bff-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="d8bff-219">它不會完全不需要 toomatch hello 實際叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="d8bff-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="d8bff-220">它會預期只有 toomake 它更容易 toomap Azure AD 成品 toohello Service Fabric 叢集是要搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d8bff-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="d8bff-221">WebApplicationReplyUrl 是 Azure AD 傳回 tooyour 使用者在完成登入之後的 hello 預設端點。</span><span class="sxs-lookup"><span data-stu-id="d8bff-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="d8bff-222">將此端點設定為叢集，其預設值是 hello Service Fabric 總管端點：</span><span class="sxs-lookup"><span data-stu-id="d8bff-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="d8bff-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="d8bff-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="d8bff-224">您必須提示的 toosign tooan 帳戶具有系統管理權限 hello Azure AD 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="d8bff-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="d8bff-225">登入之後，hello 指令碼會建立 hello web 和原生應用程式 toorepresent Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="d8bff-226">如果您查看 hello 租用戶的應用程式在 hello [Azure 傳統入口網站][azure-classic-portal]，您應該會看到兩個新項目：</span><span class="sxs-lookup"><span data-stu-id="d8bff-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="d8bff-227">*ClusterName*\_叢集</span><span class="sxs-lookup"><span data-stu-id="d8bff-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="d8bff-228">*ClusterName*\_用戶端</span><span class="sxs-lookup"><span data-stu-id="d8bff-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="d8bff-229">hello 指令碼會列印的 hello JSON，因此它是個不錯的主意 tookeep hello PowerShell 視窗，在 hello 下一步 區段中，建立 hello 叢集時，所需的 hello Azure Resource Manager 範本開啟。</span><span class="sxs-lookup"><span data-stu-id="d8bff-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="d8bff-230">建立 Service Fabric 叢集 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="d8bff-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="d8bff-231">在本節中，hello 輸出的 hello 上述 Service Fabric 叢集資源管理員範本中使用 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="d8bff-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="d8bff-232">範例資源管理員範本位於 hello [GitHub 上的 Azure 快速入門範本圖庫][azure-quickstart-templates]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="d8bff-233">這些範本可以用作叢集範本的起點。</span><span class="sxs-lookup"><span data-stu-id="d8bff-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="d8bff-234">建立 hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="d8bff-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="d8bff-235">本指南使用 hello [5 節點安全叢集][ service-fabric-secure-cluster-5-node-1-nodetype]範例範本和範本參數。</span><span class="sxs-lookup"><span data-stu-id="d8bff-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="d8bff-236">下載`azuredeploy.json`和`azuredeploy.parameters.json`tooyour 電腦並在您慣用的文字編輯器中開啟這兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="d8bff-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="d8bff-237">新增憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-237">Add certificates</span></span>
<span data-ttu-id="d8bff-238">您新增憑證 tooa 叢集資源管理員範本，藉由參考包含 hello 憑證金鑰的 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d8bff-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="d8bff-239">我們建議您在資源管理員範本參數檔案中放入 hello 金鑰保存庫的值。</span><span class="sxs-lookup"><span data-stu-id="d8bff-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="d8bff-240">這樣可防止 hello 資源管理員範本檔案可重複使用和可用的值特定 tooa 部署。</span><span class="sxs-lookup"><span data-stu-id="d8bff-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="d8bff-241">將所有憑證 toohello 虛擬機器規模都集 osProfile</span><span class="sxs-lookup"><span data-stu-id="d8bff-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="d8bff-242">安裝 hello 叢集中的每個憑證必須設定一節 hello osProfile hello 標尺之資源集 (Microsoft.Compute/virtualMachineScaleSets)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="d8bff-243">這個動作會指示 hello 資源提供者 tooinstall hello 憑證 hello Vm 上。</span><span class="sxs-lookup"><span data-stu-id="d8bff-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="d8bff-244">此安裝包括 hello 叢集憑證和任何 toouse 規劃您的應用程式的應用程式的安全性憑證：</span><span class="sxs-lookup"><span data-stu-id="d8bff-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="d8bff-245">設定 hello Service Fabric 叢集憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="d8bff-246">hello 叢集驗證憑證必須由兩個 hello Service Fabric 叢集資源 (Microsoft.ServiceFabric/clusters) 和 hello Service Fabric 擴充功能的虛擬機器規模設定中 hello 虛擬機器規模集資源。</span><span class="sxs-lookup"><span data-stu-id="d8bff-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="d8bff-247">這種安排可讓 hello Service Fabric 資源提供者 tooconfigure 它用於叢集驗證及管理端點的伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="d8bff-248">虛擬機器擴展集資源：</span><span class="sxs-lookup"><span data-stu-id="d8bff-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="d8bff-249">Service Fabric 資源︰</span><span class="sxs-lookup"><span data-stu-id="d8bff-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="d8bff-250">插入 Azure AD 組態</span><span class="sxs-lookup"><span data-stu-id="d8bff-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="d8bff-251">您稍早建立的 hello Azure AD 設定直接插入 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="d8bff-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="d8bff-252">不過，我們建議您先 hello 值擷取成參數檔案 tookeep hello 資源管理員範本可重複使用和可用值的特定 tooa 部署。</span><span class="sxs-lookup"><span data-stu-id="d8bff-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="d8bff-253"><a "configure-arm" ></a>設定 Resource Manager 範本參數</span><span class="sxs-lookup"><span data-stu-id="d8bff-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="d8bff-254">最後，使用從 hello 金鑰保存庫和 Azure AD PowerShell 命令 toopopulate hello 參數檔案的 hello 輸出值：</span><span class="sxs-lookup"><span data-stu-id="d8bff-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="d8bff-255">此時，您應該有下列項目就地 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="d8bff-256">Key Vault 資源群組</span><span class="sxs-lookup"><span data-stu-id="d8bff-256">Key vault resource group</span></span>
  * <span data-ttu-id="d8bff-257">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="d8bff-257">Key vault</span></span>
  * <span data-ttu-id="d8bff-258">叢集伺服器驗證憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="d8bff-259">資料編密憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-259">Data encipherment certificate</span></span>
* <span data-ttu-id="d8bff-260">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="d8bff-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="d8bff-261">適用於 Web 型管理和 Service Fabric Explorer 的 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="d8bff-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="d8bff-262">適用於原生用戶端管理的 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="d8bff-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="d8bff-263">使用者及其獲指派的角色</span><span class="sxs-lookup"><span data-stu-id="d8bff-263">Users and their assigned roles</span></span>
* <span data-ttu-id="d8bff-264">Service Fabric 叢集 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="d8bff-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="d8bff-265">透過 Key Vault 設定的憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="d8bff-266">已設定 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8bff-266">Azure Active Directory configured</span></span>

<span data-ttu-id="d8bff-267">hello 下列圖表說明您的金鑰保存庫和 Azure AD 設定放入 Resource Manager 範本的位置。</span><span class="sxs-lookup"><span data-stu-id="d8bff-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Resource Manager 相依性對應][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="d8bff-269">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="d8bff-269">Create hello cluster</span></span>
<span data-ttu-id="d8bff-270">現在您已經準備就緒 toocreate hello 叢集使用[Azure 資源範本部署][resource-group-template-deploy]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="d8bff-271">進行測試</span><span class="sxs-lookup"><span data-stu-id="d8bff-271">Test it</span></span>
<span data-ttu-id="d8bff-272">使用下列 PowerShell 命令 tootest hello Resource Manager 範本參數檔案：</span><span class="sxs-lookup"><span data-stu-id="d8bff-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="d8bff-273">進行部署</span><span class="sxs-lookup"><span data-stu-id="d8bff-273">Deploy it</span></span>
<span data-ttu-id="d8bff-274">如果 hello 資源管理員範本測試成功，使用下列 PowerShell 命令 toodeploy hello Resource Manager 範本參數檔案：</span><span class="sxs-lookup"><span data-stu-id="d8bff-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="d8bff-275">指派使用者 tooroles</span><span class="sxs-lookup"><span data-stu-id="d8bff-275">Assign users tooroles</span></span>
<span data-ttu-id="d8bff-276">您已建立 hello 應用程式 toorepresent 您的叢集之後，您的使用者 toohello 將角色指派支援的 Service Fabric： 唯讀和系統管理員。您可以使用 hello 指派 hello 角色[Azure 傳統入口網站][azure-classic-portal]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="d8bff-277">在 hello Azure 入口網站，移 tooyour 租用戶，然後選取**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d8bff-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="d8bff-278">選取 hello web 應用程式，有一個名稱類似`myTestCluster_Cluster`。</span><span class="sxs-lookup"><span data-stu-id="d8bff-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="d8bff-279">按一下 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d8bff-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="d8bff-280">選取使用者 tooassign，，然後按一下hello**指派**在 hello 囉 」 畫面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d8bff-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![指派使用者 tooroles 按鈕][assign-users-to-roles-button]
5. <span data-ttu-id="d8bff-282">選取 hello 角色 tooassign toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d8bff-282">Select hello role tooassign toohello user.</span></span>

    ![[指派使用者] 對話方塊][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="d8bff-284">如需 Service Fabric 中角色的詳細資訊，請參閱 [角色型存取控制 (適用於 Service Fabric 用戶端)](service-fabric-cluster-security-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="d8bff-285">在 Linux 上建立安全叢集</span><span class="sxs-lookup"><span data-stu-id="d8bff-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="d8bff-286">我們已提供 toomake hello 程序更容易， [helper 指令碼](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="d8bff-287">在使用此協助程式指令碼之前，請確定您已安裝 Azure 命令列介面 (CLI)，而且它位於您的路徑中。</span><span class="sxs-lookup"><span data-stu-id="d8bff-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="d8bff-288">請確定 hello 指令碼執行具有權限 tooexecute`chmod +x cert_helper.py`下載它之後。</span><span class="sxs-lookup"><span data-stu-id="d8bff-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="d8bff-289">hello 第一個步驟是 toosign tooyour Azure 帳戶中的使用以 hello CLI`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="d8bff-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="d8bff-290">登入 tooyour Azure 帳戶之後，使用 hello helper 簽署指令碼與您的 CA 憑證，以下列命令顯示 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="d8bff-291">hello-ifile 參數可以採用.pfx 檔案或.pem 檔案，做為輸入，與 hello 憑證類型 （pfx 或 pem 或如果它是自我簽署的憑證的 ss）。</span><span class="sxs-lookup"><span data-stu-id="d8bff-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="d8bff-292">hello 參數-h 會列印出 hello 說明文字。</span><span class="sxs-lookup"><span data-stu-id="d8bff-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="d8bff-293">此命令會傳回下列三個字串做為 hello 輸出 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="d8bff-294">SourceVaultID，是 hello 識別碼 hello 它為您建立新的 KeyVault 資源群組</span><span class="sxs-lookup"><span data-stu-id="d8bff-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="d8bff-295">CertificateUrl 存取 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="d8bff-296">CertificateThumbprint：用於驗證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="d8bff-297">hello 下列範例顯示如何 toouse hello 命令：</span><span class="sxs-lookup"><span data-stu-id="d8bff-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="d8bff-298">執行上述命令可讓您 hello 三個字串，如下所示的 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="d8bff-299">hello 憑證的主體名稱必須符合您使用 tooaccess hello Service Fabric 叢集 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="d8bff-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="d8bff-300">此比對會需要的 tooprovide hello 叢集 HTTPS 管理端點的 SSL 和 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="d8bff-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d8bff-301">您無法取得 SSL 憑證，從 CA hello`.cloudapp.azure.com`網域。</span><span class="sxs-lookup"><span data-stu-id="d8bff-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="d8bff-302">您必須為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d8bff-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="d8bff-303">當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="d8bff-304">這些主旨名稱是 hello 項目需要 toocreate 安全 Service Fabric 叢集 （不含 Azure AD)，依照[設定資源管理員範本參數](#configure-arm)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="d8bff-305">您可以依照下列指示 hello 連接 toohello 安全叢集[驗證用戶端存取 tooa 叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="d8bff-306">Linux 預覽叢集不支援 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="d8bff-307">Hello 中所述，您可以指派系統管理員和用戶端角色[指派角色 toousers](#assign-roles) > 一節。</span><span class="sxs-lookup"><span data-stu-id="d8bff-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="d8bff-308">當您指定 Linux 預覽叢集的系統管理員和用戶端角色時，您必須驗證 tooprovide 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="d8bff-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="d8bff-309">（您未提供 hello 主體名稱，因為沒有鏈結驗證或撤銷執行在此預覽版本。）</span><span class="sxs-lookup"><span data-stu-id="d8bff-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="d8bff-310">如果您想 toouse 自我簽署憑證進行測試時，您可以使用 hello 相同的指令碼 toogenerate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="d8bff-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="d8bff-311">您可以藉由提供 hello 旗標然後上傳 hello 憑證 tooyour 金鑰保存庫`ss`而不是提供 hello 憑證路徑和憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="d8bff-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="d8bff-312">例如，請參閱下列命令來建立及上傳的自我簽署的憑證的 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="d8bff-313">此命令傳回 hello 相同的三個字串： SourceVault、 CertificateUrl 和 CertificateThumbprint。</span><span class="sxs-lookup"><span data-stu-id="d8bff-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="d8bff-314">然後，您可以使用 hello 字串 toocreate hello 自我簽署的憑證所在的位置和安全的 Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="d8bff-315">您需要 hello 自我簽署的憑證 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="d8bff-316">您可以依照下列指示 hello 連接 toohello 安全叢集[驗證用戶端存取 tooa 叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="d8bff-317">hello 憑證的主體名稱必須符合您使用 tooaccess hello Service Fabric 叢集 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="d8bff-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="d8bff-318">此比對會需要的 tooprovide hello 叢集 HTTPS 管理端點的 SSL 和 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="d8bff-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d8bff-319">您無法取得 SSL 憑證，從 CA hello`.cloudapp.azure.com`網域。</span><span class="sxs-lookup"><span data-stu-id="d8bff-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="d8bff-320">您必須為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d8bff-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="d8bff-321">當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="d8bff-322">Hello 中所述，也可以填入 hello Azure 入口網站中的 hello helper 指令碼中的 hello 參數[hello Azure 入口網站中建立叢集](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d8bff-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8bff-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8bff-323">Next steps</span></span>
<span data-ttu-id="d8bff-324">此時，您已具有以 Azure Active Directory 提供管理驗證的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="d8bff-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="d8bff-325">下一步 [tooyour 叢集連線](service-fabric-connect-to-secure-cluster.md)並了解如何太[管理應用程式密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="d8bff-326">針對設定用戶端驗用的 Azure Active Directory 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d8bff-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="d8bff-327">如果遇到問題時您正要設定 Azure AD 用戶端驗證，請，檢閱本節中的 hello 可能解決方案。</span><span class="sxs-lookup"><span data-stu-id="d8bff-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="d8bff-328">Service Fabric 總管會提示您 tooselect 憑證</span><span class="sxs-lookup"><span data-stu-id="d8bff-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="d8bff-329">問題</span><span class="sxs-lookup"><span data-stu-id="d8bff-329">Problem</span></span>
<span data-ttu-id="d8bff-330">登入成功 tooAzure AD Service Fabric 總管中後，hello 瀏覽器傳回 toohello 首頁上，但會有訊息提示 tooselect 憑證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![SFX 選取憑證對話方塊][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="d8bff-332">原因</span><span class="sxs-lookup"><span data-stu-id="d8bff-332">Reason</span></span>
<span data-ttu-id="d8bff-333">hello 使用者未獲派 hello Azure AD 叢集應用程式中的角色。</span><span class="sxs-lookup"><span data-stu-id="d8bff-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="d8bff-334">因此，Azure AD 驗證在 Service Fabric 叢集上發生失敗。</span><span class="sxs-lookup"><span data-stu-id="d8bff-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="d8bff-335">Service Fabric 總管會回到 toocertificate 驗證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="d8bff-336">方案</span><span class="sxs-lookup"><span data-stu-id="d8bff-336">Solution</span></span>
<span data-ttu-id="d8bff-337">請依照 hello 指示來設定 Azure AD，與指派使用者角色。</span><span class="sxs-lookup"><span data-stu-id="d8bff-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="d8bff-338">此外，我們建議您開啟 「 指派必要的 tooaccess 應用程式的使用者 」，為`SetupApplications.ps1`沒有。</span><span class="sxs-lookup"><span data-stu-id="d8bff-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="d8bff-339">使用 PowerShell 連線失敗，發生錯誤: 「 hello 指定認證不正確 」</span><span class="sxs-lookup"><span data-stu-id="d8bff-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="d8bff-340">問題</span><span class="sxs-lookup"><span data-stu-id="d8bff-340">Problem</span></span>
<span data-ttu-id="d8bff-341">當您使用 PowerShell tooconnect toohello 叢集使用 「 AzureActiveDirectory"安全性模式，您已成功 tooAzure AD 在登入後時，hello 連線會失敗並發生錯誤: 「 hello 指定認證不正確 」。</span><span class="sxs-lookup"><span data-stu-id="d8bff-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="d8bff-342">方案</span><span class="sxs-lookup"><span data-stu-id="d8bff-342">Solution</span></span>
<span data-ttu-id="d8bff-343">這個解決方案相當的 hello 與相同 hello 之前。</span><span class="sxs-lookup"><span data-stu-id="d8bff-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="d8bff-344">Service Fabric Explorer 在您登入時傳回失敗："AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="d8bff-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="d8bff-345">問題</span><span class="sxs-lookup"><span data-stu-id="d8bff-345">Problem</span></span>
<span data-ttu-id="d8bff-346">Hello 頁面當您嘗試 toosign tooAzure AD 中 Service Fabric 總管中的時，傳回的失敗:"AADSTS50011: hello 的回覆地址&lt;url&gt; hello hello 應用程式設定的回覆地址不符： &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="d8bff-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![SFX 回覆地址不相符][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="d8bff-348">原因</span><span class="sxs-lookup"><span data-stu-id="d8bff-348">Reason</span></span>
<span data-ttu-id="d8bff-349">代表 Service Fabric 總管 hello 叢集 (web) 應用程式嘗試 tooauthenticate 針對 Azure AD，並為 hello 要求的一部分提供 hello 重新導向的傳回 URL。</span><span class="sxs-lookup"><span data-stu-id="d8bff-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="d8bff-350">Hello URL 未列在 hello Azure AD 應用程式，但是**回覆 URL**清單。</span><span class="sxs-lookup"><span data-stu-id="d8bff-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="d8bff-351">方案</span><span class="sxs-lookup"><span data-stu-id="d8bff-351">Solution</span></span>
<span data-ttu-id="d8bff-352">在 [hello**設定**hello] 索引標籤叢集 (web) 應用程式，請新增 hello Service Fabric 總管 URL toohello**回覆 URL**清單，或取代其中一個 hello hello 清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="d8bff-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="d8bff-353">完成時，請儲存變更。</span><span class="sxs-lookup"><span data-stu-id="d8bff-353">When you have finished, save your change.</span></span>

![Web 應用程式回覆 url][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="d8bff-355">Hello 叢集連線使用透過 PowerShell 的 Azure AD 驗證</span><span class="sxs-lookup"><span data-stu-id="d8bff-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="d8bff-356">tooconnect hello Service Fabric 叢集將使用下列 PowerShell 命令範例 hello:</span><span class="sxs-lookup"><span data-stu-id="d8bff-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="d8bff-357">toolearn 有關 hello Connect-servicefabriccluster cmdlet，請參閱[Connect-servicefabriccluster](https://msdn.microsoft.com/library/mt125938.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d8bff-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="d8bff-358">可以重複使用多個群集中的 hello 相同的 Azure AD 租用戶嗎？</span><span class="sxs-lookup"><span data-stu-id="d8bff-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="d8bff-359">是。</span><span class="sxs-lookup"><span data-stu-id="d8bff-359">Yes.</span></span> <span data-ttu-id="d8bff-360">但是請記住 tooadd hello Service Fabric 總管 URL tooyour 叢集 (web) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8bff-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="d8bff-361">否則 Service Fabric Explorer 無法運作。</span><span class="sxs-lookup"><span data-stu-id="d8bff-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="d8bff-362">為什麼在已啟用 Azure AD 的情況下仍然需要伺服器憑證？</span><span class="sxs-lookup"><span data-stu-id="d8bff-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="d8bff-363">FabricClient 和 FabricGateway 會執行相互驗證。</span><span class="sxs-lookup"><span data-stu-id="d8bff-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="d8bff-364">Azure AD 在驗證期間，Azure AD 的整合會提供用戶端身分識別 toohello 伺服器，且 hello 伺服器憑證使用的 tooverify hello 伺服器身分識別。</span><span class="sxs-lookup"><span data-stu-id="d8bff-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="d8bff-365">如需有關 Service Fabric 憑證的詳細資訊，請參閱 [X.509 憑證和 Service Fabric][x509-certificates-and-service-fabric]。</span><span class="sxs-lookup"><span data-stu-id="d8bff-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

