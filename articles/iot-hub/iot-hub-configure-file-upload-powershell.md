---
title: "使用 Azure PowerShell 設定檔案上傳 | Microsoft Docs"
description: "如何使用 Azure PowerShell Cmdlet 來設定 IoT 中樞，以便能夠從連接的裝置上傳檔案。 包含設定目的地 Azure 儲存體帳戶的相關資訊。"
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="1690c-104">使用 PowerShell 設定 IoT 中樞檔案上傳</span><span class="sxs-lookup"><span data-stu-id="1690c-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="1690c-105">若要使用 [IoT 中樞的檔案上傳功能][lnk-upload]，您必須先將 Azure 儲存體帳戶與您的 IoT 中樞建立關聯。</span><span class="sxs-lookup"><span data-stu-id="1690c-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="1690c-106">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="1690c-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="1690c-107">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1690c-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1690c-108">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1690c-108">An active Azure account.</span></span> <span data-ttu-id="1690c-109">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="1690c-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="1690c-110">[Azure PowerShell Cmdlet][lnk-powershell-install]。</span><span class="sxs-lookup"><span data-stu-id="1690c-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="1690c-111">Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1690c-111">An Azure IoT hub.</span></span> <span data-ttu-id="1690c-112">如果您沒有 IoT 中樞，您可以使用 [New-AzureRmIoTHub Cmdlet][lnk-powershell-iothub] 來建立一個，或使用入口網站來[建立 IoT 中樞][lnk-portal-hub]。</span><span class="sxs-lookup"><span data-stu-id="1690c-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="1690c-113">一個 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1690c-113">An Azure storage account.</span></span> <span data-ttu-id="1690c-114">如果您沒有 Azure 儲存體帳戶，您可以使用 [Azure 儲存體 PowerShell Cmdlet][lnk-powershell-storage] 來建立一個，或使用入口網站來[建立儲存體帳戶][lnk-portal-storage]。</span><span class="sxs-lookup"><span data-stu-id="1690c-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="1690c-115">登入並設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="1690c-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="1690c-116">登入您的 Azure 帳戶並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1690c-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="1690c-117">在 PowerShell 命令提示字元中，執行 **Login-AzureRmAccount** Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="1690c-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="1690c-118">如果您有多個 Azure 訂用帳戶，則登入 Azure 即會為您授與和您認證相關聯之所有 Azure 訂用帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="1690c-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="1690c-119">使用下列命令來列出可供您使用的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="1690c-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="1690c-120">使用下列命令，來選取您想要用來執行命令以管理 IoT 中樞的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1690c-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="1690c-121">您可以使用來自上一個命令之輸出內的訂用帳戶名稱或識別碼︰</span><span class="sxs-lookup"><span data-stu-id="1690c-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="1690c-122">擷取您的儲存體帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="1690c-122">Retrieve your storage account details</span></span>

<span data-ttu-id="1690c-123">下列步驟假設您使用 [Resource Manager] 部署模型，而非 [傳統] 部署模型，建立了儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1690c-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="1690c-124">若要從裝置設定檔案上傳，您需要 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1690c-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="1690c-125">儲存體帳戶必須與您的 IoT 中樞位於相同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1690c-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="1690c-126">您也需要儲存體帳戶中 blob 容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="1690c-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="1690c-127">使用下列命令來擷取儲存體帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="1690c-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="1690c-128">記下 **key1** 儲存體帳戶金鑰值。</span><span class="sxs-lookup"><span data-stu-id="1690c-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="1690c-129">您需要在後續步驟中用到此值。</span><span class="sxs-lookup"><span data-stu-id="1690c-129">You need it in the following steps.</span></span>

<span data-ttu-id="1690c-130">您可以使用現有的 blob 容器進行檔案上傳，或建立新容器：</span><span class="sxs-lookup"><span data-stu-id="1690c-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="1690c-131">若要列出儲存體帳戶中現有的 blob 容器，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1690c-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="1690c-132">若要在儲存體帳戶中建立 blob 容器，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1690c-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="1690c-133">設定 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="1690c-133">Configure your IoT hub</span></span>

<span data-ttu-id="1690c-134">您現在可以使用儲存體帳戶詳細資料來設定您的 IoT 中樞，以啟用[檔案上傳功能][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="1690c-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="1690c-135">設定需要下列值：</span><span class="sxs-lookup"><span data-stu-id="1690c-135">The configuration requires the following values:</span></span>

<span data-ttu-id="1690c-136">**儲存體容器**︰您目前 Azure 訂用帳戶內 Azure 儲存體帳戶中的 blob 容器，會與您的 IoT 中樞產生關聯。</span><span class="sxs-lookup"><span data-stu-id="1690c-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="1690c-137">您已在上一節中擷取了必要的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="1690c-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="1690c-138">IoT 中樞會自動產生具有此 Blob 容器寫入權限的 SAS URI，以供裝置上傳檔案時使用。</span><span class="sxs-lookup"><span data-stu-id="1690c-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="1690c-139">**接收已上傳檔案的通知**︰啟用或停用檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="1690c-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="1690c-140">**SAS TTL**︰這個設定是「IoT 中樞」傳回給裝置之 SAS URI 的存留時間。</span><span class="sxs-lookup"><span data-stu-id="1690c-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="1690c-141">預設會設為一小時。</span><span class="sxs-lookup"><span data-stu-id="1690c-141">Set to one hour by default.</span></span>

<span data-ttu-id="1690c-142">**檔案通知設定預設 TTL**：檔案上傳通知到期前的存留時間。</span><span class="sxs-lookup"><span data-stu-id="1690c-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="1690c-143">預設會設為一天。</span><span class="sxs-lookup"><span data-stu-id="1690c-143">Set to one day by default.</span></span>

<span data-ttu-id="1690c-144">**檔案通知最大傳遞計數**︰IoT 中樞可嘗試傳遞檔案上傳通知的次數。</span><span class="sxs-lookup"><span data-stu-id="1690c-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="1690c-145">預設會設為 10。</span><span class="sxs-lookup"><span data-stu-id="1690c-145">Set to 10 by default.</span></span>

<span data-ttu-id="1690c-146">使用下列 PowerShell Cmdlet 來設定 IoT 中樞上的檔案上傳設定：</span><span class="sxs-lookup"><span data-stu-id="1690c-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1690c-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1690c-147">Next steps</span></span>

<span data-ttu-id="1690c-148">如需 IoT 中樞檔案上傳功能的詳細資訊，請參閱[從裝置上傳檔案][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="1690c-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="1690c-149">遵循下列連結以深入了解如何管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="1690c-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="1690c-150">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="1690c-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="1690c-151">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="1690c-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="1690c-152">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="1690c-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="1690c-153">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="1690c-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1690c-154">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="1690c-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="1690c-155">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1690c-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="1690c-156">[徹底保護您的 IoT 解決方案][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="1690c-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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