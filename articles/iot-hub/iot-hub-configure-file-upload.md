---
title: "aaaUse hello Azure 入口網站 tooconfigure 檔案上傳 |Microsoft 文件"
description: "如何 toouse hello Azure 入口網站 tooconfigure IoT 中樞 tooenable 檔案上傳從連接的裝置。 包含設定 hello 目的地 Azure 儲存體帳戶的相關資訊。"
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
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="b5058-104">設定使用 hello Azure 入口網站的 IoT 中樞檔案上傳</span><span class="sxs-lookup"><span data-stu-id="b5058-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="b5058-105">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="b5058-105">File upload</span></span>

<span data-ttu-id="b5058-106">toouse hello[檔案上傳功能在 IoT 中樞][lnk-upload]，您必須先使 Azure 儲存體帳戶與您的中樞。</span><span class="sxs-lookup"><span data-stu-id="b5058-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="b5058-107">選取**檔案上傳**toodisplay hello IoT 中樞正在修改的檔案上傳內容的清單。</span><span class="sxs-lookup"><span data-stu-id="b5058-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![檢視 IoT 中樞檔案上傳 hello 入口網站中設定][13]

<span data-ttu-id="b5058-109">**儲存體容器**： 使用 Azure 入口網站 tooselect hello 您目前的 Azure 訂用帳戶 tooassociate 與 IoT 中樞中的 Azure 儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="b5058-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="b5058-110">如果有必要，您可以建立 Azure 儲存體帳戶上 hello**儲存體帳戶**刀鋒視窗和 blob 容器上 hello**容器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b5058-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="b5058-111">上傳檔案時 IoT 中心會自動與寫入權限 toothis blob 容器的裝置 toouse 產生 SAS Uri。</span><span class="sxs-lookup"><span data-stu-id="b5058-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Hello 入口網站中檢視檔案上傳的儲存體容器][14]

<span data-ttu-id="b5058-113">**接收通知的上傳的檔案**： 啟用或停用透過 hello 切換檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="b5058-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="b5058-114">**SAS TTL**： 此設定為 hello 存留時間的 SAS Uri 傳回 IoT 中樞 toohello 裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="b5058-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="b5058-115">依預設，設定 tooone 小時，但可以自訂的 tooother 值使用 hello 滑桿。</span><span class="sxs-lookup"><span data-stu-id="b5058-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="b5058-116">**檔案設定預設的 TTL 通知**: hello 的存留時間的檔案上傳通知到期。</span><span class="sxs-lookup"><span data-stu-id="b5058-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="b5058-117">依預設，設定 tooone 天，但可以自訂的 tooother 值使用 hello 滑桿。</span><span class="sxs-lookup"><span data-stu-id="b5058-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="b5058-118">**檔案通知最大傳遞計數**: hello 的次數 hello IoT 中樞嘗試 toodeliver 檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="b5058-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="b5058-119">依預設，設定 too10，但可以自訂的 tooother 值使用 hello 滑桿。</span><span class="sxs-lookup"><span data-stu-id="b5058-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![在 hello 入口網站中設定 IoT 中樞檔案上傳][15]

## <a name="next-steps"></a><span data-ttu-id="b5058-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5058-121">Next steps</span></span>

<span data-ttu-id="b5058-122">IoT 中樞的 hello 檔案上傳功能的相關資訊，請參閱[從裝置的檔案上傳][ lnk-upload] hello IoT 中樞開發人員指南 》 中。</span><span class="sxs-lookup"><span data-stu-id="b5058-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="b5058-123">請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="b5058-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="b5058-124">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="b5058-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="b5058-125">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="b5058-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="b5058-126">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="b5058-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="b5058-127">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b5058-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b5058-128">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b5058-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="b5058-129">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b5058-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="b5058-130">[保護您的 IoT 解決方案從接地 hello][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="b5058-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
