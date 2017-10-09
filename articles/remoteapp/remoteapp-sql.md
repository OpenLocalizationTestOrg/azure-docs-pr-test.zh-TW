---
title: "Azure RemoteApp 使用 Azure aaaSQL |Microsoft 文件"
description: "深入了解如何 toouse SQL Azure 與 Azure RemoteApp。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure 搭配 Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

當客戶選擇 toohost 其 Windows 應用程式與 Azure RemoteApp 一起 hello 雲端中時，通常也會想要其資料到 hello 的 SQL server 等雲端的 toomigrate 整個雲端部署。 如此一來，任何使用 Azure RemoteApp 的裝置即可隨時存取整個雲端託管解決方案。 以下是連結和參考指南 toohelp 以及您使用此程序。  

## <a name="migrate-your-sql-data"></a>移轉 SQL 資料
開頭[移轉 SQL 資料庫的 SQL Server 資料庫 tooAzure](../sql-database/sql-database-cloud-migrate.md)。 

## <a name="configure-azure-remoteapp"></a>設定 Azure RemoteApp
在 Azure RemoteApp 中裝載 Windows 應用程式。 以下是非常高階的逐步說明：

1. 建立 hello [Azure RemoteApp 範本 VM](remoteapp-imageoptions.md)。 
2. Hello VM 上安裝所需的 hello 應用程式。
3. 設定 hello 應用程式，讓它連接 toohello SQL 資料庫並確認它運作。
4. Sysprep 和關機 hello VM。 擷取 VM 作為映像以便用於 Azure。 **注意：**您將需要 tooensure hello 應用程式是透過 hello sysprep 程序可以 tooretain hello DB 連線資訊。 如果 hello 應用程式無法 tooretain hello DB 連接資訊，您可能會想 hello 應用程式 toocheck tooengage hello 廠商我們要如何指定 hello 連接字串。
5. Hello 自訂映像匯入您的 Azure RemoteApp 程式庫選取 hello 適當地理位置位於您 SQL Azure 的部署。 
6. 部署在相同的資料中心做為 SQL Azure 部署使用上述範本 hello 和發行 hello 應用程式的 hello RemoteApp 集合。 部署 Azure RemoteApp 在 hello 與 SQL Azure 部署的相同資料中心可協助確保 hello 最快的連線速度和降低延遲。 

## <a name="app-and-sql-configuration-considerations"></a>應用程式和 SQL 組態考量：
RemoteApp 搭配使用 SQL Azure 時，有幾個點 tooconsider:

深入了解[tooconfigure Azure SQL 資料庫防火牆](../sql-database/sql-database-firewall-configure.md)。 摘錄 hello 發行項狀態從 「 一開始，所有存取 tooyour Azure SQL Database 伺服器 hello 防火牆封鎖。 在使用 Azure SQL Database 伺服器的順序 toobegin，您必須移 toohello 傳統入口網站，並指定一個或多個伺服器層級防火牆規則，讓存取 tooyour Azure SQL Database 伺服器。 使用 hello 防火牆規則 toospecify 的 IP 位址範圍從 hello 允許網際網路，而且 Azure 應用程式可以嘗試 tooconnect tooyour Azure SQL Database 伺服器 」。

此外，當電腦嘗試從網際網路 hello tooconnect tooyour 資料庫伺服器，hello 防火牆會檢查 hello 源自對 hello 整組伺服器層級的 hello 要求的 IP 位址 （如有必要） 和資料庫層級防火牆規則。 "Hello 要求 hello IP 位址是其中一個 hello hello 伺服器層級防火牆規則中指定的範圍內，如果 hello 連接授與 tooyour Azure SQL Database 伺服器。 」 」 因此，我們可以使用 IP 範圍，而不只是個別的來源 IP 位址。

請依照下列中的 hello 逐步解說指示[How to： 使用 hello Azure 入口網站的 SQL 資料庫上設定防火牆設定](../sql-database/sql-database-configure-firewall-settings.md)toospecify hello IP 範圍。 當您設定 hello SQL 防火牆規則時，請提供 hello hello 子網路指定 IP 範圍 hello Azure RemoteApp 集合。 這應該 hello ARA 伺服器 tooconnect toohello SQL DB 即使仍可讓它們將會有動態指派 IP 位址。

## <a name="troubleshooting"></a>疑難排解
如果遇到 hello 使用裝載於 Azure RemoteApp 連接 tooa SQL 用戶端應用程式的資料庫其中裝載於 Azure 或內部部署速度過慢可能有幾個原因為何。  

* 從裝置 tooAzure 的網路延遲性很高。 移動 toohello 最佳且最快的網路連線，您可以為達最佳效能。 使用[azurespeed.com](http://azurespeed.com/)一般工具 tootest 為您的裝置延遲 tooAzure 資料中心。  
* 在 Azure RemoteApp 中裝載的用戶端應用程式承受壓力。 選取不同的計費方案 (例如 Premium 計費) 會改善效能。 另一個訣竅是 toomonitor hello 資源正在使用您的應用程式： 在使用中的工作階段期間執行 ctrl alt 端點索引鍵序列將會啟動的 hello SAS 畫面上，選取 [工作管理員]，觀察您的應用程式的資源使用率。
* SQL Server 承受壓力或未最佳化。 遵循 SQL 疑難排解指引。 

