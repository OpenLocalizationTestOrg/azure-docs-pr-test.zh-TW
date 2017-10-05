---
title: "使用安全地存放在 Azure Stack 上的密碼部署 VM | Microsoft Docs"
description: "了解如何使用存放在 Azure Stack Key Vault 中的密碼部署 VM"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: sngun
ms.openlocfilehash: a1137ffefbc3fafbd7e9492819058f6a72537e22
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-virtual-machine-by-retrieving-the-password-stored-in-a-key-vault"></a><span data-ttu-id="7e974-103">擷取存放在 Key Vault 中的密碼來建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7e974-103">Create a virtual machine by retrieving the password stored in a Key Vault</span></span>

<span data-ttu-id="7e974-104">當您需要在部署期間傳遞安全值 (例如密碼) 時，可以將該值儲存為 Azure Stack Key Vault 中的祕密，並在 Azure Resource Manager 範本中加以參考。</span><span class="sxs-lookup"><span data-stu-id="7e974-104">When you need to pass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in the Azure Resource Manager templates.</span></span> <span data-ttu-id="7e974-105">您不需要在每次部署資源時手動輸入祕密，您也可以指定哪些使用者或服務主體可以存取祕密。</span><span class="sxs-lookup"><span data-stu-id="7e974-105">You do not need to manually enter the secret each time you deploy the resources, you can also specify which users or service principals can access the secret.</span></span> 

<span data-ttu-id="7e974-106">在本文中，我們會針對如何擷取存放在 Key Vault 中的密碼，以完成在 Azure Stack 中部署 Windows 虛擬機器，逐步說明所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="7e974-106">In this article, we walk you through the steps required to deploy a Windows virtual machine in Azure Stack by retrieving the password that is stored in a Key Vault.</span></span> <span data-ttu-id="7e974-107">因此，密碼絕不會以純文字的形式，放在範本參數檔案中。</span><span class="sxs-lookup"><span data-stu-id="7e974-107">Therefore the password is never put in plain text in the template parameter file.</span></span> <span data-ttu-id="7e974-108">您可以從 Azure Stack 開發套件，或從外部用戶端 (如果是透過 VPN 連線) 來使用這些步驟。</span><span class="sxs-lookup"><span data-stu-id="7e974-108">You can use these steps either from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e974-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7e974-109">Prerequisites</span></span>

* <span data-ttu-id="7e974-110">Azure Stack 雲端系統管理員必須已經[建立](azure-stack-create-offer.md)包含 Azure Key Vault 服務的供應項目。</span><span class="sxs-lookup"><span data-stu-id="7e974-110">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Azure Key Vault service.</span></span>  
* <span data-ttu-id="7e974-111">使用者必須[訂閱](azure-stack-subscribe-plan-provision-vm.md)包含 Key Vault 服務的供應項目。</span><span class="sxs-lookup"><span data-stu-id="7e974-111">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="7e974-112">安裝 Azure Stack 適用的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="7e974-112">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="7e974-113">設定 Azure Stack 使用者的 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="7e974-113">Configure the Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="7e974-114">下列步驟說明擷取存放在 Key Vault 中的密碼來建立虛擬機器所需的程序：</span><span class="sxs-lookup"><span data-stu-id="7e974-114">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span></span>

1. <span data-ttu-id="7e974-115">建立 Key Vault 祕密。</span><span class="sxs-lookup"><span data-stu-id="7e974-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="7e974-116">更新 azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e974-116">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="7e974-117">部署範本。</span><span class="sxs-lookup"><span data-stu-id="7e974-117">Deploy the template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="7e974-118">建立 Key Vault 祕密</span><span class="sxs-lookup"><span data-stu-id="7e974-118">Create a Key Vault secret</span></span>

<span data-ttu-id="7e974-119">下列指令碼會建立金鑰保存庫，並將密碼存放為金鑰保存庫中的祕密。</span><span class="sxs-lookup"><span data-stu-id="7e974-119">The following script creates a key vault, and stores a password in the key vault as a secret.</span></span> <span data-ttu-id="7e974-120">建立金鑰保存庫時，請使用 `-EnabledForDeployment` 參數。</span><span class="sxs-lookup"><span data-stu-id="7e974-120">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="7e974-121">此參數可確保您能夠從 Azure Resource Manager 範本參考金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7e974-121">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

<span data-ttu-id="7e974-122">當您執行上述指令碼時，輸出會包含祕密 URI。</span><span class="sxs-lookup"><span data-stu-id="7e974-122">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="7e974-123">請記下此 URI。</span><span class="sxs-lookup"><span data-stu-id="7e974-123">Make a note of this URI.</span></span> <span data-ttu-id="7e974-124">在[使用金鑰保存庫範本中的密碼部署 Windows 虛擬機器](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) \(英文\) 中，您必須參考該 URI。</span><span class="sxs-lookup"><span data-stu-id="7e974-124">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span></span> <span data-ttu-id="7e974-125">將 [101-vm-secure-passwor](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) \(英文\) 資料夾下載至您的開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="7e974-125">Download the [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) folder onto your development computer.</span></span> <span data-ttu-id="7e974-126">此資料夾中包含 `azuredeploy.json` 和 `azuredeploy.parameters.json` 檔案，您在接下來的步驟中將需要這些檔案。</span><span class="sxs-lookup"><span data-stu-id="7e974-126">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="7e974-127">根據您的環境值，修改 `azuredeploy.parameters.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e974-127">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="7e974-128">要注意的參數是保存庫名稱、保存庫資源群組以及祕密 URI (產生自先前的指令碼)。</span><span class="sxs-lookup"><span data-stu-id="7e974-128">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="7e974-129">下列檔案是參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="7e974-129">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="7e974-130">更新 azuredeploy.parameters.json 檔案</span><span class="sxs-lookup"><span data-stu-id="7e974-130">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="7e974-131">根據您的環境，以 KeyVault URI、secretName、虛擬機器 adminUsername 的值來更新 azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e974-131">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span></span> <span data-ttu-id="7e974-132">下列 JSON 檔案會顯示範本參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="7e974-132">The following JSON file shows an example of the template parameters file:</span></span> 

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a><span data-ttu-id="7e974-133">範本部署</span><span class="sxs-lookup"><span data-stu-id="7e974-133">Template deployment</span></span>

<span data-ttu-id="7e974-134">現在，使用下列 PowerShell 指令碼部署範本：</span><span class="sxs-lookup"><span data-stu-id="7e974-134">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```
<span data-ttu-id="7e974-135">成功部署範本之後，會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7e974-135">When the template is deployed successfully, it results in the following output:</span></span>

![部署輸出](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="7e974-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e974-137">Next steps</span></span>
[<span data-ttu-id="7e974-138">使用 Key Vault 部署範例應用程式</span><span class="sxs-lookup"><span data-stu-id="7e974-138">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="7e974-139">使用 Key Vault 憑證部署 VM</span><span class="sxs-lookup"><span data-stu-id="7e974-139">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

