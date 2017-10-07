---
title: "常見連接問題 tooAzure aaaTroubleshoot SQL 資料庫"
description: "步驟 tooidentify 並解決常見連接錯誤 for Azure SQL Database。"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>疑難排解連接問題 tooAzure SQL 資料庫
Hello 連接 tooAzure SQL 資料庫失敗時，您會收到[錯誤訊息](sql-database-develop-error-messages.md)。 本文是集中式主題，可協助您針對 Azure SQL Database 連線問題進行疑難排解。 它會導致[hello 常見原因](#cause)連線問題的建議[疑難排解工具](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues)，它可協助您識別 hello 問題，並提供疑難排解步驟 toosolve [暫時性錯誤](#troubleshoot-transient-errors)和[永續性或非暫時性錯誤](#troubleshoot-persistent-errors)。 

如果您遇到 hello 連線問題，請嘗試 hello 疑難排解這篇文章所述的步驟。
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>原因
連線問題可能被因 hello 下列任何一項：

* 失敗 tooapply 最佳作法和設計指導方針 hello 應用程式在設計程序。  請參閱[SQL Database 開發概觀](sql-database-develop-overview.md)tooget 啟動。
* Azure SQL Database 重新設定
* 防火牆設定
* 連線逾時
* 不正確的登入資訊
* 部分 Azure SQL Database 資源已達上限

一般而言，SQL Database 的連接問題 tooAzure 可分類如下：

* [暫時性錯誤 (短期或間歇性)](#troubleshoot-transient-errors)
* [持續性或非暫時性錯誤 (定期重複發生的錯誤)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>再試一次 hello Azure SQL Database 連線問題疑難排解
如果您遇到特定的連線錯誤，請嘗試使用 [此工具](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)，此工具可協助您快速識別並解決您的問題。

## <a name="troubleshoot-transient-errors"></a>針對暫時性錯誤進行疑難排解

當應用程式連接 tooan Azure SQL database 時，您會收到下列錯誤訊息的 hello:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> 此錯誤訊息是通常是暫時性 (短期)。
> 
> 

這個錯誤發生在 hello Azure 資料庫正要移動 （或重新設定） 和您的應用程式將會遺失其連線 toohello SQL 資料庫。 SQL Database 重新設定事件由於規劃的事件 (例如，軟體升級) 或未規劃的事件 (例如，處理序損毀或負載平衡) 而發生。 大部分的重新設定事件通常只是短期的，至多應在不到 60 秒的時間完成。 不過，這些事件可能偶爾會需要較長的 toofinish，例如大型交易何時會導致長時間執行復原。

### <a name="steps-tooresolve-transient-connectivity-issues"></a>步驟 tooresolve 暫時性連線問題

1. 檢查 hello [Microsoft Azure 服務儀表板](https://azure.microsoft.com/status)的 hello 時間期間的 hello hello 應用程式所報告錯誤期間發生任何已知中斷。
2. 連接 tooa 雲端服務，例如 Azure SQL Database 應該預期會定期重新設定事件，並實作應用程式會重試邏輯 toohandle 而不是為應用程式錯誤 toousers 面對這些錯誤。 檢閱 hello[暫時性錯誤](sql-database-connectivity-issues.md)區段和 hello 的最佳作法和設計指導方針，在[SQL Database 開發概觀](sql-database-develop-overview.md)如需詳細資訊和一般重試策略。 如需詳細資訊，請接著參閱 [適用於 SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md) 的程式碼範例 。
3. 資料庫接近其資源限制，它看起來令 toobe 暫時性連線問題。 請參閱 [移難排解效能問題](sql-database-troubleshoot-performance.md)。
4. 如果連線問題仍然存在，或如果 hello 您的應用程式，在遇到 hello 錯誤的持續時間超過 60 秒，或您看到某一天中的 hello 錯誤的多個項目，請選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options)站台。

## <a name="troubleshoot-persistent-errors"></a>針對持續性錯誤進行疑難排解
如果 hello 應用程式持續失敗 tooconnect tooAzure SQL 資料庫，通常表示 hello 下列其中一種問題：

* 防火牆組態。 hello Azure SQL 資料庫或用戶端防火牆封鎖連線 tooAzure SQL 資料庫。
* 網路 hello 用戶端上的重新設定： 例如，新的 IP 位址或 proxy 伺服器。
* 使用者錯誤： 例如，輸入連線參數，例如 hello hello 連接字串中的伺服器名稱不正確。

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>步驟 tooresolve 持續性連線問題
1. 設定[防火牆規則](sql-database-configure-firewall-settings.md)tooallow hello 用戶端 IP 位址。 為暫存限測試用途，設定為 起始 IP 位址範圍，並使用 hello 結束 IP 位址範圍為 255.255.255.255 hello 使用 0.0.0.0 的防火牆規則。 這會開啟 hello 伺服器 tooall IP 位址。 若這樣可解決您的連線問題，請移除此規則並針對已適當限制的 IP 位址或位址範圍建立防火牆規則。 
2. 在 hello 用戶端與 hello 網際網路之間的所有防火牆，請確定連接埠 1433年是開啟傳出連接。 檢閱[設定 hello SQL Server 存取的 Windows 防火牆 tooAllow](https://msdn.microsoft.com/library/cc646023.aspx)和[混合式身分識別所需的連接埠和通訊協定](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports)是否有其他指標相關 tooadditional 連接埠，您需要的 tooopenAzure Active Directory 驗證。
3. 請確認您的連接字串和其他連線設定。 請參閱 hello 連接字串 > 一節中 hello[連線問題主題](sql-database-connectivity-issues.md#connections-to-azure-sql-database)。
4. 檢查 hello 儀表板中的服務健全狀況。 如果您認為沒有地區中斷，請參閱[從中斷復原](sql-database-disaster-recovery.md)步驟 toorecover tooa 新的區域。

## <a name="next-steps"></a>後續步驟
* [針對 Azure SQL Database 效能問題進行疑難排解](sql-database-troubleshoot-performance.md)
* [Microsoft Azure 上搜尋 hello 文件](http://azure.microsoft.com/search/documentation/)
* [檢視 hello 最新更新 toohello Azure SQL Database 服務](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>其他資源
* [SQL Database 開發概觀](sql-database-develop-overview.md)
* [一般暫時性錯誤處理指引](../best-practices-retry-general.md)
* [SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md)

