---
title: "aaaMulti 租用戶 Web 應用程式模式 |Microsoft 文件"
description: "尋找架構的概觀並說明如何 tooimplement 多租用戶 web 應用程式在 Azure 上的設計模式。"
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Azure 中的多租用戶應用程式
多租用戶應用程式是可讓個別使用者或 「 租用戶，"tooview hello 的應用程式，如同它是自己的共用的資源。 如將本身借用 tooa 多租用戶應用程式的典型案例是其中一個 hello 的所有使用者在應用程式可能會想 toocustomize hello 使用者經驗，不過不會造成 hello 相同的基本商務需求。 舉例來說，Office 365、Outlook.com 和 visualstudio.com 都屬於大型多租用戶應用程式。

從應用程式提供者的觀點而言，由於 hello 優點大部分 toooperational 和方面成本效率。 一個版本的應用程式可以滿足 hello 許多租用戶/客戶需求，讓彙總的系統管理工作，例如監視、 效能調整、 軟體維護和備份資料。

hello 以下提供一份 hello 最重要目標和需求，從提供者的觀點來看。

* **佈建**： 您必須是新的租用戶可以 tooprovision hello 應用程式。  對於使用大量的租用戶的多租用戶應用程式，它是 tooautomate 通常會需要這個程序啟用自助佈建。
* **維護性**： 您必須能夠 tooupgrade hello 應用程式並執行其他維護工作，而多個租用戶正在使用它。
* **監視**： 您必須在任何時候 tooidentify 無法 toomonitor hello 應用程式，任何問題和 tootroubleshoot 它們。 這包括監視每個租用戶 hello 應用程式中的特殊使用。

適當實作多租用戶應用程式提供 hello 下列優點 toousers。

* **隔離**: hello 的個別租用戶的活動不會影響 hello hello 受到其他租用戶的應用程式使用。 租用戶之間無法相互存取資料。 您似乎 toohello 租用戶有獨佔使用 hello 應用程式。
* **可用性**： 個別租用戶想要 hello 應用程式 toobe 經常使用，可能是與定義於 SLA 保證。 同樣地，其他租用戶的 hello 活動應該不會影響 hello hello 應用程式的可用性。
* **延展性**: hello 應用程式縮放 toomeet hello 個別租用戶需求。 hello 存在與其他租用戶的動作應該不會影響 hello 效能 hello 應用程式。
* **成本**： 成本會低於執行專用、 單一租用戶應用程式，因為多租用戶啟用 hello 共用的資源。
* **自訂能力**。 hello 能力 toocustomize hello 應用程式的個別租用戶以各種方式，例如加入或移除功能、 變更色彩及商標，或甚至加入自己的程式碼或指令碼。

簡單地說，當有許多考量，您必須考慮到帳戶 tooprovide 高度可調整的服務，另外還有一些 hello 目標和一般 toomany 多租用戶應用程式的需求。 部分不能用於特定案例與 hello 重要性的個別目標，而且需求會因每個案例中。 Hello 多租用戶應用程式提供者，您也必須目標和需求，例如，會議 hello 租用戶目標和需求、 獲利率、 計費、 多個服務層級、 佈建、 維護性監視和自動化。

若想進一步了解多租用戶應用程式的其他設計注意事項，請參閱[在 Azure 上裝載多租用戶應用程式][Hosting a Multi-Tenant Application on Azure] \(英文\)。 如需多租用戶型軟體即服務 (SaaS) 資料庫應用程式的常見資料架構模式的資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md)。 

Azure 提供許多功能可讓您 tooaddress hello 金鑰設計多租用戶的系統時，所遇到的問題。

**隔離**

* 依主機標頭區隔具有 (或沒有) SSL 通訊的網站租用戶
* 依查詢參數區隔網站租用戶
* 背景工作角色中的 Web 服務
  * 背景工作角色： 通常處理資料的 hello 後端應用程式。
  * 通常做為應用程式的 hello 前端的 web 角色。

**儲存體**

