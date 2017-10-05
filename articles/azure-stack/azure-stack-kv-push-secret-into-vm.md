---
title: "使用安全地存放在 Azure Stack 上的憑證部署虛擬機器 | Microsoft 文件"
description: "了解如何使用 Azure Stack 中的金鑰保存庫來部署虛擬機器，並將憑證推送至該虛擬機器"
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
ms.openlocfilehash: 95008e783b2597895e870ceb3514bffbd4ab1dbf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="37cf1-103">建立虛擬機器，並加入從金鑰保存庫擷取的憑證</span><span class="sxs-lookup"><span data-stu-id="37cf1-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="37cf1-104">本文可協助您在 Azure Stack 中建立虛擬機器，並將憑證推送至該虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="37cf1-104">This article helps you to create a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="37cf1-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="37cf1-105">Prerequisites</span></span>

* <span data-ttu-id="37cf1-106">Azure Stack 雲端系統管理員必須已經[建立](azure-stack-create-offer.md)包含 Azure Key Vault 服務的供應項目。</span><span class="sxs-lookup"><span data-stu-id="37cf1-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Azure Key Vault service.</span></span>  
* <span data-ttu-id="37cf1-107">使用者必須[訂閱](azure-stack-subscribe-plan-provision-vm.md)包含 Key Vault 服務的供應項目。</span><span class="sxs-lookup"><span data-stu-id="37cf1-107">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="37cf1-108">安裝 Azure Stack 適用的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="37cf1-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="37cf1-109">設定 Azure Stack 使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="37cf1-109">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="37cf1-110">Azure Stack 中的金鑰保存庫可用來存放憑證。</span><span class="sxs-lookup"><span data-stu-id="37cf1-110">A key vault in Azure Stack is used to store certificates.</span></span> <span data-ttu-id="37cf1-111">憑證在許多不同情況下都很有幫助。</span><span class="sxs-lookup"><span data-stu-id="37cf1-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="37cf1-112">例如，假設您在 Azure Stack 中有一個虛擬機器正在執行需要憑證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="37cf1-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="37cf1-113">此憑證可用於加密、向 Active Directory 進行驗證，或用於網站上的 SSL。</span><span class="sxs-lookup"><span data-stu-id="37cf1-113">This certificate can be used for encrypting, for authenticating to Active Directory, or for SSL on a website.</span></span> <span data-ttu-id="37cf1-114">將憑證存放在金鑰保存庫有助於確保憑證的安全。</span><span class="sxs-lookup"><span data-stu-id="37cf1-114">Having the certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="37cf1-115">在本文中，我們會針對如何將憑證推送至 Azure Stack 中的 Windows 虛擬機器，逐步說明所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="37cf1-115">In this article, we walk you through the steps required to push a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="37cf1-116">您可以從 Azure Stack 開發套件，或從 Windows 外部用戶端 (如果是透過 VPN 連線) 來使用這些步驟。</span><span class="sxs-lookup"><span data-stu-id="37cf1-116">You can use these steps either from the Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="37cf1-117">下列步驟說明將憑證推送至虛擬機器所需的程序：</span><span class="sxs-lookup"><span data-stu-id="37cf1-117">The following steps describe the process required to push a certificate onto the virtual machine:</span></span>

1. <span data-ttu-id="37cf1-118">建立 Key Vault 祕密。</span><span class="sxs-lookup"><span data-stu-id="37cf1-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="37cf1-119">更新 azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="37cf1-119">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="37cf1-120">部署範本</span><span class="sxs-lookup"><span data-stu-id="37cf1-120">Deploy the template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="37cf1-121">建立 Key Vault 祕密</span><span class="sxs-lookup"><span data-stu-id="37cf1-121">Create a Key Vault secret</span></span>

<span data-ttu-id="37cf1-122">下列指令碼會建立 .pfx 格式的憑證、建立金鑰保存庫，並將憑證存放在金鑰保存庫中當做祕密。</span><span class="sxs-lookup"><span data-stu-id="37cf1-122">The following script creates a certificate in the .pfx format, creates a key vault, and stores the certificate in the key vault as a secret.</span></span> <span data-ttu-id="37cf1-123">建立金鑰保存庫時，您必須使用 `-EnabledForDeployment` 參數。</span><span class="sxs-lookup"><span data-stu-id="37cf1-123">You must use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="37cf1-124">此參數可確保您能夠從 Azure Resource Manager 範本參考金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="37cf1-124">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in the .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used to export the certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in the previous step>" `
  -FilePath "<Fully qualified path where the exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload the certificate into the key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where the exported certificate can be stored>"
$certPassword = "<Password used to export the certificate>"

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

