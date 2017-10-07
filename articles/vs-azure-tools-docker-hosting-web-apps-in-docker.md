---
title: "aaaDeploy ASP.NET Core Linux Docker 容器 tooa 遠端 Docker 主機 |Microsoft 文件"
description: "了解如何 toouse Visual Studio Tools for Docker toodeploy ASP.NET Core web 應用程式 tooa Docker 容器，Azure Docker 主機 Linux VM 上執行"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>部署 ASP.NET 容器 tooa 遠端 Docker 主機
## <a name="overview"></a>概觀
Docker 是輕量級容器引擎，某些方式 tooa 虛擬機器，您可以在類似使用 toohost 應用程式和服務。
本教學課程將引導您完成使用 hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker)延伸 toodeploy 使用 PowerShell 在 Azure 上的 ASP.NET Core 應用程式 tooa Docker 主機。

## <a name="prerequisites"></a>必要條件
hello 下列是必要的 toocomplete 本教學課程：

* 中所述，建立 Azure Docker 主機 VM[如何 toouse docker 電腦與 Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* 安裝新版的 hello [Visual Studio](https://www.visualstudio.com/downloads/)
* 下載 hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)
* 安裝 [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1.建立 ASP.NET 核心 Web 應用程式
hello 下列步驟會引導您建立將用於本教學課程中的基本 ASP.NET Core 應用程式。

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2.新增 Docker 支援
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3.使用 hello DockerTask.ps1 PowerShell 指令碼
1. 開啟 PowerShell 提示 toohello 根目錄，您的專案。 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. 驗證 hello 遠端主機正在執行。 您應該會看到狀態 = 執行中 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. 組建 hello 應用程式使用 hello-組建參數
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. 執行 hello 應用程式，使用 hello-執行參數
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Docker 完成之後，您應該會看到類似 toohello 下列結果：
   
   ![檢視您的應用程式][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
