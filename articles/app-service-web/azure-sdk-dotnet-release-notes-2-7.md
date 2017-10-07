---
title: "SDK for.NET 2.7 和.NET 2.7.1 aaaAzure 版本資訊"
description: "Azure SDK for .NET 2.7 和 .NET 2.7.1 版本資訊"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Azure SDK for .NET 2.7 和 .NET 2.7.1 版本資訊
## <a name="overview"></a>概觀
本文件包含 hello hello Azure SDK for.NET 2.7 版的版本資訊。 

針對.NET 2.7.1 釋放 hello 文件也會包含 hello hello Azure SDK 版本資訊。

只有在 Visual Studio 2015 和 Visual Studio 2013 中才支援 Azure SDK 2.7。 [Azure SDK 2.6](https://azure.microsoft.com/downloads/) hello 上次支援 SDK for Visual Studio 2012。

如需此版本的詳細資訊，請參閱 [Azure SDK 2.7 公告文章](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)和 [Azure SDK 2.7.1 公告文章](http://go.microsoft.com/fwlink/?LinkId=623850)。

## <a name="azure-sdk-for-net-27"></a>Azure SDK for .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Visual Studio 2015 的登入增強功能
Visual Studio 2015 的 azure SDK 2.7 支援 Visual Studio 2015 中的 hello 新的身分識別管理功能。  這包括支援透過角色型存取控制、雲端解決方案提供者、DreamSpark 以及其他帳戶和訂用帳戶類型存取 Azure 的帳戶。

hello 登入的增強功能隨附於 Azure SDK 2.7 才可以使用 Visual Studio 2015 中。 Visual Studio 2013 的支援則包含於 Azure SDK 2.7.1 中。

### <a name="mobile-sdk"></a>Mobile SDK
更新**行動應用程式**最新的範本 tooreflect [NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)和安裝程序。

### <a name="service-bus"></a>服務匯流排
一般錯誤修正與增強功能。 更新和功能的詳細資訊，請參閱 toohello 版本資訊的最新 hello[服務匯流排 NuGet](http://www.nuget.org/packages/WindowsAzure.ServiceBus/)。

### <a name="hdinsight-tools"></a>HDInsight 工具
在此版本 hello 進行下列更新。 這些更新目前為預覽版。 如需詳細資訊，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkId=619108)。

* 為 Hive on Tez 工作繪製 Hive 圖形
* 完整的 Hive DML IntelliSense 支援
* Pig 範本支援
* Azure 服務的 Storm 範本

#### <a name="breaking-changes"></a>重大變更
* 舊**Storm**使用這個版本的 hello 工具時，就必須升級專案。 如需詳細資訊，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkId=619108)。
* 不再支援 Visual Studio Web Express。 如需詳細資訊，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkId=619108)。

### <a name="azure-app-service-tools"></a>Azure App Service 工具
在此版本 hello 下列進行的更新 tooWeb 工具擴充功能。 如需詳細資訊，請參閱[此部落格](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)。 

* 加入對 DreamSpark 帳戶的支援
* 完整變更 tooAzure 進行 toosupport hello 新的 Azure 資源管理 Api 的工具
* Azure 應用程式服務的支援加入太[Cloud Explorer](#cloud_explorer)

#### <a name="known-issues"></a>已知問題
Web 應用程式部署位置節點不會出現在 伺服器總管 hello 位置節點下，不會在 Cloud Explorer 載入 Web 應用程式部署位置的子節點。 已解決此問題並做好 hello 下一個 SDK 版本。 

### <a name="cloud_explorer"></a>適用 Visual Studio 2015 的雲端總管
Azure SDK 2.7 包含 Cloud Explorer for Visual Studio 2015 可讓您 tooview 您的 Azure 資源，檢查其屬性，並執行 Visual Studio 中的索引鍵的開發人員動作。 

Cloud explorer 支援 hello 下列：

* Azure 資源的 [資源群組] 檢視與 [資源類型] 檢視 
* 依名稱搜尋資源 (適用於 [資源類型] 檢視)
* 支援套用角色型存取控制 (RBAC) 的訂用帳戶與資源 
* 整合式的動作 面板中顯示開發人員焦點動作特定 tooselected 資源。 例如： 附加遠端偵錯工具，針對虛擬機器使用建立 hello Resource Manager 堆疊，檢視診斷資料的虛擬機器等等。
* 整合式的 [屬性] 面板會顯示以開發人員為焦點，在開發/測試期間經常需要的屬性 
* 快速切換的 hello 帳戶 toouse 列舉的資源 （使用工具列的設定命令） 時 
* 列舉的資源 （使用工具列的設定命令） 時，訂閱 toouse 的篩選 
* 深層連結 toohello Azure 入口網站進行管理的資源與資源群組 

### <a name="azure-resource-manager-tools"></a>Azure 資源管理員工具
hello Azure 資源管理員工具已更新的 toowork 使用角色型存取控制 (RBAC) 和新的訂用帳戶類型。  包含這些變更是 hello 能力 toouse 新儲存體帳戶，除了 tooclassic 儲存體，在部署期間 toostore 成品。  

如果您使用 Azure 資源群組專案從舊版 hello SDK 以 hello SDK 2.7，新的部署指令碼是使用新的儲存體帳戶，而不傳統儲存體需要的 toodeploy。  Tooyour 專案 tooadd hello 新的指令碼進行變更之前，將會提示您。  hello 舊的指令碼將會重新命名，而且您將需要 toomanually 進行任何修改 toohello 新的指令碼。

### <a name="storage-explorer-tools"></a>儲存體總管工具
* 支援檢視附加 Blob。 如需詳細資訊，請參閱 [此部落格文章](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx)。 
* 支援透過伺服器總管檢視進階儲存體帳戶。 伺服器總管只會顯示進階儲存體帳戶的分頁 blob 會經過 hello 才支援進階儲存體帳戶的類型。

### <a name="azure-data-factory-tools-for-visual-studio"></a>Visual Studio 的 Azure Data Factory 工具
介紹適用於 Visual Studio 的 **Azure Data Factory 工具** 。 以下是啟用的 hello 功能。 如需詳細資訊，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkId=617530) 。

