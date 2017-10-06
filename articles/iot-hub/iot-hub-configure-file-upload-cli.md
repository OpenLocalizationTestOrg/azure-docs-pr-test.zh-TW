---
title: "aaaConfigure 檔案上傳 tooIoT 集線器使用 Azure CLI (az.py) |Microsoft 文件"
description: "如何 tooconfigure fileuploads tooAzure IoT 中樞使用 hello 跨平台 Azure CLI 2.0 (az.py)。"
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>使用 Azure CLI 來設定 IoT 中樞檔案上傳

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello[檔案上傳功能在 IoT 中樞][lnk-upload]，您必須先使 Azure 儲存體帳戶與 IoT 中樞。 您可以使用現有的儲存體帳戶或建立新帳戶。

toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure CLI 2.0][lnk-CLI-install]。
* Azure IoT 中樞。 如果您沒有 IoT 中樞，您可以使用 hello `az iot hub create` [命令][ lnk-cli-create-iothub] toocreate 一個或使用 hello 入口網站太 [建立 IoT 中心] [lnk 入口網站-中心]。
* Azure 儲存體帳戶。 如果您沒有 Azure 儲存體帳戶，您可以使用 hello [Azure CLI 2.0-管理儲存體帳戶][ lnk-manage-storage] toocreate 其中一個或使用 hello 入口網站太[建立儲存體帳戶][lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>登入並設定 Azure 帳戶

登入 tooyour Azure 帳戶，並選取您的訂用帳戶。

1. 在 hello 命令提示字元中執行 hello[登入命令][lnk-login-command]:

    ```azurecli
    az login
    ```

    請遵循 hello 指示 tooauthenticate 使用 hello 程式碼，並登入 tooyour 透過 web 瀏覽器的 Azure 帳戶。

1. 如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 帳戶。 使用下列 hello[命令 toolist hello Azure 帳戶][ lnk-az-account-command]適用於您 toouse:

    ```azurecli
    az account list
    ```

    使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。 您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>擷取您的儲存體帳戶詳細資料

hello 下列步驟假設您建立儲存體帳戶使用 hello**資源管理員**部署模型，以及不 hello**傳統**部署模型。

tooconfigure file uploads 從您的裝置，您需要 Azure 儲存體帳戶的 hello 連接字串。 hello 儲存體帳戶必須在 hello IoT 中樞相同訂用帳戶。 您也需要 hello hello 儲存體帳戶中的 blob 容器名稱。 使用下列命令 tooretrieve hello 儲存體帳戶金鑰：

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

請記下 hello **connectionString**值。 您需要在 hello 下列步驟。

您可以使用現有的 blob 容器進行檔案上傳，或建立新容器：

* toolist hello 現有 blob 容器中儲存體帳戶，使用下列命令的 hello:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate blob 容器中儲存體帳戶，下列命令使用 hello:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>檔案上傳

您現在可以設定您的 IoT 中樞 tooenable[檔案上傳功能][ lnk-upload]使用您的儲存體帳戶詳細資料。

hello 組態需要 hello 下列值：

**儲存體容器**： 在您目前的 Azure 訂用帳戶 tooassociate 與 IoT 中樞中的 Azure 儲存體帳戶中的 blob 容器。 您擷取 hello 前面一節中的 hello 所需的儲存體帳戶資訊。 上傳檔案時 IoT 中心會自動與寫入權限 toothis blob 容器的裝置 toouse 產生 SAS Uri。

**接收已上傳檔案的通知**︰啟用或停用檔案上傳通知。

**SAS TTL**： 此設定為 hello 存留時間的 SAS Uri 傳回 IoT 中樞 toohello 裝置 hello。 依預設，設定 tooone 小時。

**檔案設定預設的 TTL 通知**: hello 的存留時間的檔案上傳通知到期。 依預設，設定 tooone 一天。

**檔案通知最大傳遞計數**: hello 的次數 hello IoT 中樞嘗試 toodeliver 檔案上傳通知。 依預設，設定 too10。

使用下列 Azure CLI 命令 tooconfigure hello 檔案上傳設定您的 IoT 中樞上的 hello:

在 Bash 殼層中使用︰

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

在 Windows 命令提示字元中使用︰

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

您可以使用下列命令的 hello IoT 中樞上檢閱 hello 檔案上傳組態：

```azurecli
az iot hub show --name {your iot hub name}
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

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create