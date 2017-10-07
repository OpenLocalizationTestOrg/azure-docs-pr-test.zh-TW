---
title: "虛擬機器上，使用安全地儲存憑證 Azure 堆疊 aaaDeploy |Microsoft 文件"
description: "了解如何 toodeploy 虛擬機器和發送至其本身的憑證，使用金鑰保存庫中 Azure 堆疊"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: b5fa0a502ba582e10ff59b8af0568bf134d3d189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="2a06e-103">建立虛擬機器，並加入從金鑰保存庫擷取的憑證</span><span class="sxs-lookup"><span data-stu-id="2a06e-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="2a06e-104">這篇文章可協助您 toocreate Azure 堆疊和發送至其本身的憑證中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2a06e-104">This article helps you toocreate a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2a06e-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a06e-105">Prerequisites</span></span>

* <span data-ttu-id="2a06e-106">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello Azure 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="2a06e-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="2a06e-107">使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="2a06e-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="2a06e-108">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a06e-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="2a06e-109">設定 hello Azure 堆疊使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="2a06e-109">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="2a06e-110">Azure 堆疊中的金鑰保存庫是使用的 toostore 憑證。</span><span class="sxs-lookup"><span data-stu-id="2a06e-110">A key vault in Azure Stack is used toostore certificates.</span></span> <span data-ttu-id="2a06e-111">憑證在許多不同情況下都很有幫助。</span><span class="sxs-lookup"><span data-stu-id="2a06e-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="2a06e-112">例如，假設您在 Azure Stack 中有一個虛擬機器正在執行需要憑證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a06e-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="2a06e-113">此憑證可用來加密驗證 tooActive 目錄，或 SSL 的網站上。</span><span class="sxs-lookup"><span data-stu-id="2a06e-113">This certificate can be used for encrypting, for authenticating tooActive Directory, or for SSL on a website.</span></span> <span data-ttu-id="2a06e-114">具有 hello 憑證金鑰保存庫可以協助確定它是安全。</span><span class="sxs-lookup"><span data-stu-id="2a06e-114">Having hello certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="2a06e-115">在本文中，我們逐步引導您 hello 步驟需要 toopush Azure 堆疊中的 Windows 虛擬機器的憑證。</span><span class="sxs-lookup"><span data-stu-id="2a06e-115">In this article, we walk you through hello steps required toopush a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="2a06e-116">如果您透過 VPN 連線，您可以使用下列步驟從 hello Azure 堆疊開發套件，或是從 windows 的外部用戶端。</span><span class="sxs-lookup"><span data-stu-id="2a06e-116">You can use these steps either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="2a06e-117">hello 下列步驟說明 hello 所需程序 toopush hello 虛擬機器上的憑證：</span><span class="sxs-lookup"><span data-stu-id="2a06e-117">hello following steps describe hello process required toopush a certificate onto hello virtual machine:</span></span>

1. <span data-ttu-id="2a06e-118">建立 Key Vault 祕密。</span><span class="sxs-lookup"><span data-stu-id="2a06e-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="2a06e-119">更新 hello azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="2a06e-119">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="2a06e-120">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="2a06e-120">Deploy hello template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="2a06e-121">建立 Key Vault 祕密</span><span class="sxs-lookup"><span data-stu-id="2a06e-121">Create a Key Vault secret</span></span>

<span data-ttu-id="2a06e-122">hello 下列指令碼會建立 hello.pfx 格式的憑證、 建立金鑰保存庫，並儲存 hello 憑證 hello 做為密碼金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="2a06e-122">hello following script creates a certificate in hello .pfx format, creates a key vault, and stores hello certificate in hello key vault as a secret.</span></span> <span data-ttu-id="2a06e-123">您必須使用 hello`-EnabledForDeployment`參數，當您要建立 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="2a06e-123">You must use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="2a06e-124">這個參數可確保您可以從 Azure 資源管理員範本參考該 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="2a06e-124">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in hello .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used tooexport hello certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in hello previous step>" `
  -FilePath "<Fully qualified path where hello exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload hello certificate into hello key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where hello exported certificate can be stored>"
$certPassword = "<Password used tooexport hello certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

