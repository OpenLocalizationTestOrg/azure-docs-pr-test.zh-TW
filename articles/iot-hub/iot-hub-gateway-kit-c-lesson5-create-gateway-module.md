---
title: "aaaCreate 第一個的 Azure IoT 閘道模組 |Microsoft 文件"
description: "建立模組，並將它加入 tooa 範例應用程式 toocustomize 模組行為。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="b68e6-103">第 5 課：建立您的第一個 Azure IoT 閘道器模組</span><span class="sxs-lookup"><span data-stu-id="b68e6-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="b68e6-104">Azure IoT 邊緣可讓您撰寫的 Java、.NET 或 Node.js 的 toobuild 模組，本教學課程中引導您 hello 步驟建置 c 模組</span><span class="sxs-lookup"><span data-stu-id="b68e6-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b68e6-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b68e6-105">What you will do</span></span>

- <span data-ttu-id="b68e6-106">編譯並執行 Intel NUC 上 hello hello_world 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68e6-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="b68e6-107">建立模組，並在 Intel NUC 上編譯。</span><span class="sxs-lookup"><span data-stu-id="b68e6-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="b68e6-108">新增 hello 新模組 toohello hello_world 範例應用程式，然後執行 Intel NUC hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b68e6-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="b68e6-109">hello 新的模組會列印出"hello_world 」 訊息時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b68e6-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b68e6-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="b68e6-110">What you will learn</span></span>

- <span data-ttu-id="b68e6-111">如何 toocompile 和 Intel NUC 上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68e6-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="b68e6-112">如何 toocreate 模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-112">How toocreate a module.</span></span>
- <span data-ttu-id="b68e6-113">如何 tooadd 模組 tooa 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68e6-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b68e6-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b68e6-114">What you need</span></span>

<span data-ttu-id="b68e6-115">已安裝在主機電腦上的 Azure IoT Edge。</span><span class="sxs-lookup"><span data-stu-id="b68e6-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="b68e6-116">資料夾結構</span><span class="sxs-lookup"><span data-stu-id="b68e6-116">Folder structure</span></span>

