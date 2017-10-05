---
title: "在 Windows 上使用 C 連接裝置 | Microsoft Docs"
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
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="1b7b5-103">將裝置連接至遠端監視預先設定方案 (Windows)</span><span class="sxs-lookup"><span data-stu-id="1b7b5-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="1b7b5-104">在 Windows 上建立 C 範例方案</span><span class="sxs-lookup"><span data-stu-id="1b7b5-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="1b7b5-105">下列步驟說明如何建立用戶端應用程式來與預先設定的遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="1b7b5-106">此應用程式是以 C 撰寫並在 Windows 上建置和執行。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="1b7b5-107">在 Visual Studio 2015 或 Visual Studio 2017 中建立入門專案，並新增 IoT 中樞的裝置用戶端 NuGet 套件︰</span><span class="sxs-lookup"><span data-stu-id="1b7b5-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="1b7b5-108">在 Visual Studio 中，使用 Visual C++ **Win32 主控台應用程式** 範本建立 C 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="1b7b5-109">將專案命名為 **RMDevice**。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="1b7b5-110">在 [Win32 應用程式精靈] 的 [應用程式設定] 頁面中，確定已選取 [主控台應用程式]，並取消核取 [預先編譯的標頭] 和 [安全性開發生命週期 (SDL) 檢查]。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="1b7b5-111">在 [方案總管] 中刪除檔案 stdafx.h、targetver.h 和 stdafx.cpp。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="1b7b5-112">在 [方案總管] 中將檔案 RMDevice.cpp 重新命名為 RMDevice.c。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="1b7b5-113">在 [方案總管] 中，以滑鼠右鍵按一下 [RMDevice] 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="1b7b5-114">按一下 [瀏覽]，然後搜尋並安裝下列 NuGet 套件︰</span><span class="sxs-lookup"><span data-stu-id="1b7b5-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="1b7b5-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="1b7b5-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="1b7b5-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="1b7b5-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="1b7b5-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="1b7b5-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="1b7b5-118">在 [方案總管] 中，以滑鼠右鍵按一下 [RMDevice] 專案，然後按一下 [屬性] 開啟專案的 [屬性頁] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="1b7b5-119">如需詳細資訊，請參閱[設定 Visual C++ 專案屬性 (英文)][lnk-c-project-properties]。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="1b7b5-120">按一下 [連結器]資料夾，然後按一下 [輸入] 屬性頁。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="1b7b5-121">將 **crypt32.lib** 新增至 [其他相依性] 屬性。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="1b7b5-122">按一下 [確定]，然後再按一下 [確定] 以儲存專案屬性值。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="1b7b5-123">將 Parson JSON 程式庫新增至 **RMDevice** 專案，並新增所需的 `#include` 陳述式︰</span><span class="sxs-lookup"><span data-stu-id="1b7b5-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="1b7b5-124">在您電腦上的適當資料夾中，使用下列命令複製 Parson GitHub 儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="1b7b5-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="1b7b5-125">將 Parson.h 和 parson.c 檔案從 Parson 儲存機制的本機複本複製到 **RMDevice** 專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="1b7b5-126">在 Visual Studio 中，以滑鼠右鍵按一下 **RMDevice** 專案，按一下 [新增]，然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="1b7b5-127">在 [新增現有項目] 對話方塊中，選取 **RMDevice** 專案資料夾中的 parson.h 和 parson.c 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="1b7b5-128">然後按一下 [新增]，將這兩個檔案新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="1b7b5-129">在 Visual Studio 中，開啟 RMDevice.c 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="1b7b5-130">以下列程式碼取代現有 `#include` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="1b7b5-130">Replace the existing `#include` statements with the following code:</span></span>
   
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
    > <span data-ttu-id="1b7b5-131">現在，您可以藉由建置專案來確認專案已設定正確的相依性。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="1b7b5-132">建置並執行範例</span><span class="sxs-lookup"><span data-stu-id="1b7b5-132">Build and run the sample</span></span>

<span data-ttu-id="1b7b5-133">新增程式碼來叫用 **remote\_monitoring\_run** 函式，然後建置並執行裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="1b7b5-134">將 **main** 函式取代為下列程式碼，以叫用 **remote\_monitoring\_run** 函式︰</span><span class="sxs-lookup"><span data-stu-id="1b7b5-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="1b7b5-135">依序按一下 [建置] 和 [建置方案] 以建置裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="1b7b5-136">在 [方案總管] 中，以滑鼠右鍵按一下 [RMDevice] 專案，並按一下 [偵錯]，然後按一下 [開始新執行個體] 來執行範例。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="1b7b5-137">主控台會在應用程式將範例遙測傳送至預先設定的解決方案時顯示訊息，接收在解決方案儀表板中設定的所需屬性值，以及回應從解決方案儀表板叫用的方法。</span><span class="sxs-lookup"><span data-stu-id="1b7b5-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