<span data-ttu-id="37cf1-125">當您執行上述指令碼時，輸出會包含祕密 URI。</span><span class="sxs-lookup"><span data-stu-id="37cf1-125">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="37cf1-126">請記下此 URI。</span><span class="sxs-lookup"><span data-stu-id="37cf1-126">Make a note of this URI.</span></span> <span data-ttu-id="37cf1-127">在[將憑證推送至 Windows Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) \(英文\) 中，您必須參考此 URI。</span><span class="sxs-lookup"><span data-stu-id="37cf1-127">You have to reference it in the [Push certificate to Windows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="37cf1-128">將 [vm-push-certificate-windows 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) \(英文\) 資料夾下載至您的開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="37cf1-128">Download the [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="37cf1-129">此資料夾中包含 `azuredeploy.json` 和 `azuredeploy.parameters.json` 檔案，您在接下來的步驟中將需要這些檔案。</span><span class="sxs-lookup"><span data-stu-id="37cf1-129">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="37cf1-130">根據您的環境值，修改 `azuredeploy.parameters.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="37cf1-130">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="37cf1-131">要注意的參數是保存庫名稱、保存庫資源群組以及祕密 URI (產生自先前的指令碼)。</span><span class="sxs-lookup"><span data-stu-id="37cf1-131">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="37cf1-132">下列檔案是參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="37cf1-132">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="37cf1-133">更新 azuredeploy.parameters.json 檔案</span><span class="sxs-lookup"><span data-stu-id="37cf1-133">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="37cf1-134">根據您的環境，以 vaultName、祕密 URI、VmName 和其他值來更新 azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="37cf1-134">Update the azuredeploy.parameters.json file with the vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="37cf1-135">下列 JSON 檔案會顯示範本參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="37cf1-135">The following JSON file shows an example of the template parameters file:</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="37cf1-136">部署範本</span><span class="sxs-lookup"><span data-stu-id="37cf1-136">Deploy the template</span></span>

<span data-ttu-id="37cf1-137">現在，使用下列 PowerShell 指令碼部署範本：</span><span class="sxs-lookup"><span data-stu-id="37cf1-137">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

<span data-ttu-id="37cf1-138">成功部署範本之後，會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="37cf1-138">When the template is deployed successfully, it results in the following output:</span></span>

![部署輸出](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="37cf1-140">部署此虛擬機器時，Azure Stack 會將憑證推送至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="37cf1-140">When this virtual machine is deployed, Azure Stack pushes the certificate onto the virtual machine.</span></span> <span data-ttu-id="37cf1-141">在 Windows 中，系統會利用使用者提供的憑證存放區，將憑證新增至 LocalMachine 憑證位置。</span><span class="sxs-lookup"><span data-stu-id="37cf1-141">In Windows, the certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span></span> <span data-ttu-id="37cf1-142">在 Linux 中，憑證會置於 /var/lib/waagent 目錄底下，其中 X509 憑證檔案的檔案名稱為 &lt;UppercaseThumbprint&gt;.crt，且私密金鑰的檔案名稱為 &lt;UppercaseThumbprint&gt;.prv。</span><span class="sxs-lookup"><span data-stu-id="37cf1-142">In Linux, the certificate is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for the private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="37cf1-143">淘汰憑證</span><span class="sxs-lookup"><span data-stu-id="37cf1-143">Retire certificates</span></span>

<span data-ttu-id="37cf1-144">在上一節中，我們示範如何將新的憑證推送至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="37cf1-144">In the preceding section, we showed you how to push a new certificate onto a virtual machine.</span></span> <span data-ttu-id="37cf1-145">您的舊憑證仍然在虛擬機器上，而且無法移除。</span><span class="sxs-lookup"><span data-stu-id="37cf1-145">Your old certificate is still on the virtual machine, and it can't be removed.</span></span> <span data-ttu-id="37cf1-146">不過，您可以使用 `Set-AzureKeyVaultSecretAttribute` Cmdlet 來停用舊版的祕密。</span><span class="sxs-lookup"><span data-stu-id="37cf1-146">However, you can disable the older version of the secret by using the `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="37cf1-147">以下是此 Cmdlet 的使用範例。</span><span class="sxs-lookup"><span data-stu-id="37cf1-147">The following is an example usage of this cmdlet.</span></span> <span data-ttu-id="37cf1-148">請務必根據您的環境，取代保存庫名稱、祕密名稱和版本值：</span><span class="sxs-lookup"><span data-stu-id="37cf1-148">Make sure to replace the vault name, secret name, and version values according to your environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="37cf1-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37cf1-149">Next steps</span></span>

* [<span data-ttu-id="37cf1-150">使用金鑰保存庫密碼部署 VM</span><span class="sxs-lookup"><span data-stu-id="37cf1-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="37cf1-151">允許應用程式存取 Key Vault</span><span class="sxs-lookup"><span data-stu-id="37cf1-151">Allow an application to access Key Vault</span></span>](azure-stack-kv-sample-app.md)


