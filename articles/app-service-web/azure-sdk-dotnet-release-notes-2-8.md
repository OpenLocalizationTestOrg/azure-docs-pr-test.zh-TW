---
title: "aaaAzure SDK for.NET 2.8 版本資訊"
description: "Azure SDK for .NET 2.8 版本資訊"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Azure SDK for .NET 2.8、2.8.1 和 2.8.2
## <a name="overview"></a>概觀
這篇文章包含 hello 版本資訊 （其中包含已知的問題和重大變更） hello Azure SDK for.NET 2.8，2.8.1 和 2.8.2 釋放。 

新功能和更新在此版本中所做的完整清單，請參閱 hello [Azure SDK 2.8 的 Visual Studio 2013 和 Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)公告。 

## <a name="azure-sdk-for-net-28"></a>Azure SDK for .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>下載 Azure SDK for .NET 2.8
[Azure SDK for .NET 2.8 for Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Azure SDK for .NET 2.8 for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>.NET 4.5.2 支援
#### <a name="known-issues"></a>已知問題
Azure.NET SDK 2.8 可讓您 toocreate.NET 4.5.2 的雲端服務封裝。 不過.NET 4.5.2 hello 預設客體 OS 映像，直到年 1 月 2016 客體作業系統版本上，未安裝 framework。 在這之前，可以透過獨立的客體作業系統版本 November 2015-02 取得 .NET 4.5.2 Framework。 請參閱 hello [Azure 客體 OS 版本與 SDK 相容性比較表](../cloud-services/cloud-services-guestos-update-matrix.md)頁面 tootrack 時就會釋出 hello 映像。  一旦解除 hello 年 11 月 2015年-02 映像您可以選擇 toouse 該映像更新您的雲端服務組態檔 (.cscfg) 檔。 Hello 服務組態中設定檔的 hello ServiceConfiguration 項目 toohello 字串 hello osVersion 屬性"WA-客體-OS-4.26_201511-02"。 如果您選擇 tooopt toouse 此映像您會不會再收到自動更新 toohello 客體 OS。 tooget hello 自動更新 hello osVersion 必須設定得"*"和.NET 4.5.2 才會透過自動更新在 2016 年 1 月。

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>已知問題
期間**資料 Factory 範本**專案建立涉及範例資料，而 azure power shell 指令碼可能會失敗 hello 電腦上安裝 azure power shell 的版本為 0.9.8 之後。

為了 toosuccessfully 建立這種類型的專案，您必須安裝[azure power shell 0.9.8 版雖](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)。

### <a name="azure-resource-manager-tools"></a>Azure 資源管理員工具
#### <a name="breaking-changes"></a>重大變更
已經在 hello 新 Azure PowerShell 指令程式 1.0 版與此版本 toowork 更新 hello hello Azure 資源群組專案所提供的 PowerShell 指令碼。  這個新的指令碼不適用於從 Visual Studio 時使用的 hello SDK 先前 too2.8 版本。  

從在舊版的 hello SDK 建立的專案的指令碼時不執行從 Visual Studio 內使用 hello 2.8 SDK。  所有指令碼會繼續與 hello Azure PowerShell cmdlet hello 適當版本 Visual Studio 外部 toowork。  

hello 2.8 SDK 需要 1.0 版的 hello Azure PowerShell cmdlet。  所有其他版本的 hello SDK 需要 0.9.8 版的 hello Azure PowerShell cmdlet。  如需詳細資訊，請參閱 [此](http://go.microsoft.com/fwlink/?LinkID=623011) 部落格。

### <a name="web-tools-extensions"></a>Web 工具擴充功能
#### <a name="known-issues"></a>已知問題
hello： 發行中，就會解決下列已知的問題的 hello。

* 非生產環境 (例如 Azure China 或 Azure Stack 客戶) 的 App Service 相關雲端與伺服器總管筆勢無效。 客戶在這些受影響的區域中下載 hello 發行設定檔與 hello Azure 入口網站將會啟用發行的功能。 未來版本將為 Azure China 或 Azure Stack 客戶修復筆勢，例如「連結偵錯工具」和「檢視資料流記錄」。 
* 客戶可能會在建立時 hello App Insights 執行個體的 toowhich 它們部署為美國東部以外的區域中的應用程式服務時看到錯誤。 在這些情況下，hello 入口網站中建立應用程式服務，以及下載 hello 發行設定檔將會啟用發行的案例。 

### <a name="azure-hdinsight-tools"></a>Azure HDInsight 工具
#### <a name="new-updates"></a>新的更新
* 您可以透過 HiveServer2 幾乎沒有的額外負荷的 hello 叢集中執行 Hive 查詢，並查看記錄中的 hello 作業即時。
* 使用 hello 新 Hive 工作執行檢視可以發掘更深入，您的工作尋找詳細資訊，並識別潛在的問題。

如需詳細資訊，請參閱 [適用於 Visual Studio 2013 和 Visual Studio 2015 的 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。 

## <a name="azure-sdk-for-net-281"></a>Azure SDK for .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 和 Visual Studio 2015 的已知問題
1. 觸發的 WebJob 發行 tooslots 會顯示和錯誤，並不會設定排程，但它將推送 hello WebJob tooAzure。 需要已排程作業的客戶可以使用 hello WebJob hello Azure 入口網站 tooset hello 排程。 
2. Python 客戶可能會遭遇到偵錯工具問題。 服務小組這個時推出修正，但如果影響客戶，請讓 Microsoft 知道 hello 論壇中或 hello 公告部落格上，或釋放提示註解 > 一節。 
3. 某些區域 (如印度南部) 的客戶將遭遇 App Service 佈建錯誤。 這是與 hello 入口網站中，相同，而且會發生此問題的客戶可以使用 Azure 入口網站 toorequest 存取 toopublish toothese 地區 hello。 一旦要求存取 toothese 區域使用 Azure 入口網站佈建的 hello 應該會運作。 

## <a name="azure-sdk-for-net-282"></a>Azure SDK for .NET 2.8.2
下列的 hello 2.8.2 工具 hello 安裝，客戶可能會遇到下列問題的 hello。         

* 如果您使用 Windows 10，且尚未安裝 Internet Explorer，您可能會收到「找不到 Internet Explorer」的錯誤。
  tooresolve hello 問題，請安裝 Internet Explorer 使用 hello 新增/移除 Windows 元件 對話方塊。

如果您發現這個問題，請使用 hello 傳送笑臉 的功能 tooreport 它。

如需詳細資訊，請參閱 [這篇](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) 文章。

## <a name="other-updates"></a>其他更新
如需其他更新，請參閱 [Azure SDK 2.8 公告文章](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。

## <a name="also-see"></a>另請參閱
[Azure SDK 2.8 公告文章](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[支援和 hello Azure SDK for.NET 和 Api 的停用資訊](https://msdn.microsoft.com/library/azure/dn479282.aspx)

