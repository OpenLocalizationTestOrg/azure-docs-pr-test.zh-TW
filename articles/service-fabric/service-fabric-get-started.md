---
title: "開發環境，如 Azure microservices aaaSet |Microsoft 文件"
description: "安裝 hello 執行階段、 SDK 和工具，並建立本機開發叢集。 完成此安裝之後，您將準備 toobuild 應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>準備您的開發環境
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild 並執行[Azure Service Fabric 應用程式][ 1]在您的開發電腦上安裝 [hello 執行階段、 SDK 和工具。 您也需要 tooenable hello hello SDK 中包含的 Windows PowerShell 指令碼執行。

## <a name="prerequisites"></a>必要條件
### <a name="supported-operating-system-versions"></a>支援的作業系統版本
開發可支援下列作業系統版本的 hello:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> 根據預設，Windows 7 只包含 Windows PowerShell 2.0。 Service Fabric PowerShell Cmdlet 需要 PowerShell 3.0 或更新版本。 您可以[下載 Windows PowerShell 5.0] [ powershell5-download]從 Microsoft 下載中心 hello。
> 
> 

## <a name="install-hello-sdk-and-tools"></a>安裝 hello SDK 和工具
### <a name="toouse-visual-studio-2017"></a>Visual Studio 2017 toouse
Service Fabric 工具是在 Visual Studio 2017 hello Azure 開發和管理工作負載的一部分。 啟用此工作負載作為 Visual Studio 安裝的一部分。
此外，您需要 tooinstall hello Microsoft Azure Service Fabric SDK，使用 Web Platform Installer。

* [安裝 Microsoft Azure Service Fabric SDK hello][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 （需要 Visual Studio 2015 Update 2 或更新版本）
Visual Studio 2015，Service Fabric 工具會安裝與 hello SDK，使用 Web Platform Installer hello:

* [安裝 Microsoft Azure Service Fabric SDK hello 和工具][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>僅限 SDK 安裝
如果您只需要 hello SDK，您可以安裝此套件：
* [安裝 Microsoft Azure Service Fabric SDK hello][core-sdk]

hello 目前的版本如下：
* Service Fabric SDK 2.7.198
* Service Fabric 執行階段 5.7.198
* Service Fabric Tools for Visual Studio 2015 1.7.50721
* Visual Studio 2017 Update 2 包含 Service Fabric Tools for Visual Studio 1.6.20170504
* Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) 包含 Service Fabric Tools for Visual Studio 1.7.20170721

如需支援版本的清單，請參閱[Service Fabric 支援](service-fabric-support.md)

## <a name="enable-powershell-script-execution"></a>啟用 PowerShell 指令碼執行
Service Fabric 會使用 Windows PowerShell 指令碼，以便建立本機開發叢集，以及從 Visual Studio 部署應用程式。 根據預設，Windows 會封鎖這些指令碼的執行。 tooenable 它們，您必須修改您的 PowerShell 執行原則。 系統管理員身分開啟 PowerShell 並輸入下列命令的 hello:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>後續步驟
現在您的開發環境已完成設定，您可以開始建置和執行應用程式。

* [在 Visual Studio 中建立第一個 Service Fabric 應用程式](service-fabric-create-your-first-application-in-visual-studio.md)
* [深入了解如何 toodeploy 和管理您的本機叢集上的應用程式](service-fabric-get-started-with-a-local-cluster.md)
* [深入了解 hello 程式設計模型： 可靠的服務和 Reliable Actors](service-fabric-choose-framework.md)
* [簽出 hello Service Fabric GitHub 上的程式碼範例](https://aka.ms/servicefabricsamples)
* [使用 Service Fabric 總管將叢集視覺化](service-fabric-visualizing-your-cluster.md)
* [請遵循 hello Service Fabric 學習路徑 tooget 廣泛簡介 toohello 平台](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* 了解 [Service Fabric 支援選項](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric 活動頁面"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI 連結"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI 連結"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI 連結"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
