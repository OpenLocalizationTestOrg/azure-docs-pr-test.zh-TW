---
title: "最安全地儲存的密碼，Azure 堆疊上的 VM aaaDeploy |Microsoft 文件"
description: "了解如何 toodeploy VM 使用的密碼儲存在 Azure 堆疊金鑰保存庫"
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
ms.openlocfilehash: 368addc1dfc5b7adadd2151fbd6d354f7892eea5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a><span data-ttu-id="b9ea5-103">藉由擷取儲存在金鑰保存庫中的 hello 密碼來建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b9ea5-103">Create a virtual machine by retrieving hello password stored in a Key Vault</span></span>

<span data-ttu-id="b9ea5-104">當您在部署期間需要 toopass 安全的值，例如密碼時，可以將該值儲存為堆疊 Azure 金鑰保存庫中的密碼，並在 hello Azure 資源管理員範本中參考它。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-104">When you need toopass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in hello Azure Resource Manager templates.</span></span> <span data-ttu-id="b9ea5-105">您不需要 toomanually 輸入 hello 密碼每次部署 hello 資源，您也可以指定哪些使用者或服務主體可以存取 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-105">You do not need toomanually enter hello secret each time you deploy hello resources, you can also specify which users or service principals can access hello secret.</span></span> 

<span data-ttu-id="b9ea5-106">在本文中，我們逐步引導您 hello 步驟需要 toodeploy Azure 堆疊中的 Windows 虛擬機器擷取 hello 密碼儲存在金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-106">In this article, we walk you through hello steps required toodeploy a Windows virtual machine in Azure Stack by retrieving hello password that is stored in a Key Vault.</span></span> <span data-ttu-id="b9ea5-107">因此 hello 密碼永遠不會放在 hello 範本參數檔案中的純文字。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-107">Therefore hello password is never put in plain text in hello template parameter file.</span></span> <span data-ttu-id="b9ea5-108">如果您透過 VPN 連線，您可以使用下列步驟從 hello Azure 堆疊開發套件，或從外部用戶端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-108">You can use these steps either from hello Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ea5-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="b9ea5-109">Prerequisites</span></span>

* <span data-ttu-id="b9ea5-110">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello Azure 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-110">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="b9ea5-111">使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-111">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="b9ea5-112">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9ea5-112">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="b9ea5-113">Hello Azure 堆疊使用者的 PowerShell 環境設定。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-113">Configure hello Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="b9ea5-114">hello 下列步驟描述 hello 所需程序 toocreate 虛擬機器擷取儲存在金鑰保存庫中的 hello 密碼：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-114">hello following steps describe hello process required toocreate a virtual machine by retrieving hello password stored in a Key Vault:</span></span>

1. <span data-ttu-id="b9ea5-115">建立 Key Vault 祕密。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="b9ea5-116">更新 hello azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-116">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="b9ea5-117">部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-117">Deploy hello template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="b9ea5-118">建立 Key Vault 祕密</span><span class="sxs-lookup"><span data-stu-id="b9ea5-118">Create a Key Vault secret</span></span>

<span data-ttu-id="b9ea5-119">hello 下列指令碼會建立金鑰保存庫，並會將密碼儲存在 hello 做為密碼金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-119">hello following script creates a key vault, and stores a password in hello key vault as a secret.</span></span> <span data-ttu-id="b9ea5-120">使用 hello`-EnabledForDeployment`參數，當您要建立 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-120">Use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="b9ea5-121">這個參數可確保您可以從 Azure 資源管理員範本參考該 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-121">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

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

<span data-ttu-id="b9ea5-122">當您執行 hello 至上一個指令碼時，hello 輸出會包括 hello 密碼 URI。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-122">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="b9ea5-123">請記下此 URI。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-123">Make a note of this URI.</span></span> <span data-ttu-id="b9ea5-124">您有 tooreference 在 hello[部署 Windows 虛擬機器，以在金鑰保存庫範本中的密碼](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password)。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-124">You have tooreference it in hello [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span></span> <span data-ttu-id="b9ea5-125">下載 hello [101-vm-安全性-密碼](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password)到開發電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-125">Download hello [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) folder onto your development computer.</span></span> <span data-ttu-id="b9ea5-126">此資料夾包含 hello`azuredeploy.json`和`azuredeploy.parameters.json`hello 後續步驟中，您將需要的檔案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-126">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="b9ea5-127">修改 hello`azuredeploy.parameters.json`根據 tooyour 環境值的檔案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-127">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="b9ea5-128">特別感興趣的 hello 參數是 hello 保存庫名稱、 hello 保存庫的資源群組，以及 hello 密碼 URI （如 hello 至上一個指令碼所產生）。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-128">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="b9ea5-129">下列檔 hello 是參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-129">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="b9ea5-130">更新 hello azuredeploy.parameters.json 檔案</span><span class="sxs-lookup"><span data-stu-id="b9ea5-130">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="b9ea5-131">以 hello KeyVault URI、 secretName adminUsername hello 虛擬機器值，根據您的環境的 hello azuredeploy.parameters.json 檔案更新。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-131">Update hello azuredeploy.parameters.json file with hello KeyVault URI, secretName, adminUsername of hello virtual machine values as per your environment.</span></span> <span data-ttu-id="b9ea5-132">hello 下列 JSON 檔案顯示 hello 範本參數檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-132">hello following JSON file shows an example of hello template parameters file:</span></span> 

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

## <a name="template-deployment"></a><span data-ttu-id="b9ea5-133">範本部署</span><span class="sxs-lookup"><span data-stu-id="b9ea5-133">Template deployment</span></span>

<span data-ttu-id="b9ea5-134">現在使用下列 PowerShell 指令碼的 hello 部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-134">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
<span data-ttu-id="b9ea5-135">Hello 範本順利部署時，它會產生下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="b9ea5-135">When hello template is deployed successfully, it results in hello following output:</span></span>

![部署輸出](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="b9ea5-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9ea5-137">Next steps</span></span>
[<span data-ttu-id="b9ea5-138">使用 Key Vault 部署範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b9ea5-138">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="b9ea5-139">使用 Key Vault 憑證部署 VM</span><span class="sxs-lookup"><span data-stu-id="b9ea5-139">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

