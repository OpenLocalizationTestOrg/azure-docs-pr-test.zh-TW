---
title: "Azure VM 的 WinRM 存取 aaaSet |Microsoft 文件"
description: "設定用於 WinRM 存取與 hello Resource Manager 部署模型中建立 Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="f49ae-103">在 Azure Resource Manager 中設定虛擬機器的 WinRM 存取</span><span class="sxs-lookup"><span data-stu-id="f49ae-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="f49ae-104">Azure Service Management 與 Azure Resource Manager 中的 WinRM</span><span class="sxs-lookup"><span data-stu-id="f49ae-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="f49ae-105">如需 hello Azure 資源管理員的概觀，請參閱本[發行項](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f49ae-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="f49ae-106">如需 Azure Service Management 與 Azure Resource Manager 之間的差異性，請參閱 [本文章](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="f49ae-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="f49ae-107">hello 中設定 WinRM 組態 hello 兩個堆疊之間的主要差異是 hello 憑證 hello VM 上安裝的方式。</span><span class="sxs-lookup"><span data-stu-id="f49ae-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="f49ae-108">Hello Azure Resource Manager 堆疊中 hello 憑證會模型化為 hello 金鑰保存庫資源提供者所管理的資源。</span><span class="sxs-lookup"><span data-stu-id="f49ae-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="f49ae-109">因此，hello 使用者需要 tooprovide 自己的憑證，並將它上傳 tooa 金鑰保存庫之前使用的 VM 中。</span><span class="sxs-lookup"><span data-stu-id="f49ae-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="f49ae-110">以下是您需要將 vm 與 WinRM 連線 tootake tooset hello 步驟</span><span class="sxs-lookup"><span data-stu-id="f49ae-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="f49ae-111">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f49ae-111">Create a Key Vault</span></span>
2. <span data-ttu-id="f49ae-112">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f49ae-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="f49ae-113">上傳您的自我簽署的憑證 tooKey 保存庫</span><span class="sxs-lookup"><span data-stu-id="f49ae-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="f49ae-114">取得您的自我簽署憑證 hello 金鑰保存庫中的 hello URL</span><span class="sxs-lookup"><span data-stu-id="f49ae-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="f49ae-115">在建立 VM 時參考您的自我簽署憑證的 URL</span><span class="sxs-lookup"><span data-stu-id="f49ae-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="f49ae-116">步驟 1︰建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f49ae-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="f49ae-117">您可以使用下列命令 toocreate hello 金鑰保存庫的 hello</span><span class="sxs-lookup"><span data-stu-id="f49ae-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="f49ae-118">步驟 2：建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f49ae-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="f49ae-119">您可以使用下列 PowerShell 指令碼建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f49ae-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="f49ae-120">步驟 3： 上傳您的自我簽署的憑證 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f49ae-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="f49ae-121">步驟 1 中上傳 hello 憑證 toohello 金鑰保存庫建立之前，它會需要 tooconverted 成格式 hello Microsoft.Compute 資源提供者就可以了解。</span><span class="sxs-lookup"><span data-stu-id="f49ae-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="f49ae-122">下列 PowerShell 指令碼的 hello 可讓您執行此動作</span><span class="sxs-lookup"><span data-stu-id="f49ae-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="f49ae-123">步驟 4： 取得您的自我簽署憑證 hello 金鑰保存庫中的 hello URL</span><span class="sxs-lookup"><span data-stu-id="f49ae-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="f49ae-124">hello Microsoft.Compute 資源提供者佈建 hello VM 時，需要 hello 金鑰保存庫內的 URL toohello 密碼。</span><span class="sxs-lookup"><span data-stu-id="f49ae-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="f49ae-125">這可讓 hello Microsoft.Compute 資源提供者 toodownload hello 密碼，並在 hello VM 上建立 hello 對等憑證。</span><span class="sxs-lookup"><span data-stu-id="f49ae-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="f49ae-126">hello 密碼 hello URL 必須 tooinclude hello 版本。</span><span class="sxs-lookup"><span data-stu-id="f49ae-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="f49ae-127">範例 URL 如下所示：https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="f49ae-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="f49ae-128">範本</span><span class="sxs-lookup"><span data-stu-id="f49ae-128">Templates</span></span>
<span data-ttu-id="f49ae-129">您可以取得 hello 連結 toohello URL 中使用程式碼底下的 hello hello 範本</span><span class="sxs-lookup"><span data-stu-id="f49ae-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="f49ae-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f49ae-130">PowerShell</span></span>
<span data-ttu-id="f49ae-131">您可以取得此 URL 使用下列 PowerShell 命令的 hello</span><span class="sxs-lookup"><span data-stu-id="f49ae-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="f49ae-132">步驟 5：在建立 VM 時參考您的自我簽署憑證的 URL</span><span class="sxs-lookup"><span data-stu-id="f49ae-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="f49ae-133">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="f49ae-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="f49ae-134">在建立時透過範本的 VM，hello 憑證取得參考 hello 機密資料區段和 hello winRM 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f49ae-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="f49ae-135">Hello 上述的範例範本可以在這裡找到在[201 vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="f49ae-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="f49ae-136">此範本的原始程式碼位於 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="f49ae-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="f49ae-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f49ae-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="f49ae-138">步驟 6： 連接 toohello VM</span><span class="sxs-lookup"><span data-stu-id="f49ae-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="f49ae-139">您可以連接 toohello VM 之前，您必須先確定您的電腦已設定 WinRM 遠端管理 toomake。</span><span class="sxs-lookup"><span data-stu-id="f49ae-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="f49ae-140">系統管理員身分啟動 PowerShell 並執行以下命令 toomake 確定您設定好 hello。</span><span class="sxs-lookup"><span data-stu-id="f49ae-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="f49ae-141">您可能需要 toomake 確定 hello WinRM 服務正在執行，如果上述 hello 無法運作。</span><span class="sxs-lookup"><span data-stu-id="f49ae-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="f49ae-142">您可以使用 `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="f49ae-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="f49ae-143">一旦 hello 安裝完成後，您可以連接 toohello VM 使用下列命令 hello</span><span class="sxs-lookup"><span data-stu-id="f49ae-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