<span data-ttu-id="b68e6-117">您在第 1 課複製 hello 範例程式碼的第 5 課 hello 子資料夾，在沒有`module`資料夾和`sample`資料夾。</span><span class="sxs-lookup"><span data-stu-id="b68e6-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="b68e6-119">hello`module/my_module`資料夾包含 hello 來源的程式碼和指令碼 toobuild hello 模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="b68e6-120">hello`sample`資料夾包含 hello 來源的程式碼和指令碼 toobuild hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68e6-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="b68e6-121">編譯及執行 Intel NUC 上 hello hello_world 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b68e6-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="b68e6-122">hello`hello_world`範例會建立閘道，根據 hello`hello_world.json`指定 hello 兩個預先定義的模組 hello 應用程式相關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="b68e6-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="b68e6-123">hello 閘道記錄檔的"hello world"訊息 tooa 檔案每隔 5 秒。</span><span class="sxs-lookup"><span data-stu-id="b68e6-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="b68e6-124">在本節中編譯並執行 hello`hello_world`應用程式使用其預設模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="b68e6-125">toocompile 和執行 hello`hello_world`應用程式中，您的主機電腦上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b68e6-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="b68e6-126">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="b68e6-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="b68e6-127">更新 hello 閘道器組態檔以 hello Intel NUC MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="b68e6-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="b68e6-128">略過此步驟，如果您已經完成 hello 課程太[設定及執行範例應用程式 b][config_ble]。</span><span class="sxs-lookup"><span data-stu-id="b68e6-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="b68e6-129">執行下列命令的 hello 開啟 hello 閘道器組態檔：</span><span class="sxs-lookup"><span data-stu-id="b68e6-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="b68e6-130">更新 hello 閘道的 MAC 位址時您[設定為 IoT 閘道 Intel NUC][setup_nuc]，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b68e6-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="b68e6-131">藉由執行下列命令的 hello 編譯 hello 範例原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="b68e6-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="b68e6-132">hello 命令會傳送 hello 範例來源的程式碼 tooIntel NUC 並執行`build.sh`toocompile 它。</span><span class="sxs-lookup"><span data-stu-id="b68e6-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="b68e6-133">執行 hello `hello_world` Intel NUC 的應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="b68e6-134">hello 命令執行`../Tools/run-hello-world.js`中指定`config.json`toostart 上 Intel NUC hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68e6-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="b68e6-136">建立新的模組，並在 Intel NUC 上編譯</span><span class="sxs-lookup"><span data-stu-id="b68e6-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="b68e6-137">hello 執行下列步驟會逐步引導您建立新的模組和 Intel NUC 上進行編譯。</span><span class="sxs-lookup"><span data-stu-id="b68e6-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="b68e6-138">hello 模組會列印出時間戳記在收到這些訊息。</span><span class="sxs-lookup"><span data-stu-id="b68e6-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="b68e6-139">本節中，您將建立您的第一個自訂閘道器模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="b68e6-140">任何 Azure IoT 邊緣模組必須實作下列介面的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="b68e6-141">您可以選擇性地實作下列介面的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="b68e6-142">hello 下列圖表顯示 hello 重要狀態路徑的模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="b68e6-143">hello 正方形矩形代表狀態之間移動 hello 模組時，實作 tooperform 作業的方法。</span><span class="sxs-lookup"><span data-stu-id="b68e6-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="b68e6-144">hello 橢圓形是 hello 模組可以處於重大狀態。</span><span class="sxs-lookup"><span data-stu-id="b68e6-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="b68e6-146">現在讓我們來建立 hello 範本為基礎的模組：</span><span class="sxs-lookup"><span data-stu-id="b68e6-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="b68e6-147">執行下列命令的 hello 開啟 hello 範本資料夾：</span><span class="sxs-lookup"><span data-stu-id="b68e6-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="b68e6-149">`src/my_module.c`做為範本，可促進 hello 建立模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="b68e6-150">hello 範本宣告 hello 介面。</span><span class="sxs-lookup"><span data-stu-id="b68e6-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="b68e6-151">您只需要 toodo 是 tooadd 邏輯 toohello`MyModule_Receive`函式。</span><span class="sxs-lookup"><span data-stu-id="b68e6-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="b68e6-152">`build.sh`是 hello 組建指令碼 toocompile hello 模組 Intel NUC 上。</span><span class="sxs-lookup"><span data-stu-id="b68e6-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="b68e6-153">開啟 hello`src/my_module.c`檔案，並包含兩個標頭檔：</span><span class="sxs-lookup"><span data-stu-id="b68e6-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="b68e6-154">新增下列程式碼 toohello hello`MyModule_Receive`函式：</span><span class="sxs-lookup"><span data-stu-id="b68e6-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="b68e6-155">更新 hello`config.json`檔案 toospecify hello `workspace` Intel NUC 上您主機電腦和 hello 部署路徑的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b68e6-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="b68e6-156">在編譯時，hello 中 hello 檔案`workspace`資料夾將會傳送的 toohello 部署路徑。</span><span class="sxs-lookup"><span data-stu-id="b68e6-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="b68e6-157">開啟 hello`config.json`檔案執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="b68e6-158">更新`config.json`以 hello 下列組態：</span><span class="sxs-lookup"><span data-stu-id="b68e6-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="b68e6-160">藉由執行下列命令的 hello 編譯 hello 模組：</span><span class="sxs-lookup"><span data-stu-id="b68e6-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="b68e6-161">hello 命令會傳送 hello 來源的程式碼 tooIntel NUC 並執行`build.sh`toocompile hello 模組。</span><span class="sxs-lookup"><span data-stu-id="b68e6-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="b68e6-162">加入 hello 模組 toohello hello_world 範例應用程式，並在 Intel NUC 執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="b68e6-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="b68e6-163">tooperform 這項工作，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b68e6-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="b68e6-164">Intel NUC 上列出所有 hello 可用模組二進位檔 （.so 檔案），藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="b68e6-165">hello 二進位路徑`my_module`您編譯應該會列出如下：</span><span class="sxs-lookup"><span data-stu-id="b68e6-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="b68e6-166">如果您變更中的 hello 預設登入使用者名稱`config-gateway.json`，hello 二進位路徑的開頭將`home/<your username>`而不是`root`。</span><span class="sxs-lookup"><span data-stu-id="b68e6-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="b68e6-167">新增`my_module`toohello`hello_world`範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="b68e6-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="b68e6-168">開啟 hello`hello_world.json`檔案執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="b68e6-169">新增下列程式碼 toohello hello `modules` > 一節：</span><span class="sxs-lookup"><span data-stu-id="b68e6-169">Add hello following code toohello `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="b68e6-170">hello 值`module.path`應該`/root/gateway_sample/module/my_module/build/libmy_module.so`。</span><span class="sxs-lookup"><span data-stu-id="b68e6-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="b68e6-171">hello 程式碼會宣告`my_module`hello 閘道，以及 hello hello 模組二進位檔中指定的位置與相關聯的 toobe `module.path`。</span><span class="sxs-lookup"><span data-stu-id="b68e6-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="b68e6-172">新增下列程式碼 toohello hello `links` > 一節：</span><span class="sxs-lookup"><span data-stu-id="b68e6-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="b68e6-173">此程式碼會指定傳送訊息時，則從 hello`hello_world`模組太`my_module`。</span><span class="sxs-lookup"><span data-stu-id="b68e6-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="b68e6-175">執行 hello`hello_world`範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b68e6-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="b68e6-176">hello`--config`參數會強制 hello`run-hello-world.js`使用 hello 來編寫 toorun`hello_world.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="b68e6-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="b68e6-178">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b68e6-178">Congratulations.</span></span> <span data-ttu-id="b68e6-179">您現在可以看到這個新模組 hello 行為，只會列印"hello world"訊息時間戳記、 hello 原始"hello_world 」 模組從不同的結果。</span><span class="sxs-lookup"><span data-stu-id="b68e6-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b68e6-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b68e6-180">Next Steps</span></span>

<span data-ttu-id="b68e6-181">您已建立新的模組，在閘道上 toohello hello_world 範例，並取得 hello 範例與 hello 新模組的應用程式 toorun 加入。</span><span class="sxs-lookup"><span data-stu-id="b68e6-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="b68e6-182">如果您想深入了解 Azure IoT 閘道模組 toolearn，您可以找到更多的模組範例這裡： [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules)。</span><span class="sxs-lookup"><span data-stu-id="b68e6-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
