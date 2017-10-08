---
title: "aaaAdding VM 映像 tooAzure 堆疊 |Microsoft 文件"
description: "加入您的組織自訂 Windows 或 Linux VM 映像的租用戶 toouse"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a>在 Azure Stack 中提供自訂虛擬機器映像

Azure 的堆疊可讓雲端系統管理員 toomake 自訂虛擬機器映像可用 tootheir 使用者。 這些映像可以參考 Azure 資源管理員範本，或加入 toothe Azure Marketplace UI hello 建立 Marketplace 項目。 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a>新增 VM 映像 toomarketplace 使用 PowerShell

執行下列必要條件 hello 從 hello[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)

* [安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。  

* 下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。  

* 準備 VHD 格式 (非 VHDX) 的 Windows 或 Linux 作業系統虛擬硬碟映像。
   
   * 針對 Windows 映像，hello 文章[上傳資源管理員部署的 Windows VM 映像 tooAzure](../virtual-machines/windows/upload-generalized-managed.md)包含映像準備指示在 hello**準備 hello VHD 上傳**> 一節。
   * 針對 Linux 映像，請遵循 hello 步驟來準備 hello 映像，或使用現有 Azure 堆疊 Linux 映像，如 hello 文章所述[Azure 堆疊上部署的 Linux 虛擬機器](azure-stack-linux.md)。  

現在，執行下列步驟 tooadd hello 映像 toohello 堆疊 Azure marketplace 的 hello:

1. 匯入 hello 連接和 ComputeAdmin 模組：
   
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
    
3. 藉由叫用 hello 新增 hello VM 映像`Add-AzsVMImage`cmdlet。 在 hello 新增 AzsVMImage cmdlet 中，指定 hello osType 為 Windows 或 Linux。 包含 hello 發行者、 方案、 SKU 和 hello VM 映像的版本。 請參閱 hello[參數](#parameters)hello 允許參數的相關資訊的區段。 這些參數會使用 Azure Resource Manager 範本 tooreference hello VM 映像。 以下是 hello 指令碼的範例引動過程：
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

hello 命令沒有 hello 遵循：

* 驗證 toohello Azure 堆疊環境
* 上傳 hello 新建立的暫存儲存體帳戶本機 VHD tooa
* 新增 hello VM 映像 toohello VM 映像儲存機制和
* 建立 Marketplace 項目

hello 命令執行成功的 tooverify 移 tooMarketplace 在 hello 入口網站，然後確認 hello VM 映像位於 hello**虛擬機器**類別目錄。

![已成功新增 VM 映像](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a>使用 PowerShell 來移除 VM 映像

當您不再需要 hello 您先前已上傳的虛擬機器映像時，則您可以使用下列 cmdlet 的 hello hello 商場刪除它：

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| **publisher** |hello 發行者名稱的使用者部署 hello 映像時所使用的 hello VM 映像的區段。 例如 ‘Microsoft’。 請勿在此欄位中包含空格或其他特殊字元。 |
| **offer** |hello 供應項目名稱 hello 使用者部署 hello VM 映像時所使用的 VM 映像的區段。 例如 ‘WindowsServer’。 請勿在此欄位中包含空格或其他特殊字元。 |
| **sku** |hello SKU 名稱 hello 使用者部署 hello VM 映像時所使用的 VM 映像的區段。 例如 ‘Datacenter2016’。 請勿在此欄位中包含空格或其他特殊字元。 |
| **version** |hello 版的 hello 使用者部署 hello VM 映像時所使用的 VM 映像。 這一版的 hello 格式 *\#。\#。\#*. 例如 ‘1.0.0’。 請勿在此欄位中包含空格或其他特殊字元。 |
| **osType** |hello osType hello 映像必須是 'Windows' 或 'Linux'。 |
| **osDiskLocalPath** |hello 本機路徑 toohello OS 磁碟的 VM 映像 tooAzure 堆疊為您上傳的 VHD。 |
| **dataDiskLocalPaths** |選擇性的 hello 可以 hello VM 映像的過程中上傳的資料磁碟的本機路徑陣列。 |
| **CreateGalleryItem** |布林旗標來判斷是否 toocreate Marketplace 中的項目。 根據預設，此屬性設定 tootrue。 |
| **title** |hello 的顯示名稱 Marketplace 項目。 根據預設，此屬性設定 toohello 發行者-優惠-Sku hello VM 映像。 |
| **description** |hello 描述 hello Marketplace 項目。 |
| **位置** |應經過發佈 hello 位置 toowhich hello VM 映像。 根據預設，這個值會設定 toolocal。|
| **osDiskBlobURI** |此指令碼也可視需要接受 osDisk 的 Blob 儲存體 URI。 |
| **dataDiskBlobURIs** |（選擇性） 此指令碼也會接受 Blob 儲存體 Uri 的陣列新增資料磁碟 toohello 映像。 |

## <a name="add-a-vm-image-through-hello-portal"></a>新增 VM 映像透過 hello 入口網站

> [!NOTE]
> 此方法需要個別建立 hello Marketplace 項目。

對映像的其中一個需求就是必須可藉由 Blob 儲存體 URI 參考它們。 準備 Windows 或 Linux 作業系統映像 VHD 格式 (不 VHDX)，然後再上傳 hello 映像 tooa Azure 或 Azure 堆疊中的儲存體帳戶。 如果您的映像已經上傳的 toohello Azure 或 Azure 堆疊中的 Blob 儲存體，您可以略過步驟 1。

1. [上傳資源管理員部署的 Windows VM 映像 tooAzure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/)或 Linux 映像，請遵循 hello 中所述的 hello 指示[Azure 堆疊上部署的 Linux 虛擬機器](azure-stack-linux.md)發行項。 您應該了解 hello 您上傳 hello 映像之前，下列考量：

   * 因為它會接受較少時間 toopush hello 映像 toohello Azure 堆疊映像儲存機制，很效率 tooupload 映像 tooAzure 堆疊 Blob 儲存體比 tooAzure Blob 儲存體。 
   
   * 上傳 hello 時[Windows VM 映像](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/)，請確定 toosubstitute hello**登入 tooAzure**步驟以 hello[設定 hello Azure 堆疊操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)步驟。  

   * 請記下 hello Blob 儲存體您上傳 hello 映像，也就是在 hello 遵循格式的 URI:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd

   * toomake hello blob 可匿名存取，請移 toohello 儲存體帳戶 blob 容器其中 hello VM 映像 VHD 上傳太**Blob，** ，然後選取 **存取原則**。 如果您想，您就可以改為產生 hello 容器的共用的存取簽章，並將它包含在 hello blob URI。

   ![瀏覽 toostorage 帳戶的 blob](./media/azure-stack-add-vm-image/image1.png)

   ![設定 blob 存取 toopublic](./media/azure-stack-add-vm-image/image2.png)

2. 登入 tooAzure 雲端系統管理員身分的堆疊 > hello 功能表中按一下**更多服務** > **資源提供者**> 選取**計算** >  **VM 映像** > **新增**

3. 在 hello**新增 VM 映像**刀鋒視窗中，輸入 hello 發行者、 方案、 SKU 和 hello 虛擬機器映像的版本。 這些名稱區段，請參閱 toohello 資源管理員範本中的 VM 映像。 請確定 tooselect **osType**正確。 如**OD 磁碟 Blob URI**、 輸入 hello 已在上傳映像的 Blob URI，然後按一下**建立**toobegin 建立 VM 映像。
   
   ![開始 toocreate hello 映像](./media/azure-stack-add-vm-image/image4.png)

   當成功建立 hello 映像時，hello VM 映像的狀態會變更 too'Succeeded'。

4. toomake hello 虛擬機器映像更輕易地可供使用者使用 hello UI 中，建議您最好太[建立 Marketplace 項目](azure-stack-create-and-publish-marketplace-item.md)。

## <a name="next-steps"></a>後續步驟

[佈建虛擬機器](azure-stack-provision-vm.md)