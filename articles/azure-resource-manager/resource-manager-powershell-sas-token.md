---
title: "使用 SAS 權杖和 PowerShell 的 Azure 範本 aaaDeploy |Microsoft 文件"
description: "從範本所保護的 Azure 資源管理員和 Azure PowerShell toodeploy 資源 tooAzure 使用 SAS 權杖。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>使用 SAS 權杖和 Azure PowerShell 部署私用 Resource Manager 範本

當您的範本位於儲存體帳戶時，就可以限制存取 toohello 範本，並在部署期間提供的共用的存取簽章 (SAS) token。 本主題說明如何使用資源管理員範本 tooprovide SAS 權杖，在部署期間 toouse Azure PowerShell。 

## <a name="add-private-template-toostorage-account"></a>加入私用的範本 toostorage 帳戶

您可以新增範本 tooa 儲存體帳戶，並將 toothem 連結在部署期間使用 SAS 權杖。

> [!IMPORTANT]
> 下列 hello 步驟，包含 hello 範本的 hello blob 是可存取 tooonly hello 帳戶擁有者。 不過，當您建立 hello blob SAS 權杖，hello blob 是可存取 tooanyone 與該 URI。 另一位使用者攔截 hello URI，該使用者能 tooaccess hello 範本。 使用 SAS 權杖是限制存取 tooyour 範本的好方法，但您不應該直接在 hello 範本中包含機密資料，例如密碼。
> 
> 

hello 下列範例設定私人儲存體帳戶容器並上傳範本：
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>在部署期間提供 SAS Token
toodeploy 私用儲存體帳戶中，範本會產生 SAS 權杖，並將它包括 hello URI hello 範本中。 設定 hello 到期時間 tooallow 足夠時間 toocomplete hello 部署。
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

如需使用包含已連結範本的 SAS Token 範例，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。


## <a name="next-steps"></a>後續步驟
* 如簡介 toodeploying 範本，請參閱[部署資源與資源管理員範本和 Azure PowerShell](resource-group-template-deploy.md)。
* 如需部署範本的完整範例指令碼，請參閱[部署 Resource Manager 範本指令碼](resource-manager-samples-powershell-deploy.md)。
* toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

