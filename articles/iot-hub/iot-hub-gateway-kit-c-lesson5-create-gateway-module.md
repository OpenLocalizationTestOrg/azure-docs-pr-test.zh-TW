---
title: "建立您的第一個 Azure IoT 閘道器模組 | Microsoft Docs"
description: "建立模組，並將它新增至範例應用程式以自訂模組行為。"
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="d24fd-103">第 5 課：建立您的第一個 Azure IoT 閘道器模組</span><span class="sxs-lookup"><span data-stu-id="d24fd-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="d24fd-104">雖然 Azure IoT Edge 可讓您建置以 Java、.NET 或 Node.js 撰寫的模組，但本教學課程會逐步引導您完成以 C 建置模組的步驟。</span><span class="sxs-lookup"><span data-stu-id="d24fd-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d24fd-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="d24fd-105">What you will do</span></span>

- <span data-ttu-id="d24fd-106">在 Intel NUC 上編譯和執行 hello_world 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d24fd-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="d24fd-107">建立模組，並在 Intel NUC 上編譯。</span><span class="sxs-lookup"><span data-stu-id="d24fd-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="d24fd-108">將新的模組新增至 hello_world 範例應用程式，然後在 Intel NUC 上執行範例。</span><span class="sxs-lookup"><span data-stu-id="d24fd-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="d24fd-109">新的模組會印出 "hello_world" 訊息加上時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d24fd-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d24fd-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="d24fd-110">What you will learn</span></span>

- <span data-ttu-id="d24fd-111">如何在 Intel NUC 上編譯和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d24fd-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="d24fd-112">如何建立模組。</span><span class="sxs-lookup"><span data-stu-id="d24fd-112">How to create a module.</span></span>
- <span data-ttu-id="d24fd-113">如何將模組新增至範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d24fd-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d24fd-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="d24fd-114">What you need</span></span>

<span data-ttu-id="d24fd-115">已安裝在主機電腦上的 Azure IoT Edge。</span><span class="sxs-lookup"><span data-stu-id="d24fd-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="d24fd-116">資料夾結構</span><span class="sxs-lookup"><span data-stu-id="d24fd-116">Folder structure</span></span>

