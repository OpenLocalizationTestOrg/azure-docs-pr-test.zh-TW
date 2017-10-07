---
title: "aaaWhat 是 Azure Analysis Services |Microsoft 文件"
description: "在 Azure 中取得 Analysis Services 的 hello 大的圖片。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>什麼是 Azure Analysis Services？
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services 提供企業級資料模型化 hello 雲端中。 這是完全受管理的平台即服務 (PaaS)，與 Azure 資料平台服務整合。 

使用 Analysis Services，您可以混搭和結合來自多個來源的資料、定義計量，以及在單一受信任的語意資料模型中保護您的資料。 hello 資料模型提供更方便且快速的方式使用者 toobrowse 像 Power BI、 Excel、 Reporting Services、 第三方和自訂應用程式的用戶端應用程式的資料量很大。

![資料來源](./media/analysis-services-overview/aas-overview-data-sources.png)

簽出[這段影片](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4)toolearn Azure Analysis Services 如何配合 Microsoft 的整體 BI 功能，以及如何防止 hello 雲端資料模型可以受益。

## <a name="built-on-sql-server-analysis-services"></a>建置在 SQL Server Analysis Services 上
Azure Analysis Services 與 SQL Server Analysis Services Enterprise Edition 中現有的許多優質功能相容。 Azure Analysis Services 支援表格式模型在 hello 1200 和 1400年[相容性層級](analysis-services-compat-level.md)。 磁碟分割、資料列層級安全性、雙向關聯性和轉譯都有支援。 記憶體內部和 DirectQuery 模式表示可以快速查詢大量且複雜的資料集。

表格式模型可供快速進行開發，並可高度自訂。 對於開發人員，表格式模型會包含 hello 表格式物件模型 (TOM) toodescribe 模型物件。 TOM 會公開在 JSON 中 hello [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) hello hello 透過 AMO 資料定義語言和[Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)命名空間。

## <a name="better-with-azure"></a>透過 Azure 獲得較佳效能
Azure Analysis Services 整合許多 Azure 服務，讓您 toobuild 複雜的分析解決方案。 與整合[Azure Active Directory](../active-directory/active-directory-whatis.md)提供安全、 以角色為基礎的存取 tooyour 重要資料。 整合與[Azure Data Factory](../data-factory/data-factory-introduction.md)藉由將資料載入至 hello 模型之活動的管線。 [Azure 自動化](../automation/automation-intro.md)和 [Azure Functions](../azure-functions/functions-overview.md) 可用於使用自訂程式碼之模型的輕量型協調流程。

## <a name="get-up-and-running-quickly"></a>快速啟動並執行
您可以在短短幾分鐘內，於 Azure 入口網站中[建立伺服器](analysis-services-create-server.md)。 此外，若是使用 Azure Resource Manager [範本](../azure-resource-manager/resource-manager-create-first-template.md)和 PowerShell，您可以使用宣告式範本來佈建伺服器。 在單一範本中，您可以部署多項服務以及其他 Azure 元件 (例如儲存體帳戶和 Azure Functions)。 

建立伺服器後，您可以在 Azure 入口網站中建立表格式模型。 以新 hello （預覽） [Web 設計工具功能](analysis-services-create-model-portal.md)，您可以連接 tooan Azure SQL Database、 Azure SQL 資料倉儲資料來源，或匯入 Power BI Desktop.pbix 檔案。 自動建立資料表之間的關聯性，您可以建立量值，或從您的瀏覽器中編輯 json 格式正確的 hello model.bim 檔案。

## <a name="scale-tooyour-needs"></a>標尺 tooyour 需求
Azure Analysis Services 會以開發人員、基本及標準層提供。 每一層，在計劃成本會更改相應 tooprocessing 電源、 QPUs 和記憶體大小。 當您建立伺服器時，可以選取一個層級內的計劃。 您可以變更計劃或向內 hello 相同層，或升級 tooa 更高的層，但是您無法從更高的層 tooa 較低層降級。

