---
title: "aaaAzure 應用程式服務的本機快取概觀 |Microsoft 文件"
description: "本文說明如何 tooenable、 調整大小，以及查詢 hello hello Azure 應用程式服務本機快取功能的狀態"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Azure App Service 本機快取概觀
Azure Web 應用程式的內容儲存在 Azure 儲存體中，並且會持久顯示為內容共用。 這項設計是為不同的應用程式的預期的 toowork 並具有下列屬性的 hello:  

* hello 內容是跨多個 hello web 應用程式的虛擬機器 (VM) 執行個體共用。
* hello 內容持久，而且可以執行 web 應用程式以修改。
* 記錄檔和診斷資料檔案位於 hello 底下可使用相同的共用內容資料夾。
* 新的內容發佈直接更新 hello 內容資料夾。 您可以立即檢視 hello 相同的 hello SCM 網站透過內容和 hello 執行 （通常某些技術，例如 ASP.NET 執行初始化 web 應用程式重新啟動某些檔案的變更 tooget hello 最新的內容） 的 web 應用程式。

雖然許多 Web 應用程式會使用上述其中一項功能或所有功能，但某些 Web 應用程式只需要可從中執行的內容存放區，而且此存放區具備高效能、唯讀和高可用性。 這些應用程式可以受益於特定本機快取的 VM 執行個體。

hello Azure 應用程式服務本機快取功能提供的 web 角色檢視您的內容。 這個內容是在網站啟動時，以非同步方式建立之儲存體內容的 write-but-discard 快取。 Hello 快取已準備好，hello 站台時，交換的 toorun 針對 hello 快取內容。 在本機快取執行的 web 應用程式有下列優點 hello:

* 它們不能免於 toolatencies 存取 Azure 儲存體上的內容時發生。
* 它們是受 toohello 計劃升級或非計劃性的停機和做 hello 內容共用的伺服器發生的任何其他 Azure 儲存體中斷。
* 它們有較少的應用程式重新啟動，因為 toostorage 共用變更。

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>本機快取如何變更應用程式服務的 hello 行為
* hello 本機快取是一份 hello /site 和 /siteextensions 資料夾 hello web 應用程式。 它會建立 hello 本機 VM 執行個體上 web 應用程式啟動。 hello hello 每個 web 應用程式的本機快取的大小會受到限制 too300 MB 的預設值，但是您可以增加總 too2 GB。
* hello 本機快取是讀寫。 不過，hello web 應用程式移動的虛擬機器，或取得重新啟動時，將會捨棄任何修改。 您不應該使用本機快取的應用程式的關鍵任務的資料儲存在 hello 內容存放區。
* Web 應用程式可以繼續 toowrite 記錄檔和診斷資料與目前。 記錄檔和資料，不過，儲存在本機上 hello VM。 再將它們複製透過定期 toohello 共用內容存放區。 hello 複製 toohello 共用內容存放區是最佳的投入時間-寫入備份可能會遺失，因為 tooa 突然損毀的 VM 執行個體。
* 沒有 hello hello 的記錄檔和資料的資料夾使用本機快取的 web 應用程式的資料夾結構中的變更。 Hello 儲存記錄檔和資料資料夾中，遵循 「 唯一識別項 」 + 時間戳記的 hello 命名模式現在有子資料夾。 每個 hello 子資料夾對應 tooa VM 執行個體 hello web 應用程式正在執行或已執行的位置。  
* 發行變更 toohello web 應用程式透過任何 hello 發佈機制會將發佈 toohello 共用內容存放區。 這是根據設計，因為我們想要 hello 發行內容 toobe 持久。 toorefresh hello 本機快取中的 hello web 應用程式，它需要 toobe 重新啟動。 這看起來像過多的步驟並嗎？toomake hello 生命週期無縫式，請參閱本文稍後的 hello 資訊。
* D:\Home 將會為 toohello 本機快取。 D:\local 會繼續指向 toohello 暫存 VM 特定儲存體。
* hello 內容的預設檢視 hello SCM 站台將會繼續 toobe 共用內容存放區的 hello。

## <a name="enable-local-cache-in-app-service"></a>在 App Service 中啟用本機快取
您可以使用保留的應用程式設定的組合，以設定本機快取。 您可以使用下列方法 hello 來設定這些應用程式設定：

