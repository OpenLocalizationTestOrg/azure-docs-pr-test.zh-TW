---
title: "aaaTroubleshooting Docker 用戶端錯誤在 Windows 上的使用 Visual Studio |Microsoft 文件"
description: "您會使用 Visual Studio toocreate 時遇到的問題進行疑難排解，並使用 Visual Studio 部署在 Windows 上的 web 應用程式 tooDocker。"
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
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="ec241-103">疑難排解 Visual Studio Docker 開發</span><span class="sxs-lookup"><span data-stu-id="ec241-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="ec241-104">當您使用 Visual Studio Tools for Docker Preview 時，您可能會由於 hello 本質之故 hello 預覽的一些問題。</span><span class="sxs-lookup"><span data-stu-id="ec241-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="ec241-105">以下是一些常見問題和解決方法。</span><span class="sxs-lookup"><span data-stu-id="ec241-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="ec241-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="ec241-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="ec241-107">**Linux 容器**</span><span class="sxs-lookup"><span data-stu-id="ec241-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="ec241-108">偵錯 .NET Core web 或主控台應用程式時發生建置錯誤</span><span class="sxs-lookup"><span data-stu-id="ec241-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="ec241-109">這可能是相關的 toonot 與 Docker for Windows 共用 hello hello 專案所在的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ec241-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="ec241-110">您可能會收到類似 hello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="ec241-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="ec241-111">tooresolve 此問題：</span><span class="sxs-lookup"><span data-stu-id="ec241-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="ec241-112">以滑鼠右鍵按一下**Docker for Windows**在 hello 通知區域，然後選取 **設定**。</span><span class="sxs-lookup"><span data-stu-id="ec241-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="ec241-113">選取**共用磁碟機**和共用 hello hello 專案所在的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ec241-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="ec241-114">**Windows 容器**</span><span class="sxs-lookup"><span data-stu-id="ec241-114">**Windows containers**</span></span>

<span data-ttu-id="ec241-115">hello 下列問題是特定 toodebugging.NET Framework web 和主控台應用程式在 Windows 容器中。</span><span class="sxs-lookup"><span data-stu-id="ec241-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="ec241-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="ec241-116">Prerequisites</span></span>

1. <span data-ttu-id="ec241-117">Visual Studio 2017 RC （或更新版本） 與 hello.NET Core，且必須安裝 Docker 預覽工作負載。</span><span class="sxs-lookup"><span data-stu-id="ec241-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="ec241-118">Windows 10 年度更新版加上最新的 Windows Update 修補檔案。</span><span class="sxs-lookup"><span data-stu-id="ec241-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="ec241-119">特別是必須安裝 [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016)。</span><span class="sxs-lookup"><span data-stu-id="ec241-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="ec241-120">必須安裝[適用於 Windows 的 Docker](https://docs.docker.com/docker-for-windows/) (組建 1.13.0 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="ec241-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="ec241-121">**切換 tooWindows 容器**必須選取。</span><span class="sxs-lookup"><span data-stu-id="ec241-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="ec241-122">在 hello 通知區域中，按一下  **Docker for Windows**，然後選取**切換 tooWindows 容器**。</span><span class="sxs-lookup"><span data-stu-id="ec241-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="ec241-123">Hello 機器重新啟動之後，請確定這個設定會保留下來。</span><span class="sxs-lookup"><span data-stu-id="ec241-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="ec241-124">主控台應用程式進行偵錯時，主控台輸出不會出現在 Visual Studio 的輸出視窗</span><span class="sxs-lookup"><span data-stu-id="ec241-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="ec241-125">這是 hello Visual Studio 偵錯工具 (msvsmon.exe)，其中目前不是此案例的已知的問題。</span><span class="sxs-lookup"><span data-stu-id="ec241-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="ec241-126">此案例的支援的可能會包含在未來的版本中。</span><span class="sxs-lookup"><span data-stu-id="ec241-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="ec241-127">從 Visual Studio 中，使用中的 hello 主控台應用程式的 toosee 輸出**Docker： 起始專案**，相當太**啟動但不偵錯**。</span><span class="sxs-lookup"><span data-stu-id="ec241-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="ec241-128">偵錯 web 應用程式以 hello 發行組態失敗，並 (403) Forbidden 錯誤</span><span class="sxs-lookup"><span data-stu-id="ec241-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="ec241-129">解決此問題，toowork hello 解決方案中開啟 web.release.config 和標記為註解或刪除 hello 下列行：</span><span class="sxs-lookup"><span data-stu-id="ec241-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="ec241-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ec241-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="ec241-131">**Linux 容器**</span><span class="sxs-lookup"><span data-stu-id="ec241-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="ec241-132">無法 toovalidate 磁碟區對應</span><span class="sxs-lookup"><span data-stu-id="ec241-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="ec241-133">磁碟區對應是應用的必要的 tooshare hello 原始程式碼和 hello hello 容器中的應用程式資料夾程式二進位檔。</span><span class="sxs-lookup"><span data-stu-id="ec241-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="ec241-134">docker-compose.dev.debug.yml 和 docker-compose.dev.release.yml 中包含特定的磁碟區對應。</span><span class="sxs-lookup"><span data-stu-id="ec241-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="ec241-135">主機電腦上的檔案已變更，hello 容器會反映這些變更的類似的資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="ec241-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="ec241-136">tooenable 磁碟區對應：</span><span class="sxs-lookup"><span data-stu-id="ec241-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="ec241-137">按一下**一定**hello 通知區域，然後選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="ec241-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="ec241-138">選取 [共用的磁碟機]。</span><span class="sxs-lookup"><span data-stu-id="ec241-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="ec241-139">選取裝載您專案和 hello 的磁碟機 %USERPROFILE%所在的 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ec241-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="ec241-140">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="ec241-140">Click **Apply**.</span></span>

