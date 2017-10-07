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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="7dd49-103">連接您的裝置 toohello 遠端監視預先設定的解決方案 (Windows)</span><span class="sxs-lookup"><span data-stu-id="7dd49-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="7dd49-104">在 Windows 上建立 C 範例方案</span><span class="sxs-lookup"><span data-stu-id="7dd49-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="7dd49-105">hello 下列步驟顯示如何 toocreate hello 遠端監視與通訊的用戶端應用程式已預先設定的方案。</span><span class="sxs-lookup"><span data-stu-id="7dd49-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="7dd49-106">此應用程式是以 C 撰寫並在 Windows 上建置和執行。</span><span class="sxs-lookup"><span data-stu-id="7dd49-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="7dd49-107">在 Visual Studio 2015 或 Visual Studio 2017 建立入門專案，並加入 hello IoT 中樞裝置用戶端 NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="7dd49-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="7dd49-108">在 Visual Studio 中建立 C 主控台應用程式使用 Visual c + + hello **Win32 主控台應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="7dd49-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="7dd49-109">名稱 hello 專案**RMDevice**。</span><span class="sxs-lookup"><span data-stu-id="7dd49-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="7dd49-110">在 hello**應用程式設定**頁面 hello **Win32 應用程式精靈**，請確認**主控台應用程式**已選取，然後取消核取**先行編譯標頭**和**安全性開發週期 (SDL) 檢查**。</span><span class="sxs-lookup"><span data-stu-id="7dd49-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="7dd49-111">在**方案總管 中**，刪除 hello 檔 stdafx.h、 targetver.h 和 stdafx.cpp。</span><span class="sxs-lookup"><span data-stu-id="7dd49-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="7dd49-112">在**方案總管 中**，重新命名 hello 檔案 RMDevice.cpp tooRMDevice.c。</span><span class="sxs-lookup"><span data-stu-id="7dd49-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="7dd49-113">在**方案總管 中**，以滑鼠右鍵按一下 hello **RMDevice**專案，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="7dd49-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="7dd49-114">按一下**瀏覽**，然後尋找並安裝下列 NuGet 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="7dd49-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="7dd49-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="7dd49-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="7dd49-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7dd49-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="7dd49-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7dd49-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="7dd49-118">在**方案總管 中**，以滑鼠右鍵按一下 hello **RMDevice**專案，然後按一下**屬性**tooopen hello 專案的**屬性頁** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7dd49-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="7dd49-119">如需詳細資訊，請參閱[設定 Visual C++ 專案屬性 (英文)][lnk-c-project-properties]。</span><span class="sxs-lookup"><span data-stu-id="7dd49-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="7dd49-120">按一下 hello**連結器**資料夾，然後按一下 hello**輸入**屬性頁。</span><span class="sxs-lookup"><span data-stu-id="7dd49-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="7dd49-121">新增**crypt32.lib** toohello**其他相依性**屬性。</span><span class="sxs-lookup"><span data-stu-id="7dd49-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="7dd49-122">按一下**確定**然後**確定**再次 toosave hello 專案的屬性值。</span><span class="sxs-lookup"><span data-stu-id="7dd49-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="7dd49-123">新增 hello Parson JSON 文件庫 toohello **RMDevice**專案，並新增所需的 hello`#include`陳述式：</span><span class="sxs-lookup"><span data-stu-id="7dd49-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="7dd49-124">在適當資料夾中您的電腦上，複製 使用下列命令的 hello hello Parson GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="7dd49-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="7dd49-125">Hello parson.h 和 parson.c 檔案複製 hello 本機副本 hello Parson 儲存機制 tooyour **RMDevice**專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="7dd49-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="7dd49-126">在 Visual Studio 中，以滑鼠右鍵按一下 hello **RMDevice**專案中，按一下 **新增**，然後按一下**現有項目**。</span><span class="sxs-lookup"><span data-stu-id="7dd49-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="7dd49-127">在 hello**加入現有項目**對話方塊中，選取 hello parson.h 和 parson.c 檔案 hello **RMDevice**專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="7dd49-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="7dd49-128">然後按一下 **新增**tooadd 這些兩個檔案 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="7dd49-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="7dd49-129">在 Visual Studio 中，開啟 hello RMDevice.c 檔案。</span><span class="sxs-lookup"><span data-stu-id="7dd49-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="7dd49-130">取代現有的 hello`#include`陳述式，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="7dd49-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="7dd49-131">現在您可以確認您的專案具有 hello 正確的依存性建置設定。</span><span class="sxs-lookup"><span data-stu-id="7dd49-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="7dd49-132">建置並執行 hello 範例</span><span class="sxs-lookup"><span data-stu-id="7dd49-132">Build and run hello sample</span></span>

<span data-ttu-id="7dd49-133">新增程式碼 tooinvoke hello**遠端\_監視\_執行**函式，然後建置並執行 hello 裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="7dd49-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="7dd49-134">取代 hello**主要**函式，以下列程式碼 tooinvoke hello**遠端\_監視\_執行**函式：</span><span class="sxs-lookup"><span data-stu-id="7dd49-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="7dd49-135">按一下**建置**然後**建置方案**toobuild hello 裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="7dd49-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="7dd49-136">在**方案總管] 中**，以滑鼠右鍵按一下 hello **RMDevice**專案中，按一下 [**偵錯**，然後按一下**開始新執行個體**toorun hello範例。</span><span class="sxs-lookup"><span data-stu-id="7dd49-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="7dd49-137">hello 主控台會顯示訊息，因為 hello 應用程式傳送範例遙測 toohello 預先設定的解決方案、 收到 hello 方案儀表板 設定所需的屬性值並予以回應 toomethods hello 方案儀表板從叫用。</span><span class="sxs-lookup"><span data-stu-id="7dd49-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
