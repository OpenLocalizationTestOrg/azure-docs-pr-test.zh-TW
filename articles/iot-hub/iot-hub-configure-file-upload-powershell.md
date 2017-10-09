---
title: "aaaUse hello Azure PowerShell tooconfigure 檔案上傳 |Microsoft 文件"
description: "如何 toouse hello Azure PowerShell cmdlet tooconfigure IoT 中樞 tooenable 檔案上傳從連接的裝置。 包含設定 hello 目的地 Azure 儲存體帳戶的相關資訊。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>使用 PowerShell 設定 IoT 中樞檔案上傳

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello[檔案上傳功能在 IoT 中樞][lnk-upload]，您必須先使 Azure 儲存體帳戶與 IoT 中樞。 您可以使用現有的儲存體帳戶或建立新帳戶。

toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure PowerShell Cmdlet][lnk-powershell-install]。
* Azure IoT 中樞。 如果您沒有 IoT 中樞，您可以使用 hello[新增 AzureRmIoTHub cmdlet] [ lnk-powershell-iothub] toocreate 一個或使用 hello 入口網站太[建立 IoT 中樞][ lnk-portal-hub].
* 一個 Azure 儲存體帳戶。 如果您沒有 Azure 儲存體帳戶，您可以使用 hello [Azure 儲存體 PowerShell cmdlet] [ lnk-powershell-storage] toocreate 一個或使用 hello 入口網站太[建立儲存體帳戶][lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>登入並設定 Azure 帳戶

登入 tooyour Azure 帳戶，並選取您的訂用帳戶。

1. Hello PowerShell 命令提示字元執行 hello**登入 AzureRmAccount** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. 如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。 使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:

    ```powershell
    Get-AzureRMSubscription
    ```

    使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toomanage IoT 中樞的 hello。 您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>擷取您的儲存體帳戶詳細資料

hello 下列步驟假設您建立儲存體帳戶使用 hello**資源管理員**部署模型，以及不 hello**傳統**部署模型。

tooconfigure file uploads 從您的裝置，您需要 Azure 儲存體帳戶的 hello 連接字串。 hello 儲存體帳戶必須在 hello IoT 中樞相同訂用帳戶。 您也需要 hello hello 儲存體帳戶中的 blob 容器名稱。 使用下列命令 tooretrieve hello 儲存體帳戶金鑰：

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

請記下 hello **key1**儲存體帳戶金鑰值。 您需要在 hello 下列步驟。

您可以使用現有的 blob 容器進行檔案上傳，或建立新容器：

* toolist hello 現有 blob 容器中儲存體帳戶，使用下列命令的 hello:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate blob 容器中儲存體帳戶，下列命令使用 hello:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>設定 IoT 中樞

您現在可以設定您的 IoT 中樞 tooenable[檔案上傳功能][ lnk-upload]使用您的儲存體帳戶詳細資料。

hello 組態需要 hello 下列值：

**儲存體容器**： 在您目前的 Azure 訂用帳戶 tooassociate 與 IoT 中樞中的 Azure 儲存體帳戶中的 blob 容器。 您擷取 hello 前面一節中的 hello 所需的儲存體帳戶資訊。 上傳檔案時 IoT 中心會自動與寫入權限 toothis blob 容器的裝置 toouse 產生 SAS Uri。

**接收已上傳檔案的通知**︰啟用或停用檔案上傳通知。

**SAS TTL**： 此設定為 hello 存留時間的 SAS Uri 傳回 IoT 中樞 toohello 裝置 hello。 依預設，設定 tooone 小時。

**檔案設定預設的 TTL 通知**: hello 的存留時間的檔案上傳通知到期。 依預設，設定 tooone 一天。

**檔案通知最大傳遞計數**: hello 的次數 hello IoT 中樞嘗試 toodeliver 檔案上傳通知。 依預設，設定 too10。

使用下列 PowerShell cmdlet tooconfigure hello 檔案上傳設定您的 IoT 中樞上的 hello:

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>後續步驟

IoT 中樞的 hello 檔案上傳功能的相關資訊，請參閱[從裝置的檔案上傳][lnk-upload]。

請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：

* [大量管理 IoT 裝置][lnk-bulk]
* [IoT 中樞度量][lnk-metrics]
* [作業監視][lnk-monitor]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 IoT Edge 來模擬裝置][lnk-iotedge]
* [保護您的 IoT 解決方案從接地 hello][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md