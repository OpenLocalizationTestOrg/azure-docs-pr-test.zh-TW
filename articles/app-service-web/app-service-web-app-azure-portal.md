---
title: "aaaReference 巡覽 hello Azure 入口網站"
description: "瞭解 hello 不同的使用者經驗之間 hello 管理入口網站和 hello Azure 入口網站應用程式服務 Web"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>瀏覽 hello Azure 入口網站的參考
Azure 網站現在稱為 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。 我們正在更新所有我們的文件 tooreflect hello Azure 入口網站的這個名稱變更和 tooprovide 指示。 等到完成該程序，您可以使用做為指南的這份文件在 hello Azure 入口網站中使用的 Web 應用程式。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>hello Azure 傳統入口網站的 hello 未來
您會注意到 hello 商標 hello Azure 傳統入口網站上的變更，而該入口網站就會處於 hello 的 hello Azure 入口網站所要取代的程序。 Hello 傳統入口網站已捨棄不用，因為新的開發工作的 hello 焦點會移位 toohello Azure 入口網站。 所有 Web 應用程式即將推出的新功能會都出現在 hello Azure 入口網站中。 開始使用的最新及最佳 Web 應用程式有 toooffer hello hello Azure 入口網站 tootake 優點。

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>版面配置 hello Azure 傳統入口網站和 Azure 入口網站之間的差異
Hello 傳統入口網站中所有 hello Azure 服務會列在 hello 左手邊。 Hello 傳統入口網站中的瀏覽遵循樹狀結構中，您從 hello 服務啟動並瀏覽至每個項目。 管理獨立元件時，此結構也會運作良好。 不過，在 Azure 上建置的應用程式是互連服務的集合，而且此樹狀結構不適合使用服務集合。 

hello Azure 入口網站可輕鬆 toobuild 應用程式端對端與多個服務的元件。 hello 入口網站會組織成*皆*。 A*旅程*是一系列的*刀鋒*、 有哪些不同元件是 hello 的容器。 例如，設定自動調整 web 應用程式*旅程*這會引領您數個刀鋒視窗中 hello 下列範例所示： hello**網站**（該刀鋒視窗標題尚未更新的 toouse 刀鋒視窗hello 新詞彙)，hello**設定**刀鋒視窗中，與 hello**向外延展**刀鋒視窗。 在 hello 範例中，自動調整正在設定 toodepend 上 CPU 使用量，因此也**CPU 百分比**刀鋒視窗。 hello 元件內 hello*刀鋒*稱為*部分*，這看起來像磚。 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>瀏覽範例：建立 Web 應用程式
建立新的 Web 應用程式仍然像 1-2-3 一樣簡單。 下列影像顯示 hello 傳統入口網站與 hello 入口網站來並行 toodemonstrate 不多 hello 幾個步驟中已變更的 hello 需要 tooget 註冊 web 應用程式並執行。 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Hello 入口網站中，您可以選擇從 hello 最常見的 web 應用程式，包括常用的組件庫的應用程式，例如 WordPress 的類型。 如需可用的應用程式的完整清單，請瀏覽 hello [Azure Marketplace]。

當您建立 web 應用程式時，您必須指定 URL，App Service 方案，就像是 hello 傳統入口網站中的 hello 入口網站中的位置。 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

此外，hello 入口網站可讓您可以定義其他常見的設定。 例如，[資源群組](../azure-resource-manager/resource-group-overview.md)讓簡單 toosee 及管理相關的 Azure 資源。 

## <a name="navigation-example-settings-and-features"></a>瀏覽範例：設定和功能
所有 hello 設定和功能現在以邏輯方式分組在單一刀鋒視窗中，從中您可以瀏覽。

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

例如，您可以建立自訂網域，依序按一下**自訂網域及 SSL**在 hello**設定**刀鋒視窗。

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset 設定監視的警示，按一下**要求與錯誤**然後**新增警示**。

![](./media/app-service-web-app-azure-portal/Monitoring.png)

按一下 tooenable 診斷**診斷記錄檔**hello 中**設定**刀鋒視窗。

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

tooconfigure 應用程式設定，請按一下**應用程式設定**在 hello**設定**刀鋒視窗。 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Hello 品牌名稱，以外 hello 入口網站中的幾件事已重新命名或以不同的方式分組 toomake 它更容易 toofind 它們。 例如，以下是應用程式設定的 hello 對應頁面的螢幕擷取畫面 (**設定**) hello 傳統入口網站中。

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>其他資源
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

