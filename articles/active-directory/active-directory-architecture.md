---
title: "Azure Active Directory 架構 aaaUnderstand |Microsoft 文件"
description: "說明什麼是 Azure AD 租用戶，以及如何 toomanage Azure 透過 Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>了解 Azure Active Directory 架構
Azure Active Directory (Azure AD) 可讓您 toosecurely 管理存取 tooAzure 服務和資源，為您的使用者。 Azure AD 隨附一套完整的身分識別管理功能。 如需 Azure AD 功能的詳細資訊，請參閱[什麼是 Azure Active Directory？](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)

使用 Azure AD，您可以建立和管理使用者和群組，和啟用權限 tooallow 並拒絕存取 tooenterprise 資源。 身分識別管理的相關資訊，請參閱[hello Azure 身分識別管理的基本概念](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)。

## <a name="azure-ad-architecture"></a>Azure AD 架構
Azure AD 的地理位置分散的架構結合了廣泛的監視、 自動重設路徑操作、 容錯移轉和復原功能可讓我們 toodeliver 企業級可用性和效能 tooour 客戶。

本文將討論 hello 下列架構項目：
 *  服務架構設計
 *  延展性 
 *  持續可用性
 *  資料中心

### <a name="service-architecture-design"></a>服務架構設計
hello 最常見方式 toobuild 可擴充、 高可用性、 豐富的資料系統是透過獨立的建置組塊或延展單位 hello Azure AD 資料層，會呼叫擴充單元*分割*。 

hello 資料層會有數個可讀寫功能的前端服務。 hello 圖會顯示 hello 元件的單一目錄磁碟分割的方式分散於不同地理 distrubuted 資料中心。 

  ![單一目錄分割](./media/active-directory-architecture/active-directory-architecture.png)

Azure AD 架構的 hello 元件包括主要複本和次要複本。

**主要複本**

hello*主要複本*接收所有*寫入*hello 其所屬的資料分割。 任何寫入作業會傳回成功 toohello 呼叫者，以確保寫入的地理備援持久性之前立即複寫的 tooa 不同資料中心中的次要複本。

**次要複本**

所有目錄「讀取」是由「次要複本」提供服務，而次要複本是在實際位於不同地理位置的資料中心。 次要複本有許多個，因為資料會以非同步方式複寫。 目錄的讀取，例如驗證要求會從資料中心是關閉 tooour 客戶服務。 hello 次要複本必須負責讀取延展性。

### <a name="scalability"></a>延展性

延展性是增加效能需求服務 tooexpand toomeet hello 能力。 撰寫延展性達成 hello 資料分割。 讀取延展性達成方式是從一個資料分割 toomultiple 次要複本分散於整個 hello world 複寫資料。

從目錄的應用程式的要求是它們是實體上最接近的一般路由的 toohello 資料中心。 寫入為以透明的方式重新導向的 toohello 主要複本 tooprovide 讀寫一致性。 次要複本會大幅擴充 hello 小數位數的資料分割，因為 hello 目錄通常是服務讀取大部分的 hello 時間。

目錄的應用程式連接 toohello 最接近的資料中心。 這可改善效能，因此有可能相應放大。 由於目錄磁碟分割可以有多個次要複本，次要複本可以放置接近 toohello 目錄用戶端。 僅內部目錄服務元件是直接密集寫入的目標 hello 作用中的主要複本。

### <a name="continuous-availability"></a>持續可用性

可用性 （或執行時間） 定義不會中斷系統 tooperform hello 能力。 hello 金鑰 tooAzure 廣告的高可用性是我們的服務，可快速切換流量跨多個地理位置分散的資料中心。 每個資料中心都是獨立的，可啟用無關聯性失敗模式。

Azure AD 的資料分割設計都是簡化的比較的 toohello 企業 AD 設計，是向上延展 hello 系統的關鍵。 我們採用了單一主設計，其包含仔細協調且具決定性的主要複本容錯移轉程序。

**容錯**

如果是容錯 toohardware、 網路和軟體失敗的更多可用的系統。 Hello 目錄上的每一個資料分割，有高可用性的主要複本： hello 主要複本。 在此複本將會寫入 toohello 分割。 此複本正在持續且嚴密的監控，和寫入可立即移位的 tooanother 複本 (會變成 hello 新的主要) 偵測到失敗時。 在容錯移轉期間，通常可能喪失寫入可用性 1-2 分鐘。 在這段期間，讀取可用性不受影響。

（這許多大幅度人數寫入） 的讀取作業只會順著 toosecondary 複本。 由於次要複本都是等冪，以控制程式 hello 讀取 tooanother 複本，通常在 hello 輕鬆地補償遺失任何給定資料分割的一個複本相同資料中心。

