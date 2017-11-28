---
title: "Azure 中的 HPC Pack 2016 叢集 | Microsoft Docs"
description: "了解如何在 Azure 中部署 HPC Pack 2016 叢集"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="f1b46-103">在 Azure 中部署 HPC Pack 2016 叢集</span><span class="sxs-lookup"><span data-stu-id="f1b46-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="f1b46-104">遵循本文中的步驟，在 Azure 虛擬機器中部署 [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) 叢集。</span><span class="sxs-lookup"><span data-stu-id="f1b46-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="f1b46-105">HPC Pack 是建置在 Microsoft Azure 和 Windows Server 技術上的 Microsoft 免費 HPC 解決方案，並支援各種 HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="f1b46-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="f1b46-106">使用其中一種 [Azure Resource Manager 範本](https://github.com/MsHpcPack/HPCPack2016) 部署 HPC Pack 2016 叢集。</span><span class="sxs-lookup"><span data-stu-id="f1b46-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="f1b46-107">您可以選擇多種叢集拓撲，當中包含不同數目的叢集前端節點，與 Linux 或 Windows 運算節點。</span><span class="sxs-lookup"><span data-stu-id="f1b46-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1b46-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f1b46-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="f1b46-109">PFX 憑證</span><span class="sxs-lookup"><span data-stu-id="f1b46-109">PFX certificate</span></span>

