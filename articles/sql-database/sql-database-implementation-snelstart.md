---
title: "aaaAzure SQL 資料庫 Azure 案例研究-Snelstart |Microsoft 文件"
description: "深入了解 SnelStart 使用 SQL Database toorapidly 展開其速率為每月 1,000 新 Azure SQL Database 的商務服務的方式"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>透過 Azure，SnelStart 以每月 1,000 個新 Azure SQL Database 的速度快速擴充其商務服務
![SnelStartLogo](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart 讓 hello 荷蘭中的熱門財務和商務管理-適用於小型和中型大小的企業 (Smb) 的軟體。 它的 55,000 個客戶是由其 110 個員工提供服務，其中包括 35 個 IT 人員。 從桌面軟體 tooa 軟體做為服務 (SaaS) 建置在 Azure 上的供應項目移動，SnelStart 進行最 hello 的自動化管理，在 C# 中，使用熟悉的環境和最佳化效能和延展性都沒有 over-內建服務或在佈建的企業，使用彈性集區。 使用 Azure 提供的內部部署與 hello 之間移動客戶 SnelStart hello 倍速雲端。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>為什麼 SnelStart 從 hello 桌面 toohello 雲端中擴充服務
> 「 Azure 使用表示我們可以更快交付軟體、 快速回應 toocustomer 要求，以及調整的解決方案，當要求增加"。
> 
> — Henry Been，軟體架構設計師
> 
> 

SnelStart 已使用下列傳統開發模型成功經營軟體業務多年：撰寫程式碼、封裝、運送，然後又重複。 經過一段時間，變更的步調 hello 成長更快和更快。 法規經常變更，客戶需要更容易的方式 tooprocess 財務記錄，並將其與這些變更共同作業會計與政府 tookeep 組成。

「 傳送軟體 toocustomers 是否高成本和限制，」 根據 tooHenry 已，軟體架構設計人員。 「生產、封裝及運送成本限制了我們發行軟體的頻率。 我們必須定期的出貨、 toopackage 更新但，使其硬 toomeet 我們的客戶需求變更。 我們可以永遠不會確保我們的客戶升級 toohello hello 產品最新版本。 因此，我們必須 toosupport 多個版本，讓 hello 也支援工作很難 toodo。 」

已加入，「 我們想要的方式在加速 tooprogram 和發行更新步調，因此我們可以更快速創新，建立新的服務，我們的客戶。 我們也想方式 tooautomate 更多程序順序 toosimplify 中客戶的企業管理需求。 」

SnelStart，如 hello 方案已 tooextend 其服務藉由成為雲端 SaaS 提供者。 hello Azure SQL Database 平台協助 SnelStart 那里取得，而不會產生 hello 主要 IT 負荷，會需要基礎結構做為服務 (IaaS) 方案。

hello 雲端模型也可讓 SnelStart toofix bug，並快速，提供新功能，而不需要 toodownload 和升級軟體的客戶。 相應 tooBeen，「 使用 Azure 雲端服務可讓我們 tooquickly 遵守變更來自第三方的需求。 您不需要 tooship 新的版本 toothousands 的客戶，我們可以採用由我們所需的第三方的桌面應用程式 toonew 格式傳送的資訊。 」

## <a name="a-modern-company-with-traditional-roots"></a>具有傳統根源的現代化公司
SnelStart 是卑微根時 hello founders 樂器組件的製造商以啟動 hello 公司目 too1964，現代化、 敏捷式軟體開發的高科技企業。 hello SnelStart 軟體商務 hello 核心真的啟動打在 hello 1980，期間 hello 激增 hello 個人電腦。 hello 公司需要適用於 hello 階段較佳替代 toohello 會計軟體，因此花費自己未授權者手會有影響。 : 1982，hello 公司建立 hello foundation 的功能最後會變得 SnelStart 會計軟體。 已從 hello 開始其簡易性和速度的 admired hello 軟體 — 太多，而 hello 公司最後變更焦點改造本身套到軟體公司。

在 1995 年，SnelStart 發行了它第一款適用於 Windows 的簿記應用程式。 hello 建置應用程式，在 Microsoft Visual Basic 1.0 和 Microsoft Access 資料庫，這樣有助於成長 hello 比 5,000 位客戶基底 toomore。

現今，SnelStart 是主要的企業營運 (LOB) 及業務管理應用程式提供者，目標對象是荷蘭的中小企業和自行開業的企業家。 Carlo Kuip，IT 架構設計人員、 顯示，如 「 我們的目標是 tooprovide 100%自動化的企業管理服務，我們的客戶。 」

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>透過彈性集區將效能和成本最佳化
SnelStart 是彈性集區的早期大規模採用者。 彈性集區協助 hello 公司限制成本，以及更有效率地管理效能需求。 根據 tooBeen，"使用彈性集區，我們可以最佳化效能根據我們的客戶，hello 需求不會過度佈建。 如果我們在 tooprovision 根據尖峰負載時，會很高。 相反地，hello 選項 tooshare 資源之間的多個使用量低的資料庫可讓我們 toocreate 也執行，且符合成本效益的解決方案。 」

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Azure SQL Database 協助將資料容器化來達到隔離及安全性目的
Azure SQL Database 可讓 SnelStart tooeasily 並無障礙地移動 客戶的內部部署企業管理資料 tooAzure。 hello Azure SQL Database 是一個方便的容器，提供隔離、 界限驗證、 授權和輕鬆備份和還原功能。 資料庫為業務管理提供了一個適當的概念模型。 相應 tooCarlo Kuip，IT 架構設計人員、 」 此容器界限內的項目會包含重要 tooa 商務，且將這些項目儲存在隔離的資料庫會保留它們保護的機密資料。 我們可以管理在 hello 資料庫層級的授權和甚至自動化 hello 管理和向外延展的資料庫而不需要資料庫管理員 (Dba) 人員。 」

Azure SQL 資料倉儲也中扮演一個角色 hello SnelStart 安全性和管理劇本藉由協助 hello 公司收集遙測資料，例如入侵偵測、 使用者活動記錄，以及連線。

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure 免除了額外負荷，讓開發人員可以將更多時間專注在實現價值上
hello Azure 平台模型移除基礎結構的額外負荷，並啟用 SnelStart tooautomate 部署使用 C# 管理程式庫。 Kuip 狀態，如 「 我們能 toogrow 我們目前的作業在非常小的員工，同時提高延展性、 速度以及災害復原時使用我們的用戶端選項。 hello shift tooservices 開發釋放資源上新的服務和功能，而不是只向上與新的規範或稅務程式碼以更新現有的程式碼 tookeep toofocus。 」 他將新增，「 自動化管理，並使用 hello SaaS 供應項目，很多個值而不需要 toomake 大型投資操作人員在我們的用戶端可以 toodeliver。 」 例如，藉由使用 Azure 和彈性集區，SnelStart 已能 tooadd 各種不同的新功能，包括更健全與銀行的客戶資料整合新的計費服務、 小型企業背景檢查和電子郵件服務。

> 「 在只 hello 2016 的前幾個月，我們擴大大約 5,500 toomore 12,000，比從我們 Azure SQL Database 部署和我們目前正在將加入每個月約 1,000 個的資料庫 」。
> 
> — Henry Been，軟體架構設計師
> 
> 

資料庫管理會進一步自動化使用 hello 彈性的作業功能。 Kuip 狀態，如 「 高感謝 hello 自動探索 SQL 資料庫的 [伺服器] 執行個體上的資料庫。 」 這可讓 SnelStart tooexecute 管理作業到動態成長客戶基底，不需要額外成本。

SnelStart 也正在開發 API，來作為客戶資料與協力廠商軟體合作夥伴所建置的應用程式之間的代理程式。 Kuip 狀態為 「 這個 API 會啟用其他廠商 tooadd 功能 tooour 軟體，例如消除資料發票和其他文件的項目。 」 客戶將不再有 toomanually 類型發票到小型企業計量軟體;hello SnelStart 軟體將會直接交換 hello 所需的資訊。 這可讓客戶 toojoin 其商務系統管理工作與 hello 生態系統的新數位轉換 hello 產業中的資訊。  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Azure 服務如何啟用適用於 SnelStart 的 SaaS
藉由使用 Azure，SnelStart 可其客戶和其會計 hello 定域機組中更順暢。 舉例來說，客戶和會計師都可以直接存取裝載在 Azure 上的 SnelStart 用戶端 API 來共用資訊。 Kuip 狀態 」 這些可重複使用的服務是使用 tooour 客戶對向 web 應用程式，並提供常見的基礎結構和函式 tooallow 存取 toobusiness 管理客戶和客戶所使用的 toothird 廠商軟體。 範例包括提供產品組態功能、管理防火牆規則，以及管理長時間執行的程序，例如備份。」

> 我們的目標是針對本公司客戶的商務系統管理服務的 tooprovide 100%自動化。 」 
> 
> — Carlo Kuip，IT 架構設計師
> 
> 

此外，SnelStart web 服務可讓客戶和 Azure SQL Database 彈性集區中的會計 tooeasily 存取資料。 這個 SaaS 模型再結合資料庫彈性與 Azure Resource Manager，可為 SnelStart 提供能夠補足每個 Azure 部署的延展性功能。 使用 C# 管理程式庫，全面自動化 hello 實作。

![SnelStart 架構](./media/sql-database-implementation-snelstart/figure1.png)

圖 1. 截至 2016 年 6 月為止，SnelStart 擁有超過 11,000 個資料庫，以及超過 50 個彈性集區

## <a name="simplicity-from-hello-cloud"></a>為了簡單起見，從 hello 雲端
因為移動 tooan Azure 雲端方案，SnelStart 已能 toosupport 客戶快速成長，同時創新功能與服務供應項目。 根據 tooBeen，"與 Azure 中，我們可以傳遞附近持續更新我們的客戶，而不會擴充我們作業人員。 當我們取得所有 hello 其他很棒的 Azure 功能，例如延展性和災害復原 — 組合在一起。"

> 「 當我們實際上透過雷德蒙德...我收到呼叫從開發人員回 hello 荷蘭打電話給我關於特定問題。 我們已能 tooget Microsoft toodeliver toosolve 48 小時內的實際執行環境中的變更，我們的問題。 」
> 
> — Henry Been，軟體架構設計師
> 
> 

SnelStart 也感謝 hello 它們與 hello Microsoft Azure SQL DB 小組所開發的強式合作關係。 為 Kuip 狀態，「 我們有功能的討論區和 toouse 技術，這不是撰寫者貢獻兩邊。 」
hello SnelStart 立即目標是 tookeep 成長其滿足的客戶的基底。 已為狀態 「 hello 技術和資源限制，我們必須身為 ISV，沒有任何目前我們所能成長的限制 toohow。 」

## <a name="more-information"></a>詳細資訊
* toolearn 深入了解 Azure 的彈性集區，請參閱[彈性集區](sql-database-elastic-pool.md)。
* toolearn 深入了解 Web 角色和背景工作角色，請參閱[背景工作角色](../fundamentals-introduction-to-azure.md#compute)。    
* toolearn 深入了解 Azure SQL 資料倉儲，請參閱[SQL 資料倉儲](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn 深入了解 SnelStart，請參閱[SnelStart](http://www.snelstart.nl)。

