---
title: "aaaDatabase 安全性-Azure Cosmos DB |Microsoft 文件"
description: "了解 Azure Cosmos DB 如何為您的資料提供資料庫保護和資料安全性。"
keywords: "nosql 資料庫安全性, 資訊安全性, 資料安全性, 資料庫加密, 資料庫保護, 安全性原則, 安全性測試"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Azure Cosmos DB 資料庫安全性

本文將討論資料庫安全性最佳作法，以及所 Azure Cosmos DB toohelp 您防止、 偵測，並回應 toodatabase 漏洞提供的重要功能。
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Azure Cosmos DB 安全性有哪些新功能？

儲存在所有 Azure 區域之 Azure Cosmos DB 中的文件和備份現在可以使用待用加密。 這些區域內的新舊客戶都會自動套用加密靜止功能。 沒有任何需要 tooconfigure 兩件事：收到 hello 相同的絕佳延遲、 輸送量、 可用性和功能之前 hello 優點知道您的資料是安全及安全與靜態加密。

## <a name="how-do-i-secure-my-database"></a>如何保護我的資料庫？ 

資料安全性是您、 hello 客戶和您的資料庫提供者之間共同的責任。 根據您選擇的 hello 資料庫提供者，當您執行的責任的 hello 數量而有所不同。 如果您選擇在內部部署方案時，您需要 tooprovide 端點保護 toophysical 的安全性，您的硬體-並不容易從所有項目。 如果您選擇 PaaS 雲端資料庫提供者，例如 Azure Cosmos DB，您關切的領域會大幅縮小。 下列映像，從 Microsoft 的借用 hello[共用責任雲端運算](https://aka.ms/sharedresponsibility)技術白皮書： 顯示您的責任則會減少使用像是 Azure Cosmos DB PaaS 提供者。

![客戶和資料庫提供者的責任](./media/database-security/nosql-database-security-responsibilities.png)

hello 上述圖表顯示高階的雲端安全性元件，但項目您需要有關 tooworry 特別為您的資料庫方案嗎？ 和您要如何比較解決方案 tooeach 其他嗎？ 

我們建議您遵循哪些 toocompare 資料庫系統的需求檢查清單的 hello:

- 網路安全性和防火牆設定
- 使用者驗證和細微的使用者控制
- 全域區域的失敗的能力 tooreplicate 資料
- 能力 tooperform 容錯移轉，從一個資料中心 tooanother
- 在資料中心內的區域資料複寫
- 自動資料備份
- 從備份中還原已刪除的資料
- 保護並隔離機密資料
- 監視攻擊
- 回應 tooattacks
- 能力 toogeo 圍欄資料 tooadhere toodata 控管限制
- 實際保護受保護資料中心內的伺服器

而即使看起來好像很明顯，最近[大規模資料庫漏洞](http://thehackernews.com/2017/01/mongodb-database-security.html)提醒我們 hello 簡單但重要的重要性，hello 下列需求：
- 修補會維持 toodate 最新狀態的伺服器
- 預設為 HTTPS/SSL 加密
- 使用強式密碼的系統管理帳戶

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Azure Cosmos DB 如何保護我的資料庫？

讓我們看看 hello 前面清單中的 上一步-多少的這些安全性需求 Azure Cosmos 資料庫提供？ 每一個。

讓我們詳細探究每一個。

|安全性需求|Azure Cosmos DB 的安全性方法|
|---|---|---|
|網路安全性|使用 IP 防火牆是 hello 第一層的保護 toosecure 您的資料庫。 Azure Cosmos DB 支援原則驅動的 IP 型存取控制，以提供輸入防火牆支援。 hello IP 為基礎的存取控制項所使用的傳統資料庫系統的類似 toohello 防火牆規則，但是它們會展開 Azure Cosmos DB 資料庫帳戶才可存取從機器或雲端服務的核准設定組。 <br><br>Azure Cosmos DB 可讓您 tooenable 特定的 IP 位址 (168.61.48.0)，IP 範圍 (168.61.48.0/8) 及 Ip 和範圍的組合。 <br><br>Azure Cosmos DB 會封鎖此允許清單之外的機器發出的所有要求。 來自要求核准的電腦，且雲端服務然後必須完成 hello 驗證程序 toobe 提供存取控制 toohello 資源。<br><br>深入了解 [Azure Cosmos DB 防火牆支援](firewall-support.md)。|
|Authorization|Azure Cosmos DB 使用雜湊式訊息驗證碼 (HMAC) 來進行授權。 <br><br>每個要求會使用 hello 密碼的帳戶金鑰，雜湊，並與每個呼叫 tooAzure Cosmos DB 傳送 hello 後續 base 64 編碼的雜湊。 hello Azure Cosmos DB 服務會使用 hello 正確的密碼金鑰和內容 toogenerate 雜湊，則它會比較以 hello 要求一個 hello hello 值要求 toovalidate hello。 如果 hello 兩個值相符，hello 作業已獲授權已成功處理 hello 要求，否則沒有授權失敗而 hello 要求遭到拒絕。<br><br>您可以使用[主要金鑰](secure-access-to-data.md#master-keys)，或[資源語彙基元](secure-access-to-data.md#resource-tokens)允許更細緻的存取 tooa 資源，例如文件。<br><br>進一步了解[保護存取 tooAzure Cosmos DB 資源](secure-access-to-data.md)。|
|使用者和權限|使用 hello[主要金鑰](#master-key)hello 帳戶，您可以建立使用者資源與每個資料庫的權限資源。 A[資源語彙基元](#resource-token)相關聯的資料庫中的權限，並判斷 hello 使用者是否具有存取 （讀寫，唯讀的或沒有存取權） tooan hello 資料庫中的應用程式資源。 應用程式資源包括集合、文件、附件、預存程序、觸發程序和 UDF。 然後驗證 tooprovide 期間使用或拒絕存取 toohello 資源 hello 資源語彙基元。<br><br>進一步了解[保護存取 tooAzure Cosmos DB 資源](secure-access-to-data.md)。|
|Azure 目錄整合 (RBAC)| 本表 hello 螢幕擷取畫面所示，您也可以提供存取 toohello 資料庫帳戶 hello Azure 入口網站中使用存取控制 (IAM)。 IAM 提供角色型存取控制，並與 Active Directory 整合。 您可以使用內建的角色或自訂的角色的個人或群組 hello 下列影像所示。|
|全球複寫|Azure Cosmos DB 會提供周全的通用散發，這可讓您 tooreplicate hello 與 Azure 的全球資料中心的其中一個按鈕的按一下您資料 tooany。 全域複寫可讓您全域調整及提供低延遲存取 tooyour hello 世界各地的資料。<br><br>在 hello 內容中的安全性，全域複寫，請確保地區故障的資料保護。<br><br>請參閱[將資料分散到全球](distribute-data-globally.md)以深入了解。|
|區域性容錯移轉|如果您已將資料複寫至多個資料中心，萬一某個區域資料中心離線，Azure Cosmos DB 會自動轉移您的作業。 您可以建立使用您的資料會複寫所在的 hello 區域的容錯移轉地區的優先順序的清單。 <br><br>請參閱 [Azure Cosmos DB 的區域性容錯移轉](regional-failover.md)以深入了解。|
|區域複寫|即使在單一資料中心中，Azure Cosmos DB 自動複寫資料對於高可用性提供 hello 選擇[一致性層級](consistency-levels.md)。 這樣可保證  [99.99% 執行時間可用性 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db)，同時帶來財務保證 - 其他任何資料庫服務都沒有這種能力。|
|自動化線上備份|Azure Cosmos DB 資料庫會定期備份，並儲存在異地備援存放區。 <br><br>請參閱[使用 Azure Cosmos DB 進行自動線上備份及還原](online-backup-and-restore.md)以深入了解。|
|還原已刪除的資料|hello 自動化的線上備份可以使用的 toorecover 資料，您可能會不小心刪除向上太 ~ hello 事件之後的 30 天。 <br><br>請參閱[使用 Azure Cosmos DB 進行自動線上備份及還原](online-backup-and-restore.md)以深入了解|
|保護並隔離機密資料|中所列的 hello 區域中的所有資料[最新消息？](#whats-new)現在會加密在靜止。<br><br>PII 和其他機密資料，可以是隔離的 toospecific 集合和讀寫或唯讀存取權可以是有限的 toospecific 使用者。|
|監視攻擊|您可以使用稽核記錄和活動記錄，以監視帳戶的正常和異常活動。 您可以檢視您的資源，hello 作業發生時 hello 狀態 hello 作業，以及更如本表格後的 hello 螢幕擷取畫面所示，起始 hello 作業上執行哪些作業。|
|回應 tooattacks|一旦您連絡 Azure 支援 tooreport 潛在的攻擊時，會開始 5 步驟事件回應程序。 hello 目標 hello 5 步驟的程序會盡快是 toorestore 一般服務的安全性和作業之後在偵測到的問題並進行調查，已啟動。<br><br>進一步了解[hello 雲端中的 Microsoft Azure 安全性回應](https://aka.ms/securityresponsepaper)。|
|異地隔離|Azure Cosmos DB 可確保主權區域 (例如，德國、中國、US Gov) 的資料控管和合規性。|
|受保護的設施|Azure Cosmos DB 中的資料儲存在 Azure 受保護資料中心內的 SSD 上。<br><br>請參閱 [Microsoft 全球資料中心](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)以深入了解|
|HTTPS/SSL/TLS 加密|用戶端對服務的所有 Azure Cosmos DB 互動都強制使用 SSL/TLS 1.2。 此外，資料中心內和跨資料中心的所有複寫也都強制使用 SSL/TLS 1.2。|
|待用加密|所有儲存至 Azure Cosmos DB 的資料都會進行待用加密。 若要深入了解，請參閱 [Azure Cosmos DB 待用加密](.\database-encryption-at-rest.md)|
|修補的伺服器|做為受管理的資料庫，Azure Cosmos DB 排除 hello 需要 toomanage 和修補程式伺服器，為您自動完成。|
|使用強式密碼的系統管理帳戶|它的硬碟 toobelieve 我們需要 toomention 這項需求，但某些競爭對手，不同於無法 toohave 系統管理員帳戶不含 Azure Cosmos DB 中的密碼。<br><br> 依預設已內建透過 SSL 和 HMAC 密碼型驗證的安全性。|
|安全性和資料保護認證|Azure Cosmos DB 已取得 [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001)、[歐盟資料隱私保護規範 (EUMC)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses) 和 [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) 認證。 還有其他認證在進行中。|

hello 下列螢幕擷取畫面顯示使用存取控制 (IAM) 的 Active directory 整合 (RBAC) 中的 hello Azure 入口網站：![在 hello Azure 入口網站-示範資料庫安全性存取控制 (IAM)](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

hello 下列螢幕擷取畫面顯示如何使用稽核記錄和活動記錄 toomonitor 您的帳戶：![活動記錄檔中的 Azure Cosmos DB](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>後續步驟

如需有關主要金鑰和資源語彙基元的詳細資訊，請參閱[保障存取 tooAzure Cosmos DB 資料](secure-access-to-data.md)。

如需 Microsoft 認證的詳細資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/)。
