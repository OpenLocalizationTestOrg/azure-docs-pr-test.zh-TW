---
title: "Azure 資料庫的 MySQL 關聯式資料庫服務的 aaaOverview |Microsoft 文件"
description: "Hello Azure 資料庫的 MySQL 關聯式資料庫服務的概觀。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>什麼是 Azure Database for MySQL？ 服務簡介
Azure 的 MySQL 資料庫是關聯式資料庫中的服務 hello 為基礎的 Microsoft 雲端[MySQL Community Edition](https://www.mysql.com/products/community/)資料庫引擎。  Azure Database for MySQL 提供：

- 多個服務層級的可預測效能
- 零應用程式停機的動態延展性
- 內建高可用性
- 資料保護

這些功能幾乎不需要管理，而且免費提供。 它們可讓您快速的應用程式開發和加速您的時間 toomarket，而不是配置寶貴的時間和資源 toomanaging 虛擬機器和基礎結構上 toofocus。 此外，您可以繼續的 toodevelop hello 的應用程式開啟原始碼工具和您選擇的平台，並傳遞的 「 hello 速度與效率，您的商業需求而不需要新技能，toolearn。

![Azure Database for MySQL 概念圖](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

本文是簡介 tooAzure 資料庫的 MySQL 核心概念和功能相關的 tooperformance、 延展性及管理能力、 連結 tooexplore 詳細資料。 這些快速開始的 tooget 您一開始，請參閱：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](quickstart-create-mysql-server-database-using-azure-cli.md)

如需一組 Azure CLI 範例，請參閱︰
- [Azure Database for MySQL 的 Azuer CLI 範例](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>無須停機即可調整效能和規模
Azure Database for MySQL 目前提供兩個服務層︰基本和標準。 每一層提供不同的效能和功能 toosupport tooheavyweight 輕量型資料庫工作負載。 您可以建立第一個應用程式上的小型資料庫數美元的月份，然後變更與您服務層 tooscale 需要您的方案不需停機。 動態擴充性可讓您變更的資源需求的資料庫 tootransparently 回應 toorapidly。 您只需支付 hello 資源時，您需要您需要的時候。

## <a name="monitoring-and-alerting"></a>監視和警示
當您撥向上和向下如何知道 hello 以滑鼠右鍵按一下 停止？ 使用 hello 內建的效能監視和警示功能，結合 hello 效能評等，根據計算的單位。 使用這些功能，您可以迅速瞭解的向上或向下調整根據您目前的 hello 影響或專案的效能需求。 如需詳細資訊，請參閱[概念︰服務層](concepts-service-tiers.md)。

## <a name="keep-your-app-and-business-running"></a>讓您的應用程式和業務持續運作
Azure 領先業界的 99.99% 可用性服務等級協定 (SLA) (由 Microsoft 管理之資料中心的全球網路提供支援)，可協助讓您的應用程式 24 小時全年無休地運作。 使用每個 Azure 資料庫的 MySQL 伺服器時，您利用內建的安全性及容錯功能，您原本必須另外 toobuy 或設計、 建置及管理的資料保護。 使用 MySQL 的 Azure 資料庫，您可以使用時間點還原 toorecover 伺服器 tooan 先前狀態時，早 35 天。

## <a name="secure-your-data"></a>保護您的資料
Azure 資料庫服務一向重視資料安全性，Azure Database for MySQL 以限制存取、保護靜止和移動中資料及協助監視活動等功能承襲了這項傳統。 請瀏覽 hello [Azure 信任中心](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx)如需有關 Azure 平台安全性資訊。

hello Azure 資料庫的 MySQL 服務會使用儲存體加密的資料在 rest。 包括備份資料會加密磁碟上 （執行查詢時，由 hello 引擎建立的暫存檔的 hello 例外狀況）。 hello 服務使用隨附於 Azure 儲存體加密的 AES 256 位元加密，且 hello 索引鍵是受管理的系統。 儲存體加密會一律啟用，且無法停用。

根據預設，hello Azure 資料庫的 MySQL 服務設定的 toorequire [SSL 連線安全性](./concepts-ssl-connection-security.md)資料中動態 hello 網路上的。 強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。  （選擇性） 您可以停用來連接 tooyour 資料庫服務，如果用戶端應用程式不支援的 SSL 連線需要 SSL。

## <a name="next-steps"></a>後續步驟
現在，您已閱讀 MySQL 簡介 tooAzure 資料庫，並回答 hello 問題 「 什麼是 Azure 的 MySQL 資料庫？ 」，您可以：
- 請參閱定價頁面成本比較和計算機 hello。 [價格](https://azure.microsoft.com/pricing/details/mysql/)
- 從建立您的第一部伺服器開始。 [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](quickstart-create-mysql-server-database-using-azure-portal.md)
- 建置您的第一個應用程式在 Python、 PHP、 Ruby、 C\#、 Java、 Node.js:[連接程式庫用於 MySQL 的 tooconnect tooAzure 資料庫](concepts-connection-libraries.md)
