---
title: "在 Azure 堆疊中使用 PowerShell aaaDeploy 範本 |Microsoft 文件"
description: "深入了解如何 toodeploy 使用資源管理員範本和 PowerShell 在虛擬機器。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: fb0d4b190e058b3c5c1273b6c91fc3d72dedeb1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a><span data-ttu-id="a7d1d-103">使用 PowerShell 部署 Azure Stack 中的範本</span><span class="sxs-lookup"><span data-stu-id="a7d1d-103">Deploy templates in Azure Stack using PowerShell</span></span>
<span data-ttu-id="a7d1d-104">使用 PowerShell toodeploy Azure Resource Manager 範本 toohello Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-104">Use PowerShell toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span>  <span data-ttu-id="a7d1d-105">Resource Manager 範本可藉由單一協調作業，來部署和佈建應用程式的所有資源。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span></span>

## <a name="run-azurerm-powershell-cmdlets"></a><span data-ttu-id="a7d1d-106">執行 AzureRM PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a7d1d-106">Run AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="a7d1d-107">在此範例中，您執行指令碼 toodeploy 虛擬機器 tooAzure 堆疊開發套件使用資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-107">In this example, you run a script toodeploy a virtual machine tooAzure Stack Development Kit using a Resource Manager template.</span></span>  <span data-ttu-id="a7d1d-108">在您繼續之前，請確保您已 [設定 PowerShell](azure-stack-powershell-configure-user.md)</span><span class="sxs-lookup"><span data-stu-id="a7d1d-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure-user.md)</span></span>  

<span data-ttu-id="a7d1d-109">hello 這個範例範本中所用的 VHD 是 WindowsServer 2012 R2-Datacenter。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-109">hello VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span></span>

1. <span data-ttu-id="a7d1d-110">跳過<http://aka.ms/AzureStackGitHub>，搜尋 hello **101 簡單的 windows vm**範本，並將它儲存 toohello 下列位置： c:\\範本\\azuredeploy-101-簡單-windows-vm.json。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-110">Go too<http://aka.ms/AzureStackGitHub>, search for hello **101-simple-windows-vm** template, and save it toohello following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span></span>
2. <span data-ttu-id="a7d1d-111">在 PowerShell 中執行下列部署指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-111">In PowerShell, run hello following deployment script.</span></span> <span data-ttu-id="a7d1d-112">以您的使用者名稱和密碼來取代「username」和「password」。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-112">Replace *username* and *password* with your username and password.</span></span> <span data-ttu-id="a7d1d-113">爾後再度使用上遞增 hello hello 值*$myNum*參數 tooprevent 覆寫您的部署。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-113">On subsequent uses, increment hello value for hello *$myNum* parameter tooprevent overwriting your deployment.</span></span>
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. <span data-ttu-id="a7d1d-114">開啟 hello Azure 堆疊入口網站中，按一下**瀏覽**，按一下 **虛擬機器**，並尋找新的虛擬機器 (*myDeployment001*)。</span><span class="sxs-lookup"><span data-stu-id="a7d1d-114">Open hello Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7d1d-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7d1d-115">Next steps</span></span>
[<span data-ttu-id="a7d1d-116">使用 Visual Studio 部署範本</span><span class="sxs-lookup"><span data-stu-id="a7d1d-116">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

