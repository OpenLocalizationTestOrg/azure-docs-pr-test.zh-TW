---
title: "aaaAzure 計費 Api |Microsoft 文件"
description: "深入了解 Azure 計費的使用量與 RateCard Api，也就是使用的 tooprovide 深入了解 Azure 資源耗用量和趨勢。"
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>使用 Azure 計費 Api tooprogrammatically 取得深入了解您的 Azure 使用量
使用 Azure 計費 Api toopull 使用情形和資源資料到您的慣用的資料分析工具。 hello Azure 資源使用量和 RateCard 應用程式開發介面可協助您準確地預測和管理您的成本。 hello Api 會實作成資源提供者和 hello 系列 hello Azure 資源管理員所公開的應用程式開發介面的一部分。  

## <a name="azure-invoice-download-api-preview"></a>Azure 發票下載 API (預覽)
一次 hello[選擇在已經過完整](billing-manage-access.md#opt-in)、 使用 hello 預覽版本的下載發票[發票 API](/rest/api/billing)。 hello 功能包括：

* **Azure 角色型存取控制**-設定存取原則在 hello [Azure 入口網站](https://portal.azure.com)或透過[Azure PowerShell cmdlet](/powershell/azure/overview) toospecify 哪些使用者或應用程式進行存取toohello 訂用帳戶的使用量資料。 呼叫端必須使用標準的 Azure Active Directory 權杖進行驗證。 加入 hello 呼叫端 tooeither hello 計費的讀取器，讀取器、 擁有者或參與者角色 tooget 存取 toohello 使用量資料特定的 Azure 訂用帳戶。
* **日期篩選**-使用 hello`$filter`參數 tooget hello 依反向時間順序中的所有 hello 發票的都發票期間的結束日期。 

> [!NOTE]
> 這項功能處於預覽第一個版本，而且可能主旨 toobackward 不相容的變更。 目前，某些訂用帳戶優惠 (不支援 EA、CSP、AIO) 和 Azure 德國無法使用此功能。

## <a name="azure-resource-usage-api-preview"></a>Azure 資源使用情況 API (預覽)
使用 hello Azure[資源使用量 API](https://msdn.microsoft.com/library/azure/mt219003) tooget 估計 Azure 耗用量資料。 hello API 包括：

* **Azure 角色型存取控制**-設定存取原則在 hello [Azure 入口網站](https://portal.azure.com)或透過[Azure PowerShell cmdlet](/powershell/azure/overview) toospecify 哪些使用者或應用程式進行存取toohello 訂用帳戶的使用量資料。 呼叫端必須使用標準的 Azure Active Directory 權杖進行驗證。 加入 hello 呼叫端 tooeither hello 計費的讀取器，讀取器、 擁有者或參與者角色 tooget 存取 toohello 使用量資料特定的 Azure 訂用帳戶。
* **每小時或每日彙總** - 呼叫端可以指定要 Azure 使用情況資料的每小時值區或每日值區。 hello 預設值是每日。
* **執行個體中繼資料 （包括資源標記）** – 取得執行個體層級詳細資料，例如 hello 完整的資源 uri (/subscriptions/ {訂閱 id} / …)，hello 資源群組資訊和資源標記。 這個中繼資料可協助您確定的方式，並以程式設計方式配置 hello 標記，例如跨充電的使用案例使用方式。
* **資源的中繼資料**-資源詳細資料，例如 hello 計量表的名稱、 計量表類別目錄、 計量表子類別目錄、 單位和區域提供 hello 呼叫者更深入了解什麼對於使用。 我們也正在 tooalign 資源的中繼資料術語跨 hello Azure 入口網站、 Azure 使用量 CSV，計費 CSV、 EA 和其他公開體驗，讓資料相互關聯跨體驗 toolet。
* **所有優惠類型的使用情況** – 所有優惠類型 (例如隨收隨付、MSDN、貨幣承諾、貨幣信用額度和 EA) 皆有提供使用情況資料。

## <a name="azure-resource-ratecard-api-preview"></a>Azure 資源 RateCard API (預覽)
使用 hello [Azure 資源 RateCard API](https://msdn.microsoft.com/library/azure/mt219005) tooget hello 清單可用的 Azure 資源和估計每個定價資訊。 hello API 包括：

* **Azure 角色型存取控制**-hello 上設定存取原則[Azure 入口網站](https://portal.azure.com)或透過[Azure PowerShell cmdlet](/powershell/azure/overview) toospecify 哪些使用者或應用程式進行存取toohello RateCard 資料。 呼叫端必須使用標準的 Azure Active Directory 權杖進行驗證。 加入 hello 呼叫端 tooeither hello 讀取器、 擁有者或參與者角色 tooget 存取 toohello 使用量資料特定的 Azure 訂用帳戶。
* **支援隨收隨付、MSDN、貨幣承諾、貨幣信用額度優惠 (不支援 EA)** - 此 API 提供 Azure 優惠層級費率資訊。  此 API 的 hello 呼叫端必須傳入 hello 優惠資訊 tooget 資源詳細資料和率。 因為 EA 優惠已自訂每個註冊的速率，我們目前無法 tooprovide EA 率。 

## <a name="scenarios"></a>案例
以下是一些 hello 實現具有 hello 使用量與 hello RateCard Api hello 組合的案例：

* **Azure 花 hello 月**-hello 月支出 hello 使用量和 RateCard Api tooget 更深入了解您的雲端使用 hello 組合。 您可以每小時分析 hello 和估計每日的值區的使用量和計量。
* **設定警示**– 使用 hello 使用量及 hello RateCard Api tooget 估計雲端耗用量和費用，並設定資源或貨幣型警示。
* **預測的帳單**– 取得您的估計耗用量和雲端的支出，和套用機器學習演算法 toopredict 哪些 hello bill 會結尾 hello hello 計費週期。
* **成本分析前耗用量**– 使用多少帳單會套用至您的預期使用量時移動工作負載 tooAzure hello RateCard API toopredict。 如果您有其他的雲端或私人雲端中的現有工作負載時，您也可以對應與 hello Azure 率 tooget 花較佳的估計值，Azure 的使用方式。 這個 hello 能力 toopivot 上提供的服務，並比較與對照隨用隨付，超出的 hello 其他優惠類型之間的估計提供，例如預付與貨幣信貸。 hello API 也可讓您 hello 能力 toosee 成本差異區域，並可讓您 toodo 假設成本分析 toohelp 進行的部署決策。
* **假設分析** -
  
  * 您可以判斷它是否符合成本效益 toorun 工作負載在另一個區域中，或在另一個組態的 hello Azure 資源。 Hello 您所使用的 Azure 區域根據 azure 資源的成本可能會不同。
  * 您也可以判斷另一個 Azure 優惠類型是否會在 Azure 資源上提供更好的費率。
  
## <a name="partner-solutions"></a>合作夥伴解決方案
[Microsoft Azure 的使用量和 RateCard Api 啟用 Cloudyn tooProvide 客戶 ITFM](billing-usage-rate-card-partner-solution-cloudyn.md)描述 hello Azure 計費 API 協力廠商所提供的整合經驗[Cloudyn](https://www.cloudyn.com/microsoft-azure/)。 此文章說明其經驗相關，且包含的視訊，示範如何使用 Cloudyn 和 hello Azure 計費 Api tooget insights 從 Azure 耗用量資料。

[雲端 Cruiser 和 Microsoft Azure 計費 API 整合](billing-usage-rate-card-partner-solution-cloudcruiser.md)描述如何[Cloud Cruiser Express for Azure 套件](http://www.cloudcruiser.com/partners/microsoft/)直接從 hello Windows Azure Pack (WAP) 入口網站的運作方式。 順暢地，您就可以從單一使用者介面管理這兩個 hello 操作及財務層面 hello Microsoft Azure 私人部署或裝載公用雲端。   

## <a name="next-steps"></a>後續步驟
* 請參閱 GitHub 上的 hello 程式碼範例：
  * [發票 API 程式碼範例 (英文)](https://go.microsoft.com/fwlink/?linkid=845124)

  * [使用情況 API 程式碼範例 (英文)](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [RateCard API 程式碼範例 (英文)](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn 深入了解 hello Azure 資源管理員，請參閱[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。 

* 多個必要 toohelp 您了解雲端的支出 hello suite 工具的資訊，請參閱 hello Gartner 文章[IT 財務管理 (ITFM) 工具的市場指南](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb)。

