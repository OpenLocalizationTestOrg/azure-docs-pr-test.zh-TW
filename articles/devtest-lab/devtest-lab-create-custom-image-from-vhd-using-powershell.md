---
title: "使用 PowerShell 從 VHD 檔案建立 Azure DevTest Labs 自訂映像 | Microsoft Docs"
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
ms.openlocfilehash: a4729f70aae80a13233fbe96a5d8a56c0c9d01d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="7eb71-103">使用 PowerShell 從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="7eb71-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="7eb71-104">逐步指示</span><span class="sxs-lookup"><span data-stu-id="7eb71-104">Step-by-step instructions</span></span>

<span data-ttu-id="7eb71-105">下列步驟將逐步引導您使用 PowerShell 從 VHD 檔案建立自訂映像：</span><span class="sxs-lookup"><span data-stu-id="7eb71-105">The following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="7eb71-106">在 PowerShell 提示字元中，使用下列對 **Login-AzureRmAccount** Cmdlet 的呼叫來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7eb71-106">At a PowerShell prompt, log in to your Azure account with the following call to the **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="7eb71-107">呼叫 **Select-AzureRmSubscription** Cmdlet 來選取想要的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7eb71-107">Select the desired Azure subscription by calling the **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="7eb71-108">以有效的 Azure 訂用帳戶 ID 取代 **$subscriptionId** 變數的下列預留位置。</span><span class="sxs-lookup"><span data-stu-id="7eb71-108">Replace the following placeholder for the **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="7eb71-109">呼叫 **Get-AzureRmResource** Cmdlet 來取得實驗室物件。</span><span class="sxs-lookup"><span data-stu-id="7eb71-109">Get the lab object by calling the **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="7eb71-110">以您環境的適當值取代 **$labRg** 和 **$labName** 變數的下列預留位置。</span><span class="sxs-lookup"><span data-stu-id="7eb71-110">Replace the following placeholders for the **$labRg** and **$labName** variables with the appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="7eb71-111">從實驗室物件取得實驗室儲存體帳戶和實驗室儲存體帳戶金鑰值。</span><span class="sxs-lookup"><span data-stu-id="7eb71-111">Get the lab storage account and lab storage account key values from the lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="7eb71-112">以您所上傳 VHD 檔案的 URI 取代 **$vhdUri** 變數的下列預留位置。</span><span class="sxs-lookup"><span data-stu-id="7eb71-112">Replace the following placeholder for the **$vhdUri** variable with the URI to your uploaded VHD file.</span></span> <span data-ttu-id="7eb71-113">您可以從 Azure 入口網站中儲存體帳戶的 Blob 刀鋒視窗取得 VHD 檔案的 URI。</span><span class="sxs-lookup"><span data-stu-id="7eb71-113">You can get the VHD file's URI from the storage account's blob blade in the Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  <span data-ttu-id="7eb71-114">使用 **New-AzureRmResourceGroupDeployment** Cmdlet 來建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="7eb71-114">Create the custom image using the **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="7eb71-115">將 **$customImageName** 和 **$customImageDescription** 變數的下列預留位置取代為對您環境有意義的名稱。</span><span class="sxs-lookup"><span data-stu-id="7eb71-115">Replace the following placeholders for the **$customImageName** and **$customImageDescription** variables to meaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="7eb71-116">可從 VHD 檔案建立自訂映像的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="7eb71-116">PowerShell script to create a custom image from a VHD file</span></span>

<span data-ttu-id="7eb71-117">您可以使用下列 PowerShell 指令碼從 VHD 檔案建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="7eb71-117">The following PowerShell script can be used to create a custom image from a VHD file.</span></span> <span data-ttu-id="7eb71-118">以符合您需求的適當值取代預留位置 (開頭和結尾是角括弧)。</span><span class="sxs-lookup"><span data-stu-id="7eb71-118">Replace the placeholders (starting and ending with angle brackets) with the appropriate values for your needs.</span></span> 

```PowerShell
# Log in to your Azure account.  
Login-AzureRmAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="7eb71-119">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="7eb71-119">Related blog posts</span></span>

- [<span data-ttu-id="7eb71-120">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="7eb71-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="7eb71-121">在 Azure DevTest Labs 之間複製自訂映像</span><span class="sxs-lookup"><span data-stu-id="7eb71-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="7eb71-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7eb71-122">Next steps</span></span>

- [<span data-ttu-id="7eb71-123">將 VM 新增到實驗室</span><span class="sxs-lookup"><span data-stu-id="7eb71-123">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
