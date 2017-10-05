---
title: "在 Linux 上使用 C 連接裝置| Microsoft Docs"
description: "描述如何在 Linux 上使用已寫入 C 的應用程式，將裝置連接至 Azure IoT Suite 預先設定遠端監視方案。"
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
ms.openlocfilehash: 9adbc9cc13f0b4cafa3a3a7703c46f8085b15232
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="f376b-103">將裝置連接至遠端監視預先設定方案 (Linux)</span><span class="sxs-lookup"><span data-stu-id="f376b-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="f376b-104">建置並執行範例 C 用戶端 Linux</span><span class="sxs-lookup"><span data-stu-id="f376b-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="f376b-105">下列步驟說明如何建立用戶端應用程式來與預先設定的遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f376b-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="f376b-106">此應用程式是以 C 撰寫並在 Ubuntu Linux 上建置和執行。</span><span class="sxs-lookup"><span data-stu-id="f376b-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="f376b-107">若要完成這些步驟，您需要執行 Ubuntu 版本 15.04 或 15.10 的裝置。</span><span class="sxs-lookup"><span data-stu-id="f376b-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="f376b-108">繼續之前，使用下列命令在 Ubuntu 裝置上安裝的必要條件封裝：</span><span class="sxs-lookup"><span data-stu-id="f376b-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="f376b-109">在裝置上安裝用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="f376b-109">Install the client libraries on your device</span></span>
<span data-ttu-id="f376b-110">Azure IoT 中樞用戶端程式庫可當成封裝來使用，而您可以使用 **apt get** 命令在 Ubuntu 裝置上安裝這類封裝。</span><span class="sxs-lookup"><span data-stu-id="f376b-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="f376b-111">完成下列步驟來安裝套件，其中包含 Ubuntu 電腦上的 IoT 中樞用戶端程式庫和標頭檔：</span><span class="sxs-lookup"><span data-stu-id="f376b-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="f376b-112">在殼層中，將 AzureIoT 儲存機制新增至電腦：</span><span class="sxs-lookup"><span data-stu-id="f376b-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="f376b-113">安裝 azure-iot-sdk-c-dev 封裝</span><span class="sxs-lookup"><span data-stu-id="f376b-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="f376b-114">安裝 Parson JSON 剖析器</span><span class="sxs-lookup"><span data-stu-id="f376b-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="f376b-115">IoT 中樞用戶端程式庫會使用 Parson JSON 剖析器來剖析訊息承載。</span><span class="sxs-lookup"><span data-stu-id="f376b-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="f376b-116">在您電腦上的適當資料夾中，使用下列命令複製 Parson GitHub 儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="f376b-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="f376b-117">準備您的專案</span><span class="sxs-lookup"><span data-stu-id="f376b-117">Prepare your project</span></span>
<span data-ttu-id="f376b-118">在 Ubuntu 電腦上，建立稱為 **remote\_monitoring** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f376b-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="f376b-119">在 **remote\_monitoring** 資料夾中︰</span><span class="sxs-lookup"><span data-stu-id="f376b-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="f376b-120">建立四個檔案︰**main.c**、**remote\_monitoring.c**、**remote\_monitoring.h** 和 **CMakeLists.txt**。</span><span class="sxs-lookup"><span data-stu-id="f376b-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="f376b-121">建立一個名為 **parson** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f376b-121">Create folder called **parson**.</span></span>

<span data-ttu-id="f376b-122">將 **parson.c** 和 **parson.h** 檔案從 Parson 儲存機制的本機複本複製到 **remote\_monitoring/parson** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f376b-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="f376b-123">在文字編輯器中，開啟 **remote\_monitoring.c** 檔案。</span><span class="sxs-lookup"><span data-stu-id="f376b-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="f376b-124">新增下列 `#include` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="f376b-124">Add the following `#include` statements:</span></span>
   
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

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="f376b-125">呼叫 remote\_monitoring\_run 函式</span><span class="sxs-lookup"><span data-stu-id="f376b-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="f376b-126">在文字編輯器中，開啟 **remote_monitoring.h** 檔案。</span><span class="sxs-lookup"><span data-stu-id="f376b-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="f376b-127">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f376b-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="f376b-128">在文字編輯器中，開啟 **main.c** 檔案。</span><span class="sxs-lookup"><span data-stu-id="f376b-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="f376b-129">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f376b-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="f376b-130">建置並執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f376b-130">Build and run the application</span></span>
<span data-ttu-id="f376b-131">下列步驟說明如何使用 *CMake* 建置用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f376b-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="f376b-132">在文字編輯器中，開啟 **remote_monitoring** 資料夾中的 **CMakeLists.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="f376b-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="f376b-133">新增下列指示來定義如何建置用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="f376b-133">Add the following instructions to define how to build your client application:</span></span>
   
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
1. <span data-ttu-id="f376b-134">在 **remote_monitoring** 資料夾中，建立資料夾來儲存 CMake 產生的 *make* 檔案，然後執行 **cmake** 和 **make** 命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f376b-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="f376b-135">執行用戶端應用程式，並將遙測傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="f376b-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

