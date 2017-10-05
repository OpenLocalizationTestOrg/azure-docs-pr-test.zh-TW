---
title: "使用 Visual Studio 疑難排解 Windows 上的 Docker 用戶端錯誤 | Microsoft Docs"
description: "疑難排解使用 Visual Studio 在 Windows 上建立及部署 Web 應用程式到 Docker 時您會遇到的問題。"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="2eb31-103">疑難排解 Visual Studio Docker 開發</span><span class="sxs-lookup"><span data-stu-id="2eb31-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="2eb31-104">使用 Visual Studio Tools for Docker Preview 時，可能會因預覽本質而發生一些問題。</span><span class="sxs-lookup"><span data-stu-id="2eb31-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="2eb31-105">以下是一些常見問題和解決方法。</span><span class="sxs-lookup"><span data-stu-id="2eb31-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="2eb31-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="2eb31-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="2eb31-107">**Linux 容器**</span><span class="sxs-lookup"><span data-stu-id="2eb31-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="2eb31-108">偵錯 .NET Core web 或主控台應用程式時發生建置錯誤</span><span class="sxs-lookup"><span data-stu-id="2eb31-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="2eb31-109">這可能與未共用專案搭配適用於 Windows 的 Docker 所在的磁碟機有關。</span><span class="sxs-lookup"><span data-stu-id="2eb31-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="2eb31-110">您可能會收到類似下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="2eb31-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="2eb31-111">若要解決此問題︰</span><span class="sxs-lookup"><span data-stu-id="2eb31-111">To resolve this issue:</span></span>

1. <span data-ttu-id="2eb31-112">以滑鼠右鍵按一下通知區域中的 [適用於 Windows 的 Docker]，然後選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="2eb31-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="2eb31-113">選取 [共用磁碟機] 並共用專案所在的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2eb31-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="2eb31-114">**Windows 容器**</span><span class="sxs-lookup"><span data-stu-id="2eb31-114">**Windows containers**</span></span>

<span data-ttu-id="2eb31-115">下列問題特定於偵錯 Windows 容器中的 .NET Framework web 和主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2eb31-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="2eb31-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="2eb31-116">Prerequisites</span></span>

