---
title: "在 Azure 入口網站中建立 Service Fabric 叢集 | Microsoft Docs"
description: "本文說明如何使用 Azure 入口網站和 Azure 金鑰保存庫在 Azure 中建立安全的 Service Fabric 叢集。"
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
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="31f4b-103">使用 Azure 入口網站在 Azure 中建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="31f4b-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31f4b-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31f4b-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="31f4b-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="31f4b-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="31f4b-106">這是一個逐步指南，可逐步引導您使用 Azure 入口網站在 Azure 中設定安全的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="31f4b-107">本指南將逐步引導您完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="31f4b-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="31f4b-108">設定金鑰保存庫來管理叢集安全性的金鑰。</span><span class="sxs-lookup"><span data-stu-id="31f4b-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="31f4b-109">透過 Azure 入口網站在 Azure 中建立安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="31f4b-110">使用憑證驗證系統管理員。</span><span class="sxs-lookup"><span data-stu-id="31f4b-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="31f4b-111">如需更進階的安全性選項 (例如使用 Azure Active Directory 進行使用者驗證及設定應用程式安全性的憑證)，請參閱[使用 Azure Resource Manager 建立您的叢集][create-cluster-arm]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="31f4b-112">安全的叢集是可以防止未經授權存取管理作業的叢集，那些作業包括部署、升級及刪除應用程式、服務和它們包含的資料。</span><span class="sxs-lookup"><span data-stu-id="31f4b-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="31f4b-113">不安全的叢集是任何人都可以隨時連線並執行管理作業的叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="31f4b-114">雖然可以建立不安全的叢集，但 **強烈建議您建立安全的叢集**。</span><span class="sxs-lookup"><span data-stu-id="31f4b-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="31f4b-115">不安全的叢集 **無法在事後保護其安全** - 必須建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="31f4b-116">不論叢集是 Linux 叢集或 Windows 叢集，建立安全叢集的概念都一樣。</span><span class="sxs-lookup"><span data-stu-id="31f4b-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="31f4b-117">如需建立安全 Linux 叢集的詳細資訊和協助程式指令碼，請參閱[在 Linux 上建立安全叢集](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters)。</span><span class="sxs-lookup"><span data-stu-id="31f4b-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="31f4b-118">由所提供的協助程式指令碼所取得的參數可以直接輸入到入口網站，如[在 Azure 入口網站中建立叢集](#create-cluster-portal)一節所述。</span><span class="sxs-lookup"><span data-stu-id="31f4b-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="31f4b-119">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="31f4b-119">Log in to Azure</span></span>
<span data-ttu-id="31f4b-120">本指南使用 [Azure PowerShell][azure-powershell]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="31f4b-121">開始新的 PowerShell 工作階段時，請先登入您的 Azure 帳戶並選取您的訂用帳戶，然後再執行 Azure 命令。</span><span class="sxs-lookup"><span data-stu-id="31f4b-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="31f4b-122">登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="31f4b-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="31f4b-123">選取您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="31f4b-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="31f4b-124">設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="31f4b-124">Set up Key Vault</span></span>
<span data-ttu-id="31f4b-125">這部分的指南將逐步引導您為 Azure 中的 Service Fabric 叢集和為 Service Fabric 應用程式建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="31f4b-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="31f4b-126">如需 Key Vault 的完整指引，請參閱 [Key Vault入門指南][key-vault-get-started]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="31f4b-127">Service Fabric 會使用 X.509 憑證來保護叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="31f4b-128">Azure 金鑰保存庫可用來管理 Azure 中 Service Fabric 叢集的憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="31f4b-129">在 Azure 中部署叢集時，負責建立 Service Fabric 叢集的 Azure 資源提供者會從金鑰保存庫提取憑證，並將它們安裝在叢集 VM 上。</span><span class="sxs-lookup"><span data-stu-id="31f4b-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="31f4b-130">下圖說明金鑰保存庫、Service Fabric 叢集，以及 Azure 資源提供者 (會在建立叢集時使用金鑰保存庫中所存憑證) 之間的關係：</span><span class="sxs-lookup"><span data-stu-id="31f4b-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![憑證安裝][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="31f4b-132">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="31f4b-132">Create a Resource Group</span></span>
<span data-ttu-id="31f4b-133">第一個步驟是為金鑰保存庫建立一個專用的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="31f4b-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="31f4b-134">建議將金鑰保存庫放入它自己的資源群組，您就可以移除計算和儲存體資源群組 (例如擁有您 Service Fabric 叢集的資源群組) 而不會遺失您的金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="31f4b-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="31f4b-135">擁有您金鑰保存庫的資源群組必須和正在使用它的叢集位於相同區域。</span><span class="sxs-lookup"><span data-stu-id="31f4b-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="31f4b-136">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="31f4b-136">Create Key Vault</span></span>
<span data-ttu-id="31f4b-137">在新的資源群組中建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="31f4b-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="31f4b-138">金鑰保存庫 **必須啟用以用於部署** ，才能讓 Service Fabric 資源提供者從中取得憑證並安裝在叢集節點上：</span><span class="sxs-lookup"><span data-stu-id="31f4b-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="31f4b-139">如果您有現有金鑰保存庫，可以使用 Azure CLI 將它啟用以用於部署：</span><span class="sxs-lookup"><span data-stu-id="31f4b-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="31f4b-140">新增憑證至金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="31f4b-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="31f4b-141">憑證是在 Service Fabric 中用來提供驗證與加密，以保護叢集和其應用程式的各個層面。</span><span class="sxs-lookup"><span data-stu-id="31f4b-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="31f4b-142">如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例][service-fabric-cluster-security]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="31f4b-143">叢集和伺服器憑證 (必要)</span><span class="sxs-lookup"><span data-stu-id="31f4b-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="31f4b-144">需要此憑證來保護叢集安全及防止未經授權存取叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="31f4b-145">它會透過幾種方式提供叢集安全性：</span><span class="sxs-lookup"><span data-stu-id="31f4b-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="31f4b-146">**叢集驗證：** 驗證叢集同盟的節點對節點通訊。</span><span class="sxs-lookup"><span data-stu-id="31f4b-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="31f4b-147">只有可使用此憑證提供其身分識別的節點可以加入叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="31f4b-148">**伺服器驗證：** 向管理用戶端驗證叢集管理端點，管理用戶端就能知道它正在交談的對象是真正的叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="31f4b-149">此憑證也會為 HTTPS 管理 API，以及為透過 HTTPS 使用的 Service Fabric Explorer 提供 SSL。</span><span class="sxs-lookup"><span data-stu-id="31f4b-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="31f4b-150">為用於這些用途，憑證必須符合下列要求：</span><span class="sxs-lookup"><span data-stu-id="31f4b-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="31f4b-151">憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="31f4b-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="31f4b-152">憑證必須是為了進行金鑰交換而建立，且可匯出成個人資訊交換檔 (.pfx)。</span><span class="sxs-lookup"><span data-stu-id="31f4b-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="31f4b-153">憑證的主體名稱必須符合用來存取 Service Fabric 叢集的網域。</span><span class="sxs-lookup"><span data-stu-id="31f4b-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="31f4b-154">這是必要的，以便為叢集的 HTTPS 管理端點和 Service Fabric Explorer 提供 SSL。</span><span class="sxs-lookup"><span data-stu-id="31f4b-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="31f4b-155">您無法向憑證授權單位 (CA) 取得 `.cloudapp.azure.com` 網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="31f4b-156">為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="31f4b-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="31f4b-157">當您向 CA 要求憑證時，憑證的主體名稱必須符合用於您叢集的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="31f4b-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="31f4b-158">用戶端驗證憑證</span><span class="sxs-lookup"><span data-stu-id="31f4b-158">Client authentication certificates</span></span>
<span data-ttu-id="31f4b-159">其他用戶端憑證會驗證系統管理員以執行叢集管理工作。</span><span class="sxs-lookup"><span data-stu-id="31f4b-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="31f4b-160">Service Fabric 有兩個存取層級：[系統管理員] 和 [唯讀使用者]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="31f4b-161">您至少應使用一個單一憑證以用於進行系統管理存取。</span><span class="sxs-lookup"><span data-stu-id="31f4b-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="31f4b-162">若要進行其他使用者層級存取，則必須提供個別憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="31f4b-163">如需存取角色的詳細資訊，請參閱[角色型存取控制 (適用於 Service Fabric 用戶端)][service-fabric-cluster-security-roles]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="31f4b-164">若要使用 Service Fabric，您並不需要將用戶端驗證憑證上傳至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="31f4b-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="31f4b-165">這些憑證只需要提供給獲得授權來管理叢集的使用者。</span><span class="sxs-lookup"><span data-stu-id="31f4b-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="31f4b-166">建議使用 Azure Active Directory 驗證用戶端以執行叢集管理作業。</span><span class="sxs-lookup"><span data-stu-id="31f4b-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="31f4b-167">若要使用 Azure Active Directory，您必須[使用 Azure Resource Manager 建立叢集][create-cluster-arm]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="31f4b-168">應用程式憑證 (選用)</span><span class="sxs-lookup"><span data-stu-id="31f4b-168">Application certificates (optional)</span></span>
<span data-ttu-id="31f4b-169">您可以針對應用程式安全性目的，在叢集上安裝任何數目的其他憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="31f4b-170">在建立您的叢集之前，請考量需要在節點上安裝憑證的應用程式安全性案例，例如：</span><span class="sxs-lookup"><span data-stu-id="31f4b-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="31f4b-171">加密和解密應用程式組態值</span><span class="sxs-lookup"><span data-stu-id="31f4b-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="31f4b-172">在複寫期間跨節點加密資料</span><span class="sxs-lookup"><span data-stu-id="31f4b-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="31f4b-173">透過 Azure 入口網站建立叢集時無法設定應用程式憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="31f4b-174">若要在建立叢集時設定應用程式憑證，您必須[使用 Azure Resource Manager 建立叢集][create-cluster-arm]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="31f4b-175">您也可以在建立叢集之後將應用程式憑證新增到叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="31f4b-176">設定憑證格式以供 Azure 資源提供者使用</span><span class="sxs-lookup"><span data-stu-id="31f4b-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="31f4b-177">私密金鑰檔案 (.pfx) 可以直接透過金鑰保存庫來新增及使用。</span><span class="sxs-lookup"><span data-stu-id="31f4b-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="31f4b-178">但是，Azure 資源提供者需要以特殊 JSON 格式儲存金鑰，該格式包含 .pfx 作為 Base-64 編碼字串和私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="31f4b-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="31f4b-179">為符合這些要求，金鑰必須放入 JSON 字串中，然後在金鑰保存庫中儲存為密碼  。</span><span class="sxs-lookup"><span data-stu-id="31f4b-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="31f4b-180">若要讓這個程序更容易，可使用 PowerShell 模組 ([GitHub 上有提供][service-fabric-rp-helpers])。</span><span class="sxs-lookup"><span data-stu-id="31f4b-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="31f4b-181">請依照這些步驟使用模組：</span><span class="sxs-lookup"><span data-stu-id="31f4b-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="31f4b-182">將儲存機制的完整內容下載到本機目錄中。</span><span class="sxs-lookup"><span data-stu-id="31f4b-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="31f4b-183">在您的 PowerShell 視窗中匯入模組：</span><span class="sxs-lookup"><span data-stu-id="31f4b-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="31f4b-184">此 PowerShell 模組中的 `Invoke-AddCertToKeyVault` 命令會自動將憑證私密金鑰的格式設定為 JSON 字串，並將它上傳到金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="31f4b-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="31f4b-185">請用它來將叢集憑證與任何其他應用程式憑證新增到金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="31f4b-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="31f4b-186">請為您想在叢集中安裝的任何其他憑證重複這個步驟。</span><span class="sxs-lookup"><span data-stu-id="31f4b-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="31f4b-187">這些是設定 Service Fabric 叢集 Resource Manager 範本時的所有金鑰保存庫必要條件，該範本會安裝用於節點驗證、管理端點安全性和驗證，以及使用 X.509 憑證的任何其他應用程式安全性功能的憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="31f4b-188">此時，您應該已經在 Azure 中建立以下項目：</span><span class="sxs-lookup"><span data-stu-id="31f4b-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="31f4b-189">金鑰保存庫資源群組</span><span class="sxs-lookup"><span data-stu-id="31f4b-189">Key Vault resource group</span></span>
  * <span data-ttu-id="31f4b-190">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="31f4b-190">Key Vault</span></span>
    * <span data-ttu-id="31f4b-191">叢集伺服器驗證憑證</span><span class="sxs-lookup"><span data-stu-id="31f4b-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="31f4b-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="31f4b-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="31f4b-193">在 Azure 入口網站中建立叢集</span><span class="sxs-lookup"><span data-stu-id="31f4b-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="31f4b-194">搜尋 Service Fabric 叢集資源</span><span class="sxs-lookup"><span data-stu-id="31f4b-194">Search for the Service Fabric cluster resource</span></span>
![在 Azure 入口網站上搜尋 Service Fabric 叢集範本。][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="31f4b-196">登入 [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="31f4b-197">按一下 [新增]  來新增資源範本。</span><span class="sxs-lookup"><span data-stu-id="31f4b-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="31f4b-198">在 [全部內容] 下方的 [Marketplace] 中搜尋 Service Fabric 叢集範本。</span><span class="sxs-lookup"><span data-stu-id="31f4b-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="31f4b-199">選取清單中的 [Service Fabric 叢集]  。</span><span class="sxs-lookup"><span data-stu-id="31f4b-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="31f4b-200">瀏覽至 [Service Fabric 叢集] 刀鋒視窗，按一下 [建立]，</span><span class="sxs-lookup"><span data-stu-id="31f4b-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="31f4b-201">[建立 Service Fabric 叢集]  刀鋒視窗具有下列四個步驟。</span><span class="sxs-lookup"><span data-stu-id="31f4b-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="31f4b-202">1.基本概念</span><span class="sxs-lookup"><span data-stu-id="31f4b-202">1. Basics</span></span>
![建立新資源群組的螢幕擷取畫面。][CreateRG]

<span data-ttu-id="31f4b-204">在 [基本] 刀鋒視窗中，您必須提供您的叢集的基本詳細資料。</span><span class="sxs-lookup"><span data-stu-id="31f4b-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="31f4b-205">輸入您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="31f4b-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="31f4b-206">輸入 VM 遠端桌面的 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="31f4b-207">請務必選取您要部署叢集的 [訂用帳戶]  ，尤其是在您擁有多個訂用帳戶時。</span><span class="sxs-lookup"><span data-stu-id="31f4b-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="31f4b-208">建立 **新的資源群組**。</span><span class="sxs-lookup"><span data-stu-id="31f4b-208">Create a **new resource group**.</span></span> <span data-ttu-id="31f4b-209">最好讓它與叢集同名，因為這有助於稍後尋找它們，尤其是當您嘗試變更您的部署及刪除您的叢集時，特別有用。</span><span class="sxs-lookup"><span data-stu-id="31f4b-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31f4b-210">雖然您可以決定使用現有的資源群組，但最好還是建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="31f4b-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="31f4b-211">這可讓您輕鬆地刪除您不需要的叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="31f4b-212">選取您要在其中建立叢集的 [區域]  。</span><span class="sxs-lookup"><span data-stu-id="31f4b-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="31f4b-213">您必須使用金鑰保存庫所在的相同區域。</span><span class="sxs-lookup"><span data-stu-id="31f4b-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="31f4b-214">2.叢集組態</span><span class="sxs-lookup"><span data-stu-id="31f4b-214">2. Cluster configuration</span></span>
![建立節點類型][CreateNodeType]

<span data-ttu-id="31f4b-216">設定您的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="31f4b-216">Configure your cluster nodes.</span></span> <span data-ttu-id="31f4b-217">可用來定義定義 VM 的大小、VM 的數目，以及 VM 的屬性。</span><span class="sxs-lookup"><span data-stu-id="31f4b-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="31f4b-218">您的叢集可以有多個節點類型，但主要節點類型 (您在入口網站定義的第一個節點類型) 必須至少有 5 個 VM。這是 Service Fabric 系統服務放置所在的節點類型。</span><span class="sxs-lookup"><span data-stu-id="31f4b-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="31f4b-219">請勿設定 [放置屬性]，因為會自動新增 "NodeTypeName" 預設放置屬性。</span><span class="sxs-lookup"><span data-stu-id="31f4b-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="31f4b-220">多個節點類型的常見案例是包含前端服務和後端服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="31f4b-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="31f4b-221">您想要將「前端」服務放在連接埠對網際網路開放的較小型 VM (D2 等 VM 大小) 上，但想要將「後端」服務放在沒有對網際網路開放連接埠的較大型 VM (D4、D6、D15 等 VM 大小) 上。</span><span class="sxs-lookup"><span data-stu-id="31f4b-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="31f4b-222">選擇節點類型的名稱 (1 到 12 個字元，只能包含字母和數字)。</span><span class="sxs-lookup"><span data-stu-id="31f4b-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="31f4b-223">主要節點類型的 VM **大小**下限取決於您為叢集選擇的**持久性**層級。</span><span class="sxs-lookup"><span data-stu-id="31f4b-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="31f4b-224">持久性層級的預設值為 Bronze。</span><span class="sxs-lookup"><span data-stu-id="31f4b-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="31f4b-225">如需持久性的詳細資訊，請參閱[如何選擇 Service Fabric 叢集可靠性和持久性][service-fabric-cluster-capacity]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="31f4b-226">選取 VM 大小和定價層。</span><span class="sxs-lookup"><span data-stu-id="31f4b-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="31f4b-227">D 系列 VM 擁有 SSD 磁碟機，且強烈建議用於具狀態應用程式。</span><span class="sxs-lookup"><span data-stu-id="31f4b-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="31f4b-228">請勿使用只有部分核心或可用磁碟容量少於 7 GB 的任何 VM SKU。</span><span class="sxs-lookup"><span data-stu-id="31f4b-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="31f4b-229">主要節點類型的 VM **數目**下限取決於您選擇的**可靠性**層級。</span><span class="sxs-lookup"><span data-stu-id="31f4b-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="31f4b-230">可靠性層級的預設值為 Silver。</span><span class="sxs-lookup"><span data-stu-id="31f4b-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="31f4b-231">如需可靠性的詳細資訊，請參閱[如何選擇 Service Fabric 叢集可靠性和持久性][service-fabric-cluster-capacity]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="31f4b-232">選擇節點類型的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="31f4b-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="31f4b-233">您可以在稍後相應增加或相應減少節點類型中的 VM 數目，但在主要節點類型上，數目下限取決於您選擇的可靠性層級。</span><span class="sxs-lookup"><span data-stu-id="31f4b-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="31f4b-234">其他節點類型可以有 1 個 VM 的下限。</span><span class="sxs-lookup"><span data-stu-id="31f4b-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="31f4b-235">設定自訂端點。</span><span class="sxs-lookup"><span data-stu-id="31f4b-235">Configure custom endpoints.</span></span> <span data-ttu-id="31f4b-236">此欄位可讓您輸入以逗號區隔的連接埠清單，您可以透過 Azure Load Balancer 針對您的應用程式向公用網際網路公開這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="31f4b-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="31f4b-237">例如，如果您計劃對您的叢集部署 Web 應用程式，請在這裡輸入「80」來允許連接埠 80 的流量進入您的叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="31f4b-238">如需端點的詳細資訊，請參閱[與應用程式通訊][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="31f4b-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="31f4b-239">設定叢集**診斷**。</span><span class="sxs-lookup"><span data-stu-id="31f4b-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="31f4b-240">預設會在您的叢集上啟用診斷功能，以協助排解疑難問題。</span><span class="sxs-lookup"><span data-stu-id="31f4b-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="31f4b-241">如果您要停用診斷，請將其 [狀態] 切換至 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="31f4b-242">**不**建議將診斷關閉。</span><span class="sxs-lookup"><span data-stu-id="31f4b-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="31f4b-243">選取您想要為叢集設定的 Fabric 升級模式。</span><span class="sxs-lookup"><span data-stu-id="31f4b-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="31f4b-244">如果您要讓系統自動挑選最新可用的版本，並嘗試將叢集升級到此版本，請選取 [自動] 。</span><span class="sxs-lookup"><span data-stu-id="31f4b-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="31f4b-245">如果您想要選擇支援的版本，將模式設定為 [手動] 。</span><span class="sxs-lookup"><span data-stu-id="31f4b-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="31f4b-246">我們支援的叢集限於執行支援的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="31f4b-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="31f4b-247">如果選取 [手動]  模式，您必須負責將叢集升級到支援的版本。</span><span class="sxs-lookup"><span data-stu-id="31f4b-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="31f4b-248">如需 Fabric 升級模式的詳細資訊，請參閱 [service-fabric-cluster-upgrade 文件][service-fabric-cluster-upgrade]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="31f4b-249">3.安全性</span><span class="sxs-lookup"><span data-stu-id="31f4b-249">3. Security</span></span>
![Azure 入口網站中安全性組態的螢幕擷取畫面。][SecurityConfigs]

<span data-ttu-id="31f4b-251">最後一個步驟是使用金鑰保存庫和稍早建立的憑證資訊，提供憑證資訊來保護叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="31f4b-252">將使用 **PowerShell 命令把** 叢集憑證 `Invoke-AddCertToKeyVault` 上傳至金鑰保存庫時取得的輸出填入主要憑證欄位。</span><span class="sxs-lookup"><span data-stu-id="31f4b-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="31f4b-253">選取 [設定進階設定] 核取方塊來輸入**系統管理用戶端**和**唯讀用戶端**的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31f4b-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="31f4b-254">在這些欄位中，輸入系統管理用戶端憑證的指紋和唯讀使用者用戶端憑證的指紋 (如果適用)。</span><span class="sxs-lookup"><span data-stu-id="31f4b-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="31f4b-255">當系統管理員嘗試連線叢集時，只有在他們的憑證指紋和這裡輸入的指紋值相符時，才會被授與存取權。</span><span class="sxs-lookup"><span data-stu-id="31f4b-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="31f4b-256">4.摘要</span><span class="sxs-lookup"><span data-stu-id="31f4b-256">4. Summary</span></span>
![<span data-ttu-id="31f4b-257">顯示 [部署 Service Fabric 叢集] 的開始面板的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="31f4b-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="31f4b-258">若要完成叢集建立程序，請按一下 [摘要]  來查看您提供的組態，或是下載用來部署叢集的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="31f4b-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="31f4b-259">在您提供必要的設定之後，[確定]  按鈕會變成綠色，您只要按一下該按鈕就可以啟動叢集建立程序。</span><span class="sxs-lookup"><span data-stu-id="31f4b-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="31f4b-260">您可以在通知功能中看到叢集的建立進度。</span><span class="sxs-lookup"><span data-stu-id="31f4b-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="31f4b-261">(請按一下畫面右上角狀態列附近的鈴噹圖示。)如果您在建立叢集時按了 [釘選到「開始面板」]，您將會看到 [部署 Service Fabric 叢集] 已釘選到 [開始] 面板。</span><span class="sxs-lookup"><span data-stu-id="31f4b-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="31f4b-262">檢視叢集狀態</span><span class="sxs-lookup"><span data-stu-id="31f4b-262">View your cluster status</span></span>
![顯示叢集詳細資料的儀表板螢幕擷取畫面。][ClusterDashboard]

<span data-ttu-id="31f4b-264">建立叢集之後，您就可以在入口網站檢查您的叢集：</span><span class="sxs-lookup"><span data-stu-id="31f4b-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="31f4b-265">移至 [瀏覽]，然後按一下 [Service Fabric 叢集]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="31f4b-266">找出您的叢集，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="31f4b-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="31f4b-267">現在儀表板會顯示叢集的詳細資料，包括叢集的公用端點和 Service Fabric Explorer 的連結。</span><span class="sxs-lookup"><span data-stu-id="31f4b-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="31f4b-268">叢集之儀表板刀鋒視窗上的 [節點監視器]  區段會指出健康狀態良好和不良的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="31f4b-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="31f4b-269">如需進一步了解叢集健康狀態，請參閱 [Service Fabric 健康狀態模型簡介][service-fabric-health-introduction]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="31f4b-270">Service Fabric 叢集需要有一定數量的節點保持運作中，以維護可用性並維持狀態 - 稱為「維持仲裁」。</span><span class="sxs-lookup"><span data-stu-id="31f4b-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="31f4b-271">因此，除非您已先執行[狀態的完整備份][service-fabric-reliable-services-backup-restore]，否則關閉叢集中的所有電腦通常並不安全。</span><span class="sxs-lookup"><span data-stu-id="31f4b-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="31f4b-272">遠端連接到虛擬機器擴展集執行個體或叢集節點</span><span class="sxs-lookup"><span data-stu-id="31f4b-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="31f4b-273">您在叢集中指定的每個 NodeTypes 都會形成虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="31f4b-274">如需詳細資料，請參閱[遠端連接到虛擬機器擴展集執行個體][remote-connect-to-a-vm-scale-set]。</span><span class="sxs-lookup"><span data-stu-id="31f4b-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f4b-275">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31f4b-275">Next steps</span></span>
<span data-ttu-id="31f4b-276">此時，您擁有一個使用憑證來管理驗證的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="31f4b-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="31f4b-277">接下來，請[連線到您的叢集](service-fabric-connect-to-secure-cluster.md)並了解如何[管理應用程式密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="31f4b-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="31f4b-278">同時，了解 [Service Fabric 支援選項](service-fabric-support.md)。</span><span class="sxs-lookup"><span data-stu-id="31f4b-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