* [Azure 入口網站](#Configure-Local-Cache-Portal)
* [Azure Resource Manager](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站來設定本機快取
<a name="Configure-Local-Cache-Portal"></a>

您可以使用下列應用程式設定來針對每個 Web 應用程式啟用本機快取︰ `WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Azure 入口網站應用程式設定︰本機快取](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>使用 Azure Resource Manager 設定本機快取
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>變更在本機快取中的 hello 大小設定
根據預設，hello 本機快取大小是**300 MB**。 這包括 hello /site 和 /siteextensions 資料夾從複製 hello 內容存放區，以及任何在本機建立的記錄檔和資料的資料夾。 tooincrease 此限制，請使用 hello 應用程式設定`WEBSITE_LOCAL_CACHE_SIZEINMB`。 您可以增加 hello 大小太向上**2GB** (2000 MB) 每個 web 應用程式。

## <a name="best-practices-for-using-app-service-local-cache"></a>使用 App Service 本機快取的最佳作法
我們建議您使用本機快取，配合 hello[預備環境](../app-service-web/web-sites-staged-publishing.md)功能。

* 新增 hello*自黏*應用程式設定`WEBSITE_LOCAL_CACHE_OPTION`hello 值`Always`tooyour**生產**位置。 如果您使用`WEBSITE_LOCAL_CACHE_SIZEINMB`，也將它新增為自黏設定 tooyour 生產位置。
* 建立**臨時**位置及發行 tooyour 預備位置。 您通常不需要設定 hello 暫存位置 toouse 本機快取 tooenable 無縫式的建置-部署-測試生命週期臨時區域，如果您的本機快取的 hello 優點取得 hello 生產位置。
* 針對預備位置測試您的網站。  
* 準備好後，請在您的「預備環境」和「生產環境」位置之間發出 [交換作業](../app-service-web/web-sites-staged-publishing.md#Swap) 。  
* 自黏便箋的設定包括名稱和自黏 tooa 位置。 因此 hello 預備位置取得交換至生產環境中，它會繼承 hello 本機快取應用程式設定。 hello 新交換的生產位置針對 hello 本機快取幾分鐘後執行時間，以及將會接手一部分插槽熱身交換之後。 因此 hello 位置交換完成時，將會針對 hello 本機快取執行生產位置。

## <a name="frequently-asked-questions-faq"></a>常見問題集 (FAQ)
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>我可以判斷是否本機快取適用於 toomy web 應用程式？
如果您的 web 應用程式需要高效能、 可靠的內容存放區，不會在執行階段，使用 hello 內容存放區 toowrite 重要資料，而且總大小為小於 2 GB，然後 hello 回應為"yes"！ tooget hello 的大小總計 /site 和 /siteextensions 資料夾，您可以使用 hello 網站擴充功能"Azure Web 應用程式磁碟使用量 」。  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>如何分辨我的網站即使已切換 toousing 本機快取？
如果您使用預備環境的 hello 本機快取功能，hello 交換作業才能完成本機快取就緒。 如果您的站台執行的本機快取 toocheck，您可以檢查 hello 背景工作處理序環境變數`WEBSITE_LOCALCACHE_READY`。 使用 hello 指示在 hello[背景工作處理序環境變數](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable)頁面 tooaccess hello 多個執行個體上的背景工作處理序環境變數。  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>我剛發行新的變更，但我的 web 應用程式似乎未 toohave 它們。 原因為何？
如果您的 web 應用程式會使用本機快取，則您需要 toorestart 網站 tooget hello 最近的變更。 不想 toopublish 變更 tooa 生產網站嗎？ 請參閱 hello 先前最佳作法 > 一節中的 hello 位置選項。

### <a name="where-are-my-logs"></a>我的記錄檔在哪裡？
使用本機快取，您的記錄檔和資料的資料夾看起來會有點不同。 不過，hello 結構的子資料夾維持 hello 相同，不同之處在於底下的子資料夾以 hello 緊貼放置 hello 子資料夾，是格式 「 唯一 VM 識別碼 」 + 時間戳記。

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>我已啟用「本機快取」，但我的 Web 應用程式仍然重新啟動。 這是為什麼？ 我以為「本機快取」有助於頻繁的應用程式重新啟動。
「本機快取」確實有助於防止儲存體相關 Web 應用程式重新啟動。 不過，您的 web 應用程式仍無法接受重新啟動的 hello VM 的計劃的基礎結構升級期間。 hello 整體應用程式重新啟動與啟用的本機快取會遇到應較少。

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>本機快取並排除任何目錄進行複製 toohello 更快的本機磁碟機嗎？
複製 hello 儲存內容的 hello 步驟會排除任何名為資料夾，儲存機制。 這有助於您網站內容其中可能包含天 tooday 作業 hello web 應用程式中可能不需要原始檔控制儲存機制的案例。 