1. <span data-ttu-id="2eb31-117">必須先安裝具有 .NET Core 和 Docker 預覽工作負載的 Visual Studio 2017 RC (或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="2eb31-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="2eb31-118">Windows 10 年度更新版加上最新的 Windows Update 修補檔案。</span><span class="sxs-lookup"><span data-stu-id="2eb31-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="2eb31-119">特別是必須安裝 [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016)。</span><span class="sxs-lookup"><span data-stu-id="2eb31-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="2eb31-120">必須安裝[適用於 Windows 的 Docker](https://docs.docker.com/docker-for-windows/) (組建 1.13.0 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="2eb31-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="2eb31-121">必須選取**切換至 Windows 容器**。</span><span class="sxs-lookup"><span data-stu-id="2eb31-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="2eb31-122">在通知區域中，按一下的 [適用於 Windows 的 Docker]，然後選取 [切換至 Windows 容器]。</span><span class="sxs-lookup"><span data-stu-id="2eb31-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="2eb31-123">在機器重新啟動之後，請確定此設定會保留下來。</span><span class="sxs-lookup"><span data-stu-id="2eb31-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="2eb31-124">主控台應用程式進行偵錯時，主控台輸出不會出現在 Visual Studio 的輸出視窗</span><span class="sxs-lookup"><span data-stu-id="2eb31-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="2eb31-125">這是 Visual Studio 偵錯工具 (msvsmon.exe) 的已知問題，目前不適用於此案例。</span><span class="sxs-lookup"><span data-stu-id="2eb31-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="2eb31-126">此案例的支援的可能會包含在未來的版本中。</span><span class="sxs-lookup"><span data-stu-id="2eb31-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="2eb31-127">若要查看 Visual Studio 主控台應用程式中的輸出，請使用 **Docker︰啟動專案**，這相當於**啟動但不偵錯**。</span><span class="sxs-lookup"><span data-stu-id="2eb31-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="2eb31-128">偵錯 web 應用程式發生發行組態失敗，錯誤碼 (403) 禁止使用</span><span class="sxs-lookup"><span data-stu-id="2eb31-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="2eb31-129">若要解決此問題，請在方案中開啟 web.release.config，並標記為註解或刪除下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="2eb31-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="2eb31-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="2eb31-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="2eb31-131">**Linux 容器**</span><span class="sxs-lookup"><span data-stu-id="2eb31-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="2eb31-132">無法驗證磁碟區對應</span><span class="sxs-lookup"><span data-stu-id="2eb31-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="2eb31-133">需要磁碟區對應才能與容器中的應用程式資料夾共用應用程式的原始程式碼和二進位檔。</span><span class="sxs-lookup"><span data-stu-id="2eb31-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="2eb31-134">docker-compose.dev.debug.yml 和 docker-compose.dev.release.yml 中包含特定的磁碟區對應。</span><span class="sxs-lookup"><span data-stu-id="2eb31-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="2eb31-135">當主機電腦上的檔案變更時，容器就會在類似的資料夾結構中反映這些變更。</span><span class="sxs-lookup"><span data-stu-id="2eb31-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="2eb31-136">若要啟用磁碟區對應︰</span><span class="sxs-lookup"><span data-stu-id="2eb31-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="2eb31-137">在通知區域中按一下 [白鯨]，然後選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="2eb31-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="2eb31-138">選取 [共用的磁碟機]。</span><span class="sxs-lookup"><span data-stu-id="2eb31-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="2eb31-139">選取裝載您專案的磁碟機和 %USERPROFILE% 所在的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2eb31-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="2eb31-140">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="2eb31-140">Click **Apply**.</span></span>

<span data-ttu-id="2eb31-141">若要測試磁碟區對應功能是否正常，請在共用一個或多個磁碟機之後，從 Visual Studio 內重建並選取 F5，或從命令提示字元執行下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2eb31-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="2eb31-142">此範例假設您的 [使用者] 資料夾位於已共用的磁碟機 C 上。</span><span class="sxs-lookup"><span data-stu-id="2eb31-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="2eb31-143">如果您共用的是不同磁碟機，請視需要修訂。</span><span class="sxs-lookup"><span data-stu-id="2eb31-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="2eb31-144">在 Linux 容器中執行下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2eb31-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="2eb31-145">您應該會看到「使用者/公用」資料夾中的目錄清單。</span><span class="sxs-lookup"><span data-stu-id="2eb31-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="2eb31-146">如果未顯示任何檔案，而且「/c/使用者/公用」資料夾不是空的，則未正確地設定磁碟區對應。</span><span class="sxs-lookup"><span data-stu-id="2eb31-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="2eb31-147">切換至 wormhole 目錄，以查看 `/c/Users/Public` 目錄的內容：</span><span class="sxs-lookup"><span data-stu-id="2eb31-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="2eb31-148">使用 Linux VM 時，容器檔案系統會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="2eb31-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="2eb31-149">建置："PrepareForBuild" 工作意外失敗</span><span class="sxs-lookup"><span data-stu-id="2eb31-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="2eb31-150">Microsoft.DotNet.Docker.CommandLine.ClientException︰嘗試連線時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2eb31-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="2eb31-151">請確認預設的 Docker 主機正在執行。</span><span class="sxs-lookup"><span data-stu-id="2eb31-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="2eb31-152">開啟命令提示字元並執行︰</span><span class="sxs-lookup"><span data-stu-id="2eb31-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="2eb31-153">如果此命令傳回錯誤，則請嘗試啟動 **Docker For Windows** 桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2eb31-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="2eb31-154">如果桌面應用程式正在執行，則應該可以在通知區域中看到 [白鯨]。</span><span class="sxs-lookup"><span data-stu-id="2eb31-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="2eb31-155">以滑鼠右鍵按一下 [白鯨] 並開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="2eb31-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="2eb31-156">按一下 [重設]，然後重新啟動 Docker。</span><span class="sxs-lookup"><span data-stu-id="2eb31-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="2eb31-157">嘗試選取 [新增] -> [Docker 支援] 或偵錯 (F5) 容器中的 ASP.NET 核心應用程式時出現錯誤對話方塊</span><span class="sxs-lookup"><span data-stu-id="2eb31-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="2eb31-158">先解除安裝再重新安裝擴充功能之後，Visual Studio 中的 Managed Extensibility Framework (MEF) 快取會損毀。</span><span class="sxs-lookup"><span data-stu-id="2eb31-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="2eb31-159">若發生這種情況，就會導致在新增 Docker 支援和 (或) 嘗試執行或偵錯 (F5) ASP.NET 核心應用程式時出現各種錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2eb31-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="2eb31-160">暫時的解決方法是使用下列步驟來刪除和重新產生 MEF 快取。</span><span class="sxs-lookup"><span data-stu-id="2eb31-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="2eb31-161">關閉所有 Visual Studio 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2eb31-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="2eb31-162">開啟 %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\。</span><span class="sxs-lookup"><span data-stu-id="2eb31-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="2eb31-163">刪除下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="2eb31-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="2eb31-164">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2eb31-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="2eb31-165">再次嘗試案例。</span><span class="sxs-lookup"><span data-stu-id="2eb31-165">Attempt the scenario again.</span></span>
