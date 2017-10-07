---
title: "Azure App Service 的 aaaBest 作法"
description: "了解 Azure App service 的最佳作法和疑難排解。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Azure App Service 的最佳作法
本文將摘要說明使用 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)的最佳作法。 

## <a name="colocation"></a>共置
當 Azure 資源撰寫的解決方案，例如 web 應用程式和資料庫位於不同區域 hello 效果可以如下 hello:

* 資源之間的通訊延遲更久
* 貨幣費用傳出資料傳輸跨區域上 hello [Azure 定價頁面](https://azure.microsoft.com/pricing/details/data-transfers)。

共置在 hello 相同的區域是最佳的 Azure 資源撰寫的 web 應用程式之類的解決方案，而且資料庫或儲存體帳戶使用 toohold 內容或資料。 當建立資源，您應該確定它們處於 hello 相同 Azure 地區，除非您有特定商務或設計為他們不 toobe 的原因。 您可以移動應用程式服務應用程式 toohello 利用 hello 資料庫與相同的區域[複製功能的應用程式服務](app-service-web-app-cloning-portal.md)目前適用於 Premium App Service 方案的應用程式。   

## <a name="memoryresources"></a>當應用程式耗用超出預期的記憶體時
當您注意到的應用程式耗用更多的記憶體比預期示透過監視程式或服務建議考慮 hello[應用程式服務自動修復功能](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites)。 Hello 自動修復功能的 hello 選項的其中一個所花費的記憶體臨界值為基礎的自訂動作。 從電子郵件通知 tooinvestigation 透過回收 hello 背景工作處理序的記憶體傾印 tooon 特別補救動作範圍 hello 頻譜。 自動修復可設定透過 web.config，並透過好記的使用者介面中的 hello 此部落格文章所述[應用程式服務支援站台擴充](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps)。   

## <a name="CPUresources"></a>當應用程式耗用超出預期的 CPU 時
透過監視所示，當您注意到的應用程式耗用的 CPU 越多超過預期，或發生重複 CPU 尖峰或服務的建議，請考慮向上或向外延展 hello 應用程式服務方案。 如果您的應用程式開發，向上擴充時，hello 唯一的選項，如果您的應用程式是無狀態、 縮放比例超出可讓您更多的彈性和小數位數可能會更高版本。 

如需「具狀態」與「無狀態」應用程式的相關資訊，請觀賞這段影片︰ [在 Microsoft Azure Web 應用程式上規劃可調整的端對端多層應用程式](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid)。 如需 App Service 調整和自動調整選項的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。  

## <a name="socketresources"></a>當通訊端資源耗盡時
耗盡對外 TCP 連線的一個常見原因是 hello 使用用戶端程式庫不是實作的 tooreuse TCP 連線，或更高的層級通訊協定，例如 HTTP 為 Keep-alive 不運用 hello 案例。 請檢閱每個 hello 文件庫中設定或在您的傳出連線的有效率地重複使用的程式碼中存取您 App Service 方案的 tooensure hello 應用程式所參考的 hello 文件。 也請遵循正確的建立和發行版本或清除 tooavoid 遺漏連線的 hello 程式庫文件指引。 這類用戶端程式庫調查時進行影響可能會降低透過向外延展 toomultiple 執行個體。  

## <a name="appbackup"></a>當您的應用程式備份啟動失敗時
hello 為何應用程式備份失敗的兩個最常見的原因： 無效的儲存體設定和無效的資料庫組態。 變更 toostorage 或資料庫資源或如何變更時，通常會發生這些失敗 tooaccess 這些資源 （例如 hello hello 備份設定中所選取的資料庫已更新的認證）。 備份通常會排程上執行，而且需要存取 toostorage （適用於輸出 hello 備份的檔案） 和資料庫 （用於複製和讀取 hello 備份中包含的內容 toobe）。 hello 結果失敗的 tooaccess 任一這些資源會是一致的備份失敗。 

若備份失敗，請檢閱最新結果 toounderstand 何種失敗狀況。 在 hello 案例中的儲存體存取失敗，請檢閱並更新 hello hello 備份組態中所使用的存放裝置設定。 在 hello 案例中的資料庫存取失敗，請檢閱並更新連接字串做為應用程式設定; 的一部分然後繼續 tooupdate 備份設定 tooproperly 包含所需的 hello 資料庫。 如需應用程式備份的詳細資訊，請參閱 hello[備份 web 應用程式在 Azure App Service 中](web-sites-backup.md)文件。

## <a name="nodejs"></a>當新的 Node.js 應用程式是部署的 tooAzure 應用程式服務
Node.js 應用程式的 azure App Service 預設組態是預定的 toobest 勝利 hello 需求的最常見的應用程式。 如果 Node.js 應用程式組態會從個人化微調 tooimprove 效能獲益，或最佳化 CPU/記憶體/網路資源的資源使用狀況，您可以檢閱我們的最佳作法和疑難排解步驟。 文件本文描述您可能需要的 hello iisnode 設定 tooconfigure Node.js 應用程式中，說明如何 hello 各種案例或問題可能會遇到應用程式，並顯示 tooaddress 這些問題：[最佳做法和Azure App Service 上的 Node 應用程式的疑難排解指南](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md)。   

