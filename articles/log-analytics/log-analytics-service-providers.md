---
title: "aaaLog 服務提供者的分析功能 |Microsoft 文件"
description: "Log Analytics 可協助管理服務提供者 (MSP)、大型企業、獨立軟體廠商 (ISV) 和主機服務提供者管理和監視客戶的內部部署或雲端基礎結構中的伺服器。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>服務提供者的 Log Analytics 功能
Log Analytics 可協助管理服務提供者 (MSP)、大型企業、獨立軟體廠商 (ISV) 和主機服務提供者管理和監視客戶的內部部署或雲端基礎結構中的伺服器。 

大型企業與服務提供者有許多相似之處，特別是當有集中式的 IT 團隊負責管理許多不同業務單位的 IT 時。 為了簡單起見，本文件會使用 hello 詞彙*服務提供者*但 hello 相同的功能也適用於企業和其他客戶。

## <a name="cloud-solution-provider"></a>雲端解決方案提供者
合作夥伴和服務提供者屬於 hello[雲端方案提供者 (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview)程式，記錄分析是其中一個 hello CSP 訂用帳戶可用的 Azure 服務。 

供記錄分析中啟用下列功能的 hello*雲端方案提供者*訂用帳戶。

身為「雲端解決方案提供者」，您可以：

* 在租用戶 (客戶) 訂用帳戶中建立 Log Analytics 工作區。
* 存取租用戶建立的工作區。 
* 加入和移除使用者存取 toohello 工作區中使用 Azure 的使用者管理。 租用戶的工作區中 hello OMS 入口網站的 hello 使用者管理頁面，設定下無法使用時
  * 記錄分析不支援以角色為基礎的存取權但-讓使用者`reader`hello Azure 入口網站中的權限可讓它們 toomake 組態變更 hello OMS 入口網站中

toolog tooa 租用戶的訂用帳戶中，您需要 toospecify hello 租用戶識別碼。 hello 租用戶識別碼通常是 hello 電子郵件地址使用 toosign 中的最後一部分。

* 在 hello OMS 入口網站，加入`?tenant=contoso.com`hello hello 入口網站的 URL 中。 例如， `mms.microsoft.com/?tenant=contoso.com`
* 在 PowerShell 中，使用 hello`-Tenant contoso.com`參數使用時`Add-AzureRmAccount`cmdlet
* 當您使用 hello hello 租用戶識別碼會自動加入`OMS portal`從 hello Azure 入口網站 tooopen 連結並登入 toohello hello 選取工作區的 OMS 入口網站

身為「雲端解決方案提供者」的「客戶」，您可以：

* 在 CSP 訂用帳戶中建立 Log Analytics 工作區
* 存取工作區建立 hello CSP
  * 使用 hello`OMS portal`從 hello Azure 入口網站 tooopen 連結並登入 toohello hello 選取工作區的 OMS 入口網站
* 檢視及使用 hello 使用者管理頁面設定下 hello OMS 入口網站中

> [!NOTE]
> hello 包含備份和記錄分析的 Site Recovery 解決方案都不能 tooconnect tooa 復原服務保存庫無法設定 CSP 的訂用帳戶中。 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>使用 Log Analytics 管理多個客戶
建議您為每個您管理的客戶建立 Log Analytics 工作區。 Log Analytics 工作區提供：

* 儲存資料 toobe 地理位置。 
* 計費的細微度 
* 資料隔離 
* 唯一的組態

藉由建立每個客戶的工作區，您可以 tookeep 個別的每個客戶的資料而且也追蹤 hello 每一位客戶的使用方式。

時間和原因 toocreate 多個工作區中描述的詳細[管理存取 toolog 分析](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need)。

建立及設定客戶工作區可以使用自動化[PowerShell](log-analytics-powershell-workspace-configuration.md)，[資源管理員範本](log-analytics-template-workspace-configuration.md)，或使用 hello [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/)。

hello 使用工作區中設定資源管理員範本可讓您 toohave 主要的設定，可以使用的 toocreate 並設定工作區。 您可以放心工作區建立的客戶會自動設定 tooyour 需求。 當您更新您的需求時，hello 範本會更新，然後重新套用 hello 現有工作區。 此程序可確保現有的工作區符合新的標準。    

當管理多個記錄分析工作區，我們建議您與您現有的票證系統整合每個工作區 / operations 主控台使用 hello[警示](log-analytics-alerts.md)功能。 藉由整合與您現有的系統，支援人員可以繼續 toofollow 其熟悉的程序。 記錄分析會定期檢查 hello 警示的準則，您指定針對每個工作區，並不需要採取動作時產生警示。

個人化資料的檢視，使用 hello[儀表板](../azure-portal/azure-portal-dashboards.md)hello Azure 入口網站中的功能。  

執行層級報表來總結資料工作區，您可以使用跨 hello 之間記錄分析的整合和[PowerBI](log-analytics-powerbi.md)。 如果您需要 toointegrate 與另一個報告系統，您可以使用 hello 搜尋 API (透過 PowerShell 或[REST](log-analytics-log-search-api.md)) toorun 查詢和匯出搜尋結果。

## <a name="next-steps"></a>後續步驟
* 使用 [Resource Manager 範本](log-analytics-template-workspace-configuration.md)建立和設定工作區
* 使用 [PowerShell](log-analytics-powershell-workspace-configuration.md)自動建立工作區 
* 使用[警示](log-analytics-alerts.md)toointegrate 與現有系統
* 使用 [PowerBI](log-analytics-powerbi.md)產生摘要報告