資料管理，例如 Azure SQL Database 或 Azure 儲存體服務，例如 hello 資料表來儲存大量非結構化資料服務提供服務，並 hello Blob 服務提供服務 toostore 大量非結構化文字或二進位資料，例如視訊、 音訊和影像。

* 在 SQL Database 中保護多租用戶資料的安全：適當的個別租用戶 SQL Server 登入。
* 使用應用程式資源藉由指定容器層級存取原則的 Azure 資料表，您可以不用 tooissue 新 URL 的受保護的共用的存取簽章與 hello 資源 hello 能力 tooadjust 權限。
* Azure 佇列用於應用程式資源 Azure 佇列常用的 toodrive 處理代表租用戶，但也可能使用的 toodistribute 工作需要佈建或管理。
* 服務匯流排佇列用於應用程式資源的推播通知工作 tooa 共用服務，您可以使用單一佇列每個租用戶寄件者只具有唯一 hello 接收者 hello 服務時，權限 （如同 ACS 發出之通告所衍生） toopush toothat 佇列有權限 toopull hello 佇列 hello 資料來自多個租用戶。

**連接和安全性服務**

* Azure 的服務匯流排、 位於應用程式提升的規模和恢復功能鬆散偶合的方式讓 tooexchange 訊息之間的訊息基礎架構。

**網路服務**

Azure 提供了幾項支援驗證、並且可讓受到代管的應用程式提升可管理性的網路服務。 這些服務包括 hello 下列：

* Azure 虛擬網路可讓您在 Azure 中佈建及管理虛擬私人網路 (VPN)，並使用內部部署 IT 基礎結構安全地連結這些網路。
* 虛擬網路 Traffic Manager 可讓您連入流量，跨多個 Azure 託管服務，無論它們是在 hello tooload 平衡相同的資料中心或跨越 hello 世界各地的不同資料中心。
* Azure Active Directory (Azure AD) 是以 REST 為基礎的新式服務，可為您的雲端應用程式提供身分識別管理和存取控制功能。 使用 Azure AD 應用程式資源 Azure AD tooprovides 驗證和授權使用者 toogain 存取 tooyour web 應用程式和服務，同時允許超出中分解出來的驗證和授權 toobe hello 功能讓您輕鬆地進行程式程式碼。
* Azure 服務匯流排可為分散式和混合式應用程式提供安全訊息和資料流程功能 (例如 Azure 代管的應用程式與內部部署應用程式和服務之間的通訊)，而無須使用複雜的防火牆和安全性基礎結構。 服務匯流排轉送用於應用程式資源 toohello 服務會公開為端點可能屬於 toohello 租用戶 （例如，外部 hello 系統，例如在內部部署裝載），或者可能是特別針對 hello 租用戶 （佈建服務因為敏感性、 租用戶專屬的資料會在其中移動）。

**佈建資源**

Azure 提供數種方式新增租用戶佈建 hello 應用程式。 對於使用大量的租用戶的多租用戶應用程式，它是 tooautomate 通常會需要這個程序啟用自助佈建。

* 背景工作角色 tooprovision 和取消佈建每個租用戶資源 （例如當新的租用戶註冊或取消） 可讓您，收集度量的計量使用和管理遵循特定排程的小數位數或回應 toohello 橫跨臨界值的索引鍵效能指標。 這個相同的角色也可能使用的 toopush 出更新和升級 toohello 方案。
* Azure Blob 可以是使用的 tooprovision 計算或新租用戶的預先初始化的儲存體資源，同時提供容器層級存取原則 tooprotect hello 計算服務封裝，VHD 映像和其他資源。
* 為租用戶佈建 SQL Database 資源的選項包括：
  
  * 指令碼中的 DDL，或在組件中內嵌為資源的 DDL
  * 以程式設計方式部署的 SQL Server 2008 R2 DAC 封裝。
  * 從主要參考資料庫複製
  * 使用檔案中的資料庫匯入和匯出 tooprovision 新資料庫。

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
