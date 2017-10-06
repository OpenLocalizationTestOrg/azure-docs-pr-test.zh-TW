---
title: "PostgreSQL 關聯式資料庫服務的 Azure 資料庫 aaaOverview |Microsoft 文件"
description: "提供 Azure Database for PostgreSQL 關聯式資料庫服務的概觀。"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>什麼是 Azure Database for PostgreSQL？

Azure PostgreSQL 資料庫是關聯式資料庫中的服務 hello 以開放原始碼的 hello community 版本為基礎的開發人員建置 Microsoft 雲端[PostgreSQL](https://www.postgresql.org/)資料庫引擎。 此服務目前為公開預覽狀態。 Azure Database for PostgreSQL 提供：
- 多個服務層級的可預測效能
- 零應用程式停機的動態延展性
- 內建高可用性
- 資料保護

上述所有功能幾乎不需要管理，而且免費提供。 這些功能可讓您快速應用程式開發和加速您的時間 toomarket，而不是配置寶貴的時間和資源 toomanaging 虛擬機器和基礎結構上 toofocus。 此外，您可以繼續的 toodevelop hello 的應用程式開啟原始碼工具和您選擇的平台，並傳遞的 「 hello 速度與效率，您的商業需求而不需要新技能，toolearn。 

這篇文章是針對 PostgreSQL 核心概念和功能相關的 tooperformance、 延展性及管理性簡介 tooAzure 資料庫。 這些快速開始的 tooget 您一開始，請參閱：

- [使用 Azure 入口網站建立 Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)
- [建立 Azure 資料庫，使用 Azure CLI hello PostgreSQL](quickstart-create-server-database-azure-cli.md)

如需一組 Azure CLI 和 PowerShell 範例，請參閱︰

- [Azure Database for PostgreSQL 的 Azuer CLI 範例](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>無須停機即可調整效能和規模

Azure Database for PostgreSQL 目前提供兩個服務層︰基本和標準。 每個服務層提供[不同層級的效能、 IOPS 保證和功能](concepts-service-tiers.md)toosupport tooheavyweight 輕量型資料庫工作負載。 您可以為一個月的幾個 bucks 小型的伺服器上建置您的第一個應用程式，然後[變更 hello 效能層級](scripts/sample-scale-server-up-or-down.md)服務內層手動或以程式設計方式在您的方案的任何時間 toomeet hello 需求。 您可以不需要停機時間 tooyour 應用程式或 tooyour 客戶。 動態擴充性可讓資料庫 tootransparently 回應 toorapidly 資源需求，並可讓您 tooonly 支付 hello 的資源，您需要在需要時變更。

## <a name="monitoring-and-alerting"></a>監視和警示
您如何決定何時上下 toodial？ 您可以使用 hello 內建的效能監視和警示功能，結合 hello 效能評等，根據計算的單位。 您使用這些工具，迅速瞭解 hello 影響計算的單位向上或向下根據您的目前或規劃效能需求。 如需詳細資訊，請參閱 [Azure Database for PostgreSQL 選項和效能：了解每個服務層中可用的項目](./concepts-service-tiers.md)。

## <a name="keep-your-app-and-business-running"></a>讓您的應用程式和業務持續運作
Azure 領先業界的 99.99% 可用性 (不是預覽狀態) 服務等級協定 (SLA) (由 Microsoft 管理之資料中心的全球網路提供支援)，可協助讓您的應用程式 24 小時全年無休地運作。 使用每個 Azure 資料庫 PostgreSQL 伺服器時，您利用內建的安全性及容錯功能，您原本必須另外 toobuy 或設計、 建置及管理的資料保護。 PostgreSQL 的 Azure 資料庫，每個服務層提供一組完整的業務續航力功能和選項，您可以用 tooget 和執行使用並持續如此。 您可以使用[時間點還原](howto-restore-server-portal.md)tooreturn 資料庫 tooan 先前狀態時，早 35 天。 此外，如果裝載資料庫的 hello 資料中心發生中斷，您可以從最近的備份的異地備援複本還原資料庫。

## <a name="secure-your-data"></a>保護您的資料
Azure 資料庫服務一向重視資料安全性，Azure Database for PostgreSQL 以限制存取、保護靜止和移動中資料及協助監視活動等功能承襲了這項傳統。 請瀏覽 hello [Azure 信任中心](https://www.microsoft.com/TrustCenter/Security/default.aspx)如需有關 Azure 平台安全性資訊。

PostgreSQL 服務的 hello Azure 資料庫的資料在 rest 使用儲存體加密。 包括備份資料會加密磁碟上 （執行查詢時，由 hello 引擎建立的暫存檔的 hello 例外狀況）。 hello 服務使用隨附於 Azure 儲存體加密的 AES 256 位元加密，且 hello 索引鍵是受管理的系統。 儲存體加密會一律啟用，且無法停用。

根據預設，hello Azure Database PostgreSQL 服務是設定的 toorequire [SSL 連線安全性](./concepts-ssl-connection-security.md)資料中動態 hello 網路上的。 強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。  （選擇性） 您可以停用來連接 tooyour 資料庫服務，如果用戶端應用程式不支援的 SSL 連線需要 SSL。

## <a name="next-steps"></a>後續步驟
- 請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/postgresql/)成本比較和計算機。
- 從[建立您的第一個 Azure Database for PostgreSQL](./quickstart-create-server-database-portal.md) 開始。
- 使用 Python、PHP、Ruby、C\#、Java、Node.js 建立您的第一個應用程式：[連線庫](./concepts-connection-libraries.md)
