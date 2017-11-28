---
title: "從範本建立 Azure Service Fabric 叢集 | Microsoft Docs"
description: "本文說明如何使用 Azure Resource Manager、Azure Key Vault 及 Azure Active Directory (Azure AD) 來進行用戶端驗證，在 Azure 中設定安全的 Service Fabric 叢集。"
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
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="57d85-103">使用 Azure Resource Manager 來建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="57d85-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57d85-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57d85-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="57d85-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="57d85-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="57d85-106">此逐步指南可逐步引導您使用 Azure Resource Manager 在 Azure 中設定安全的 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="57d85-107">我們承認本文很長。</span><span class="sxs-lookup"><span data-stu-id="57d85-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="57d85-108">不過，除非您已經徹底熟悉內容，否則請務必仔細遵循每個步驟。</span><span class="sxs-lookup"><span data-stu-id="57d85-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="57d85-109">本指南涵蓋下列程序：</span><span class="sxs-lookup"><span data-stu-id="57d85-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="57d85-110">設定 Azure Key Vault 以上傳叢集和應用程式安全性的憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="57d85-111">使用 Azure Resource Manager 在 Azure 中建立受保護的叢集</span><span class="sxs-lookup"><span data-stu-id="57d85-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="57d85-112">使用適用於叢集管理的 Azure Active Directory (Azure AD) 來驗證使用者</span><span class="sxs-lookup"><span data-stu-id="57d85-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="57d85-113">安全的叢集是可防止以未經授權的方式存取管理作業的叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="57d85-114">這包括部署、升級和刪除應用程式、服務及其包含的資料。</span><span class="sxs-lookup"><span data-stu-id="57d85-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="57d85-115">不安全的叢集是任何人都可以隨時連線並執行管理作業的叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="57d85-116">雖然可以建立不安全的叢集，但強烈建議您從一開始就建立安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="57d85-117">由於無法在稍後再針對不安全的叢集進行保護，因此必須建立新叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="57d85-118">不論是 Linux 叢集還是 Windows 叢集，建立安全叢集的概念都是相同的。</span><span class="sxs-lookup"><span data-stu-id="57d85-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="57d85-119">如需建立安全 Linux 叢集的詳細資訊和協助程式指令碼，請參閱[在 Linux 上建立安全叢集](#secure-linux-clusters)。</span><span class="sxs-lookup"><span data-stu-id="57d85-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="57d85-120">登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="57d85-120">Sign in to your Azure account</span></span>
<span data-ttu-id="57d85-121">本指南使用 [Azure PowerShell][azure-powershell]。</span><span class="sxs-lookup"><span data-stu-id="57d85-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="57d85-122">開始新的 PowerShell 工作階段時，請先登入您的 Azure 帳戶並選取您的訂用帳戶，然後再執行 Azure 命令。</span><span class="sxs-lookup"><span data-stu-id="57d85-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="57d85-123">登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="57d85-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="57d85-124">選取您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="57d85-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="57d85-125">設定 Key Vault</span><span class="sxs-lookup"><span data-stu-id="57d85-125">Set up a key vault</span></span>
<span data-ttu-id="57d85-126">本節說明如何為 Azure 中的 Service Fabric 叢集和為 Service Fabric 應用程式建立 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="57d85-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="57d85-127">如需 Azure Key Vault 的完整指南，請參閱 [Key Vault 入門指南][key-vault-get-started]。</span><span class="sxs-lookup"><span data-stu-id="57d85-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="57d85-128">Service Fabric 會使用 X.509 憑證來保護叢集，並提供應用程式的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="57d85-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="57d85-129">您可以使用 Key Vault 來管理 Azure 中 Service Fabric 叢集的憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="57d85-130">在 Azure 中部署叢集時，負責建立 Service Fabric 叢集的 Azure 資源提供者會從 Key Vault 提取憑證，然後將它們安裝在叢集 VM 上。</span><span class="sxs-lookup"><span data-stu-id="57d85-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="57d85-131">下圖說明 Azure Key Vault、Service Fabric 叢集及 Azure 資源提供者 (會在建立叢集時使用 Key Vault 中所存憑證) 之間的關係：</span><span class="sxs-lookup"><span data-stu-id="57d85-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![憑證安裝圖][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="57d85-133">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="57d85-133">Create a resource group</span></span>
<span data-ttu-id="57d85-134">第一個步驟是特別針對 Key Vault 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="57d85-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="57d85-135">建議您將 Key Vault 放入其自己的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="57d85-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="57d85-136">此動作可讓您移除計算和儲存體資源群組 (包括含有 Service Fabric 叢集的資源群組)，而不會遺失您的金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="57d85-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="57d85-137">含有您 Key Vault 的資源群組必須與正在使用它的叢集位於「相同區域」。</span><span class="sxs-lookup"><span data-stu-id="57d85-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="57d85-138">如果您打算在多個區域中部署叢集，建議您在命名資源群組和 Key Vault 時，使用能指出其所屬區域的方式。</span><span class="sxs-lookup"><span data-stu-id="57d85-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="57d85-139">輸出應該會看起來如下：</span><span class="sxs-lookup"><span data-stu-id="57d85-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="57d85-140">在新的資源群組中建立 Key Vault</span><span class="sxs-lookup"><span data-stu-id="57d85-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="57d85-141">Key Vault 「必須經啟用為可供部署使用」，才能讓計算資源提供者從它取得憑證，然後將它安裝在虛擬機器執行個體上：</span><span class="sxs-lookup"><span data-stu-id="57d85-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="57d85-142">輸出應該會看起來如下：</span><span class="sxs-lookup"><span data-stu-id="57d85-142">The output should look like this:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="57d85-143">使用現有的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="57d85-143">Use an existing key vault</span></span>

<span data-ttu-id="57d85-144">若要使用現有的 Key Vault，您「必須將它啟用為可供部署使用」，才能讓計算資源提供者從它取得憑證，然後將它安裝在叢集節點上：</span><span class="sxs-lookup"><span data-stu-id="57d85-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="57d85-145">將憑證新增至 Key Vault</span><span class="sxs-lookup"><span data-stu-id="57d85-145">Add certificates to your key vault</span></span>

<span data-ttu-id="57d85-146">憑證是在 Service Fabric 中用來提供驗證與加密，以保護叢集和其應用程式的各個層面。</span><span class="sxs-lookup"><span data-stu-id="57d85-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="57d85-147">如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例][service-fabric-cluster-security]。</span><span class="sxs-lookup"><span data-stu-id="57d85-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="57d85-148">叢集和伺服器憑證 (必要)</span><span class="sxs-lookup"><span data-stu-id="57d85-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="57d85-149">需要此憑證來保護叢集安全及防止未經授權存取叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="57d85-150">它會透過兩種方式提供叢集安全性：</span><span class="sxs-lookup"><span data-stu-id="57d85-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="57d85-151">叢集驗證：驗證叢集同盟的節點對節點通訊。</span><span class="sxs-lookup"><span data-stu-id="57d85-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="57d85-152">只有可使用此憑證提供其身分識別的節點可以加入叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="57d85-153">伺服器驗證：向管理用戶端驗證叢集管理端點，讓管理用戶端知道正在交談的對象是真正的叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="57d85-154">此憑證也會為 HTTPS 管理 API 及透過 HTTPS 使用的 Service Fabric Explorer 提供 SSL。</span><span class="sxs-lookup"><span data-stu-id="57d85-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="57d85-155">為用於這些用途，憑證必須符合下列要求：</span><span class="sxs-lookup"><span data-stu-id="57d85-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="57d85-156">憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="57d85-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="57d85-157">憑證必須是為了進行金鑰交換而建立，且可匯出成個人資訊交換 (.pfx) 檔案。</span><span class="sxs-lookup"><span data-stu-id="57d85-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="57d85-158">憑證的主體名稱必須與您用來存取 Service Fabric 叢集的網域相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="57d85-159">必須如此相符，才能為叢集的 HTTPS 管理端點和 Service Fabric Explorer 提供 SSL。</span><span class="sxs-lookup"><span data-stu-id="57d85-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="57d85-160">您無法從憑證授權單位 (CA) 取得 .cloudapp.azure.com 網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="57d85-161">您必須為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="57d85-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="57d85-162">當您向 CA 要求憑證時，憑證的主體名稱必須與用於您叢集的自訂網域名稱相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="57d85-163">應用程式憑證 (選用)</span><span class="sxs-lookup"><span data-stu-id="57d85-163">Application certificates (optional)</span></span>
<span data-ttu-id="57d85-164">您可以針對應用程式安全性目的，在叢集上安裝任何數目的其他憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="57d85-165">在建立您的叢集之前，請考量需要在節點上安裝憑證的應用程式安全性案例，例如：</span><span class="sxs-lookup"><span data-stu-id="57d85-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="57d85-166">將應用程式組態值加密和解密。</span><span class="sxs-lookup"><span data-stu-id="57d85-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="57d85-167">在複寫期間將資料跨節點加密。</span><span class="sxs-lookup"><span data-stu-id="57d85-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="57d85-168">格式化憑證以供 Azure 資源提供者使用</span><span class="sxs-lookup"><span data-stu-id="57d85-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="57d85-169">您可以透過 Key Vault 來直接新增和使用私密金鑰檔案 (.pfx)。</span><span class="sxs-lookup"><span data-stu-id="57d85-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="57d85-170">不過，Azure 計算資源提供者要求必須以特殊「JavaScript 物件標記法」(JSON) 格式儲存金鑰。</span><span class="sxs-lookup"><span data-stu-id="57d85-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="57d85-171">此格式包含 .pfx 檔案作為 Base-64 編碼字串和私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="57d85-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="57d85-172">為了符合這些要求，金鑰必須放在 JSON 字串中，然後在 Key Vault 中儲存為「密碼」。</span><span class="sxs-lookup"><span data-stu-id="57d85-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="57d85-173">若要讓這個程序更容易，可使用 PowerShell 模組 ([GitHub 上有提供][service-fabric-rp-helpers])。</span><span class="sxs-lookup"><span data-stu-id="57d85-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="57d85-174">若要使用該模組，請執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="57d85-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="57d85-175">將儲存機制的完整內容下載到本機目錄中。</span><span class="sxs-lookup"><span data-stu-id="57d85-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="57d85-176">移至本機目錄。</span><span class="sxs-lookup"><span data-stu-id="57d85-176">Go to the local directory.</span></span>
2. <span data-ttu-id="57d85-177">在您的 PowerShell 視窗中匯入 ServiceFabricRPHelpers 模組：</span><span class="sxs-lookup"><span data-stu-id="57d85-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="57d85-178">此 PowerShell 模組中的 `Invoke-AddCertToKeyVault` 命令會自動將憑證私密金鑰的格式設定為 JSON 字串，並將它上傳到 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="57d85-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="57d85-179">請使用此命令將叢集憑證及任何其他應用程式憑證新增到 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="57d85-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="57d85-180">請為您想在叢集中安裝的任何其他憑證重複這個步驟。</span><span class="sxs-lookup"><span data-stu-id="57d85-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="57d85-181">上傳現有的憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="57d85-182">如果您收到如這裡顯示的錯誤，通常表示有資源 URL 發生衝突的情形。</span><span class="sxs-lookup"><span data-stu-id="57d85-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="57d85-183">為了解決衝突，請變更 Key Vault 名稱。</span><span class="sxs-lookup"><span data-stu-id="57d85-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="57d85-184">解決衝突之後，輸出看起來應該會像這樣：</span><span class="sxs-lookup"><span data-stu-id="57d85-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="57d85-185">您需要 CertificateThumbprint、SourceVault 及 CertificateURL 這前三個字串，才能設定安全的 Service Fabric 叢集及取得您可能用於應用程式安全性的任何應用程式憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="57d85-186">如果您未儲存這些字串，可能很難在稍後透過查詢 Key Vault 來擷取它們。</span><span class="sxs-lookup"><span data-stu-id="57d85-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="57d85-187">建立自我簽署憑證並上傳到 Key Vault</span><span class="sxs-lookup"><span data-stu-id="57d85-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="57d85-188">如果您已將憑證上傳到 Key Vault，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="57d85-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="57d85-189">此步驟是用來產生新的自我簽署憑證，並將其上傳到 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="57d85-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="57d85-190">在變更下列指令碼中的參數並執行它之後，系統應該會提示您輸入憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="57d85-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="57d85-191">如果您收到如這裡顯示的錯誤，通常表示有資源 URL 發生衝突的情形。</span><span class="sxs-lookup"><span data-stu-id="57d85-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="57d85-192">為了解決衝突，請變更 Key Vault 名稱、RG 名稱等。</span><span class="sxs-lookup"><span data-stu-id="57d85-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="57d85-193">解決衝突之後，輸出看起來應該會像這樣：</span><span class="sxs-lookup"><span data-stu-id="57d85-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="57d85-194">您需要 CertificateThumbprint、SourceVault 及 CertificateURL 這前三個字串，才能設定安全的 Service Fabric 叢集及取得您可能用於應用程式安全性的任何應用程式憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="57d85-195">如果您未儲存這些字串，可能很難在稍後透過查詢 Key Vault 來擷取它們。</span><span class="sxs-lookup"><span data-stu-id="57d85-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="57d85-196">此時，您應該已經備妥下列元素：</span><span class="sxs-lookup"><span data-stu-id="57d85-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="57d85-197">Key Vault 資源群組。</span><span class="sxs-lookup"><span data-stu-id="57d85-197">The key vault resource group.</span></span>
* <span data-ttu-id="57d85-198">Key Vault 及其 URL (在先前的 PowerShell 輸出中稱為 SourceVault)。</span><span class="sxs-lookup"><span data-stu-id="57d85-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="57d85-199">在 Key Vault 中的叢集伺服器驗證憑證及其 URL。</span><span class="sxs-lookup"><span data-stu-id="57d85-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="57d85-200">在 Key Vault 中的應用程式憑證及其 URL。</span><span class="sxs-lookup"><span data-stu-id="57d85-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="57d85-201">設定用戶端驗用的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57d85-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="57d85-202">Azure AD 可讓組織 (稱為租用戶) 管理使用者對應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="57d85-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="57d85-203">應用程式分成具有 Web 型登入 UI 的應用程式，以及具有原生用戶端體驗的應用程式。</span><span class="sxs-lookup"><span data-stu-id="57d85-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="57d85-204">在本文中，我們假設您已經建立租用戶。</span><span class="sxs-lookup"><span data-stu-id="57d85-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="57d85-205">如果您尚未建立租用戶，請從閱讀[如何取得 Azure Active Directory 租用戶][active-directory-howto-tenant]開始進行。</span><span class="sxs-lookup"><span data-stu-id="57d85-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="57d85-206">Service Fabric 叢集提供其管理功能的各種進入點 (包括 Web 型 [Service Fabric Explorer][service-fabric-visualizing-your-cluster] 和 [Visual Studio][service-fabric-manage-application-in-visual-studio])。</span><span class="sxs-lookup"><span data-stu-id="57d85-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="57d85-207">因此，您將建立兩個 Azure AD 應用程式來控制對叢集的存取：一個 Web 應用程式和一個原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="57d85-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="57d85-208">為了簡化與設定 Azure AD 搭配 Service Fabric 叢集相關的一些步驟，我們建立了一組 Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="57d85-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="57d85-209">建立叢集之前，您必須先完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="57d85-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="57d85-210">由於指令碼會預期叢集名稱和端點，因此這些值應該是計劃的值，而不是您已經建立的值。</span><span class="sxs-lookup"><span data-stu-id="57d85-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="57d85-211">[下載指令碼][sf-aad-ps-script-download]到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="57d85-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="57d85-212">在 zip 檔案上按一下滑鼠右鍵，選取 [屬性]、選取 [解除封鎖] 核取方塊，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="57d85-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="57d85-213">解壓縮 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="57d85-213">Extract the zip file.</span></span>
4. <span data-ttu-id="57d85-214">執行 `SetupApplications.ps1`，並且提供 TenantId、ClusterName 和 WebApplicationReplyUrl 作為參數。</span><span class="sxs-lookup"><span data-stu-id="57d85-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="57d85-215">例如：</span><span class="sxs-lookup"><span data-stu-id="57d85-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="57d85-216">您可以執行 PowerShell 命令 `Get-AzureSubscription` 來找出您的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="57d85-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="57d85-217">執行此命令會顯示每個訂用帳戶的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="57d85-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="57d85-218">ClusterName 是用來加在指令碼所建立 Azure AD 應用程式的前面。</span><span class="sxs-lookup"><span data-stu-id="57d85-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="57d85-219">它不需要與實際叢集名稱完全相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="57d85-220">其用意只是要讓您更容易將 Azure AD 構件對應到與之搭配使用的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="57d85-221">WebApplicationReplyUrl 是在您的使用者完成登入之後，Azure AD 傳回給他們的預設端點。</span><span class="sxs-lookup"><span data-stu-id="57d85-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="57d85-222">請將此端點設定為您叢集的 Service Fabric Explorer 端點，預設為︰</span><span class="sxs-lookup"><span data-stu-id="57d85-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="57d85-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="57d85-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="57d85-224">系統會提示您登入具有 Azure AD 租用戶系統管理權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="57d85-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="57d85-225">在您登入之後，指令碼會建立 Web 和原生應用程式來代表 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="57d85-226">如果您在 [Azure 傳統入口網站][azure-classic-portal]中查看租用戶的應用程式，則應該會看到兩個新項目︰</span><span class="sxs-lookup"><span data-stu-id="57d85-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="57d85-227">*ClusterName*\_叢集</span><span class="sxs-lookup"><span data-stu-id="57d85-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="57d85-228">*ClusterName*\_用戶端</span><span class="sxs-lookup"><span data-stu-id="57d85-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="57d85-229">此指令碼會列印您在下一節建立叢集時 Azure Resource Manager 範本所需的 JSON，因此建議讓 PowerShell 視窗保持開啟。</span><span class="sxs-lookup"><span data-stu-id="57d85-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="57d85-230">建立 Service Fabric 叢集 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="57d85-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="57d85-231">在本節中，Service Fabric 叢集 Resource Manager 範本中會使用上述 PowerShell 命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="57d85-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="57d85-232">您可以從 [GitHub 上的 Azure 快速啟動範本資源庫][azure-quickstart-templates]取得範例 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="57d85-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="57d85-233">這些範本可以用作叢集範本的起點。</span><span class="sxs-lookup"><span data-stu-id="57d85-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="57d85-234">建立 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="57d85-234">Create the Resource Manager template</span></span>
<span data-ttu-id="57d85-235">本指南使用[五節點安全叢集][service-fabric-secure-cluster-5-node-1-nodetype]範例範本和範本參數。</span><span class="sxs-lookup"><span data-stu-id="57d85-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="57d85-236">下載 `azuredeploy.json` 和 `azuredeploy.parameters.json` 到您的電腦並在您最愛的文字編輯器中開啟這兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="57d85-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="57d85-237">新增憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-237">Add certificates</span></span>
<span data-ttu-id="57d85-238">您可以藉由參考包含憑證金鑰的 Key Vault，將憑證新增到叢集 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="57d85-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="57d85-239">建議您將 Key Vault 值置於 Resource Manager 範本參數檔案中。</span><span class="sxs-lookup"><span data-stu-id="57d85-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="57d85-240">這麼做會讓 Resource Manager 範本檔案保持可重複使用，而不會含有某項部署特定的值。</span><span class="sxs-lookup"><span data-stu-id="57d85-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="57d85-241">將所有憑證都新增到虛擬機器擴展集 osProfile</span><span class="sxs-lookup"><span data-stu-id="57d85-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="57d85-242">安裝在叢集中的每個憑證都必須在擴展集資源 (Microsoft.Compute/virtualMachineScaleSets) 的 osProfile 區段中設定妥當。</span><span class="sxs-lookup"><span data-stu-id="57d85-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="57d85-243">此動作會指示資源提供者在 VM 上安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="57d85-244">此安裝既包含叢集憑證，也包含任何您打算用於應用程式的應用程式安全性憑證︰</span><span class="sxs-lookup"><span data-stu-id="57d85-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

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

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="57d85-245">設定 Service Fabric 叢集憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="57d85-246">不論是在 Service Fabric 叢集資源 (Microsoft.ServiceFabric/clusters) 中，還是在虛擬機器擴展集資源中虛擬機器擴展集的 Service Fabric 延伸模組中，都必須設定叢集驗證憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="57d85-247">這個安排可讓 Service Fabric 資源提供者設定它，以用於管理端點的叢集驗證和伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="57d85-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="57d85-248">虛擬機器擴展集資源：</span><span class="sxs-lookup"><span data-stu-id="57d85-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="57d85-249">Service Fabric 資源︰</span><span class="sxs-lookup"><span data-stu-id="57d85-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="57d85-250">插入 Azure AD 組態</span><span class="sxs-lookup"><span data-stu-id="57d85-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="57d85-251">您稍早建立的 Azure AD 組態可以直接插入到您的 Resource Manager 範本中。</span><span class="sxs-lookup"><span data-stu-id="57d85-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="57d85-252">不過，建議您先將值擷取到參數檔案中，以便讓 Resource Manager 範本保持可重複使用，而不會含有某項部署特定的值。</span><span class="sxs-lookup"><span data-stu-id="57d85-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

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

### <span data-ttu-id="57d85-253"><a "configure-arm" ></a>設定 Resource Manager 範本參數</span><span class="sxs-lookup"><span data-stu-id="57d85-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="57d85-254">最後，請使用 Key Vault 和 Azure AD PowerShell 命令的輸出值來填入參數檔案︰</span><span class="sxs-lookup"><span data-stu-id="57d85-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

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
<span data-ttu-id="57d85-255">此時，您應該已經備妥下列元素：</span><span class="sxs-lookup"><span data-stu-id="57d85-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="57d85-256">Key Vault 資源群組</span><span class="sxs-lookup"><span data-stu-id="57d85-256">Key vault resource group</span></span>
  * <span data-ttu-id="57d85-257">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="57d85-257">Key vault</span></span>
  * <span data-ttu-id="57d85-258">叢集伺服器驗證憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="57d85-259">資料編密憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-259">Data encipherment certificate</span></span>
* <span data-ttu-id="57d85-260">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="57d85-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="57d85-261">適用於 Web 型管理和 Service Fabric Explorer 的 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="57d85-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="57d85-262">適用於原生用戶端管理的 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="57d85-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="57d85-263">使用者及其獲指派的角色</span><span class="sxs-lookup"><span data-stu-id="57d85-263">Users and their assigned roles</span></span>
* <span data-ttu-id="57d85-264">Service Fabric 叢集 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="57d85-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="57d85-265">透過 Key Vault 設定的憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="57d85-266">已設定 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57d85-266">Azure Active Directory configured</span></span>

<span data-ttu-id="57d85-267">下圖說明 Key Vault 和 Azure AD 組態在 Resource Manager 範本中發生作用的位置。</span><span class="sxs-lookup"><span data-stu-id="57d85-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Resource Manager 相依性對應][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="57d85-269">建立叢集</span><span class="sxs-lookup"><span data-stu-id="57d85-269">Create the cluster</span></span>
<span data-ttu-id="57d85-270">您現在已準備好使用 [Azure 資源範本部署][resource-group-template-deploy]來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="57d85-271">進行測試</span><span class="sxs-lookup"><span data-stu-id="57d85-271">Test it</span></span>
<span data-ttu-id="57d85-272">使用下列 PowerShell 命令，以參數檔案來測試 Resource Manager 範本︰</span><span class="sxs-lookup"><span data-stu-id="57d85-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="57d85-273">進行部署</span><span class="sxs-lookup"><span data-stu-id="57d85-273">Deploy it</span></span>
<span data-ttu-id="57d85-274">如果 Resource Manager 範本測試通過，使用下列 PowerShell 命令，以參數檔案來部署 Resource Manager 範本︰</span><span class="sxs-lookup"><span data-stu-id="57d85-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="57d85-275">將使用者指派給角色</span><span class="sxs-lookup"><span data-stu-id="57d85-275">Assign users to roles</span></span>
<span data-ttu-id="57d85-276">建立應用程式來代表您的叢集之後，請將使用者指派給 Service Fabric 所支援的角色︰唯讀和系統管理員。您可以使用 [Azure 傳統入口網站][azure-classic-portal]來指派角色。</span><span class="sxs-lookup"><span data-stu-id="57d85-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="57d85-277">在 Azure 入口網站中，移至您的租用戶，然後選取 [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="57d85-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="57d85-278">選取 Web 應用程式 (其名稱類似 `myTestCluster_Cluster`)。</span><span class="sxs-lookup"><span data-stu-id="57d85-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="57d85-279">按一下 [使用者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="57d85-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="57d85-280">選取要指派的使用者，然後按一下畫面底部的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="57d85-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![將使用者指派給角色按鈕][assign-users-to-roles-button]
5. <span data-ttu-id="57d85-282">選取要指派給使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="57d85-282">Select the role to assign to the user.</span></span>

    ![[指派使用者] 對話方塊][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="57d85-284">如需 Service Fabric 中角色的詳細資訊，請參閱 [角色型存取控制 (適用於 Service Fabric 用戶端)](service-fabric-cluster-security-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="57d85-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="57d85-285">在 Linux 上建立安全叢集</span><span class="sxs-lookup"><span data-stu-id="57d85-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="57d85-286">為了簡化此程序，我們提供了一個[協助程式指令碼](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux)。</span><span class="sxs-lookup"><span data-stu-id="57d85-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="57d85-287">在使用此協助程式指令碼之前，請確定您已安裝 Azure 命令列介面 (CLI)，而且它位於您的路徑中。</span><span class="sxs-lookup"><span data-stu-id="57d85-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="57d85-288">下載指令碼後，請執行 `chmod +x cert_helper.py` ，以確定指令碼有執行權限。</span><span class="sxs-lookup"><span data-stu-id="57d85-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="57d85-289">第一個步驟是使用 CLI 搭配 `azure login` 命令來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57d85-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="57d85-290">登入 Azure 帳戶之後，請使用協助程式搭配您 CA 簽署的憑證，如下列命令所示︰</span><span class="sxs-lookup"><span data-stu-id="57d85-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="57d85-291">-ifile 參數可以搭配憑證類型 (pfx 或 pem，如果是自我簽署的憑證則是 ss) 接受 .pfx 檔案或 .pem 檔案作為輸入。</span><span class="sxs-lookup"><span data-stu-id="57d85-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="57d85-292">參數 -h 會列印出說明文字。</span><span class="sxs-lookup"><span data-stu-id="57d85-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="57d85-293">此命令會傳回下列三個字串做為輸出︰</span><span class="sxs-lookup"><span data-stu-id="57d85-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="57d85-294">SourceVaultID：這是它為您建立的新 KeyVault ResourceGroup 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="57d85-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="57d85-295">CertificateUrl：用於存取憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="57d85-296">CertificateThumbprint：用於驗證。</span><span class="sxs-lookup"><span data-stu-id="57d85-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="57d85-297">下列範例示範如何使用此命令︰</span><span class="sxs-lookup"><span data-stu-id="57d85-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="57d85-298">執行上述命令會提供下列三個字串給您︰</span><span class="sxs-lookup"><span data-stu-id="57d85-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="57d85-299">憑證的主體名稱必須與您用來存取 Service Fabric 叢集的網域相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="57d85-300">必須如此相符，才能為叢集的 HTTPS 管理端點和 Service Fabric Explorer 提供 SSL。</span><span class="sxs-lookup"><span data-stu-id="57d85-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="57d85-301">您無法從 CA 取得 `.cloudapp.azure.com` 網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="57d85-302">您必須為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="57d85-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="57d85-303">當您向 CA 要求憑證時，憑證的主體名稱必須與用於您叢集的自訂網域名稱相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="57d85-304">這些主體名稱是您建立安全 Service Fabric 叢集 (不含 Azure AD) 所需的項目，如[設定 Resource Manager 範本參數](#configure-arm)所述。</span><span class="sxs-lookup"><span data-stu-id="57d85-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="57d85-305">您可以依照[驗證用戶端對叢集的存取權](service-fabric-connect-to-secure-cluster.md)的指示來連接到安全叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="57d85-306">Linux 預覽叢集不支援 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="57d85-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="57d85-307">您可以指派系統管理員和用戶端角色，如[將使用者指派給角色](#assign-roles)一節所述。</span><span class="sxs-lookup"><span data-stu-id="57d85-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="57d85-308">為 Linux 預覽叢集指定系統管理員和用戶端角色時，您必須提供用於驗證的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="57d85-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="57d85-309">(您不須提供主體名稱，因為在此預覽版本中不會執行任何鏈結驗證或撤銷)。</span><span class="sxs-lookup"><span data-stu-id="57d85-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="57d85-310">如果您想要使用自我簽署的憑證來進行測試，可以使用相同的指令碼來產生該憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="57d85-311">您可以接著提供旗標 `ss` 而不是提供憑證名稱和憑證路徑，來將該憑證上傳到 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="57d85-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="57d85-312">例如，請參閱下列命令來建立及上傳自我簽署的憑證︰</span><span class="sxs-lookup"><span data-stu-id="57d85-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="57d85-313">此命令會傳回相同的三個字串：SourceVault、CertificateUrl 及 CertificateThumbprint。</span><span class="sxs-lookup"><span data-stu-id="57d85-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="57d85-314">您可以接著使用這些字串來建立安全的 Linux 叢集，以及放置自我簽署憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="57d85-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="57d85-315">您需要有自我簽署的憑證才能連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="57d85-316">您可以依照[驗證用戶端對叢集的存取權](service-fabric-connect-to-secure-cluster.md)的指示來連接到安全叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="57d85-317">憑證的主體名稱必須與您用來存取 Service Fabric 叢集的網域相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="57d85-318">必須如此相符，才能為叢集的 HTTPS 管理端點和 Service Fabric Explorer 提供 SSL。</span><span class="sxs-lookup"><span data-stu-id="57d85-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="57d85-319">您無法從 CA 取得 `.cloudapp.azure.com` 網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="57d85-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="57d85-320">您必須為您的叢集取得自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="57d85-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="57d85-321">當您向 CA 要求憑證時，憑證的主體名稱必須與用於您叢集的自訂網域名稱相符。</span><span class="sxs-lookup"><span data-stu-id="57d85-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="57d85-322">您可以在 Azure 入口網站中從協助程式指令碼填入參數，如[在 Azure 入口網站中建立叢集](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)一節所述。</span><span class="sxs-lookup"><span data-stu-id="57d85-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57d85-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57d85-323">Next steps</span></span>
<span data-ttu-id="57d85-324">此時，您已具有以 Azure Active Directory 提供管理驗證的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="57d85-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="57d85-325">接下來，請[連線到您的叢集](service-fabric-connect-to-secure-cluster.md)並了解如何[管理應用程式密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="57d85-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="57d85-326">針對設定用戶端驗用的 Azure Active Directory 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="57d85-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="57d85-327">如果您在設定用於用戶端驗證的 Azure AD 時遇到問題，請檢閱本節中可能的解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d85-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="57d85-328">Service Fabric Explorer 會提示您選取憑證</span><span class="sxs-lookup"><span data-stu-id="57d85-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="57d85-329">問題</span><span class="sxs-lookup"><span data-stu-id="57d85-329">Problem</span></span>
<span data-ttu-id="57d85-330">在 Service Fabric Explorer 中順利登入 Azure AD 之後，瀏覽器會返回首頁，但是會出現提示您選取憑證的訊息。</span><span class="sxs-lookup"><span data-stu-id="57d85-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![SFX 選取憑證對話方塊][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="57d85-332">原因</span><span class="sxs-lookup"><span data-stu-id="57d85-332">Reason</span></span>
<span data-ttu-id="57d85-333">使用者未獲指派 Azure AD 叢集應用程式中的角色。</span><span class="sxs-lookup"><span data-stu-id="57d85-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="57d85-334">因此，Azure AD 驗證在 Service Fabric 叢集上發生失敗。</span><span class="sxs-lookup"><span data-stu-id="57d85-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="57d85-335">Service Fabric Explorer 會回復到憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="57d85-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="57d85-336">方案</span><span class="sxs-lookup"><span data-stu-id="57d85-336">Solution</span></span>
<span data-ttu-id="57d85-337">請依照設定 Azure AD 的指示進行操作，然後指派使用者角色。</span><span class="sxs-lookup"><span data-stu-id="57d85-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="57d85-338">另外，建議您如 `SetupApplications.ps1` 所做的一樣，開啟 [存取應用程式需要使用者指派]。</span><span class="sxs-lookup"><span data-stu-id="57d85-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="57d85-339">使用 PowerShell 進行連線時失敗，發生錯誤：「指定的認證無效」</span><span class="sxs-lookup"><span data-stu-id="57d85-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="57d85-340">問題</span><span class="sxs-lookup"><span data-stu-id="57d85-340">Problem</span></span>
<span data-ttu-id="57d85-341">在您順利登入 Azure AD 之後，於使用 PowerShell 以 “AzureActiveDirectory” 安全性模式連接到叢集時連線失敗，發生錯誤：「指定的認證無效」。</span><span class="sxs-lookup"><span data-stu-id="57d85-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="57d85-342">方案</span><span class="sxs-lookup"><span data-stu-id="57d85-342">Solution</span></span>
<span data-ttu-id="57d85-343">此解決方案與前一個相同。</span><span class="sxs-lookup"><span data-stu-id="57d85-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="57d85-344">Service Fabric Explorer 在您登入時傳回失敗："AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="57d85-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="57d85-345">問題</span><span class="sxs-lookup"><span data-stu-id="57d85-345">Problem</span></span>
<span data-ttu-id="57d85-346">當您嘗試在 Service Fabric Explorer 中登入 Azure AD 時，頁面傳回失敗：「AADSTS50011：回覆地址 &lt;url&gt; 與針對應用程式設定的回覆地址不符：&lt;guid&gt;」。</span><span class="sxs-lookup"><span data-stu-id="57d85-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![SFX 回覆地址不相符][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="57d85-348">原因</span><span class="sxs-lookup"><span data-stu-id="57d85-348">Reason</span></span>
<span data-ttu-id="57d85-349">代表 Service Fabric Explorer 的叢集 (Web) 應用程式嘗試對照 Azure AD 來進行驗證，而它在要求中提供重新導向傳回 URL。</span><span class="sxs-lookup"><span data-stu-id="57d85-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="57d85-350">但該 URL 並未列在 Azure AD 應用程式 [回覆 URL] 清單中。</span><span class="sxs-lookup"><span data-stu-id="57d85-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="57d85-351">方案</span><span class="sxs-lookup"><span data-stu-id="57d85-351">Solution</span></span>
<span data-ttu-id="57d85-352">在叢集 (Web) 應用程式的 [設定] 索引標籤上，將 Service Fabric Explorer 的 URL 新增到 [回覆 URL] 清單中，或取代清單內的其中一個項目。</span><span class="sxs-lookup"><span data-stu-id="57d85-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="57d85-353">完成時，請儲存變更。</span><span class="sxs-lookup"><span data-stu-id="57d85-353">When you have finished, save your change.</span></span>

![Web 應用程式回覆 url][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="57d85-355">透過 PowerShell 使用 Azure AD 驗證來連接叢集</span><span class="sxs-lookup"><span data-stu-id="57d85-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="57d85-356">若要連接 Service Fabric 叢集，請使用下列 PowerShell 命令範例︰</span><span class="sxs-lookup"><span data-stu-id="57d85-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="57d85-357">若要了解 Connect-ServiceFabricCluster Cmdlet，請參閱 [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57d85-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="57d85-358">我是否可以在多個叢集中重複使用相同的 Azure AD 租用戶？</span><span class="sxs-lookup"><span data-stu-id="57d85-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="57d85-359">是。</span><span class="sxs-lookup"><span data-stu-id="57d85-359">Yes.</span></span> <span data-ttu-id="57d85-360">但是請務必將 Service Fabric Explorer 的 URL 新增到叢集 (Web) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57d85-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="57d85-361">否則 Service Fabric Explorer 無法運作。</span><span class="sxs-lookup"><span data-stu-id="57d85-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="57d85-362">為什麼在已啟用 Azure AD 的情況下仍然需要伺服器憑證？</span><span class="sxs-lookup"><span data-stu-id="57d85-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="57d85-363">FabricClient 和 FabricGateway 會執行相互驗證。</span><span class="sxs-lookup"><span data-stu-id="57d85-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="57d85-364">在 Azure AD 驗證期間，Azure AD 整合會將用戶端身分識別提供給伺服器，而伺服器憑證則用來驗證伺服器身分識別。</span><span class="sxs-lookup"><span data-stu-id="57d85-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="57d85-365">如需有關 Service Fabric 憑證的詳細資訊，請參閱 [X.509 憑證和 Service Fabric][x509-certificates-and-service-fabric]。</span><span class="sxs-lookup"><span data-stu-id="57d85-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

