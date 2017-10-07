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
# <a name="troubleshoot-visual-studio-docker-development"></a>疑難排解 Visual Studio Docker 開發

當您使用 Visual Studio Tools for Docker Preview 時，您可能會由於 hello 本質之故 hello 預覽的一些問題。
以下是一些常見問題和解決方法。  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Linux 容器**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>偵錯 .NET Core web 或主控台應用程式時發生建置錯誤  

這可能是相關的 toonot 與 Docker for Windows 共用 hello hello 專案所在的磁碟機。  您可能會收到類似 hello 下列錯誤：

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve 此問題：

1. 以滑鼠右鍵按一下**Docker for Windows**在 hello 通知區域，然後選取 **設定**。  
2. 選取**共用磁碟機**和共用 hello hello 專案所在的磁碟機。

### <a name="windows-containers"></a>**Windows 容器**

hello 下列問題是特定 toodebugging.NET Framework web 和主控台應用程式在 Windows 容器中。

#### <a name="prerequisites"></a>必要條件

1. Visual Studio 2017 RC （或更新版本） 與 hello.NET Core，且必須安裝 Docker 預覽工作負載。
2. Windows 10 年度更新版加上最新的 Windows Update 修補檔案。 特別是必須安裝 [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016)。 
3. 必須安裝[適用於 Windows 的 Docker](https://docs.docker.com/docker-for-windows/) (組建 1.13.0 或更新版本)。
4. **切換 tooWindows 容器**必須選取。 在 hello 通知區域中，按一下  **Docker for Windows**，然後選取**切換 tooWindows 容器**。 Hello 機器重新啟動之後，請確定這個設定會保留下來。

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>主控台應用程式進行偵錯時，主控台輸出不會出現在 Visual Studio 的輸出視窗

這是 hello Visual Studio 偵錯工具 (msvsmon.exe)，其中目前不是此案例的已知的問題。 此案例的支援的可能會包含在未來的版本中。 從 Visual Studio 中，使用中的 hello 主控台應用程式的 toosee 輸出**Docker： 起始專案**，相當太**啟動但不偵錯**。

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>偵錯 web 應用程式以 hello 發行組態失敗，並 (403) Forbidden 錯誤

解決此問題，toowork hello 解決方案中開啟 web.release.config 和標記為註解或刪除 hello 下列行：

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Linux 容器**

#### <a name="unable-toovalidate-volume-mapping"></a>無法 toovalidate 磁碟區對應
磁碟區對應是應用的必要的 tooshare hello 原始程式碼和 hello hello 容器中的應用程式資料夾程式二進位檔。  docker-compose.dev.debug.yml 和 docker-compose.dev.release.yml 中包含特定的磁碟區對應。 主機電腦上的檔案已變更，hello 容器會反映這些變更的類似的資料夾結構。

tooenable 磁碟區對應：

1. 按一下**一定**hello 通知區域，然後選取**設定**。
2. 選取 [共用的磁碟機]。
3. 選取裝載您專案和 hello 的磁碟機 %USERPROFILE%所在的 hello 磁碟機。
4. 按一下 [Apply (套用)] 。

tootest 若磁碟區對應運作時，重建並後一或多個磁碟機已共用，或執行命令提示字元中的下列程式碼的 hello，選取 Visual Studio 中的從 F5。

> [!NOTE]
> 此範例假設您的 [使用者] 資料夾位於已共用的磁碟機 C 上。
> 如果您共用的是不同磁碟機，請視需要修訂。

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

執行下列程式碼 hello Linux 容器中的 hello。

```
/ # ls
```

您應該會看到目錄，從 hello 使用者/公用資料夾清單。 如果未顯示任何檔案，而且「/c/使用者/公用」資料夾不是空的，則未正確地設定磁碟區對應。

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

變更 toohello 蟲孔目錄 toosee hello 內容 hello`/c/Users/Public`目錄：

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> 當您使用 Linux Vm 時，hello 容器檔案系統是區分大小寫。

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>建置："PrepareForBuild" 工作意外失敗

Microsoft.DotNet.Docker.CommandLine.ClientException： 發生嘗試 tooconnect 錯誤。

請確認該 hello 預設 Docker 主機正在執行。 開啟命令提示字元並執行︰

```
docker info
```

如果傳回錯誤，然後嘗試 toostart hello **Docker for Windows**傳統型應用程式。 如果執行的 hello 桌面應用程式，然後**一定**hello 通知區域中應該可以看到。 以滑鼠右鍵按一下 [白鯨] 並開啟 [設定]。 按一下 [重設]，然後重新啟動 Docker。

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>發生於嘗試 tooadd Docker 的支援是錯誤對話方塊，或 ASP.NET Core 應用程式容器中的偵錯 (F5)

解除安裝並安裝擴充功能之後, 可以損毀 hello Visual Studio 中的 Managed Extensibility Framework (MEF) 快取。 當發生這種情況時，它可以會造成不同的錯誤訊息，當您正在新增 Docker 的支援和/或嘗試 toorun 或 ASP.NET Core 應用程式偵錯 (F5)。 暫時的解決方法，使用下列步驟 toodelete 和重新建立 hello 的 MEF 快取的 hello。

1. 關閉所有 Visual Studio 執行個體。
1. 開啟 %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\。
1. 刪除下列資料夾的 hello:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. 開啟 Visual Studio。
1. 再次嘗試 hello 案例。
