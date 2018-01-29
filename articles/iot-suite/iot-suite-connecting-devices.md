---
title: "以 C 將 Windows 裝置佈建到遠端監視 - Azure | Microsoft Docs"
description: "描述如何在 Windows 上使用已寫入 C 的應用程式，將裝置連接至 Azure IoT Suite 預先設定遠端監視方案。"
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
ms.date: 12/12/2017
ms.author: dobett
ms.openlocfilehash: a6453c8d84b7025f1f510db5e675cde8685c23ed
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a>將裝置連接至遠端監視預先設定方案 (Windows)

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

本教學課程會示範如何將實體裝置連線到遠端監視預先設定的解決方案。

## <a name="create-a-c-client-solution-on-windows"></a>在 Windows 上建立 C 用戶端解決方案

如同大部分在受條件約束裝置上執行的內嵌應用程式，裝置應用程式的用戶端程式碼是以 C 撰寫的。在此教學課程中，您要在執行 Windows 的電腦上建置應用程式。

### <a name="create-the-starter-project"></a>建立入門專案

在 Visual Studio 2017 中建立入門專案，並新增 IoT 中樞的裝置用戶端 NuGet 套件︰

1. 在 Visual Studio 中，使用 Visual C++ **Windows 主控台應用程式**範本建立 C 主控台應用程式。 將專案命名為 **RMDevice**。

    ![建立 Visual C++ Windows 主控台應用程式](media/iot-suite-connecting-devices/visualstudio01.png)

1. 在 [方案總管] 中，將 `stdafx.h`、`targetver.h` 和 `stdafx.cpp` 檔案刪除。

1. 在 [方案總管] 中，將 `RMDevice.cpp` 檔案重新命名為 `RMDevice.c`。

    ![顯示重新命名之 RMDevice.c 檔案的方案總管](media/iot-suite-connecting-devices/visualstudio02.png)

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [RMDevice] 專案，然後按一下 [管理 NuGet 套件]。 選擇 [瀏覽]，然後搜尋並安裝下列 NuGet 套件︰

    * Microsoft.Azure.IoTHub.Serializer
    * Microsoft.Azure.IoTHub.IoTHubClient
    * Microsoft.Azure.IoTHub.MqttTransport

    ![NuGet 套件管理員會顯示已安裝的 Microsoft.Azure.IoTHub 套件](media/iot-suite-connecting-devices/visualstudio03.png)

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [RMDevice] 專案，然後選擇 [屬性] 以開啟專案的 [屬性頁] 對話方塊。 如需詳細資訊，請參閱[設定 Visual C++ 專案屬性](https://docs.microsoft.com/cpp/ide/working-with-project-properties)。

1. 選擇 [C/C++] 資料夾，然後選擇 [先行編譯標頭檔] 屬性頁。

1. 將**先行編譯標頭檔**設定為**未使用先行編譯標頭檔**。 然後選擇 [套用]。

    ![專案屬性會顯示未使用先行編譯標頭檔的專案](media/iot-suite-connecting-devices/visualstudio04.png)

1. 選擇 [連結器]資料夾，然後選擇 [輸入] 屬性頁。

1. 將 `crypt32.lib` 新增至 **Additional Dependencies** 屬性。 若要儲存專案屬性值，請選擇 [確定]，然後再選擇一次 [確定]。

    ![專案屬性會顯示包括 crypt32.lib 的連結器](media/iot-suite-connecting-devices/visualstudio05.png)

### <a name="add-the-parson-json-library"></a>新增 Parson JSON 文件庫

將 Parson JSON 程式庫新增至 **RMDevice** 專案，並新增所需的 `#include` 陳述式︰

1. 在您電腦上的適當資料夾中，使用下列命令複製 Parson GitHub 儲存機制︰

    ```cmd
    git clone https://github.com/kgabis/parson.git
    ```

1. 將 `parson.h` 和 `parson.c` 檔案從 Parson 存放庫的本機複本複製到 **RMDevice** 專案資料夾。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 **RMDevice** 專案，選擇 [新增]，然後選擇 [現有項目]。

1. 在 [新增現有項目] 對話方塊中，選取 **RMDevice** 專案資料夾中的 `parson.h` 和 `parson.c` 檔案。 若要將這兩個檔案新增至您的專案，請選擇 [新增]。

    ![[方案總管] 會顯示 parson.h 和 parson.c 檔案](media/iot-suite-connecting-devices/visualstudio06.png)

1. 在 Visual Studio 中，開啟 `RMDevice.c` 檔案。 以下列程式碼取代現有 `#include` 陳述式：

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
    > 現在，您可以藉由建置解決方案來確認專案已設定正確的相依性。

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a>建置並執行範例

新增程式碼來叫用 **remote\_monitoring\_run** 函式，然後建置並執行裝置應用程式：

1. 若要叫用 **remote\_monitoring\_run** 函式，請將 **main** 函式取代為下列程式碼︰

    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. 依序選擇 [建置] 和 [建置方案] 以建置裝置應用程式。 忽略關於 **gmtime** 函式的警告。

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [RMDevice] 專案，並選擇 [偵錯]，然後選擇 [開始新執行個體] 來執行範例。 主控台會將訊息顯示為：

    * 應用程式會將範例遙測傳送到預先設定的解決方案。
    * 在解決方案儀表板中收到所需的屬性值。
    * 回應從解決方案儀表板叫用的方法。

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]
