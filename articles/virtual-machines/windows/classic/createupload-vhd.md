---
title: "aaaCreate 和上傳 VM 映像使用 Powershell |Microsoft 文件"
description: "了解 toocreate 和上傳一般化的 Windows Server 映像 (VHD) 使用 hello 傳統部署模型和 Azure Powershell。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>建立及上傳 Windows Server VHD tooAzure
本文章將示範如何 tooupload 一般化的 VM 映像做為虛擬硬碟 (VHD)，您可以使用它 toocreate 虛擬機器。 如需 Microsoft Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 您也可以[上傳](../upload-generalized-managed.md)使用 hello 資源管理員模型在虛擬機器。

## <a name="prerequisites"></a>必要條件
本文假設您具有：

* **Azure 訂用帳戶** - 如果您沒有帳戶，您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -您已擁有 hello Microsoft Azure PowerShell 模組安裝並設定 toouse 訂用帳戶。
* **A。VHD 檔案**-支援的 Windows 作業系統中的.vhd 檔案和附加的 tooa 虛擬機器儲存。 如果 hello 伺服器角色上執行 hello VHD 的核取 toosee 都支援 Sysprep。 如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。

    > [!IMPORTANT]
    > 在 Microsoft Azure 中不支援 hello VHDX 格式。 您可以將轉換 hello 磁碟 tooVHD 格式使用 HYPER-V 管理員] 或 [hello [CONVERT-VHD 指令程式](http://technet.microsoft.com/library/hh848454.aspx)。 如需詳細資料，請參閱 [部落格文章](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)。

## <a name="step-1-prep-hello-vhd"></a>步驟 1： 準備 hello VHD
您上傳 hello VHD tooAzure 之前，它會需要 toobe 使用 hello Sysprep 工具一般化。 這可讓準備 hello VHD toobe 做為映像。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。 執行 Sysprep 之前先備份 hello VM。

從 hello hello 作業系統的虛擬機器已安裝，請以完成下列程序的 hello:

1. 登入 toohello 作業系統。
2. 以系統管理員身分開啟 [命令提示字元] 視窗。 變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。

    ![開啟 [命令提示字元] 視窗](./media/createupload-vhd/sysprep_commandprompt.png)
3. hello**系統準備工具** 對話方塊隨即出現。

   ![啟動 Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. 在 hello**系統準備工具**，選取**輸入系統全新體驗 (OOBE)**並確定**一般化**已核取。
5. 在 [關機選項] 中選取 [關機]。
6. 按一下 [確定] 。

## <a name="step-2-create-a-storage-account-and-a-container"></a>步驟 2：建立儲存體帳戶和容器
您需要在 Azure 中的儲存體帳戶，因此您需要的地方 tooupload hello.vhd 檔案。 此步驟說明如何 toocreate 帳戶或 get hello 資訊您需要從現有的帳戶。 取代中的 hello 變數&lsaquo;方括號&rsaquo;具有您個人資訊。

1. 登入

    ```powershell
    Add-AzureAccount
    ```

2. 設定您的 Azure 訂用帳戶

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. 建立新的儲存體帳戶。 hello hello 儲存體帳戶名稱是唯一的 3-24 個字元。 hello 名稱可以是字母和數字的任意組合。 您也需要 toospecify 位置，例如"East US"

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. 設定 hello 新儲存體帳戶做為 hello 預設值。

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. 建立新的容器。

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>步驟 3: Hello.vhd 檔案上傳
使用 hello [Add-azurevhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD。

從 hello 先前步驟中的 hello Azure PowerShell 視窗，輸入 hello 下列命令，並取代中的 hello 變數&lsaquo;方括號&rsaquo;具有您個人資訊。

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>步驟 4： 加入 hello 影像 tooyour 清單的自訂映像
使用 hello [Add-azurevmimage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello 影像 toohello 清單的自訂映像。

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>後續步驟
您現在可以[建立自訂 VM](createportal.md)使用 hello 映像上傳。
