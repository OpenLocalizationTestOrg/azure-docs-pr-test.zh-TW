---
title: "aaaCreate Azure DevTest Labs 自訂映像從 VHD 檔案，使用 PowerShell |Microsoft 文件"
description: "使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案自動建立自訂映像"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>使用 PowerShell 從 VHD 檔案建立自訂映像

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>逐步指示

hello 下列步驟引導您完成從 VHD 檔案，使用 PowerShell 建立自訂映像：

1. 在 PowerShell 提示字元中，登入 tooyour Azure 帳戶以下列呼叫 toohello hello**登入 AzureRmAccount** cmdlet。  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  選取 hello 需要 Azure 訂用帳戶，請呼叫 hello**選取 AzureRmSubscription** cmdlet。 取代下列預留位置 hello hello **$subscriptionId**變數並提供有效的 Azure 訂用帳戶識別碼。 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  取得呼叫 hello hello 實驗室物件**Get AzureRmResource** cmdlet。 取代下列預留位置 hello hello **$labRg**和**$labName**變數以 hello 適當環境的值。 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  收到 hello 實驗室儲存體帳戶和實驗室儲存體帳戶金鑰值 hello 實驗室物件。 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  取代下列預留位置 hello hello **$vhdUri**變數以 hello URI tooyour 所上傳 VHD 檔案。 您可以從 hello Azure 入口網站中的 hello 儲存體帳戶之 blob 刀鋒視窗取得 hello VHD 檔案的 URI。

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  建立 hello 自訂映像使用 hello**新增 AzureRmResourceGroupDeployment** cmdlet。 取代下列預留位置 hello hello **$customImageName**和**$customImageDescription**為您的環境變數 toomeaningful 名稱。

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>PowerShell 指令碼 toocreate 從 VHD 檔案的自訂映像

hello 下列 PowerShell 指令碼可以使用的 toocreate 從 VHD 檔案的自訂映像。 Hello 預留位置 （開始和結尾角括弧） 取代 hello 適當的值，針對您的需求。 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a>相關部落格文章

- [自訂映像或公式？](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [在 Azure DevTest Labs 之間複製自訂映像](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>後續步驟

- [新增 VM tooyour 實驗室](./devtest-lab-add-vm-with-artifacts.md)
