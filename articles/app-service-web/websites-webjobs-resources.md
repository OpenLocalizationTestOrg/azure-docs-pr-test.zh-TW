---
title: "aaaAzure WebJobs 文件資源"
description: "建議的學習資源如何 toouse Azure WebJobs 和 hello Azure WebJobs SDK。"
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Azure WebJobs 文件資源
## <a name="overview"></a>概觀
本主題會連結 toodocumentation 資源 toouse Azure WebJobs 和 hello Azure WebJobs SDK。 Azure WebJobs 提供簡單的方式 toorun 指令碼或程式為背景處理程序中的 hello 內容[App Service web 應用程式、 應用程式開發介面應用程式或行動裝置應用程式](../app-service/app-service-value-prop-what-is.md)。 您可以上傳並執行 cmd、bat、exe (.NET)、ps1、sh、php、py、js 和 jar 這類可執行檔。 這些程式會依照排程 (cron) 或持續當作 WebJobs 執行。

hello 目的 hello [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) toosimplify hello 程式碼，您可以執行的 WebJob，例如映像處理、 佇列的處理、 RSS 彙總、 檔案維護的一般工作為撰寫，且傳送電子郵件。 hello WebJobs SDK 有內建的功能，使用 Azure 儲存體和 Service Bus、 工作排程和處理錯誤，以及許多其他常見的案例。 此外，它擁有設計 toobe 可擴充，而且沒有[擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。 [Azure 函數](../azure-functions/functions-overview.md)（目前處於預覽） 為基礎的 hello 適用於 C# 指令碼、 Node.js 和其他語言的 WebJobs SDK 版本。 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

使用 Visual Studio 中的整合工具可完美地建立、部署和管理 WebJobs。 您可以從範本建立 WebJobs、加以發佈並進行管理 (執行、停止、監視與偵錯)。 

hello Azure 入口網站中的 hello WebJobs 儀表板會提供功能強大的管理功能，可讓您完全掌控 hello 執行 WebJobs，包括 hello 能力 tooinvoke 個別函式內 WebJobs。 函式執行階段和記錄輸出，也會顯示 hello 儀表板。 

## <a name="getstarted"></a>開始使用 WebJobs 與 hello WebJobs SDK
* [簡介 tooAzure WebJobs](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Azure WebJobs 太酷了，趕快使用，不要猶豫！](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (取自 Troy Hunt 的部落格文章，英文。)
* [Azure WebJobs 功能 (英文)](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Hello WebJobs SDK 是什麼](websites-dotnet-webjobs-sdk.md)
* [Microsoft Patterns and Practices 提供的背景工作指引 (英文)](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [發表 hello 1.1.0 RTM 的 Microsoft Azure WebJobs SDK](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [開始使用 hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md)
* [如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [如何 toouse Azure blob 儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [如何 toouse Azure 資料表儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [如何 toouse Azure 服務匯流排與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)
* [Azure WebJobs SDK 快速參考 (PDF 下載)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [GitHub 中的 WebJobs 設定文件](https://github.com/projectkudu/kudu/wiki/Web-jobs)(英文)。
* 影片
  * [WebJobs 和 hello WebJobs SDK](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Channel 9 上的 Azure WebJobs 影片系列 (英文)](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Visual Studio 的 WebJobs 工具簡介 (英文)](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [WebJobs 工具和遠端偵錯 (英文)](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [透過 Pranav Rastogi 更新 Azure WebJobs - 1.1 版的擴充性](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

另請參閱下列各節 hello[部署 WebJobs](#deploy)和[測試和偵錯 Webjob](#debug)。

## <a name="deploy"></a>部署 WebJobs
* [如何使用 Visual Studio 的 Azure WebJobs tooDeploy](websites-dotnet-deploy-webjobs.md)
* [如何 toodeploy WebJobs 使用 hello Azure 入口網站](web-sites-create-web-jobs.md)
* [啟用 Azure WebJobs 的命令列或連續傳遞](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Git 部署使用 WebJobs.NET 主控台應用程式 tooAzure](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [部署 F # WebJob tooAzure](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [將自訂服務部署為 Azure WebJob (英文)](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* 影片
  * [Visual Studio 的 WebJobs 工具簡介 (英文)](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [WebJobs 工具和遠端偵錯 (英文)](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>排程 WebJob
* [hello 新增 Azure WebJob 對話方塊](websites-dotnet-deploy-webjobs.md#configure)
* [在 hello Azure 入口網站中建立排程 web 工作](web-sites-create-web-jobs.md#CreateScheduled)
* [連結的排程器工作 tooa WebJob](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [使用 cron 運算式排程 Azure WebJob (英文)](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [使用 WebJobs SDK TimerTrigger hello 排程個別 WebJob 函數](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>測試和偵錯 WebJobs
* [Visual Studio 中 Azure WebJobs 的新開發人員與偵錯功能 (英文)](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [檢視 hello WebJobs 儀表板](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Toowrite 記錄使用 hello WebJobs SDK，並在 hello 儀表板檢視](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [WebJobs 的遠端偵錯](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [是誰撰寫該 Blob？(英文)](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [裝載在 hello 雲端中的互動式程式碼](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [加入追蹤 tooAzure WebJobs](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [監視、診斷與疑難排解 Microsoft Azure 儲存體](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* 影片
  * [WebJobs 工具和遠端偵錯 (英文)](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>調整 WebJob 的規模
* [利用 Azure 網站調整 Web 應用程式規模 (英文)](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Azure App Service：架構大規模商務 Web 應用程式](https://channel9.msdn.com/Events/Build/2014/3-626)(英文)。 涵蓋調整以 WebJobs，包括 hello WebJobs SDK 的 web 應用程式。
* 影片
  * [向外擴充 WebJobs (英文)](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>其他 WebJobs 資源
* [Magnus Mårtensson 的 Azure WebJobs GA 部落格文章 (英文)](http://magnusmartensson.com/azure-webjobs-ga)
* [在 Azure 網站上執行 Powershell WebJobs (英文)](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [在 Azure 觸發的 WebJobs 完成時接獲通知 (英文)](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [WebJobs 的簡單 Web 應用程式備份保留原則 (英文)](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [第一個要求的 Azure Web 應用程式和雲端服務緩慢](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/)(英文)。 顯示如何 toouse WebJobs toosimulate hello 的 hello 標準定價層才可使用的 AlwaysOn 功能。
* [WebJobs 順利關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl)(英文)。 對於 WebJobs SDK 順利關機，請參閱 [順利關機](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)。
* [使用 Azure WebJobs & AzCopy 自動化備份](http://markjbrown.com/azure-webjobs-azcopy/)
* 影片
  * [Magnus Mårtensson 的 Azure WebJobs 影片 (英文)](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Channel 9 上的 Azure WebJobs 影片系列 (英文)](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>其他 WebJobs SDK 資源
* [WebJobs SDK 版本資訊](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [WebJobs SDK 原始程式碼](https://github.com/Azure/azure-webjobs-sdk)
* [WebJobs SDK 延伸模組的原始程式碼](https://github.com/Azure/azure-webjobs-sdk-extensions)，與[詳細的指引 toohello 擴充性模型](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。  
* [WebJobs SDK 指令碼原始程式碼](https://github.com/Azure/azure-webjobs-sdk-script/) (用於 [Azure Functions](../azure-functions/functions-overview.md))
* [: WebJob tooupload FREB 檔案 tooAzure 儲存體使用 hello WebJobs SDK](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [裝載於 Azure 外部的 Azure webjobs，以從 Azure 記錄優點 hello 裝載 webjob](http://bypassion.dk/?p=510)
* [建置 Azure WebJobs 的資料匯入工具 (英文)](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Azure Functions 概觀](../azure-functions/functions-overview.md)
* 影片
  * [Channel 9 上的 Azure WebJobs 影片系列 (英文)](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>範例 WebJob 應用程式
* [GitHub 上的 hello WebJobs 小組所提供的範例應用程式](https://github.com/azure/azure-webjobs-sdk-samples)
* [簡單的 Azure Web 應用程式使用 WebJobs 後端使用 hello WebJobs SDK](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77)。 示範如何使用已排程和事件驅動的 WebJobs。 請參閱 hello 部落格文章[重建 hello SiteMonitR 使用 Azure WebJobs SDK](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs)。

## <a name="blogs"></a>部落格
* [Azure 部落格](/blog)
* [Amit Apple 的部落格](http://blog.amitapple.com/)。 著重於 WebJobs (不 hello SDK)。
* [Magnus Mårtensson 的部落格](http://magnusmartensson.com/)

## <a name="gethelp"></a>取得使用 WebJobs 的說明
* [StackOverflow for WebJobs](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow hello WebJobs SDK](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow for Azure Functions](http://stackoverflow.com/questions/tagged/azure-functions)
* [Azure 和 ASP.NET 論壇](http://forums.asp.net/1247.aspx)
* [Azure App Service Web Apps 論壇](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Azure Web Apps 使用者心聲網站](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/)。 使用 hello 雜湊標記 #AzureWebJobs。
* [報告 WebJobs 錯誤或問題](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

