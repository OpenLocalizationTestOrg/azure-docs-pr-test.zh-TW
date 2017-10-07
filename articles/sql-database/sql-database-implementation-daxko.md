---
title: "aaaAzure SQL 資料庫 Azure 案例研究-Daxko/CSI |Microsoft 文件"
description: "其客戶服務及效能，了解其開發週期和 tooenhance Daxko/CSI 如何使用 SQL Database tooaccelerate"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI tooenhance 及其開發週期，請使用 Azure tooaccelerate 其客戶服務及效能
![Daxko CSI/標誌](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Daxko/CSI 軟體面臨挑戰： 快速成長，謝謝 toohello 成功其全方位的企業軟體解決方案，但 IT 基礎結構需要該成長的 hello 與保持其客戶的基底適用性和娛樂中心基底的客戶已測試 hello 公司的 IT 人員。 hello 公司已逐漸受到上升的作業負荷，特別是針對管理其持續成長的資料庫。 更糟的，該作業的額外負荷已剪下到新的方案，例如 hello 公司的軟體的新行動功能的開發資源。

根據 tooDavid Molina，產品開發的主管在 Daxko/CSI、 hello 平台做為服務 (PaaS) 模型，它需要 toosimplify 資料庫管理，提供 Azure CSI 軟體增加延展性，以及釋出資源 toofocus 上而不是 ops 軟體。 「Azure SQL Database 是非常適合我們的選項。 不需要維護 SQL Server、 容錯移轉叢集，以及所有 hello tooworry 其他基礎結構需求適合我們。 」

因為移轉 tooAzure，CSI 軟體需要的只有兩個 toomanage 作業人員透過 600 客戶資料庫。 hello 公司使用 Azure SQL Database 彈性集區 toomove 客戶資料庫大小為基礎，而且需要。

Molina 仍繼續，「 我們的客戶認為 hello 立即變更。 在使用彈性集區之前，他們在高載期間有時會遇到逾時和其他問題。 使用 Azure 的彈性集區高載視便能使用 hello 軟體，而不發生問題。 」

此外 tooimproving 效能的客戶，Azure 的彈性集區釋放 CSI 軟體資源 toofocus 上開發新的服務和功能，而不是使用 管理和作業的處理。 這些 IT 資源，幫助改善企業軟體供應項目，SpectrumNG，toohelp CSI 軟體連絡健身房成員，提升員工的效率，並提供人員和成員存取行動裝置互動工作和即時通知。

Azure 也有幫助 CSI 軟體加速並啟用自動化選項來提升 hello 開發和品質保證 (QA) 循環。 Hello 公司的 Azure 實作中，與組建管理員可以封裝元件中以 hello 按一下按鈕。 如 Molina 所述，"hello 發行週期的一部分，不必在 QA 現在是在 Azure 中慎我們實際執行的堆疊可以 toodeploy tooa 測試環境。 立即 tooour 開發人員環境 toovet 變更，我們可以部署組建。 這對我們而言是一大優點，因為之前我們沒有類似的環境可供進行測試。」

## <a name="offloading-toohello-cloud"></a>卸載 toohello 雲端
日前 toohello 雲端 CSI 軟體已成功建立本身的本機資料中心內的多租用戶基礎結構。 為 hello 公司展開時，它面臨不斷增加的初期難題，從購買、 佈建，及維護所有的 hello 硬體和軟體所需 toosupport 其客戶。 IT 人員雇用 toohandle 作業變成另一個瓶頸，導致佈建新的資源和推出新服務 toocustomers tooa 速度變慢。

為了消除該額外負荷，CSI Software 研究了雲端選項，以便能夠將焦點放在程式碼，而不是作業。 hello 公司探索到許多 hello 最上層的雲端提供者只提供仍然需要大型 IT 人員 toomanage hello IaaS 堆疊的基礎結構做為服務 (IaaS) 方案。 在 hello 結束時，CSI 軟體會決定 hello Azure PaaS 解決方案已符合其需求有最佳 hello。 Molina 說明: 「 讓我們能夠專注於我們的軟體供應項目，同時降低我們 IT 負荷 Azure 取得 hello hello 方法不足的硬體和系統軟體 」。

## <a name="making-hello-transition-tooazure"></a>進行 hello 轉換 tooAzure
選取 Azure 其 PaaS 解決方案之後, CSI 軟體會開始移轉它的後端基礎結構和資料庫 toohello 雲端。 先前的 tooAzure SpectrumNG 客戶需要 tooinstall hello 後端的 Windows Communication Foundation (WCF) 服務與通訊的用戶端應用程式。 根據 tooMolina，"雖然某些客戶可以裝載自己的資料中心內的所有項目，我們建置出 hello 產品 toobe 多租用戶。 我們裝載的資料中心中的所有使用 SQL Server 做為 hello 資料存放區。

「 我們產品供應項目也包含成員向入口網站 （寫在 ASP.net 中），這是設計的 toobe 白色標示 toomatch hello 客戶的網頁存在，以及 SOAP API toosupport hello 線上頁面和任何協力廠商整合 」。

hello 移轉 toohello 雲端不需花 hello 架構。 根據 tooMolina，"hello 多數 hello 投入時間的人選修改 hello 方式，我們讀取設定檔案資訊、 集中式的連接字串修改，以及封裝、 上傳，及我們的發行部署自動化 hello。 」

toodevelop hello 建置自動化、 CSI 軟體工程師會使用 Azure PowerShell 和 REST Api toocreate 封裝並上傳 tooa 發行每晚的預備環境。
hello 整體轉換 tooan Azure 雲端部署更快速且順暢 hello CSI 軟體 IT 團隊。 說明 Molina: 」 中，我們必須 beta 環境 hello 雲端中的 hello 專案上的三個 toofour 週內。 對我們而言是一項意外的勝利。」

CSI 軟體設定和測試 hello 環境之後，開始移轉客戶。 對於已經使用 CSI 軟體裝載客戶，hello 轉換為幾乎順暢。 從內部部署移轉的客戶，hello 移轉 toohello 雲端採取一些額外的時間，但仍主要免客戶和 CSI 軟體。

針對新客戶，CSI 軟體的 IT 人員使用 hello 下列程序 tooon 面板它們 tooAzure:

1. Azure PowerShell 指令碼會使用的 toospin 向上 hello 客戶; 新的資料庫所有客戶一都開始在 premium 層 tooensure hello 轉換足夠初始的輸送量。
2. 如果可能的話，CSI 軟體會使用 hello Azure SQL 移轉精靈 toomove 現有資料 tooan Azure SQL Database 執行個體。
3. 最後，Microsoft SQL Server Integration Services (SSIS) 會使用的 tooreconcile 所需的任何不一致的地方 hello 資料或 tooperform 做為任何資料的清除作業。

現在，大約 99% 的 CSI Software 都是裝載在 Azure 中，遍及四個區域資料中心 (中北部、中南部、東部及西部)。 每個客戶的地理區域中有資料中心，延遲就會保留 tooa 最小值。

## <a name="azure-elastic-pools-free-up-it-resources"></a>Azure 彈性集區釋出 IT 資源
Azure 的數個功能協助了 CSI 軟體 shift 鍵，從基礎結構和操作焦點的 toobeing 功能和已取得焦點的開發。 可能是 hello 大的優勢已從彈性集區。

CSI Software 目前為客戶提供大約 550 個資料庫。 在之前彈性集區，它是難以 toomanage 內的許多資料庫層結構。 Ops 管理員必須根據 hello 尖峰需求的客戶，需要大量 IT 資源的額外負荷 tooassign 效能層級。 透過彈性集區，管理員則可以視情況為租用戶指派高階或標準集區，然後再根據大小和需求來移動客戶。 客戶認為 hello 彈性集區的影響，hello 幾乎會立即;彈性集區，客戶在尖峰使用量期間，已逾時以及其他問題，但使用彈性集區，客戶可能會遇到活動暴增如有需要前後他們可以繼續 toouse SpectrumNG 而不發生問題。

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure 作用中異地複寫加速報表處理速度
有數個 CSI Software 客戶也利用 Azure 作用中異地複寫功能。 具有作用中地理複寫中，向上 toofour 可讀取次要資料庫可以設定在 hello 相同或不同資料中心區域。 CSI 軟體會使用兩種方式的作用中地理複寫： 首先，hello 次要資料庫中可用的資料中心中斷或 hello 無法 tooconnect toohello 主要資料庫的 hello 大小寫與第二，hello 次要資料庫都可以讀取也可以使用的 toooffload 唯讀工作負載，例如報告工作。 有些 CSI 軟體客戶使用此報告的工作流程的好處 tooaccelerate。

## <a name="csi-software-application-logic-and-architecture"></a>CSI Software 應用程式邏輯與架構
SpectrumNG 使用 Web 角色。 Hello 應用程式是多租用戶，因為 WCF 服務是從客戶使用的 toohandle hello 初始連線要求。 Molina 狀態為 「 hello 要求識別每個客戶，然後可以讓我們建立的連接字串出 tootheir 資料庫 toodo 我們需要的任何 toodo。 」

其服務的 hello web 層，CSI 軟體會利用 Azure 自動縮放功能，根據日期和時間。 可用的資源包括自動增加的 tooaccommodate 高使用量在營業時間內，根據每個地區資料中心 toohello 時區。 資源也設定 tooscale 週末，當客戶的需求會降低。

![Daxko/CSI 架構](./media/sql-database-implementation-daxko/figure1.png)

圖 1. 雲端服務背景工作角色會從 Azure SQL Database 抽取結構化資料，以及從資料表儲存體抽取半結構化資料。 SpectrumNG 使用者會透過雲端服務 Web 角色與該資料進行互動。

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>將 Web 應用程式和 Web 方案層用於行動應用程式
使用 Azure SQL Database CSI 軟體 tooenable 的資源釋出新的方案，包括完整的行動平台為基礎之裝載於 Azure web 應用程式的自訂 API。 hello 平台可讓健身房成員和人員 toouse 行動裝置 toocheck 排程活頁簿的類別，和接收訊息。

hello 平台會使用服務導向架構 (SOA) tootake 單一元件 — 例如銷售點 (POS) 系統或銷售的系統 — 將它移 hello 飛 tooanother web 計劃，然後備妥服務 toosupport 該元件，但保留其他所有項目hello 原始 web 方案。 此功能為 CSI Software 提供了極大的彈性，並且有助於降低成本。

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure 讓 CSI Software 開發人員專注於應用程式和服務
Azure SQL Database 不只 boon tooSpectrumNG 客戶，享受 hello 快速、 可靠的服務，它也是 CSI 軟體的最大優點 IT 人員和開發人員。 藉由卸載 ops tooAzure hello 雲端中的，CSI 軟體減少其對資源和基礎結構的額外負荷、 大幅加速開發循環，而且不再需要為其租用戶的 toomicromanage 資料庫 toooptimize 效能。

## <a name="more-information"></a>詳細資訊
* toolearn 深入了解 Azure 的彈性集區，請參閱[彈性集區](sql-database-elastic-pool.md)。
* toolearn 深入了解資料庫工具和彈性調整的效果，請參閱[彈性資料庫工具和彈性調整](sql-database-elastic-scale-get-started.md)。
* toolearn 進一步了解移轉 SQL Server 資料庫，請參閱 < 請參閱[移轉 SQL Server 資料庫 tooAzure](sql-database-cloud-migrate.md)。
* toolearn 進一步了解作用中的地理複寫，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)。
* toolearn 深入了解 Web 角色和背景工作角色，請參閱[背景工作角色](../fundamentals-introduction-to-azure.md#compute)。    
* toolearn 深入了解 Azure 服務匯流排，請參閱[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)。
* toolearn 深入了解自動調整規模，請參閱[調整雲端服務](../cloud-services/cloud-services-how-to-scale.md)。

