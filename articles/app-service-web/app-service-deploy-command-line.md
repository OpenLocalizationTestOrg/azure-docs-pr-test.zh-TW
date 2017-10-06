---
title: "您的 Azure 應用程式的命令列工具 aaaAutomate 部署 |Microsoft 文件"
description: "探索有關如何部署 Azure 應用程式以從命令列 hello"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>使用命令列工具來自動部署 Azure 應用程式
您可以使用命令列工具來自動部署 Azure 應用程式。 本文列出可用的工具與 hello 有用的連結，教您如何 toouse 您部署工作流程中。 

## <a name="msbuild"></a>使用 MSBuild 自動化部署
如果您使用 hello [Visual Studio IDE](#vs)進行開發，您可以使用[MSBuild](http://msbuildbook.com/) tooautomate 您可以在您的 IDE 中的任何項目。 您可以設定 MSBuild toouse 或是[Web Deploy](#webdeploy)或[FTP/FTPS](#ftp) toocopy 檔案。 Web Deploy 也可自動化其他多種部署相關工作，例如部署資料庫。

如需使用 MSBuild 命令列部署的詳細資訊，請參閱下列資源的 hello:

* [使用 Visual Studio 的 ASP.NET Web 部署：命令列部署](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment)。 一系列有關使用 Visual Studio 部署 tooAzure 教學課程中的第十個。 顯示如何 toouse hello 設定之後的命令列 toodeploy Visual Studio 中發行設定檔。
* [內部 hello Microsoft Build Engine： 使用 MSBuild 和 Team Foundation Build](http://msbuildbook.com/)。 硬碟複製活頁簿，其中包含有關章節 toouse MSBuild 部署。

## <a name="powershell"></a>使用 Windows PowerShell 自動化部署
您可以從 [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx)(英文) 執行 MSBuild 或 FTP 部署功能。 如果您這樣做，您也可以使用 Windows PowerShell cmdlet，讓 hello Azure REST 管理 API 輕鬆 toocall 的集合。

如需詳細資訊，請參閱下列資源的 hello:

* [部署 web 應用程式連結 tooa GitHub 儲存機制](app-service-web-arm-from-github-provision.md)
* [佈建 Web 應用程式與 SQL Database](app-service-web-arm-with-sql-database-provision.md)
* [透過可預測方式在 Azure 中佈建和部署微服務](app-service-deploy-complex-application-predictably.md)
* [使用 Azure 建置真實世界的雲端應用程式 - 自動化各個項目](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything)。 說明如何顯示 hello 電子書中的 hello 範例應用程式使用 Windows PowerShell 指令碼 toocreate Azure 的電子書章測試環境，並部署 tooit。 請參閱 hello[資源](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources)連結 tooadditional Azure PowerShell 文件的區段。
* [使用 Windows PowerShell 指令碼 tooPublish tooDev 和測試環境](../vs-azure-tools-publishing-using-powershell-scripts.md)。 如何 toouse Windows PowerShell 部署指令碼，Visual Studio 會產生。

## <a name="api"></a>使用 .NET 管理 API 自動化部署
您可以撰寫 C# 程式碼部署 tooperform MSBuild 或 FTP 函式。 如果您這樣做，您可以存取 hello Azure 管理 REST API tooperform 網站管理功能。

如需詳細資訊，請參閱下列資源的 hello:

* [一切自動化 hello Azure 管理程式庫和.NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。 簡介 toohello.NET 管理 API 和連結 toomore 文件。

## <a name="cli"></a>從 Azure 命令列介面 (Azure CLI) 部署
您可以使用在 Windows、 Mac 或 Linux 機器 toodeploy hello 命令列，可以使用 FTP。 如果您這樣做，您也可以存取使用 hello Azure CLI hello Azure REST 管理 API。

如需詳細資訊，請參閱下列資源的 hello:

* [Azure 命令列工具](https://azure.microsoft.com/downloads/)。 Azure.com 中提供命令列工具資訊的入口網站頁面。

## <a name="webdeploy"></a>從 Web Deploy 命令列部署
[Web 部署](http://www.iis.net/downloads/microsoft/web-deploy)是 Microsoft 軟體的部署 tooIIS 不僅提供智慧型檔案同步處理功能，但也可以執行或協調許多其他部署相關的工作無法自動化，當您使用 FTP。 例如，Web Deploy 可對您的 Web 應用程式部署新的資料庫或資料庫更新。 Web Deploy 也可以減少 hello 所需時間 tooupdate 現有的站台，因為它有智慧地將複製只變更的檔案。 Microsoft Visual Studio 和 Team Foundation Server 沒有支援 Web Deploy 內建功能，但您也可以使用 Web Deploy 直接從 hello 命令列 tooautomate 部署。 Web 部署命令是非常強大，但 hello 可能並不容易學習。

## <a name="more-resources"></a>其他資源
另一個選項 toocommand 行自動化部署是以雲端為基礎的 toouse 服務例如[綜合部署](http://en.wikipedia.org/wiki/Octopus_Deploy)。 如需詳細資訊，請參閱[部署 ASP.NET 應用程式 tooAzure 網站](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites)。

如需有關命令列工具的詳細資訊，請參閱下列資源的 hello:

* [簡單的 Web 應用程式：部署](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/)。 他所撰寫的 toomake 部落格所需的工具 David Ebbo 它更容易 toouse Web Deploy。
* [Web 部署工具](http://technet.microsoft.com/library/dd568996)。 Hello Microsoft TechNet 網站上的官方文件集。 但仍是很好的起點 toostart 張貼日期。
* [使用 Web Deploy](http://www.iis.net/learn/publish/using-web-deploy)。 Hello Microsoft IIS.NET 網站上的官方文件集。 也很好的起點 toostart 但年。
* [使用 Visual Studio 的 ASP.NET Web 部署：命令列部署](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment)。 Hello 建置引擎使用 Visual Studio 中，而它也可以用 hello 命令列 toodeploy web 應用程式 tooWeb 應用程式從 MSBuild。 這是系列中的教學課程之一，主要與 Visual Studio 部署有關。