相應增加、相應減少或暫停您的伺服器。 使用 hello Azure 入口網站，或使用完全掌控上立即使用 PowerShell。 您只需依據使用量付費。 toolearn 進一步了解 hello 不同的計劃和層級及使用 hello 定價計算機 toodetermine hello 右計劃，請參閱[Azure Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。

## <a name="keep-your-data-close"></a>將您的資料放在鄰近區域
Azure Analysis Services 伺服器可由 hello 下列[Azure 區域](https://azure.microsoft.com/regions/):

| 美洲 | 歐洲 | 亞太地區 |
|----------|--------|--------------|
|  巴西南部<br> 加拿大中部<br> 美國東部 2<br> 美國中北部<br> 美國中南部<br> 美國中西部<br> 美國西部 | 北歐<br> 英國南部<br> 西歐 |   澳大利亞東南部<br> 日本東部<br> 東南亞<br> 印度西部  |

新的區域新增所有 hello 時間，因此這份清單可能會不完整。 在 Azure 入口網站中或使用 Azure Resource Manager 範本建立伺服器時，請選擇一個位置。 tooget hello 最佳效能，請選擇最接近的最大的使用者基底的位置。 在多個區域中的備援伺服器上部署您的模型，以確保[高可用性](analysis-services-bcdr.md)。

## <a name="migrate-your-existing-tabular-models"></a>移轉現有的表格式模型
如果您已經有現有的內部部署 SQL Server Analysis Services 模型方案，您可以移轉 tooAzure Analysis Services 沒有重大變更。 toomigrate，您可以使用 SSDT toodeploy 模型 tooyour 伺服器。 也可以在 SSMS 中使用備份和還原或 TMSL。

如果您有內部部署資料來源，您需要 tooinstall 並設定[在內部部署資料閘道](analysis-services-gateway.md)。 如果您有角色和角色成員已經設定，移轉您的角色，但您使用 SSMS 或 PowerShell 的 tooreadd 角色成員。

## <a name="connect-toopopular-data-sources"></a>連接 toopopular 資料來源
Azure Analysis Services 支援[連接 toodata 來源](analysis-services-datasource.md)在內部部署組織中與 hello 雲端中。 結合內部部署和雲端資料來源的資料，可成就混和式解決方案。 

新的表格式 1400年模型會使用 hello 現代取得資料 功能在 SSDT 中，根據 hello M 公式的查詢語言。 取得資料，您可以有更多的資料轉換和交互式功能，以及 hello 能力 toocreate 和編輯您自己的進階的 M 公式語言查詢。 比方說，對於表格式 1400 模型，您可以在 Azure Blob 儲存體中將資料檔案模型化。

## <a name="use-hello-tools-you-already-know"></a>使用您已經知道 hello 工具

![BI 開發人員工具](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) for Visual Studio
開發和部署模型，以可用的 hello [SQL Server Data Tools (SSDT) for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)。 SSDT 包含可讓您快速啟動並執行的 Analysis Services 專案範本。 SSDT 現在包含 hello 現代取得資料的資料來源查詢的功能和交互式功能 1400年的表格式模型。 如果您是熟悉使用 Power BI Desktop 和 Excel 2016 中的 取得資料，您已經知道是多麼的輕鬆 toocreate 高度自訂的資料來源查詢。

#### <a name="sql-server-management-studio"></a>Sql Server Management Studio
使用 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) 來管理伺服器及建立資料庫模型。 連線 tooyour hello 雲端中的伺服器。 Hello XMLA 查詢視窗中，從權限執行 TMSL 指令碼，並使用 TMSL 指令碼自動化工作。 快速提供新特性與功能 - 每個月更新 SSMS。

#### <a name="powershell"></a>PowerShell
伺服器資源管理工作，例如建立伺服器、 暫停或繼續伺服器作業，或變更 hello 服務層級 （層級） 會使用 Azure 資源管理員 (AzureRM) cmdlet。 管理資料庫，例如加入或移除角色成員的其他工作，處理，或執行 TMSL 指令碼使用 cmdlet hello SqlServer 模組中。 AzureRM 和 SQLServer 模組位於 hello [PowerShell 資源庫](https://www.powershellgallery.com/)。


## <a name="your-data-is-secure"></a>您的資料很安全
![資料視覺效果](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>驗證
Azure Analysis 服務的使用者驗證由 [Azure Active Directory (AAD)](../active-directory/active-directory-whatis.md) 處理。 當嘗試 toolog tooan Azure Analysis Services 資料庫中，使用者使用組織帳戶的身分識別與存取 toohello 資料庫正在 tooaccess。 這些使用者的身分識別必須是 hello Azure Analysis Services 伺服器所在 hello 預設 Azure Active Directory hello 訂用帳戶的成員。 詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。

#### <a name="data-security"></a>資料安全性
Azure Analysis Services 會利用 Azure Blob 儲存體 toopersist 儲存體及 Analysis Services 資料庫的中繼資料。 Blob 內的資料檔案是使用 Azure Blob 伺服器端加密 (SSE) 來加密。 使用直接查詢模式時，只會儲存中繼資料。 在查詢階段 hello 資料來源存取 hello 實際的資料。

#### <a name="on-premises-data-sources"></a>內部部署資料來源
安全存取 toodata 位於內部部署組織中達成方式是安裝和設定[在內部部署資料閘道](analysis-services-gateway.md)。 閘道會存取 toodata 提供直接查詢和記憶體中模式。 Azure Analysis Services 模型連接 tooan 在內部部署資料來源時，會建立查詢以及 hello 在內部部署資料來源的 hello 加密認證。 hello 閘道器雲端服務會分析 hello 查詢，並將推送 hello 要求 tooan Azure 服務匯流排。 hello 在內部部署閘道會輪詢 hello 適用於 Azure 服務匯流排擱置的要求。 hello 閘道再取得 hello 查詢、 解密 hello 認證和連接 toohello 資料來源，以便執行。 hello 結果，然後傳送嗨資料來源，回 toohello 閘道，然後針對 toohello Azure Analysis Services 資料庫。

Azure Analysis Services 由 hello [Microsoft Online Services 條款](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)和 hello [Microsoft Online Services Privacy Statement](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx)。
toolearn 進一步了解 Azure 的安全性，請參閱 hello [Microsoft 信任中心](https://www.microsoft.com/trustcenter/Security/AzureSecurity)。

## <a name="supports-hello-latest-client-tools"></a>支援 hello 最新的用戶端工具
![資料視覺效果](./media/analysis-services-overview/aas-overview-clients.png)

新式資料探索和視覺效果工具 (像是 Power BI、Excel 和第三方工具) 可讓使用者以高度互動和豐富的視覺化方式，深入了解您的模型資料。

用戶端會使用 MSOLAP、 AMO 或 ADOMD[用戶端程式庫](analysis-services-data-providers.md)tooconnect tooAnalysis 服務伺服器。 Microsoft 用戶端應用程式 (像是 Power BI Desktop 和 Excel) 會安裝這三個用戶端程式庫。 但是請記住，根據 hello 版本或更新的頻率，用戶端程式庫可能 hello Azure Analysis Services 所需的最新版本。 hello 一樣 toocustom 應用程式或其他介面，例如 AsCmd，TOM，ADOMD.NET。 這些應用程式通常需要手動安裝 hello 程式庫封裝的一部分。


## <a name="get-help"></a>取得說明

#### <a name="documentation"></a>文件
註冊簡單 tooset 而 toomanage azure Analysis Services。 您可以找到您需要 toocreate 和管理您的伺服器服務的所有 hello 資訊。 在建立資料模型 toodeploy tooyour 伺服器時，它有很多 hello 相同因為其適用於建立資料模型，您將部署 tooan 在內部部署伺服器。 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services) 有一個內容廣泛的程式庫，包含概念、程序、教學課程及參考文件。

#### <a name="videos"></a>影片
觀看 [Channel 9 上有關 Azure Analysis Services](https://channel9.msdn.com/series/Azure-Analysis-Services) 的實用影片。

#### <a name="blogs"></a>部落格
事情變化得很快。 您一律可以取得最新資訊 hello hello [Analysis Services 團隊部落格](https://blogs.msdn.microsoft.com/analysisservices/)和[Azure 部落格](https://azure.microsoft.com/blog/)。

#### <a name="community"></a>社群
Analysis Services 有活躍的使用者社群。 聯結 hello 交談上[Azure Analysis Services 論壇](https://aka.ms/azureanalysisservicesforum)。

## <a name="feedback"></a>意見反應
您有任何建議或功能要求嗎？ 在您的註解是確定 tooleave [Azure Analysis Services 的意見反應](https://aka.ms/azureanalysisservicesfeedback)。

有關於 hello 文件的建議？ 您可以新增註解使用 Livefyre 在每個發行項的 hello 底部。

## <a name="next-steps"></a>後續步驟
既然您深入了解 Azure Analysis Services，就開始 tooget 啟動。 了解如何太[建立伺服器](analysis-services-create-server.md)在 Azure 中。 當您的伺服器都已就緒，逐步執行 hello [Adventure Works 教學課程](tutorials/aas-adventure-works-tutorial.md)toolearn 如何 toocreate 完全正常運作的表格式模型並將其部署 tooyour 伺服器。