**資料耐久性**

在寫入作業內容經過永久認可的 tooat 至少兩個資料中心之前 tooit 接受通知。 這是第一次認可 hello 寫 hello 主要，然後立即複寫 hello 寫入 tooat 至少一個其他資料中心。 如此可確保發生災難性的損失的 hello 資料中心裝載 hello 主要並不會導致資料遺失的可能性。

Azure AD 會維護一個零[復原時間目標 (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective)權杖發行和目錄讀取，並依照 hello 分鐘 （5 分鐘） RTO 目錄的寫入。 我們也會維持零[復原點目標 (RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective) 且在容錯移轉時不會遺失資料。

### <a name="data-centers"></a>資料中心

Azure AD 的複本會儲存在位於 hello 全球資料中心。 如需詳細資訊，請參閱 [Azure 資料中心](https://azure.microsoft.com/en-us/overview/datacenters)。

Azure AD 運作方式跨資料中心以 hello 下列特性：

 * 驗證、 圖形及其他 AD 服務位於背後 hello 閘道服務。 hello 閘道管理這些服務的負載平衡。 如果使用交易健康狀態探查偵測到任何狀況不良的伺服器，它就會自動容錯移轉。 根據這些健全狀況探查，hello 閘道動態路由傳送流量 toohealthy 資料中心。
 * 如*讀取*，hello 目錄已在多個資料中心操作主動-主動組態中的次要複本與對應的前端服務。 失敗時的整個資料中心，流量將會自動路由的 tooa 不同資料中心。
 *  如*寫入*，hello 目錄將會容錯移轉主要 （主要） 複本跨資料中心，透過計劃 （新的主要複本是主要的同步處理的 tooold） 或緊急容錯移轉程序。 資料持久性達成複寫任何認可 tooat 至少兩個資料中心。

**資料一致性**

最終一致性的其中一個 hello 目錄模型。 以非同步方式複寫的分散式系統一個典型問題是 hello 「 特定 」 複本所傳回的資料可能不是向上 toodate。 

Azure AD 提供應用程式的路由它寫入 toohello 的主要複本，目標次要複本的讀寫一致性，並以同步方式提取 hello 寫回 toohello 次要複本。

應用程式寫入使用 Graph API 的 Azure AD 會維護親和性 tooa 目錄複本的讀寫一致性抽象的 hello。 hello Azure AD Graph 服務會維護具有親和性 tooa 次要複本用於讀取; 的邏輯工作階段親和性的 「 複本語彙基元"hello 圖形服務快取使用分散式快取中擷取。 這個語彙基元接著用於後續作業 hello 相同邏輯工作階段。 

 >[!NOTE]
 >立即複寫寫入發出 toohello 次要複本 toowhich hello 邏輯工作階段的讀取。
 >

**備份保護**

hello 目錄實作非永久性刪除，而不是對使用者以及簡單復原發生意外刪除客戶的租用戶的永久刪除。 如果您的租用戶管理員意外刪除使用者，他們就可以輕鬆地復原，並還原 hello 刪除使用者。 

Azure AD 會實作所有資料的每日備份，因此可以在任何邏輯刪除或損毀的情況下可靠地還原資料。 我們的資料層會運用錯誤修正碼，以便檢查有錯誤並自動更正特定類型的磁碟錯誤。

**計量和監視**

執行高可用性服務需要世界級的計量和監視功能。 Azure AD 會持續分析及報告其每項服務的重要服務健康狀態計量和成功準則。 我們會持續開發並微調計量，以及監視與警示每項 Azure AD 服務及所有服務內的每個案例。

如果任何 Azure AD 服務無法如預期般運作，我們立即採取動作 toorestore 功能盡快。 hello 最重要的度量 Azure AD 的曲目就是我們，速度偵測和降低客戶或即時網站問題。 我們投入大量中監視和警示 toominimize 時間 toodetect (TTD 目標： < 5 分鐘) 和操作整備 toominimize 時間 toomitigate (TTM 目標： < 30 分鐘)。

**安全作業**

我們會運用任何作業的作業控制項 (例如 Multi-Factor Authentication (MFA))，以及稽核所有的作業。 此外，任何操作工作以隨持續不斷上針對使用中 just-in-time 提高權限系統 toogrant 需暫存的存取權。 如需詳細資訊，請參閱[hello 信任雲端](https://azure.microsoft.com/en-us/support/trust-center)。

## <a name="next-steps"></a>後續步驟
[Azure Active Directory 開發人員指南](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

