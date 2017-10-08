---
title: "資料庫待用加密：Azure Cosmos DB | Microsoft Docs"
description: "了解 Azure Cosmos DB 如何提供所有資料的預設加密。"
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Azure Cosmos DB 資料庫待用加密

靜態加密是片語時，通常是指 toohello 加密非動態儲存裝置上的資料，例如固態磁碟機 (Ssd) 和硬碟 (Hdd)。 Cosmos DB 會在 SSD 上儲存其主要資料庫。 其媒體附件和備份會儲存在通常由 HDD 備份的 Azure Blob 儲存體中。 Hello Cosmos db 靜止的加密版本會加密所有您的資料庫、 媒體附件和備份。 您的資料現在在傳輸過程中加密 （透過 hello 網路），並在靜止 （靜態儲存體），讓您端對端加密。

您可以非常輕易 toouse PaaS 服務，Cosmos DB 原狀。 因為儲存 Cosmos DB 中的所有使用者資料已都加密待用和傳輸中，您不需要 tootake 任何動作。 這是在加密的另一個方式 tooput 其餘部分是 「 on 」 預設。 不有任何控制項 tooturn 它關閉或開啟。 我們會提供這項功能，我們會持續 toomeet 我們[效能和可用性的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db)。

## <a name="implement-encryption-at-rest"></a>實作待用加密

待用加密是使用數種安全性技術來實作的，這些技術包括安全金鑰儲存體系統、加密的網路，以及密碼編譯 API。 解密及處理資料的系統有 toocommunicate 的系統管理金鑰。 hello 圖表會顯示儲存體加密的資料與 hello 管理的索引鍵分隔的方式。 

![設計圖表](./media/database-encryption-at-rest/design-diagram.png)

使用者要求的 hello 基本流程如下所示：
- hello 使用者資料庫的帳戶會成為準備好，並透過要求 toohello 管理服務資源提供者擷取儲存體金鑰。
- 使用者建立透過 HTTPS/安全傳輸的連線 tooCosmos DB。 （Sdk 抽象 hello 詳細資料的 hello）。
- hello 使用者傳送 JSON 文件 toobe 儲存一段 hello 先前建立安全連線。
- hello JSON 文件會編製索引，除非 hello 使用者已關閉的索引。
- Hello JSON 文件和索引資料會寫入 toosecure 儲存體。
- 定期從 hello 安全儲存體讀取資料及備份 toohello Azure 加密 Blob 存放區。

## <a name="frequently-asked-questions"></a>常見問題集

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>問︰如果已啟用儲存體服務加密，Azure 儲存體的成本會多出多少？
答：沒有任何額外成本。

### <a name="q-who-manages-hello-encryption-keys"></a>問： 誰管理 hello 加密金鑰？
答： hello 金鑰是由 Microsoft 管理。

### <a name="q-how-often-are-encryption-keys-rotated"></a>問︰加密金鑰多久輪替一次？
答：Microsoft 針對加密金鑰輪替有一套 Cosmos DB 會遵循的內部方針。 不會發行 hello 的特定指導方針。 Microsoft 並未發行 hello[安全性開發週期 (SDL)](https://www.microsoft.com/sdl/default.aspx)，被視為是子集內部的指引以及開發人員已經很有用的最佳作法。

### <a name="q-can-i-use-my-own-encryption-keys"></a>問︰我是否可以使用自己的加密金鑰？
答： cosmos DB 是 PaaS 服務，且我們致力硬 tookeep hello 服務簡單 toouse。 我們注意到會詢問此問題的使用者，通常是想詢問有關符合如 PCI-DSS 等合規性需求的 Proxy 問題。 建立這項功能的一部分，我們致力與相容性稽核員 tooensure 使用 Cosmos DB 客戶符合其需求沒有 hello 需要 toomanage 金鑰本身。
如此一來，我們目前不提供使用者 hello 選項 tooburden 本身與金鑰管理。

### <a name="q-what-regions-have-encryption-turned-on"></a>問：有哪些區域已開啟加密？
答：所有的 Azure Cosmos DB 區域皆已針對所有使用者資料開啟加密。

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>問： 沒有加密會影響 hello 效能延遲和輸送量的 Sla 嗎？
答： 沒有任何影響或變更 toohello 效能 Sla 現在，所有現有和新的帳戶已啟用靜態加密。 閱讀更多在 hello [SLA Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db)頁面 toosee hello 最新的保證。

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>問： hello 本機模擬器，可支援靜態加密？
答： hello 模擬器是獨立的開發/測試工具，並不會使用 hello hello managed 的 Cosmos DB 服務所使用的金鑰管理服務。 我們建議您儲存機密模擬器測試資料的磁碟機上的 tooenable BitLocker。 hello[模擬器支援將變更 hello 預設資料目錄](local-emulator.md)也可使用的已知位置。

## <a name="next-steps"></a>後續步驟

如需 Cosmos DB 安全性和 hello 最新的增強功能的概觀，請參閱[Azure Cosmos DB 資料庫安全性](database-security.md)。
如需有關 Microsoft 認證的詳細資訊，請參閱 hello [Azure 信任中心](https://azure.microsoft.com/en-us/support/trust-center/)。
