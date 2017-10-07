---
title: "aaaAzure 資料庫安全性檢查清單 |Microsoft 文件"
description: "本文提供一組 Azure 資料庫安全性的檢查清單。"
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Azure 資料庫安全性檢查清單

toohelp 改善安全性，Azure 資料庫包含數個內建的安全性控制，您可以使用 toolimit 和控制的存取。

其中包含：

-   防火牆可讓您 toocreate[防火牆規則](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure)依 IP 位址限制的連線
-   可從 hello Azure 入口網站存取的伺服器層級防火牆
-   可從 SSMS 存取的資料庫層級防火牆規則
-   使用安全的連接字串的安全連線 tooyour 資料庫
-   使用存取管理
-   資料加密
-   SQL Database 稽核
-   SQL Database 威脅偵測

## <a name="introduction"></a>簡介
雲端運算需要為不熟悉 toomany 應用程式使用者、 資料庫管理員和程式設計人員的新安全性架構。 如此一來，某些組織會因為遲疑 tooimplement 雲端基礎結構進行資料管理，因為 tooperceived 安全性風險。 不過，大部分的這個問題可以減輕透過內建於 Microsoft Azure 和 Microsoft Azure SQL Database 的 hello 安全性功能的進一步了解。

## <a name="checklist"></a>檢查清單
我們建議您先閱讀 hello [Azure 資料庫的安全性最佳作法](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices)文章先前 tooreviewing 這份檢查清單。 您了解 hello 最佳作法之後，您就可以充分利用這份檢查清單可以 tooget hello。 然後，您可以使用此檢查清單 toomake 確定您已在 Azure 資料庫安全性解決 hello 重要問題。


|檢查清單類別| 說明|
| ------------ | -------- |
|**保護資料**||
| <br> 移動/傳輸中加密| <ul><li>[傳輸層安全性](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol)，當資料移動 toohello 網路的資料加密。</li><li>資料庫需要從用戶端 hello 為基礎的安全通訊[TDS （表格式資料流）](https://msdn.microsoft.com/en-in/library/dd357628.aspx) 5060，TLS （傳輸層安全性） 的通訊協定。</li></ul> |
|<br>待用加密| <ul><li>[透明資料加密](http://go.microsoft.com/fwlink/?LinkId=526242)，適用於非作用中資料實際以任何數位形式儲存時。</li></ul>|
|**控制存取**||  
|<br> 資料庫存取 | <ul><li>[驗證](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Azure Active Directory 驗證) AD 驗證會使用由 Azure Active Directory 管理的身分識別。</li><li>[授權](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)授與使用者 hello 最低必要權限。</li></ul> |
|<br>應用程式存取| <ul><li>[資料列層級安全性](https://msdn.microsoft.com/library/dn765131)（使用安全性原則，在相同的時間限制的資料列層級存取根據使用者的身分識別、 角色或執行內容的 hello）。</li><li>[動態資料遮罩](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started)（使用的權限與原則，會限制機密資料暴露其 toonon 權限的使用者）</li></ul>|
|**主動式監視**||  
| <br>追蹤和偵測| <ul><li>[稽核](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing)追蹤資料庫事件，並將其寫入 tooan 稽核記錄檔 / 活動記錄檔您[Azure 儲存體帳戶](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account)。</li><li>使用 [Azure 監視器活動記錄](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)來追蹤 Azure 資料庫健康情況。</li><li>[威脅偵測](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection)偵測到潛在的安全性威脅 toohello 資料庫異常資料庫活動。 </li></ul> |
|<br>Azure 資訊安全中心| <ul><li>[資料監視](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) 使用 Azure 資訊安全中心作為 SQL 和其他 Azure 服務的集中式安全性監視解決方案。</li></ul>|     

## <a name="conclusion"></a>結論
Azure 資料庫是強固的資料庫平台，具有完整的安全性功能，能符合許多組織及法務相容性需求。 您可以輕鬆地保護資料，控制 tooyour hello 實體存取的資料，並提供資料安全性，在 hello 檔案-資料行，或資料列層級使用透明資料加密、 資料格層級加密或資料列層級安全性使用各種不同的選項。 永遠加密也可讓您操作對加密資料，簡化的應用程式更新的 hello 程序。 接著，存取 tooauditing 活動會提供您的需要可讓您存取資料的方式和時機的 tooknow hello 資訊的 SQL 資料庫記錄。

## <a name="next-steps"></a>後續步驟
您可以改善 hello 保護您的資料庫在對惡意使用者或未經授權的存取，執行幾個簡單的步驟。 您會在本教學課程中學到：

- 設定伺服器和/或資料庫的[防火牆規則](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure)。
- 使用[加密](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption)來保護您的資料。
- 啟用 [SQL Database 稽核](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing)。