<span data-ttu-id="2a06e-125">當您執行 hello 至上一個指令碼時，hello 輸出會包括 hello 密碼 URI。</span><span class="sxs-lookup"><span data-stu-id="2a06e-125">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="2a06e-126">請記下此 URI。</span><span class="sxs-lookup"><span data-stu-id="2a06e-126">Make a note of this URI.</span></span> <span data-ttu-id="2a06e-127">您有 tooreference 在 hello[推播憑證 tooWindows Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows)。</span><span class="sxs-lookup"><span data-stu-id="2a06e-127">You have tooreference it in hello [Push certificate tooWindows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="2a06e-128">下載 hello [vm 推播憑證-windows 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows)到開發電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a06e-128">Download hello [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="2a06e-129">此資料夾包含 hello`azuredeploy.json`和`azuredeploy.parameters.json`hello 後續步驟中，您將需要的檔案。</span><span class="sxs-lookup"><span data-stu-id="2a06e-129">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="2a06e-130">修改 hello`azuredeploy.parameters.json`根據 tooyour 環境值的檔案。</span><span class="sxs-lookup"><span data-stu-id="2a06e-130">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="2a06e-131">特別感興趣的 hello 參數是 hello 保存庫名稱、 hello 保存庫的資源群組，以及 hello 密碼 URI （如 hello 至上一個指令碼所產生）。</span><span class="sxs-lookup"><span data-stu-id="2a06e-131">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="2a06e-132">下列檔 hello 是參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="2a06e-132">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="2a06e-133">更新 hello azuredeploy.parameters.json 檔案</span><span class="sxs-lookup"><span data-stu-id="2a06e-133">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="2a06e-134">更新 hello azuredeploy.parameters.json 檔案 hello vaultName、 與密碼的 URI、 VmName，根據您的環境的其他值。</span><span class="sxs-lookup"><span data-stu-id="2a06e-134">Update hello azuredeploy.parameters.json file with hello vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="2a06e-135">hello 下列 JSON 檔案顯示 hello 範本參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="2a06e-135">hello following JSON file shows an example of hello template parameters file:</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-hello-template"></a><span data-ttu-id="2a06e-136">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="2a06e-136">Deploy hello template</span></span>

<span data-ttu-id="2a06e-137">現在使用下列 PowerShell 指令碼的 hello 部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="2a06e-137">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

<span data-ttu-id="2a06e-138">Hello 範本順利部署時，它會產生下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a06e-138">When hello template is deployed successfully, it results in hello following output:</span></span>

![部署輸出](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="2a06e-140">在部署此虛擬機器時，Azure 堆疊推入 hello hello 虛擬機器上的憑證。</span><span class="sxs-lookup"><span data-stu-id="2a06e-140">When this virtual machine is deployed, Azure Stack pushes hello certificate onto hello virtual machine.</span></span> <span data-ttu-id="2a06e-141">在 Windows hello 憑證會新增 toohello LocalMachine 存放區提供該 hello 使用者的憑證位置，與 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="2a06e-141">In Windows, hello certificate is added toohello LocalMachine certificate location, with hello certificate store that hello user provided.</span></span> <span data-ttu-id="2a06e-142">在 Linux 中 hello 憑證會放在 hello 檔名的 hello /var/lib/waagent 目錄下&lt;UppercaseThumbprint&gt;.crt hello X509 憑證檔案和&lt;UppercaseThumbprint&gt;.prv hello私用的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2a06e-142">In Linux, hello certificate is placed under hello /var/lib/waagent directory, with hello file name &lt;UppercaseThumbprint&gt;.crt for hello X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for hello private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="2a06e-143">淘汰憑證</span><span class="sxs-lookup"><span data-stu-id="2a06e-143">Retire certificates</span></span>

<span data-ttu-id="2a06e-144">在前一節的 hello，我們也示範了您如何 toopush 虛擬機器到新的憑證。</span><span class="sxs-lookup"><span data-stu-id="2a06e-144">In hello preceding section, we showed you how toopush a new certificate onto a virtual machine.</span></span> <span data-ttu-id="2a06e-145">舊的憑證仍在 hello 虛擬機器，且無法移除。</span><span class="sxs-lookup"><span data-stu-id="2a06e-145">Your old certificate is still on hello virtual machine, and it can't be removed.</span></span> <span data-ttu-id="2a06e-146">不過，您可以使用停用舊版 hello 密碼 hello hello `Set-AzureKeyVaultSecretAttribute` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2a06e-146">However, you can disable hello older version of hello secret by using hello `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="2a06e-147">hello 以下是這個 cmdlet 的範例使用方式。</span><span class="sxs-lookup"><span data-stu-id="2a06e-147">hello following is an example usage of this cmdlet.</span></span> <span data-ttu-id="2a06e-148">請確定 tooreplace hello 保存庫名稱、 密碼的名稱和版本值根據 tooyour 環境：</span><span class="sxs-lookup"><span data-stu-id="2a06e-148">Make sure tooreplace hello vault name, secret name, and version values according tooyour environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="2a06e-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a06e-149">Next steps</span></span>

* [<span data-ttu-id="2a06e-150">使用金鑰保存庫密碼部署 VM</span><span class="sxs-lookup"><span data-stu-id="2a06e-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="2a06e-151">允許應用程式 tooaccess 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="2a06e-151">Allow an application tooaccess Key Vault</span></span>](azure-stack-kv-sample-app.md)


