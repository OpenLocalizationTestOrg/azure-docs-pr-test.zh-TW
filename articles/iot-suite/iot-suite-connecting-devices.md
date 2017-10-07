---
title: "一部裝置的 Windows 上使用 C aaaConnect |Microsoft 文件"
description: "描述如何 tooconnect 裝置 toohello Azure IoT 套件預先設定的遠端使用 Windows 上執行的 C 撰寫的應用程式的監視解決方案。"
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>連接您的裝置 toohello 遠端監視預先設定的解決方案 (Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>在 Windows 上建立 C 範例方案
hello 下列步驟顯示如何 toocreate hello 遠端監視與通訊的用戶端應用程式已預先設定的方案。 此應用程式是以 C 撰寫並在 Windows 上建置和執行。

在 Visual Studio 2015 或 Visual Studio 2017 建立入門專案，並加入 hello IoT 中樞裝置用戶端 NuGet 封裝：

1. 在 Visual Studio 中建立 C 主控台應用程式使用 Visual c + + hello **Win32 主控台應用程式**範本。 名稱 hello 專案**RMDevice**。
2. 在 hello**應用程式設定**頁面 hello **Win32 應用程式精靈**，請確認**主控台應用程式**已選取，然後取消核取**先行編譯標頭**和**安全性開發週期 (SDL) 檢查**。
3. 在**方案總管 中**，刪除 hello 檔 stdafx.h、 targetver.h 和 stdafx.cpp。
4. 在**方案總管 中**，重新命名 hello 檔案 RMDevice.cpp tooRMDevice.c。
5. 在**方案總管 中**，以滑鼠右鍵按一下 hello **RMDevice**專案，然後按一下**管理 NuGet 封裝**。 按一下**瀏覽**，然後尋找並安裝下列 NuGet 套件 hello:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. 在**方案總管 中**，以滑鼠右鍵按一下 hello **RMDevice**專案，然後按一下**屬性**tooopen hello 專案的**屬性頁** 對話方塊。 如需詳細資訊，請參閱[設定 Visual C++ 專案屬性 (英文)][lnk-c-project-properties]。 
7. 按一下 hello**連結器**資料夾，然後按一下 hello**輸入**屬性頁。
8. 新增**crypt32.lib** toohello**其他相依性**屬性。 按一下**確定**然後**確定**再次 toosave hello 專案的屬性值。

新增 hello Parson JSON 文件庫 toohello **RMDevice**專案，並新增所需的 hello`#include`陳述式：

1. 在適當資料夾中您的電腦上，複製 使用下列命令的 hello hello Parson GitHub 儲存機制：

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Hello parson.h 和 parson.c 檔案複製 hello 本機副本 hello Parson 儲存機制 tooyour **RMDevice**專案資料夾。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello **RMDevice**專案中，按一下 **新增**，然後按一下**現有項目**。

1. 在 hello**加入現有項目**對話方塊中，選取 hello parson.h 和 parson.c 檔案 hello **RMDevice**專案資料夾。 然後按一下 **新增**tooadd 這些兩個檔案 tooyour 專案。

1. 在 Visual Studio 中，開啟 hello RMDevice.c 檔案。 取代現有的 hello`#include`陳述式，以下列程式碼的 hello:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > 現在您可以確認您的專案具有 hello 正確的依存性建置設定。

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>建置並執行 hello 範例

新增程式碼 tooinvoke hello**遠端\_監視\_執行**函式，然後建置並執行 hello 裝置應用程式。

1. 取代 hello**主要**函式，以下列程式碼 tooinvoke hello**遠端\_監視\_執行**函式：
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. 按一下**建置**然後**建置方案**toobuild hello 裝置應用程式。

1. 在**方案總管] 中**，以滑鼠右鍵按一下 hello **RMDevice**專案中，按一下 [**偵錯**，然後按一下**開始新執行個體**toorun hello範例。 hello 主控台會顯示訊息，因為 hello 應用程式傳送範例遙測 toohello 預先設定的解決方案、 收到 hello 方案儀表板 設定所需的屬性值並予以回應 toomethods hello 方案儀表板從叫用。

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
