---
title: "aaaTroubleshoot 使用 Application Insights 雲端服務 |Microsoft 文件"
description: "了解如何使用 Application Insights tooprocess 資料從 Azure 診斷會發出 tootroubleshoot 雲端服務。"
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>使用 Application Insights 疑難排解雲端服務
與[Azure SDK 2.8](https://azure.microsoft.com/downloads/)和 Azure 診斷擴充功能 1.5，可以傳送 Azure 診斷資料，針對您的雲端服務直接 tooApplication 深入資訊。 hello Azure 診斷所收集的記錄檔&mdash;包括應用程式記錄檔、 Windows 事件記錄檔、 ETW 記錄檔，以及效能計數器&mdash;可以傳送 tooApplication 深入資訊。 然後，您可以視覺化 hello Application Insights 入口網站 UI 中的此資訊。 然後，您可以使用 hello Application Insights SDK tooget 深入了解標準和來自您的應用程式，以及 hello 系統和來自 Azure 診斷基礎結構層級資料的記錄檔。

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>設定 Azure 診斷 toosend 資料 tooApplication Insights
請遵循這些步驟 tooset，設定您雲端服務專案 toosend Azure 診斷資料 tooApplication Insights。

1. 在 Visual Studio 方案總管 中，以滑鼠右鍵按一下角色，然後選取**屬性**tooopen hello 角色設計工具。

    ![方案總管角色屬性][1]

2. 在 hello**診斷**區段 hello 角色設計工具中，選取 hello**傳送診斷資料 tooApplication Insights**選項。

    ![角色設計工具將診斷傳送資料 tooapplication insights][2]

3. 在快顯的 hello 對話方塊中，選取您想要 toosend hello Azure 診斷資料的 hello Application Insights 資源。 hello 對話方塊可讓您從您的訂用帳戶的現有 Application Insights 資源 tooselect 或 toomanually，請指定 Application Insights 資源的檢測金鑰。 如需建立 Application Insights 資源的詳細資訊，請參閱[建立新的 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。

    ![選取 Application Insights 資源][3]

    一旦您加入 hello Application Insights 資源，該資源的 hello 檢測金鑰會儲存為 hello 名稱的服務組態設定**APPINSIGHTS_INSTRUMENTATIONKEY**。 您可以針對每個服務設定或環境變更此組態設定。 toodo 因此，選取不同的組態從 hello**服務組態**清單，並指定新的檢測金鑰，該設定。

    ![選取服務組態][4]

    hello **APPINSIGHTS_INSTRUMENTATIONKEY**的 Visual Studio tooconfigure hello 診斷延伸模組的 hello 適當 Application Insights 資源資訊發行期間會使用組態設定。 hello 組態設定會定義不同的檢測金鑰不同的服務組態的便利的方式。 Visual Studio 會轉譯該設定，並將其插入期間 hello 的 hello 診斷擴充功能公用組態發佈程序。 toosimplify hello 程序使用 PowerShell 設定 hello 診斷延伸模組，從 Visual Studio 的 hello 封裝輸出也包含 hello 公用組態 XML hello 適當 Application Insights 檢測金鑰。 hello 公用組態檔會在 hello 擴充功能 資料夾中建立，並遵循 hello 模式*Paasdiagnostics.<rolename>.pubconfig.xml。&lt;RoleName&gt;。模式*。 任何 PowerShell 為基礎的部署可以使用此模式 toomap 每個組態 tooa 角色。

4) tooconfigure Azure 診斷 toosend hello Azure 診斷代理程式 tooApplication 見解，收集所有效能計數器和錯誤層級記錄檔啟用 hello**傳送診斷資料 tooApplication Insights**選項。 

    如果您想 toofurther 設定哪些資料會傳送 tooApplication Insights，您必須手動編輯 hello *diagnostics.wadcfgx*每個角色的檔案。 請參閱[設定 Azure 診斷 toosend 資料 tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn 更多關於手動更新 hello 組態。

設定的 toosend Azure 診斷資料 tooapplication insights hello 雲端服務時，您可以部署它 tooAzure 正常，並確定已啟用 hello Azure 診斷擴充功能。 如需詳細資訊，請參閱[使用 Visual Studio 發佈雲端服務](../vs-azure-tools-publishing-a-cloud-service.md)。  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>在 Application Insights 中檢視 Azure 診斷資料
hello Azure 診斷遙測會顯示 hello Application Insights 資源設定為您的雲端服務中。

Azure 診斷記錄類型對應 tooApplication Insights 概念，以下列方式：

* 效能計數器在 Application Insights 中會顯示為自訂計量。
* Windows 事件記錄在 Application Insights 中會顯示為追蹤和自訂事件。
* 應用程式記錄、ETW 記錄和任何診斷基礎結構記錄在 Application Insights 中會顯示為追蹤。

tooview Application Insights 中的 Azure 診斷資料執行 hello 下列其中一種動作：

* 使用[計量瀏覽器](../application-insights/app-insights-metrics-explorer.md)toovisualize 任何自訂效能計數器，或不同類型的 Windows 事件記錄檔事件的計數。

    ![[計量瀏覽器] 中的自訂計量][5]

* 使用[搜尋](../application-insights/app-insights-diagnostic-search.md)toosearch 跨 hello Azure 診斷所傳送的追蹤記錄檔。 比方說，如果未處理的例外狀況造成 hello 角色 toocrash 和回收，hello 例外狀況的相關資訊就會出現在 hello*應用程式*通道*Windows 事件記錄檔*。 您可以使用搜尋 toolook 在 hello Windows 事件記錄檔錯誤，並取得 hello 例外狀況 toohelp 尋找 hello hello 問題原因的 hello 完整的堆疊追蹤。

    ![搜尋追蹤][6]

## <a name="next-steps"></a>後續步驟
* [新增 hello Application Insights SDK tooyour 雲端服務](../application-insights/app-insights-cloudservices.md)toosend 要求、 例外狀況、 相依性，以及從您的應用程式的任何自訂遙測資料。 當與 hello Azure 診斷資料，您可以取得完整的應用程式和系統中，檢視此資訊結合全都在 hello 相同 Application Insight 資源。  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
