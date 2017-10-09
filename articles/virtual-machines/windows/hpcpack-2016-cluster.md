---
title: "組件 2016 aaaHPC 叢集在 Azure 中 |Microsoft 文件"
description: "了解 toodeploy HPC Pack 2016 在 Azure 中的叢集化"
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
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="8ad14-103">在 Azure 中部署 HPC Pack 2016 叢集</span><span class="sxs-lookup"><span data-stu-id="8ad14-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="8ad14-104">請遵循本文章 toodeploy 中的 hello 步驟[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) Azure 虛擬機器中的叢集。</span><span class="sxs-lookup"><span data-stu-id="8ad14-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="8ad14-105">HPC Pack 是建置在 Microsoft Azure 和 Windows Server 技術上的 Microsoft 免費 HPC 解決方案，並支援各種 HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="8ad14-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="8ad14-106">使用其中一種 hello [Azure 資源管理員範本](https://github.com/MsHpcPack/HPCPack2016)toodeploy hello HPC Pack 2016 叢集。</span><span class="sxs-lookup"><span data-stu-id="8ad14-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="8ad14-107">您可以選擇多種叢集拓撲，當中包含不同數目的叢集前端節點，與 Linux 或 Windows 運算節點。</span><span class="sxs-lookup"><span data-stu-id="8ad14-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ad14-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="8ad14-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="8ad14-109">PFX 憑證</span><span class="sxs-lookup"><span data-stu-id="8ad14-109">PFX certificate</span></span>

<span data-ttu-id="8ad14-110">Microsoft HPC Pack 2016 叢集需要 hello HPC 節點之間的個人資訊交換 (PFX) 憑證 toosecure hello 通訊。</span><span class="sxs-lookup"><span data-stu-id="8ad14-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="8ad14-111">hello 憑證必須符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ad14-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="8ad14-112">它必須有能夠進行金鑰交換的私密金鑰</span><span class="sxs-lookup"><span data-stu-id="8ad14-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="8ad14-113">金鑰使用方法包含數位簽章和金鑰加密</span><span class="sxs-lookup"><span data-stu-id="8ad14-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="8ad14-114">增強金鑰使用方法包含用戶端驗證和伺服器驗證</span><span class="sxs-lookup"><span data-stu-id="8ad14-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="8ad14-115">如果您還沒有符合這些需求的憑證，您可以從憑證授權單位要求 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="8ad14-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="8ad14-116">或者，您可以使用下列命令 toogenerate hello 自我簽署的憑證 hello 的作業系統執行 hello 命令，並使用私密金鑰匯出 hello PFX 格式憑證為基礎的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ad14-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="8ad14-117">**Windows 10 或 Windows Server 2016**，執行內建的 hello **New-selfsignedcertificate** PowerShell cmdlet，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8ad14-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="8ad14-118">**適用於作業系統比 Windows 10 或 Windows Server 2016 更早**，下載 hello[自我簽署的憑證的產生器](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/)從 Microsoft 指令碼中心 hello。</span><span class="sxs-lookup"><span data-stu-id="8ad14-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="8ad14-119">將其內容解壓縮，然後執行下列 PowerShell 命令提示字元命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ad14-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="8ad14-120">上傳憑證 tooan Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="8ad14-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="8ad14-121">在部署之前 hello HPC 叢集上, 傳 hello 憑證 tooan [Azure 金鑰保存庫](../../key-vault/index.md)為下列 hello 部署期間使用資訊的密碼，並記錄 hello:**保存庫名稱**， **保存庫的資源群組**，**憑證 URL**，和**憑證指紋**。</span><span class="sxs-lookup"><span data-stu-id="8ad14-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="8ad14-122">以下範例 PowerShell 指令碼 tooupload hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="8ad14-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="8ad14-123">如需有關上傳憑證 tooan Azure 金鑰保存庫的詳細資訊，請參閱[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8ad14-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
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
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="8ad14-124">支援的拓撲</span><span class="sxs-lookup"><span data-stu-id="8ad14-124">Supported topologies</span></span>

