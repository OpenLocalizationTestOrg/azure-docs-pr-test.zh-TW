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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="93cac-104">使用 PowerShell 設定 IoT 中樞檔案上傳</span><span class="sxs-lookup"><span data-stu-id="93cac-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="93cac-105">toouse hello[檔案上傳功能在 IoT 中樞][lnk-upload]，您必須先使 Azure 儲存體帳戶與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="93cac-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="93cac-106">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="93cac-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="93cac-107">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="93cac-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="93cac-108">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93cac-108">An active Azure account.</span></span> <span data-ttu-id="93cac-109">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="93cac-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="93cac-110">[Azure PowerShell Cmdlet][lnk-powershell-install]。</span><span class="sxs-lookup"><span data-stu-id="93cac-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="93cac-111">Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="93cac-111">An Azure IoT hub.</span></span> <span data-ttu-id="93cac-112">如果您沒有 IoT 中樞，您可以使用 hello[新增 AzureRmIoTHub cmdlet] [ lnk-powershell-iothub] toocreate 一個或使用 hello 入口網站太[建立 IoT 中樞][ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="93cac-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="93cac-113">一個 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93cac-113">An Azure storage account.</span></span> <span data-ttu-id="93cac-114">如果您沒有 Azure 儲存體帳戶，您可以使用 hello [Azure 儲存體 PowerShell cmdlet] [ lnk-powershell-storage] toocreate 一個或使用 hello 入口網站太[建立儲存體帳戶][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="93cac-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="93cac-115">登入並設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="93cac-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="93cac-116">登入 tooyour Azure 帳戶，並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="93cac-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="93cac-117">Hello PowerShell 命令提示字元執行 hello**登入 AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93cac-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="93cac-118">如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="93cac-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="93cac-119">使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="93cac-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="93cac-120">使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toomanage IoT 中樞的 hello。</span><span class="sxs-lookup"><span data-stu-id="93cac-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="93cac-121">您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：</span><span class="sxs-lookup"><span data-stu-id="93cac-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="93cac-122">擷取您的儲存體帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="93cac-122">Retrieve your storage account details</span></span>

<span data-ttu-id="93cac-123">hello 下列步驟假設您建立儲存體帳戶使用 hello**資源管理員**部署模型，以及不 hello**傳統**部署模型。</span><span class="sxs-lookup"><span data-stu-id="93cac-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="93cac-124">tooconfigure file uploads 從您的裝置，您需要 Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="93cac-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="93cac-125">hello 儲存體帳戶必須在 hello IoT 中樞相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="93cac-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="93cac-126">您也需要 hello hello 儲存體帳戶中的 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="93cac-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="93cac-127">使用下列命令 tooretrieve hello 儲存體帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="93cac-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="93cac-128">請記下 hello **key1**儲存體帳戶金鑰值。</span><span class="sxs-lookup"><span data-stu-id="93cac-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="93cac-129">您需要在 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="93cac-129">You need it in hello following steps.</span></span>

<span data-ttu-id="93cac-130">您可以使用現有的 blob 容器進行檔案上傳，或建立新容器：</span><span class="sxs-lookup"><span data-stu-id="93cac-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="93cac-131">toolist hello 現有 blob 容器中儲存體帳戶，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="93cac-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="93cac-132">toocreate blob 容器中儲存體帳戶，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="93cac-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="93cac-133">設定 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="93cac-133">Configure your IoT hub</span></span>

<span data-ttu-id="93cac-134">您現在可以設定您的 IoT 中樞 tooenable[檔案上傳功能][ lnk-upload]使用您的儲存體帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="93cac-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="93cac-135">hello 組態需要 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="93cac-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="93cac-136">**儲存體容器**： 在您目前的 Azure 訂用帳戶 tooassociate 與 IoT 中樞中的 Azure 儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="93cac-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="93cac-137">您擷取 hello 前面一節中的 hello 所需的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="93cac-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="93cac-138">上傳檔案時 IoT 中心會自動與寫入權限 toothis blob 容器的裝置 toouse 產生 SAS Uri。</span><span class="sxs-lookup"><span data-stu-id="93cac-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="93cac-139">**接收已上傳檔案的通知**︰啟用或停用檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="93cac-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="93cac-140">**SAS TTL**： 此設定為 hello 存留時間的 SAS Uri 傳回 IoT 中樞 toohello 裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="93cac-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="93cac-141">依預設，設定 tooone 小時。</span><span class="sxs-lookup"><span data-stu-id="93cac-141">Set tooone hour by default.</span></span>

<span data-ttu-id="93cac-142">**檔案設定預設的 TTL 通知**: hello 的存留時間的檔案上傳通知到期。</span><span class="sxs-lookup"><span data-stu-id="93cac-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="93cac-143">依預設，設定 tooone 一天。</span><span class="sxs-lookup"><span data-stu-id="93cac-143">Set tooone day by default.</span></span>

<span data-ttu-id="93cac-144">**檔案通知最大傳遞計數**: hello 的次數 hello IoT 中樞嘗試 toodeliver 檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="93cac-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="93cac-145">依預設，設定 too10。</span><span class="sxs-lookup"><span data-stu-id="93cac-145">Set too10 by default.</span></span>

<span data-ttu-id="93cac-146">使用下列 PowerShell cmdlet tooconfigure hello 檔案上傳設定您的 IoT 中樞上的 hello:</span><span class="sxs-lookup"><span data-stu-id="93cac-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93cac-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93cac-147">Next steps</span></span>

<span data-ttu-id="93cac-148">IoT 中樞的 hello 檔案上傳功能的相關資訊，請參閱[從裝置的檔案上傳][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="93cac-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="93cac-149">請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="93cac-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="93cac-150">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="93cac-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="93cac-151">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="93cac-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="93cac-152">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="93cac-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="93cac-153">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="93cac-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="93cac-154">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="93cac-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="93cac-155">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="93cac-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="93cac-156">[保護您的 IoT 解決方案從接地 hello][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="93cac-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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