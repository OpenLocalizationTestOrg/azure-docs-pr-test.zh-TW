---
title: "使用 Azure 入口網站設定檔案上傳 | Microsoft Docs"
description: "如何使用 Azure 入口網站來設定 IoT 中樞，以便能夠從連接的裝置上傳檔案。 包含設定目的地 Azure 儲存體帳戶的相關資訊。"
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
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="c5ffd-104">使用 Azure 入口網站設定 IoT 中樞檔案上傳</span><span class="sxs-lookup"><span data-stu-id="c5ffd-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="c5ffd-105">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="c5ffd-105">File upload</span></span>

<span data-ttu-id="c5ffd-106">若要使用 [IoT 中樞的檔案上傳功能][lnk-upload]，您必須先將 Azure 儲存體帳戶與您的中樞建立關聯。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="c5ffd-107">選取 [檔案上傳] ，可顯示正在修改之 IoT 中樞的檔案上傳屬性清單。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![在入口網站中檢視 IoT 中樞檔案上傳設定][13]

<span data-ttu-id="c5ffd-109">**儲存體容器**︰使用 Azure 入口網站在您目前的 Azure 訂用帳戶中選取 Azure 儲存體帳戶中的 blob 容器，來與您的 IoT 中樞建立關聯。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="c5ffd-110">如果有需要，您可以在 [儲存體帳戶] 刀鋒視窗上建立 Azure 儲存體帳戶，並在 [容器] 刀鋒視窗上建立 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="c5ffd-111">IoT 中樞會自動產生具有此 Blob 容器寫入權限的 SAS URI，以供裝置上傳檔案時使用。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![在入口網站中檢視檔案上傳的儲存體容器][14]

<span data-ttu-id="c5ffd-113">**接收已上傳檔案的通知**︰透過切換來啟用或停用檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="c5ffd-114">**SAS TTL**︰這個設定是「IoT 中樞」傳回給裝置之 SAS URI 的存留時間。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="c5ffd-115">預設為 1 小時，但可以使用滑桿來自訂成其他值。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="c5ffd-116">**檔案通知設定預設 TTL**：檔案上傳通知到期前的存留時間。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="c5ffd-117">預設為 1 天，但可以使用滑桿來自訂成其他值。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="c5ffd-118">**檔案通知最大傳遞計數**︰IoT 中樞可嘗試傳遞檔案上傳通知的次數。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="c5ffd-119">預設為 10，但可以使用滑桿來自訂成其他值。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![在入口網站中設定 IoT 中樞檔案上傳][15]

## <a name="next-steps"></a><span data-ttu-id="c5ffd-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5ffd-121">Next steps</span></span>

<span data-ttu-id="c5ffd-122">如需 IoT 中樞檔案上傳功能的詳細資訊，請參閱 IoT 中樞開發人員指南中的[從裝置上傳檔案][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="c5ffd-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="c5ffd-123">遵循下列連結以深入了解如何管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="c5ffd-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="c5ffd-124">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="c5ffd-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="c5ffd-125">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="c5ffd-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="c5ffd-126">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="c5ffd-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="c5ffd-127">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="c5ffd-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c5ffd-128">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="c5ffd-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="c5ffd-129">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c5ffd-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="c5ffd-130">[徹底保護您的 IoT 解決方案][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="c5ffd-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