<span data-ttu-id="d24fd-117">您在第 1 課複製的範例程式碼的第 5 課子資料夾中，有一個 `module` 資料夾和 `sample` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d24fd-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="d24fd-119">`module/my_module` 資料夾包含用來建置模組的原始程式碼和指令碼。</span><span class="sxs-lookup"><span data-stu-id="d24fd-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="d24fd-120">`sample` 資料夾包含用來建置範例應用程式的原始程式碼和指令碼。</span><span class="sxs-lookup"><span data-stu-id="d24fd-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="d24fd-121">在 Intel NUC 上編譯和執行 hello_world 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="d24fd-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="d24fd-122">`hello_world` 範例會根據 `hello_world.json` 檔案建立閘道，此檔案中指定應用程式相關聯的兩個預先定義模組。</span><span class="sxs-lookup"><span data-stu-id="d24fd-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="d24fd-123">閘道器每隔 5 秒會將 "hello world" 訊息記錄至檔案。</span><span class="sxs-lookup"><span data-stu-id="d24fd-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="d24fd-124">本節中，您以預設模組編譯和執行 `hello_world` 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d24fd-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="d24fd-125">若要編譯和執行 `hello_world` 應用程式，請在主機電腦上依照下列步驟進行︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="d24fd-126">執行下列命令以初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="d24fd-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="d24fd-127">以 Intel NUC 的 MAC 位址更新閘道器組態檔。</span><span class="sxs-lookup"><span data-stu-id="d24fd-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="d24fd-128">如果您已經完成[設定和執行 BLE 範例應用程式][config_ble]的課程，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="d24fd-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="d24fd-129">執行下列命令以開啟閘道器組態檔：</span><span class="sxs-lookup"><span data-stu-id="d24fd-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="d24fd-130">當您[將 Intel NUC 設定為 IoT 閘道器][setup_nuc]時，更新閘道器的 MAC 位址，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="d24fd-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="d24fd-131">執行下列命令以編譯範例原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="d24fd-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="d24fd-132">此命令會將範例原始程式碼轉送至 Intel NUC，並執行`build.sh` 來編譯它。</span><span class="sxs-lookup"><span data-stu-id="d24fd-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="d24fd-133">執行下列命令，在 Intel NUC 上執行 `hello_world` 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="d24fd-134">此命令會執行 `config.json`中所指定的 `../Tools/run-hello-world.js`，在 Intel NUC 上啟動範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d24fd-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="d24fd-136">建立新的模組，並在 Intel NUC 上編譯</span><span class="sxs-lookup"><span data-stu-id="d24fd-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="d24fd-137">下列步驟逐步引導您建立新的模組，並在 Intel NUC 上進行編譯。</span><span class="sxs-lookup"><span data-stu-id="d24fd-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="d24fd-138">此模組收到訊息時會印出這些訊息加上時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d24fd-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="d24fd-139">本節中，您將建立您的第一個自訂閘道器模組。</span><span class="sxs-lookup"><span data-stu-id="d24fd-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="d24fd-140">所有 Azure IoT Edge 模組都必須實作下列介面︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="d24fd-141">您可以選擇性地實作下列介面︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="d24fd-142">下圖顯示模組的重要狀態路徑。</span><span class="sxs-lookup"><span data-stu-id="d24fd-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="d24fd-143">正方形代表您實作的方法，可在模組移轉狀態時執行作業。</span><span class="sxs-lookup"><span data-stu-id="d24fd-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="d24fd-144">橢圓形是模組可能的主要狀態。</span><span class="sxs-lookup"><span data-stu-id="d24fd-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="d24fd-146">現在讓我們根據範本建立模組︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="d24fd-147">執行下列命令以開啟範本資料夾：</span><span class="sxs-lookup"><span data-stu-id="d24fd-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="d24fd-149">`src/my_module.c` 當作範本協助建立模組。</span><span class="sxs-lookup"><span data-stu-id="d24fd-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="d24fd-150">此範本宣告介面。</span><span class="sxs-lookup"><span data-stu-id="d24fd-150">The template declares the interfaces.</span></span> <span data-ttu-id="d24fd-151">您只需要將邏輯新增至 `MyModule_Receive` 函式即可。</span><span class="sxs-lookup"><span data-stu-id="d24fd-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="d24fd-152">`build.sh` 是組建指令碼，用於在 Intel NUC 上編譯模組。</span><span class="sxs-lookup"><span data-stu-id="d24fd-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="d24fd-153">開啟 `src/my_module.c` 檔案並加入兩個標頭檔︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="d24fd-154">將下列程式碼新增至 `MyModule_Receive` 函式：</span><span class="sxs-lookup"><span data-stu-id="d24fd-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="d24fd-155">更新 `config.json` 檔，指定您主機電腦上的 `workspace` 資料夾和 Intel NUC 上的部署路徑。</span><span class="sxs-lookup"><span data-stu-id="d24fd-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="d24fd-156">在編譯期間，`workspace` 資料夾中的檔案會轉送至部署路徑。</span><span class="sxs-lookup"><span data-stu-id="d24fd-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="d24fd-157">執行下列命令以開啟 `config.json` 檔案：</span><span class="sxs-lookup"><span data-stu-id="d24fd-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="d24fd-158">使用下列設定更新 `config.json`：</span><span class="sxs-lookup"><span data-stu-id="d24fd-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="d24fd-160">執行下列命令以編譯模組：</span><span class="sxs-lookup"><span data-stu-id="d24fd-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="d24fd-161">此命令會將原始程式碼轉送至 Intel NUC，並執行 `build.sh` 來編譯模組。</span><span class="sxs-lookup"><span data-stu-id="d24fd-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="d24fd-162">將模組新增至 hello_world 範例應用程式，然後在 Intel NUC 上執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d24fd-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="d24fd-163">若要執行這項工作，請按照下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="d24fd-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="d24fd-164">執行下列命令，以列出 Intel NUC 上所有可用的模組二進位檔 (.so 檔案)︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="d24fd-165">已編譯之 `my_module` 的二進位檔路徑應該會列出如下︰</span><span class="sxs-lookup"><span data-stu-id="d24fd-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="d24fd-166">如果您在 `config-gateway.json` 中變更預設登入使用者名稱，則二進位檔路徑的開頭為 `home/<your username>`，而不是 `root`。</span><span class="sxs-lookup"><span data-stu-id="d24fd-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="d24fd-167">將 `my_module` 新增至 `hello_world` 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="d24fd-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="d24fd-168">執行下列命令以開啟 `hello_world.json` 檔案：</span><span class="sxs-lookup"><span data-stu-id="d24fd-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="d24fd-169">將下列程式碼新增至 `modules` 區段：</span><span class="sxs-lookup"><span data-stu-id="d24fd-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="d24fd-170">`module.path` 的值應該是 `/root/gateway_sample/module/my_module/build/libmy_module.so`。</span><span class="sxs-lookup"><span data-stu-id="d24fd-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="d24fd-171">此程式碼宣告要與閘道器相關聯的 `my_module`，以及 `module.path` 中指定之模組二進位檔的位置。</span><span class="sxs-lookup"><span data-stu-id="d24fd-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="d24fd-172">將下列程式碼新增至 `links` 區段：</span><span class="sxs-lookup"><span data-stu-id="d24fd-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="d24fd-173">此程式碼指定將訊息從 `hello_world` 模組轉送至 `my_module`。</span><span class="sxs-lookup"><span data-stu-id="d24fd-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="d24fd-175">執行下列命令，以執行 `hello_world` 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="d24fd-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="d24fd-176">`--config` 參數強制使用 `hello_world.json` 檔案執行 `run-hello-world.js` 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d24fd-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="d24fd-178">恭喜！</span><span class="sxs-lookup"><span data-stu-id="d24fd-178">Congratulations.</span></span> <span data-ttu-id="d24fd-179">您現在可以看到這個新模組的行為，只是印出 "hello world" 訊息加上時間戳記，與原始 "hello_world" 模組的結果不同。</span><span class="sxs-lookup"><span data-stu-id="d24fd-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d24fd-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d24fd-180">Next Steps</span></span>

<span data-ttu-id="d24fd-181">您已建立新的模組，將它新增至 hello_world 範例，並在您的閘道器以新的模組執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d24fd-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="d24fd-182">如果您想要深入了解 Azure IoT 閘道器模組，您可以在這裡找到更多模組範例︰[https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules)。</span><span class="sxs-lookup"><span data-stu-id="d24fd-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
