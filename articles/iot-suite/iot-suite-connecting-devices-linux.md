---
title: "一部裝置在 Linux 上使用 C aaaConnect |Microsoft 文件"
description: "描述如何 tooconnect 裝置 toohello Azure IoT 套件預先設定的遠端使用撰寫 C 在 Linux 上執行的應用程式的監視解決方案。"
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>連接您的裝置 toohello 遠端監視預先設定的解決方案 (Linux)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>建置並執行範例 C 用戶端 Linux
hello 下列步驟顯示如何 toocreate hello 遠端監視與通訊的用戶端應用程式已預先設定的方案。 此應用程式是以 C 撰寫並在 Ubuntu Linux 上建置和執行。

toocomplete 這些步驟，您需要執行 Ubuntu 15.04 或 15.10 版的裝置。 繼續之前，請使用下列命令的 hello 在 Ubuntu 裝置上安裝 hello 先決條件封裝：

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>在裝置上安裝 hello 用戶端程式庫
hello Azure IoT 中樞的用戶端程式庫都可做為封裝，您可以使用 hello Ubuntu 裝置安裝**apt get**命令。 完成下列步驟 tooinstall hello 套件，其中包含 hello IoT 中樞的用戶端程式庫和 Ubuntu 電腦上的標頭檔的 hello:

1. 在命令介面中加入 hello AzureIoT 儲存機制 tooyour 電腦：
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. 安裝 hello azure-iot-sdk-c-開發人員套件
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>安裝 hello Parson JSON 剖析器
hello IoT 中樞的用戶端程式庫使用 hello Parson JSON 剖析器 tooparse 訊息裝載。 在適當資料夾中您的電腦上，複製 使用下列命令的 hello hello Parson GitHub 儲存機制：

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>準備您的專案
在 Ubuntu 電腦上，建立稱為 **remote\_monitoring** 的資料夾。 在 hello**遠端\_監視**資料夾：

- 四個檔案建立 hello **main.c**，**遠端\_monitoring.c**，**遠端\_monitoring.h**，和**CMakeLists.txt**.
- 建立一個名為 **parson** 的資料夾。

複製 hello **parson.c**和**parson.h**從 hello Parson 儲存機制的本機複本到 hello**遠端\_parson 監視**資料夾。

在文字編輯器中，開啟 hello**遠端\_monitoring.c**檔案。 新增下列 hello`#include`陳述式：
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a>呼叫 hello 遠端\_監視\_執行函式
在文字編輯器中，開啟 hello **remote_monitoring.h**檔案。 加入下列程式碼的 hello:

```
void remote_monitoring_run(void);
```

在文字編輯器中，開啟 hello **main.c**檔案。 加入下列程式碼的 hello:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>建置並執行 hello 應用程式
hello 下列步驟說明如何 toouse *CMake* toobuild 用戶端應用程式。

1. 在文字編輯器中，開啟 hello **CMakeLists.txt**檔案在 hello **remote_monitoring**資料夾。

1. 新增下列指示 toodefine 如何 hello toobuild 用戶端應用程式：
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. 在 hello **remote_monitoring**資料夾中，建立資料夾 toostore hello*進行*檔案該 CMake 產生，然後再執行 hello **cmake**和**進行**命令，如下所示：
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. 執行 hello 用戶端應用程式，並傳送遙測 tooIoT 中樞：
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