<span data-ttu-id="ec241-141">tootest 若磁碟區對應運作時，重建並後一或多個磁碟機已共用，或執行命令提示字元中的下列程式碼的 hello，選取 Visual Studio 中的從 F5。</span><span class="sxs-lookup"><span data-stu-id="ec241-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="ec241-142">此範例假設您的 [使用者] 資料夾位於已共用的磁碟機 C 上。</span><span class="sxs-lookup"><span data-stu-id="ec241-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="ec241-143">如果您共用的是不同磁碟機，請視需要修訂。</span><span class="sxs-lookup"><span data-stu-id="ec241-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="ec241-144">執行下列程式碼 hello Linux 容器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ec241-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="ec241-145">您應該會看到目錄，從 hello 使用者/公用資料夾清單。</span><span class="sxs-lookup"><span data-stu-id="ec241-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="ec241-146">如果未顯示任何檔案，而且「/c/使用者/公用」資料夾不是空的，則未正確地設定磁碟區對應。</span><span class="sxs-lookup"><span data-stu-id="ec241-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="ec241-147">變更 toohello 蟲孔目錄 toosee hello 內容 hello`/c/Users/Public`目錄：</span><span class="sxs-lookup"><span data-stu-id="ec241-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="ec241-148">當您使用 Linux Vm 時，hello 容器檔案系統是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="ec241-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="ec241-149">建置："PrepareForBuild" 工作意外失敗</span><span class="sxs-lookup"><span data-stu-id="ec241-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="ec241-150">Microsoft.DotNet.Docker.CommandLine.ClientException： 發生嘗試 tooconnect 錯誤。</span><span class="sxs-lookup"><span data-stu-id="ec241-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="ec241-151">請確認該 hello 預設 Docker 主機正在執行。</span><span class="sxs-lookup"><span data-stu-id="ec241-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="ec241-152">開啟命令提示字元並執行︰</span><span class="sxs-lookup"><span data-stu-id="ec241-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="ec241-153">如果傳回錯誤，然後嘗試 toostart hello **Docker for Windows**傳統型應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec241-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="ec241-154">如果執行的 hello 桌面應用程式，然後**一定**hello 通知區域中應該可以看到。</span><span class="sxs-lookup"><span data-stu-id="ec241-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="ec241-155">以滑鼠右鍵按一下 [白鯨] 並開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="ec241-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="ec241-156">按一下 [重設]，然後重新啟動 Docker。</span><span class="sxs-lookup"><span data-stu-id="ec241-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="ec241-157">發生於嘗試 tooadd Docker 的支援是錯誤對話方塊，或 ASP.NET Core 應用程式容器中的偵錯 (F5)</span><span class="sxs-lookup"><span data-stu-id="ec241-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="ec241-158">解除安裝並安裝擴充功能之後, 可以損毀 hello Visual Studio 中的 Managed Extensibility Framework (MEF) 快取。</span><span class="sxs-lookup"><span data-stu-id="ec241-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="ec241-159">當發生這種情況時，它可以會造成不同的錯誤訊息，當您正在新增 Docker 的支援和/或嘗試 toorun 或 ASP.NET Core 應用程式偵錯 (F5)。</span><span class="sxs-lookup"><span data-stu-id="ec241-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="ec241-160">暫時的解決方法，使用下列步驟 toodelete 和重新建立 hello 的 MEF 快取的 hello。</span><span class="sxs-lookup"><span data-stu-id="ec241-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="ec241-161">關閉所有 Visual Studio 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec241-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="ec241-162">開啟 %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\。</span><span class="sxs-lookup"><span data-stu-id="ec241-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="ec241-163">刪除下列資料夾的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec241-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="ec241-164">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ec241-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="ec241-165">再次嘗試 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="ec241-165">Attempt hello scenario again.</span></span>
