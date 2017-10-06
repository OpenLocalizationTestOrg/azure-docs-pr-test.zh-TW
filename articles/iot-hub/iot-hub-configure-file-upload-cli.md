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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="8dffc-103">使用 Azure CLI 來設定 IoT 中樞檔案上傳</span><span class="sxs-lookup"><span data-stu-id="8dffc-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="8dffc-104">toouse hello[檔案上傳功能在 IoT 中樞][lnk-upload]，您必須先使 Azure 儲存體帳戶與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8dffc-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="8dffc-105">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="8dffc-106">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="8dffc-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="8dffc-107">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-107">An active Azure account.</span></span> <span data-ttu-id="8dffc-108">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="8dffc-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="8dffc-109">[Azure CLI 2.0][lnk-CLI-install]。</span><span class="sxs-lookup"><span data-stu-id="8dffc-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="8dffc-110">Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8dffc-110">An Azure IoT hub.</span></span> <span data-ttu-id="8dffc-111">如果您沒有 IoT 中樞，您可以使用 hello `az iot hub create` [命令][ lnk-cli-create-iothub] toocreate 一個或使用 hello 入口網站太 [建立 IoT 中心] [lnk 入口網站-中心]。</span><span class="sxs-lookup"><span data-stu-id="8dffc-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="8dffc-112">Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-112">An Azure Storage account.</span></span> <span data-ttu-id="8dffc-113">如果您沒有 Azure 儲存體帳戶，您可以使用 hello [Azure CLI 2.0-管理儲存體帳戶][ lnk-manage-storage] toocreate 其中一個或使用 hello 入口網站太[建立儲存體帳戶][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="8dffc-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="8dffc-114">登入並設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="8dffc-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="8dffc-115">登入 tooyour Azure 帳戶，並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="8dffc-116">在 hello 命令提示字元中執行 hello[登入命令][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="8dffc-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="8dffc-117">請遵循 hello 指示 tooauthenticate 使用 hello 程式碼，並登入 tooyour 透過 web 瀏覽器的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="8dffc-118">如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="8dffc-119">使用下列 hello[命令 toolist hello Azure 帳戶][ lnk-az-account-command]適用於您 toouse:</span><span class="sxs-lookup"><span data-stu-id="8dffc-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="8dffc-120">使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。</span><span class="sxs-lookup"><span data-stu-id="8dffc-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="8dffc-121">您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：</span><span class="sxs-lookup"><span data-stu-id="8dffc-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="8dffc-122">擷取您的儲存體帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="8dffc-122">Retrieve your storage account details</span></span>

<span data-ttu-id="8dffc-123">hello 下列步驟假設您建立儲存體帳戶使用 hello**資源管理員**部署模型，以及不 hello**傳統**部署模型。</span><span class="sxs-lookup"><span data-stu-id="8dffc-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="8dffc-124">tooconfigure file uploads 從您的裝置，您需要 Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="8dffc-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="8dffc-125">hello 儲存體帳戶必須在 hello IoT 中樞相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dffc-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="8dffc-126">您也需要 hello hello 儲存體帳戶中的 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="8dffc-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="8dffc-127">使用下列命令 tooretrieve hello 儲存體帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="8dffc-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="8dffc-128">請記下 hello **connectionString**值。</span><span class="sxs-lookup"><span data-stu-id="8dffc-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="8dffc-129">您需要在 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="8dffc-129">You need it in hello following steps.</span></span>

<span data-ttu-id="8dffc-130">您可以使用現有的 blob 容器進行檔案上傳，或建立新容器：</span><span class="sxs-lookup"><span data-stu-id="8dffc-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="8dffc-131">toolist hello 現有 blob 容器中儲存體帳戶，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8dffc-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="8dffc-132">toocreate blob 容器中儲存體帳戶，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="8dffc-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="8dffc-133">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="8dffc-133">File upload</span></span>

<span data-ttu-id="8dffc-134">您現在可以設定您的 IoT 中樞 tooenable[檔案上傳功能][ lnk-upload]使用您的儲存體帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8dffc-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="8dffc-135">hello 組態需要 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="8dffc-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="8dffc-136">**儲存體容器**： 在您目前的 Azure 訂用帳戶 tooassociate 與 IoT 中樞中的 Azure 儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="8dffc-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="8dffc-137">您擷取 hello 前面一節中的 hello 所需的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="8dffc-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="8dffc-138">上傳檔案時 IoT 中心會自動與寫入權限 toothis blob 容器的裝置 toouse 產生 SAS Uri。</span><span class="sxs-lookup"><span data-stu-id="8dffc-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="8dffc-139">**接收已上傳檔案的通知**︰啟用或停用檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="8dffc-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="8dffc-140">**SAS TTL**： 此設定為 hello 存留時間的 SAS Uri 傳回 IoT 中樞 toohello 裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="8dffc-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="8dffc-141">依預設，設定 tooone 小時。</span><span class="sxs-lookup"><span data-stu-id="8dffc-141">Set tooone hour by default.</span></span>

<span data-ttu-id="8dffc-142">**檔案設定預設的 TTL 通知**: hello 的存留時間的檔案上傳通知到期。</span><span class="sxs-lookup"><span data-stu-id="8dffc-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="8dffc-143">依預設，設定 tooone 一天。</span><span class="sxs-lookup"><span data-stu-id="8dffc-143">Set tooone day by default.</span></span>

<span data-ttu-id="8dffc-144">**檔案通知最大傳遞計數**: hello 的次數 hello IoT 中樞嘗試 toodeliver 檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="8dffc-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="8dffc-145">依預設，設定 too10。</span><span class="sxs-lookup"><span data-stu-id="8dffc-145">Set too10 by default.</span></span>

<span data-ttu-id="8dffc-146">使用下列 Azure CLI 命令 tooconfigure hello 檔案上傳設定您的 IoT 中樞上的 hello:</span><span class="sxs-lookup"><span data-stu-id="8dffc-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="8dffc-147">在 Bash 殼層中使用︰</span><span class="sxs-lookup"><span data-stu-id="8dffc-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="8dffc-148">在 Windows 命令提示字元中使用︰</span><span class="sxs-lookup"><span data-stu-id="8dffc-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="8dffc-149">您可以使用下列命令的 hello IoT 中樞上檢閱 hello 檔案上傳組態：</span><span class="sxs-lookup"><span data-stu-id="8dffc-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="8dffc-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8dffc-150">Next steps</span></span>

<span data-ttu-id="8dffc-151">IoT 中樞的 hello 檔案上傳功能的相關資訊，請參閱[從裝置的檔案上傳][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="8dffc-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="8dffc-152">請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="8dffc-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="8dffc-153">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="8dffc-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="8dffc-154">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="8dffc-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="8dffc-155">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="8dffc-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="8dffc-156">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8dffc-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8dffc-157">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8dffc-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="8dffc-158">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8dffc-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="8dffc-159">[保護您的 IoT 解決方案從接地 hello][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="8dffc-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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