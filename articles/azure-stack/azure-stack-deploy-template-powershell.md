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
# <a name="deploy-templates-in-azure-stack-using-powershell"></a>使用 PowerShell 部署 Azure Stack 中的範本
使用 PowerShell toodeploy Azure Resource Manager 範本 toohello Azure 堆疊開發套件。  Resource Manager 範本可藉由單一協調作業，來部署和佈建應用程式的所有資源。

## <a name="run-azurerm-powershell-cmdlets"></a>執行 AzureRM PowerShell Cmdlet
在此範例中，您執行指令碼 toodeploy 虛擬機器 tooAzure 堆疊開發套件使用資源管理員範本。  在您繼續之前，請確保您已 [設定 PowerShell](azure-stack-powershell-configure-user.md)  

hello 這個範例範本中所用的 VHD 是 WindowsServer 2012 R2-Datacenter。

1. 跳過<http://aka.ms/AzureStackGitHub>，搜尋 hello **101 簡單的 windows vm**範本，並將它儲存 toohello 下列位置： c:\\範本\\azuredeploy-101-簡單-windows-vm.json。
2. 在 PowerShell 中執行下列部署指令碼的 hello。 以您的使用者名稱和密碼來取代「username」和「password」。 爾後再度使用上遞增 hello hello 值*$myNum*參數 tooprevent 覆寫您的部署。
   
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
3. 開啟 hello Azure 堆疊入口網站中，按一下**瀏覽**，按一下 **虛擬機器**，並尋找新的虛擬機器 (*myDeployment001*)。


## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 部署範本](azure-stack-deploy-template-visual-studio.md)

