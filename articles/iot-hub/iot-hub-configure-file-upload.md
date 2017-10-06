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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>設定使用 hello Azure 入口網站的 IoT 中樞檔案上傳

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>檔案上傳

toouse hello[檔案上傳功能在 IoT 中樞][lnk-upload]，您必須先使 Azure 儲存體帳戶與您的中樞。 選取**檔案上傳**toodisplay hello IoT 中樞正在修改的檔案上傳內容的清單。

![檢視 IoT 中樞檔案上傳 hello 入口網站中設定][13]

**儲存體容器**： 使用 Azure 入口網站 tooselect hello 您目前的 Azure 訂用帳戶 tooassociate 與 IoT 中樞中的 Azure 儲存體帳戶中的 blob 容器。 如果有必要，您可以建立 Azure 儲存體帳戶上 hello**儲存體帳戶**刀鋒視窗和 blob 容器上 hello**容器**刀鋒視窗。 上傳檔案時 IoT 中心會自動與寫入權限 toothis blob 容器的裝置 toouse 產生 SAS Uri。

![Hello 入口網站中檢視檔案上傳的儲存體容器][14]

**接收通知的上傳的檔案**： 啟用或停用透過 hello 切換檔案上傳通知。

**SAS TTL**： 此設定為 hello 存留時間的 SAS Uri 傳回 IoT 中樞 toohello 裝置 hello。 依預設，設定 tooone 小時，但可以自訂的 tooother 值使用 hello 滑桿。

**檔案設定預設的 TTL 通知**: hello 的存留時間的檔案上傳通知到期。 依預設，設定 tooone 天，但可以自訂的 tooother 值使用 hello 滑桿。

**檔案通知最大傳遞計數**: hello 的次數 hello IoT 中樞嘗試 toodeliver 檔案上傳通知。 依預設，設定 too10，但可以自訂的 tooother 值使用 hello 滑桿。

![在 hello 入口網站中設定 IoT 中樞檔案上傳][15]

## <a name="next-steps"></a>後續步驟

IoT 中樞的 hello 檔案上傳功能的相關資訊，請參閱[從裝置的檔案上傳][ lnk-upload] hello IoT 中樞開發人員指南 》 中。

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
