---
title: "aaaAdd hello 預設 VM 映像 toohello Azure 堆疊 marketplace |Microsoft 文件"
description: "新增 hello Windows Server 2016 VM 預設映像 toohello 堆疊 Azure marketplace。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a>新增 hello Windows Server 2016 VM 映像 toohello 堆疊 Azure marketplace

根據預設，沒有任何虛擬機器映像 hello Azure 堆疊 marketplace 中。 hello Azure 堆疊雲端管理員必須將映像 toohello marketplace，使用者才能使用它們。 您可以加入 hello Windows Server 2016 映像 toohello 堆疊 Azure marketplace 使用其中一種 hello 下列兩種方法：

* [從 hello Azure Marketplace 下載並新增 hello 映像](#add-the-image-by-downloading-it-from-the-Azure-marketplace)-如果您正在連線的案例中，而且您 Azure 堆疊的執行個體向 Azure 使用此選項。

* [使用 PowerShell 新增 hello 映像](#add-the-image-by-using-powershell)-使用此選項，如果您部署了 Azure 堆疊在中斷連接案例或案例中具有有限的連線。

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a>從 hello Azure Marketplace 下載並新增 hello 映像

1. 部署之後 Azure 堆疊，請登入 tooyour Azure 堆疊開發套件。

2. 按一下 [更多服務] > [市集管理] > [從 Azure 新增] 

3. 尋找或搜尋 hello **Windows Server 2016 Datacenter Eval**影像 > 按一下**下載**

   ![從 Azure 下載映像](media/azure-stack-add-default-image/download-image.png)

Hello 影像 hello 下載完成之後，會新增 toohello **Marketplace 管理**刀鋒視窗，它也可從 hello**虛擬機器**刀鋒視窗。

## <a name="add-hello-image-by-using-powershell"></a>使用 PowerShell 新增 hello 映像

### <a name="prerequisites"></a>必要條件 

執行下列必要條件 hello 從 hello[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* 安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。  

* 下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。  

* Toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016，並下載 Windows Server 2016 hello 評估。 出現提示時，選取 hello **ISO** hello 下載的版本。 資料錄 hello 路徑 toohello 下載位置，使用稍後的步驟執行。 此步驟需要網際網路連線能力。  

現在，執行下列步驟 tooadd hello 映像 toohello 堆疊 Azure marketplace 的 hello:
   
1. 使用下列命令的 hello 匯入 hello Azure 堆疊 Connect 和 ComputeAdmin 模組：

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. 登入 tooyour Azure 堆疊環境。 如果您的 Azure 堆疊環境部署使用 AAD 或 AD FS （請確定 tooreplace hello AAD 租用戶名稱），取決於指令碼執行的 hello 下列：  

   a. **Azure Active Directory**，使用下列 cmdlet 的 hello:

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. **Active Directory Federation Services**，使用下列 cmdlet 的 hello:
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. 新增 Windows Server 2016 hello 映像 toohello 堆疊 Azure marketplace (請確定 tooreplace hello *Path_to_ISO*與 hello 路徑 toohello WS2016 您下載的 ISO):

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

hello Windows Server 2016 VM 映像的 tooensure 具有 hello 最新累積更新，包括 hello`IncludeLatestCU`參數執行 hello 時`New-AzsServer2016VMImage`cmdlet。 請參閱 hello[參數](#parameters)> 一節有關如何允許參數 hello `New-AzsServer2016VMImage` cmdlet。 它採用有關小時 toopublish hello 映像 toohello 堆疊 Azure marketplace。 

## <a name="parameters"></a>參數

|New-AzsServer2016VMImage 參數|必要？|說明|
|-----|-----|------|
|ISOPath|是|hello 的完整的路徑 toohello 下載 Windows Server 2016 ISO。|
|Net35|否|這個參數可讓您 tooinstall hello.NET 3.5 執行階段 hello Windows Server 2016 映像上。 根據預設，這個值會設定 tootrue。 它是強制該 hello 映像包含.NET 3.5 hello 執行階段 tooinstall hello SQL 和 MYSQL 資源提供者。 |
|版本|否|此參數可讓您 toochoose 是否 tooadd**核心**或**完整**或**兩者**Windows Server 2016 映像。 根據預設，這個值會設定過 「 完整。 」|
|VHDSizeInMB|否|設定 hello 大小 （以 mb 為單位） 的 hello VHD 映像 toobe 加入 tooyour Azure 堆疊環境。 根據預設，這個值會設定 too40960 MB。|
|CreateGalleryItem|否|指定是否應建立 hello Windows Server 2016 映像的 Marketplace 項目。 根據預設，這個值會設定 tootrue。|
|location |否 |指定應該發行 hello 位置 toowhich hello Windows Server 2016 映像。|
|IncludeLatestCU|否|設定此參數 tooapply hello 最新 Windows Server 2016 累計更新 toohello 新的 VHD。|
|CUUri |否 |從特定的 URI 設定此值 toochoose hello Windows Server 2016 累計更新。 |
|CUPath |否 |設定此值 toochoose hello Windows Server 2016 累積更新從本機路徑。 這個選項很有用，如果您已部署的 hello Azure 堆疊的執行個體中斷連線的環境中。|

## <a name="next-steps"></a>後續步驟

[佈建虛擬機器](azure-stack-provision-vm.md)