* **Template 基礎撰寫**： 選取使用的大小寫慣例根據的範本、 資料移動範本或資料處理範本 toodeploy 端對端資料整合解決方案，並開始實際快速使用 Data Factory。 
* **整合方案總管，方便撰寫和部署 Data Factory 實體**：建立和部署管線與相關實體做為 Visual Studio 專案。 
* **圖表檢視時撰寫視覺化與互動與整合**： 以視覺化方式撰寫的管線並協助 hello 圖表檢視的資料集。 
* **使用伺服器總管瀏覽和已部署的實體與互動的整合**： 利用 hello 伺服器總管 toobrowse 已部署的資料處理站和對應的實體。 將已部署的資料處理站或任何實體 (管線、連結的服務、資料集) 匯入您的專案。 
* **使用結構描述驗證與豐富的 IntelliSense 進行 JSON 編輯**：使用豐富的 IntelliSense 與結構描述驗證，有效率地設定和編輯 Data Factory 實體的 JSON 文件 
* **多重環境發行**： 藉由建立個別的組態檔中是否每個環境中發行撰寫的管線 toodev、 測試或生產環境。
* **支援以 Pig、Hive 和 .Net 為基礎的資料處理**：支援在 Data Factory 專案中使用 Pig 和 Hive 指令碼。 支援參考 C# 專案來管理 .Net 活動。

## <a name="azure-sdk-for-net-271"></a>Azure SDK for .NET 2.7.1
下列章節的 hello 包含引進 hello Azure SDK for.NET 2.7.1 發行的更新。

### <a name="hdinsight-tools"></a>HDInsight 工具
如需更多有關 HDInsight 工具更新的詳細說明，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkId=623831)。

* Hive 工作運算子檢視 (新功能)
  
    已加入 toohelp 您了解您的 Hive 查詢更好、 hello Hive 運算子檢視功能。 toosee 所有 hello 運算子內的頂點，都按兩下 hello 作業圖形的 hello 頂點。 tooview 更多詳細資料的特定運算子，將滑鼠停留在該運算子。
* Hive 錯誤標記 (新功能)
  
    tooenable 您 tooview hello 文法錯誤立即 hello hive 控制檔的錯誤標記功能已加入。 此外，已增強的錯誤訊息，您現在可以立即看到詳細的文法錯誤 （之前此版本中，您必須 toosubmit Hive 指令碼 toohello 叢集並等候一些時間才能取得有關錯誤訊息的詳細資料）。  
* Storm 拓撲圖表 (新功能)
  
    當您想 toosee，如果您的拓撲正常運作時，視覺化是非常重要。 在這個版本中，我們新增了適用於 Storm 圖表的視覺效果。 您可以為您的拓撲視覺化 hello 重要度量 （例如，一種色彩表示天氣特定閃電是否為 「 忙碌 」）。 您也可以按兩下 hello 閃電/Spout tooview 更多詳細資料。
* Hello Azure 入口網站 （修正） 中所建立的 HDInsight 叢集的支援
  
    您現在可以使用 Visual Studio tooview 並送出您的 HDInsight 叢集，無論 hello 叢集建立所在的工作 tooall。
* 多個 IntelliSense 支援與更快速載入 Hive 中繼資料 (一個改進功能)
  
    我們已經改善 hello IntelliSense 藉由新增更多使用者易記的建議。 例如，現在也建議在 IntelliSense 中使用資料表別名，讓您能夠更輕鬆地撰寫查詢。 此外，我們已經改善 hello Hive 中繼資料載入，讓它將只需要幾秒 toolist 所有 hello 資料庫、 資料表和您 Hive 中繼存放區的資料行。

如需更多有關 HDInsight 工具更新的詳細說明，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkId=623831)。

### <a name="improvements-in-visual-studio-2013"></a>Visual Studio 2013 的增強功能
* Azure SDK 2.7.1 可讓 Visual Studio 2013 tooaccess Azure 帳戶並透過 Role Based Access Control、 雲端方案提供者和 Dreamspark 訂用帳戶。
* Azure sdk 2.7.1，hello 新 Cloud Explorer 工具視窗現在也會提供在 Visual Studio 2013。

### <a name="known-issues"></a>已知問題
安裝 Azure SDK 2.6 hello 或 2.7.1 for Visual Studio Community 2013 在非英文版作業系統會顯示 hello 英文警告而非英文版的 Visual Studio 的資源可能不相符。 您可以安全地關閉此警告。 如果 hello 機器不能包含先前安裝的 Visual Studio Community 2013，並且您想要安裝 hello SDK 在非英文作業系統時，它只會發生。 hello 語言套件套用 hello RTM 資源 tooVisual Studio 中，但它適用於更新 4 之前，會顯示 hello 警告。 解除 hello 警告可以讓 hello 語言組件 toocontinue 和完整套用 hello Update 4 版本 hello 語言套件的內容。

LightSwitch 專案與這個版本不相容。 將以 hello 下一個 SDK 版本中解決這個問題。

## <a name="also-see"></a>另請參閱
[Azure SDK 2.7.1 公告文章](http://go.microsoft.com/fwlink/?LinkId=623850)

[Azure SDK 2.7 公告文章](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[支援和 hello Azure SDK for.NET 和 Api 的停用資訊](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

