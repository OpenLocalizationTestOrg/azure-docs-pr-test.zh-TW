---
title: "瀏覽 Azure 入口網站的參考"
description: "了解管理入口網站與 Azure 入口網站間之應用程式服務 Web 的不同使用者體驗"
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
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a>瀏覽 Azure 入口網站的參考
Azure 網站現在稱為 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。 我們正在更新所有的文件，以反映這項名稱變更，同時為 Azure 入口網站提供相關說明。 除非完成該程序，否則您可以使用這份文件作為指南，以在 Azure 入口網站中使用 Web Apps 。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a>Azure 傳統入口網站的未來
您會發現 Azure 傳統入口網站上的品牌有所變更，該入口網站正取代為 Azure 入口網站。 傳統入口網站捨棄不用時，新開發的焦點就會移至 Azure 入口網站。 Azure 入口網站會有 Web Apps 之所有即將推出的新功能。 開始使用 Azure 入口網站，以利用 Web Apps 必須提供的最新和最大部分。

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a>Azure 傳統入口網站與 Azure 入口網站的版面配置差異
在傳統入口網站中，所有 Azure 服務都會列在左邊。 在傳統入口網站中進行瀏覽時會遵循樹狀結構，在其中，您會從服務開始並瀏覽到每個元素。 管理獨立元件時，此結構也會運作良好。 不過，在 Azure 上建置的應用程式是互連服務的集合，而且此樹狀結構不適合使用服務集合。 

Azure 入口網站可讓您使用多個服務的元件，輕鬆地以端對端方式建置應用程式。 入口網站會組織成*旅程*。 *旅程*是一系列的*刀鋒視窗*，這些是不同元件的容器。 例如，設定 Web 應用程式的自動調整是一個*旅程*，後者會採用數個刀鋒視窗 (如下列範例所示)：[網站] 刀鋒視窗 (刀鋒視窗標題尚未更新為使用新的術語)、[設定] 刀鋒視窗和 [相應放大] 刀鋒視窗。 在此範例中，自動調整設定為相依於 CPU 使用量，因此也會有 [CPU 百分比] 刀鋒視窗。 *刀鋒視窗*內的元件稱為*組件*，看起來就像磚。 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>瀏覽範例：建立 Web 應用程式
建立新的 Web 應用程式仍然像 1-2-3 一樣簡單。 下圖並排顯示傳統入口網站和入口網站，以示範啟動並執行 Web 應用程式所需的步驟數目變更並不多。 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

在入口網站中，您可以選擇最常見類型的 Web 應用程式，包括 WordPress 這類常見資源庫應用程式。 如需可用應用程式的完整清單，請瀏覽 [Azure Marketplace]。

建立 Web 應用程式時，請指定入口網站中的 URL、App Service 方案和位置，就像在傳統入口網站中進行的作業一樣。 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

此外，入口網站還可讓您定義其他常見的設定。 例如，[資源群組](../azure-resource-manager/resource-group-overview.md)可簡單地查看和管理相關的 Azure 資源。 

## <a name="navigation-example-settings-and-features"></a>瀏覽範例：設定和功能
所有設定和功能現在都以邏輯方式分組在單一刀鋒視窗中，而您可以從中進行瀏覽。

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

例如，按一下 [設定] 刀鋒視窗中的 [自訂網域和 SSL]，即可建立自訂網域。

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

若要設定監視警示，請依序按一下 [要求和錯誤] 和 [新增警示]。

![](./media/app-service-web-app-azure-portal/Monitoring.png)

若要啟用診斷，請按一下 [設定] 刀鋒視窗中的 [診斷記錄檔]。

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

若要設定應用程式設定，請按一下 [設定] 刀鋒視窗中的 [應用程式設定]。 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

入口網站中有些項目已使用不同的方式重新命名或分組，讓您更輕鬆地找到它們，而不是品牌名稱。 例如，下面是傳統入口網站中應用程式設定之對應頁面的螢幕擷取畫面 (**設定**)。

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>其他資源
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> 如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)

