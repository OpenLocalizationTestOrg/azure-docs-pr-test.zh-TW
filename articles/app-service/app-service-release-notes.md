---
title: "aaaAzure SDK for.net 2.5.1 版本資訊"
description: "Azure SDK for .NET 2.5.1 版本資訊"
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Azure SDK for .NET 2.5.1 版本資訊
這份文件包含.NET 2.5.1 釋放 hello hello Azure SDK 版本資訊。 

## <a name="azure-sdk-for-net-251-release-notes"></a>Azure SDK for .NET 2.5.1 版本資訊
hello 以下是新功能和更新 hello Azure SDK for.net 2.5.1 中。

* 太相關的新功能 \**Web Tools Extensions**。 
  
  * Azure 網站已重新命名的 tooAzure 應用程式服務。 如需詳細資訊，請參閱 [Azure 應用程式服務與現有的 Azure 服務](../app-service-web/app-service-changes-existing-services.md)。
  * Azure API 應用程式 （預覽） 支援已加入，以便客戶可以發行應用程式開發介面應用程式，為 ASP.NET 專案，然後使用 新增 hello > C# 專案 toogenerate 程式碼中的 hello hello 結構為基礎的 Azure API 應用程式用戶端手勢部署 API 應用程式。 
  * 在伺服器總管 中的 hello 網站節點已被取代，就不需 hello Azure App Service 節點，其中包含資源群組為基礎的 Azure API 應用程式、 行動應用程式和 Web 應用程式群組的支援。
  * Azure 行動應用程式 （預覽） 支援已加入，以便客戶可以建立新的行動應用程式專案，將行動應用程式的控制站新增、 發佈 hello 專案和遠端偵錯應用程式。
  * 新增 > Azure API 應用程式用戶端手勢現在支援本機 Swagger JSON 檔案，讓 Web 應用程式開發介面開發人員可以使用第三方 NuGets 像 Swashbuckle toogenerate Swagger 或手動撰寫它。 如此一來，用戶端開發人員可以使用 hello 程式碼產生功能 tooconsume 任何 Swagger 端點在 C# 專案中。 
  * Web 應用程式及 API 應用程式發行對話方塊已增強的 toosupport hello Azure 入口網站概念資源群組，以及選取項目/建立 Azure 資源群組和應用程式服務方案會表示 hello 新 Web 應用程式及 API 應用程式佈建 對話方塊中。 
  * Azure API 應用程式伺服器總管 節點會提供連結 toohello hello Azure 入口網站，以及其他功能，例如記錄檔資料流和遠端偵錯的應用程式開發介面應用程式深層連結。
    
    若想了解 Azure SDK .NET 2.5.1 中的已知問題和目前的限制，請參閱下方的 [此](app-service-release-notes.md#known_issues_2_5_1) 節。
* 太相關的新功能 \**HDInsight Tools**在 Visual Studio 才會啟用在此版本中。 
  
  * hive 指令碼的本機驗證。 如果您的指令碼中有任何錯誤，請按一下 [在 hello 工具列 toosee hello 驗證指令碼] 按鈕。 
  * 改善了 Hive 工作的偵錯功能。 您現在可以藉由在 Visual Studio 中存取 Yarn 記錄檔，對 Hive 工作進行偵錯。 如果您的應用程式有效能問題，調查 YARN 記錄檔將會提供有用的資訊。
  * (公用預覽) 為 Hive 提供關鍵字自動完成和 IntelliSense 支援。 您撰寫的 Hive 指令碼，HDInsight Tools for Visual Studio toohelp 加入關鍵字自動完成和 Hive 的 IntelliSense 支援。
  * Storm 支援。 您現在可以使用 HDInsight Tools for Visual Studio toodevelop Storm 拓撲/Spouts/發射 C# 中。 然後您就可以提交 hello 開發拓撲 tooa Storm 叢集並查看 hello spout/拓撲/閃電狀態。 您可以使用系統記錄檔和客戶記錄 tootroubleshoot 您 Storm 為拓撲/發射/Spouts。 您也可以在 Storm on HDInsight 中使用現有的 JAVA 資產。
    
    如需詳細資訊，請參閱 [開始使用 HDInsight Hadoop Tools for Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md)。

## <a id="known_issues_2_5_1"></a>Azure SDK for.NET 2.5.1 的已知問題和限制
* Azure API 應用程式會顯示為行動應用程式的部署目標。 Web 應用程式後續在發行之前應該 hello 行動應用程式的唯一目的。 
* 佈建的 azure API 應用程式可能會導致成功但間歇性失敗 tooupdate hello 進度 hello Azure 應用程式服務活動視窗中。 因應措施是 toocheck 狀態 hello 新 Azure API 應用程式的 hello Azure 入口網站中。 
* 在使用 [檔案] > [新增專案] > [API 應用程式] > [F5] 時，會因為沒有 default/index.html 會產生 HTTP 錯誤。 因應措施是 toomanually 瀏覽 toohello/api/值的 URL。 
* 伺服器總管圖示偶爾會呈現扁平狀。 重新啟動 VS 可解決這個問題。 
* 如果 Web 應用程式或應用程式開發介面應用程式佈建 （例如超過的配額錯誤或重複的 Azure API 應用程式閘道名稱） 期間擲回例外狀況，hello 錯誤會顯示某些未經處理的 JSON 文字。 
* 在建立專案期間查看 Application Insights 時，偶爾會發生專案建立問題。
* 有時候，產生的 hello Azure API 應用程式用戶端程式碼缺少命名空間，就必須手動包含 toobe （或透過 Visual Studio 提示自動匯入） 的程式碼 toocompile。 
* 行動裝置應用程式專案應該要已發佈的 tooweb 應用程式，但您必須選取您建立 hello Azure 入口網站中的行動裝置應用程式因為行動裝置應用程式專案需要資料庫的站台。 
* 行動應用程式的 hello 起始頁會使用 hello 詞彙而不是 「 行動應用程式 」 的 「 行動服務 」 
* Tooa 分鐘 toocreate 可能需要建立行動裝置應用程式專案。 
* 在 API 應用程式 （在某些情況下），佈建錯誤來自 hello Azure 應用程式開發介面反映，hello 權限無法設定正確，hello API 應用程式正確佈建，並可供使用時。 您可以手動設定使用 hello Azure 入口網站的權限。
* Application Insights 在 API 應用程式範本和行動應用程式範本上不受支援。
* API 應用程式專案無法與雲端服務專案搭配使用。
* API 應用程式專案範本僅適用於 C# 中。
* 在 C# 中才支援 API 應用程式透過 hello 「 加入 Azure API 應用程式用戶端 」 的操作功能表的耗用量。

