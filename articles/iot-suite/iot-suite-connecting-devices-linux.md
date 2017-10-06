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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="dc670-103">連接您的裝置 toohello 遠端監視預先設定的解決方案 (Linux)</span><span class="sxs-lookup"><span data-stu-id="dc670-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="dc670-104">建置並執行範例 C 用戶端 Linux</span><span class="sxs-lookup"><span data-stu-id="dc670-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="dc670-105">hello 下列步驟顯示如何 toocreate hello 遠端監視與通訊的用戶端應用程式已預先設定的方案。</span><span class="sxs-lookup"><span data-stu-id="dc670-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="dc670-106">此應用程式是以 C 撰寫並在 Ubuntu Linux 上建置和執行。</span><span class="sxs-lookup"><span data-stu-id="dc670-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="dc670-107">toocomplete 這些步驟，您需要執行 Ubuntu 15.04 或 15.10 版的裝置。</span><span class="sxs-lookup"><span data-stu-id="dc670-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="dc670-108">繼續之前，請使用下列命令的 hello 在 Ubuntu 裝置上安裝 hello 先決條件封裝：</span><span class="sxs-lookup"><span data-stu-id="dc670-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="dc670-109">在裝置上安裝 hello 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="dc670-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="dc670-110">hello Azure IoT 中樞的用戶端程式庫都可做為封裝，您可以使用 hello Ubuntu 裝置安裝**apt get**命令。</span><span class="sxs-lookup"><span data-stu-id="dc670-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="dc670-111">完成下列步驟 tooinstall hello 套件，其中包含 hello IoT 中樞的用戶端程式庫和 Ubuntu 電腦上的標頭檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc670-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="dc670-112">在命令介面中加入 hello AzureIoT 儲存機制 tooyour 電腦：</span><span class="sxs-lookup"><span data-stu-id="dc670-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="dc670-113">安裝 hello azure-iot-sdk-c-開發人員套件</span><span class="sxs-lookup"><span data-stu-id="dc670-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="dc670-114">安裝 hello Parson JSON 剖析器</span><span class="sxs-lookup"><span data-stu-id="dc670-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="dc670-115">hello IoT 中樞的用戶端程式庫使用 hello Parson JSON 剖析器 tooparse 訊息裝載。</span><span class="sxs-lookup"><span data-stu-id="dc670-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="dc670-116">在適當資料夾中您的電腦上，複製 使用下列命令的 hello hello Parson GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="dc670-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="dc670-117">準備您的專案</span><span class="sxs-lookup"><span data-stu-id="dc670-117">Prepare your project</span></span>
<span data-ttu-id="dc670-118">在 Ubuntu 電腦上，建立稱為 **remote\_monitoring** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="dc670-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="dc670-119">在 hello**遠端\_監視**資料夾：</span><span class="sxs-lookup"><span data-stu-id="dc670-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="dc670-120">四個檔案建立 hello **main.c**，**遠端\_monitoring.c**，**遠端\_monitoring.h**，和**CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="dc670-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="dc670-121">建立一個名為 **parson** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="dc670-121">Create folder called **parson**.</span></span>

<span data-ttu-id="dc670-122">複製 hello **parson.c**和**parson.h**從 hello Parson 儲存機制的本機複本到 hello**遠端\_parson 監視**資料夾。</span><span class="sxs-lookup"><span data-stu-id="dc670-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="dc670-123">在文字編輯器中，開啟 hello**遠端\_monitoring.c**檔案。</span><span class="sxs-lookup"><span data-stu-id="dc670-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="dc670-124">新增下列 hello`#include`陳述式：</span><span class="sxs-lookup"><span data-stu-id="dc670-124">Add hello following `#include` statements:</span></span>
   
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

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="dc670-125">呼叫 hello 遠端\_監視\_執行函式</span><span class="sxs-lookup"><span data-stu-id="dc670-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="dc670-126">在文字編輯器中，開啟 hello **remote_monitoring.h**檔案。</span><span class="sxs-lookup"><span data-stu-id="dc670-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="dc670-127">加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc670-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="dc670-128">在文字編輯器中，開啟 hello **main.c**檔案。</span><span class="sxs-lookup"><span data-stu-id="dc670-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="dc670-129">加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc670-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="dc670-130">建置並執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="dc670-130">Build and run hello application</span></span>
<span data-ttu-id="dc670-131">hello 下列步驟說明如何 toouse *CMake* toobuild 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc670-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="dc670-132">在文字編輯器中，開啟 hello **CMakeLists.txt**檔案在 hello **remote_monitoring**資料夾。</span><span class="sxs-lookup"><span data-stu-id="dc670-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="dc670-133">新增下列指示 toodefine 如何 hello toobuild 用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="dc670-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
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
1. <span data-ttu-id="dc670-134">在 hello **remote_monitoring**資料夾中，建立資料夾 toostore hello*進行*檔案該 CMake 產生，然後再執行 hello **cmake**和**進行**命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc670-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="dc670-135">執行 hello 用戶端應用程式，並傳送遙測 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="dc670-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

