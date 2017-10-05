---
title: "Azure App Service 的最佳作法"
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
ms.openlocfilehash: fd94f5b17f69dec91c78c8acfbac2eaf5787c010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-azure-app-service"></a>Azure App Service 的最佳作法
本文將摘要說明使用 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)的最佳作法。 

## <a name="colocation"></a>共置
當組成解決方案 (例如 Web 應用程式和資料庫) 的 Azure 資源位於不同區域時，可能會有下列效果︰

* 資源之間的通訊延遲更久
* 跨區域的輸出資料傳輸需要收費，如 [Azure 定價頁面](https://azure.microsoft.com/pricing/details/data-transfers)所示。

相同區域中的共置最適合用於組成解決方案的 Azure 資源，例如 Web 應用程式，以及用來保存內容或資料的資料庫或儲存體帳戶。 建立資源時，應該確定它們位於相同的 Azure 區域，除非有特定的商務或設計理由不要如此。 您可以利用進階 App Service 方案 App 目前可用的 [App Service 複製功能](app-service-web-app-cloning-portal.md) ，將 App Service App 移至資料庫所在的區域。   

## <a name="memoryresources"></a>當應用程式耗用超出預期的記憶體時
當您經由監視或服務建議而發現 App 耗用超出預期的記憶體時，請考慮使用 [App Service 自動修復功能](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites)。 自動修復功能的其中一個選項是根據記憶體臨界值來採取自訂動作。 動作包括電子郵件通知、透過記憶體傾印來調查，乃至於回收背景工作處理序以當場緩和情況。 自動修復可透過 web.config 和易於使用的使用者介面來設定，如這篇部落格文章所述： [App Service 支援網站擴充功能](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps)。   

## <a name="CPUresources"></a>當應用程式耗用超出預期的 CPU 時
當您經由監視或服務建議，發現應用程式耗用超出預期的記憶體，或 CPU 用量連續暴增時，請考慮相應增加或相應放大 App Service 方案。 如果應用程式是具狀態，則相應增加是唯一選項，如果應用程式是無狀態，則相應放大提供較大彈性和更高的調整可能性。 

如需「具狀態」與「無狀態」應用程式的相關資訊，請觀賞這段影片︰ [在 Microsoft Azure Web 應用程式上規劃可調整的端對端多層應用程式](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid)。 如需 App Service 調整和自動調整選項的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。  

## <a name="socketresources"></a>當通訊端資源耗盡時
耗盡輸出 TCP 連線的常見原因是使用的用戶端程式庫未實作為重複使用 TCP 連線，或因為沒有利用更高階的通訊協定，例如 HTTP - Keep-Alive。 請檢閱 App Service 方案中各應用程式所參考的每個程式庫的說明文件，以確保在程式碼中設定或存取程式庫時，能夠有效率地重複使用輸出連線。 此外，請遵循程式庫文件指引，適當地建立和釋放或清除，以免連線流失。 在進行這類用戶端程式庫調查時，可相應放大至多個執行個體來緩和影響。  

## <a name="appbackup"></a>當您的應用程式備份啟動失敗時
應用程式備份為什麼會失敗有兩個最常見的原因：儲存體設定無效和資料庫組態無效。 這些失敗通常會在下列情況中發生：對儲存體或資料庫資源進行變更，或者針對存取這些資源的方式進行變更 (例如，針對備份設定中所選取的資料庫更新了認證)。 備份通常會依排程執行，而且需要存取儲存體 (用於輸出的備份檔案) 和資料庫 (用於複製和讀取要包含於備份中的內容)。 無法存取這其中一個資源的結果就是備份一律會失敗。 

發生備份失敗時，請檢閱最新的結果，以了解發生了哪種類型的失敗。 發生儲存體存取失敗時，請檢閱並更新備份組態中所使用的存放體設定。 發生資料庫存取失敗時，請檢閱並更新連接字串以做為應用程式設定的一部分，然後繼續更新您的備份組態，以便正確包含所需的資料庫。 如需應用程式備份的詳細資訊，請參閱 [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md) 文件。

## <a name="nodejs"></a>當新的 Node.js 應用程式部署至 Azure App Service 時
適用於 Node.js app 的 Azure App Service 預設組態是為了符合大部分應用程式的需求。 如果您 Node.js 應用程式的組態可受益於透過個人化調整來改善效能或將 CPU/記憶體/網路資源的資源使用量最佳化，您可以檢閱我們的最佳作法和疑難排解步驟。 本文章說明您可能需針對您的 Node.js 應用程式設定的 iisnode 設定、說明您的應用程式可能會面臨的各種案例或問題，以及示範如何解決這些問題： [Azure App Service 上 Node 應用程式的最佳作法和疑難排解指南](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md)。   