<span data-ttu-id="8ad14-125">選擇其中一個 hello [Azure 資源管理員範本](https://github.com/MsHpcPack/HPCPack2016)toodeploy hello HPC Pack 2016 叢集。</span><span class="sxs-lookup"><span data-stu-id="8ad14-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="8ad14-126">以下是三個受支援叢集拓撲的高層架構。</span><span class="sxs-lookup"><span data-stu-id="8ad14-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="8ad14-127">高可用性拓撲包含多個叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="8ad14-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="8ad14-128">包含 Active Directory 網域的高可用性叢集</span><span class="sxs-lookup"><span data-stu-id="8ad14-128">High-availability cluster with Active Directory domain</span></span>

    ![AD 網域中的 HA 叢集](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="8ad14-130">不包含 Active Directory 網域的高可用性叢集</span><span class="sxs-lookup"><span data-stu-id="8ad14-130">High-availability cluster without Active Directory domain</span></span>

    ![不包含 AD 網域的 HA 叢集](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="8ad14-132">包含單一前端節點的叢集</span><span class="sxs-lookup"><span data-stu-id="8ad14-132">Cluster with a single head node</span></span>

   ![包含單一前端節點的叢集](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="8ad14-134">部署叢集</span><span class="sxs-lookup"><span data-stu-id="8ad14-134">Deploy a cluster</span></span>

<span data-ttu-id="8ad14-135">toocreate hello 叢集中，選擇的範本，然後按一下 **部署 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="8ad14-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="8ad14-136">在 hello [Azure 入口網站](https://portal.azure.com)，hello 步驟中所述，請指定 hello 範本參數。</span><span class="sxs-lookup"><span data-stu-id="8ad14-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="8ad14-137">每個範本建立 hello HPC 叢集基礎結構所需的所有 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="8ad14-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="8ad14-138">資源包括 Azure 虛擬網路、公用 IP 位址、負載平衡器 (僅適用於高可用性叢集)、網路介面、可用性設定組、儲存體帳戶和虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ad14-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="8ad14-139">步驟 1： 選取 hello 訂用帳戶、 位置和資源群組</span><span class="sxs-lookup"><span data-stu-id="8ad14-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="8ad14-140">hello**訂用帳戶**和 hello**位置**必須維持相同，指定當您上傳 PFX 憑證 （請參閱必要條件）。</span><span class="sxs-lookup"><span data-stu-id="8ad14-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="8ad14-141">我們建議您建立**資源群組**hello 部署。</span><span class="sxs-lookup"><span data-stu-id="8ad14-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="8ad14-142">步驟 2： 指定 hello 參數設定</span><span class="sxs-lookup"><span data-stu-id="8ad14-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="8ad14-143">輸入或修改 hello 範本參數的值。</span><span class="sxs-lookup"><span data-stu-id="8ad14-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="8ad14-144">按一下 hello 圖示下一步 tooeach 參數的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="8ad14-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="8ad14-145">另請參閱 hello 指導[可用的 VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="8ad14-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="8ad14-146">指定您記錄中的下列參數的 hello 的 hello 必要條件的 hello 值：**保存庫名稱**，**保存庫的資源群組**，**憑證 URL**，和**憑證指紋**。</span><span class="sxs-lookup"><span data-stu-id="8ad14-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="8ad14-147">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="8ad14-147">Step 3.</span></span> <span data-ttu-id="8ad14-148">檢閱法律條款並建立</span><span class="sxs-lookup"><span data-stu-id="8ad14-148">Review legal terms and create</span></span>
<span data-ttu-id="8ad14-149">按一下**檢查 法律條款**tooreview hello 條款。</span><span class="sxs-lookup"><span data-stu-id="8ad14-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="8ad14-150">如果您同意，請按一下**購買**，然後按一下**建立**toostart hello 部署。</span><span class="sxs-lookup"><span data-stu-id="8ad14-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="8ad14-151">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="8ad14-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="8ad14-152">Hello HPC Pack 叢集部署之後，請繼續 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8ad14-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8ad14-153">按一下**資源群組**，與叢集部署中的 hello 尋找 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8ad14-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="8ad14-154">您可以找到 hello 前端節點的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ad14-154">You can find hello head node virtual machines.</span></span>

    ![Hello 入口網站中的叢集前端節點](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="8ad14-156">按一下一個前端節點 （在高可用性叢集上，按一下任何 hello 前端節點）。</span><span class="sxs-lookup"><span data-stu-id="8ad14-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="8ad14-157">在**Essentials**，您可以找到 hello 公用 IP 位址或 hello 叢集的完整 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="8ad14-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![叢集連線設定](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="8ad14-159">按一下**連接**toolog tooany 的 hello 與您指定的系統管理員的使用者名稱中使用遠端桌面的前端節點上。</span><span class="sxs-lookup"><span data-stu-id="8ad14-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="8ad14-160">如果您部署的 hello 叢集是 Active Directory 網域中，hello 使用者名稱為 hello 表單的<privateDomainName> \<adminUsername > (例如，hpc.local\hpcadmin)。</span><span class="sxs-lookup"><span data-stu-id="8ad14-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ad14-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ad14-161">Next steps</span></span>
* <span data-ttu-id="8ad14-162">提交工作 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="8ad14-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="8ad14-163">請參閱[提交作業 tooHPC 在 Azure 中的 HPC Pack 叢集](hpcpack-cluster-submit-jobs.md)和[管理使用 Azure Active Directory 在 Azure 中的 HPC Pack 2016 叢集](hpcpack-cluster-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="8ad14-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