<span data-ttu-id="f1b46-110">Microsoft HPC Pack 2016 叢集需要個人資訊交換 (PFX) 憑證來保護 HPC 節點之間的通訊安全。</span><span class="sxs-lookup"><span data-stu-id="f1b46-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="f1b46-111">憑證必須符合下列要求：</span><span class="sxs-lookup"><span data-stu-id="f1b46-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="f1b46-112">它必須有能夠進行金鑰交換的私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f1b46-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="f1b46-113">金鑰使用方法包含數位簽章和金鑰加密</span><span class="sxs-lookup"><span data-stu-id="f1b46-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="f1b46-114">增強金鑰使用方法包含用戶端驗證和伺服器驗證</span><span class="sxs-lookup"><span data-stu-id="f1b46-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="f1b46-115">如果您還沒有符合這些需求的憑證，可以從憑證授權單位要求憑證。</span><span class="sxs-lookup"><span data-stu-id="f1b46-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="f1b46-116">或者，您可以根據您用來執行命令的作業系統，使用下列命令產生自我簽署的憑證，並以私密金鑰匯出 PFX 格式的憑證。</span><span class="sxs-lookup"><span data-stu-id="f1b46-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="f1b46-117">**Windows 10 或 Windows Server 2016**，執行內建 **New-SelfSignedCertificate** PowerShell cmdlet，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f1b46-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="f1b46-118">**若為 Windows 10 或 Windows Server 2016 以前的作業系統**，則必須從 Microsoft 指令碼中心下載[自我簽署憑證產生器](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/)。</span><span class="sxs-lookup"><span data-stu-id="f1b46-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="f1b46-119">將其內容解壓縮，並在 PowerShell 提示字元執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f1b46-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="f1b46-120">將憑證上傳至 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f1b46-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="f1b46-121">在部署 HPC 叢集之前，將憑證上傳至 [Azure 金鑰保存庫](../../key-vault/index.md)做為密碼，並記錄下列資訊以在部署期間使用︰**保存庫名稱**、**保存庫資源群組**、**憑證 URL** 及**憑證指紋**。</span><span class="sxs-lookup"><span data-stu-id="f1b46-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="f1b46-122">以下為上傳憑證的範例 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f1b46-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="f1b46-123">如需將憑證上傳至 Azure 金鑰保存庫的詳細資訊，請參閱[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f1b46-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="f1b46-124">支援的拓撲</span><span class="sxs-lookup"><span data-stu-id="f1b46-124">Supported topologies</span></span>

<span data-ttu-id="f1b46-125">選取其中一種 [Azure Resource Manager 範本](https://github.com/MsHpcPack/HPCPack2016) 部署 HPC Pack 2016 叢集。</span><span class="sxs-lookup"><span data-stu-id="f1b46-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="f1b46-126">以下是三個受支援叢集拓撲的高層架構。</span><span class="sxs-lookup"><span data-stu-id="f1b46-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="f1b46-127">高可用性拓撲包含多個叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="f1b46-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="f1b46-128">包含 Active Directory 網域的高可用性叢集</span><span class="sxs-lookup"><span data-stu-id="f1b46-128">High-availability cluster with Active Directory domain</span></span>

    ![AD 網域中的 HA 叢集](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="f1b46-130">不包含 Active Directory 網域的高可用性叢集</span><span class="sxs-lookup"><span data-stu-id="f1b46-130">High-availability cluster without Active Directory domain</span></span>

    ![不包含 AD 網域的 HA 叢集](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="f1b46-132">包含單一前端節點的叢集</span><span class="sxs-lookup"><span data-stu-id="f1b46-132">Cluster with a single head node</span></span>

   ![包含單一前端節點的叢集](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="f1b46-134">部署叢集</span><span class="sxs-lookup"><span data-stu-id="f1b46-134">Deploy a cluster</span></span>

<span data-ttu-id="f1b46-135">若要建立叢集，請選擇範本並按一下 [部署至 Azure]。</span><span class="sxs-lookup"><span data-stu-id="f1b46-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="f1b46-136">在 [Azure 入口網站](https://portal.azure.com)中，如下列步驟中所述指定範本的參數。</span><span class="sxs-lookup"><span data-stu-id="f1b46-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="f1b46-137">每個範本會建立 HPC 叢集基礎結構所需的所有 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f1b46-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="f1b46-138">資源包括 Azure 虛擬網路、公用 IP 位址、負載平衡器 (僅適用於高可用性叢集)、網路介面、可用性設定組、儲存體帳戶和虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f1b46-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="f1b46-139">步驟 1︰選取訂用帳戶、位置和資源群組</span><span class="sxs-lookup"><span data-stu-id="f1b46-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="f1b46-140">**訂用帳戶**和**位置**必須與您上傳 PFX 憑證 (請參閱必要條件) 時所指定的相同。</span><span class="sxs-lookup"><span data-stu-id="f1b46-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="f1b46-141">建議您建立部署的**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="f1b46-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="f1b46-142">步驟 2︰指定參數設定</span><span class="sxs-lookup"><span data-stu-id="f1b46-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="f1b46-143">輸入或修改範本參數的值。</span><span class="sxs-lookup"><span data-stu-id="f1b46-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="f1b46-144">按一下說明資訊的每個參數旁邊的圖示。</span><span class="sxs-lookup"><span data-stu-id="f1b46-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="f1b46-145">另請參閱[可用 VM 大小](sizes.md)的指引。</span><span class="sxs-lookup"><span data-stu-id="f1b46-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="f1b46-146">指定您在必要條件中記錄之下列參數的值︰**保存庫名稱**、**保存庫資源群組**、**憑證 URL** 和 **憑證指紋**。</span><span class="sxs-lookup"><span data-stu-id="f1b46-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="f1b46-147">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="f1b46-147">Step 3.</span></span> <span data-ttu-id="f1b46-148">檢閱法律條款並建立</span><span class="sxs-lookup"><span data-stu-id="f1b46-148">Review legal terms and create</span></span>
<span data-ttu-id="f1b46-149">按一下 [檢閱法律條款] 檢閱條款。</span><span class="sxs-lookup"><span data-stu-id="f1b46-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="f1b46-150">如果您同意，請按一下 [購買]，然後按一下 [建立] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="f1b46-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="f1b46-151">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="f1b46-151">Connect to the cluster</span></span>
1. <span data-ttu-id="f1b46-152">部署 HPC Pack 叢集之後，請移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f1b46-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f1b46-153">按一下 [資源群組]，並尋找已在當中部署叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f1b46-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="f1b46-154">您可以找到前端節點虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f1b46-154">You can find the head node virtual machines.</span></span>

    ![入口網站中的叢集前端節點](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="f1b46-156">按一個前端節點 (在高可用性叢集中，按一下任一個前端節點)。</span><span class="sxs-lookup"><span data-stu-id="f1b46-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="f1b46-157">在 [基本資訊] 中，您可以找到叢集的公用 IP 位址或完整 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="f1b46-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![叢集連線設定](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="f1b46-159">按一下 [連接]，使用遠端桌面搭配您指定的系統管理員使用者名稱登入任何前端節點。</span><span class="sxs-lookup"><span data-stu-id="f1b46-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="f1b46-160">如果您部署的叢集在 Active Directory 網域中，使用者名稱是表單 <privateDomainName>\<adminUsername > (例如，hpc.local\hpcadmin)。</span><span class="sxs-lookup"><span data-stu-id="f1b46-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1b46-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1b46-161">Next steps</span></span>
* <span data-ttu-id="f1b46-162">將工作提交至叢集。</span><span class="sxs-lookup"><span data-stu-id="f1b46-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="f1b46-163">請參閱 [提交工作至 Azure 中 HPC Pack 叢集的 HPC](hpcpack-cluster-submit-jobs.md) 和 [使用 Azure Active Directory 管理 Azure 中的 HPC Pack 2016 叢集](hpcpack-cluster-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="f1b46-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

