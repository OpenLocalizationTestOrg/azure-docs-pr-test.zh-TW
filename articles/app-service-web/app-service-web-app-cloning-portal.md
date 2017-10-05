---
title: "使用 Azure 入口網站複製 Web 應用程式"
description: "了解如何使用 Azure 入口網站，將您的 Web Apps 複製到新的 Web Apps。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>使用 Azure 入口網站的 Azure App Service 應用程式複製
[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 中的複製功能，可讓您輕鬆地將現有的 Web 應用程式複製到位於不同區域或相同區域的新建立 app。 這可讓客戶輕鬆且快速地跨不同區域部署許多 app。

應用程式複製目前僅支援 Premium 層 App Service 方案。 新的功能使用與 Web Apps 備份功能相同的限制，請參閱 [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>複製現有的應用程式
Web 應用程式必須在 [進階]  模式中執行，您才能為 Web 應用程式建立複製。

1. 在 [Azure 入口網站](https://portal.azure.com/)中，開啟 Web 應用程式的刀鋒視窗。
2. 按一下 [工具] 。 然後，在 [工具] 刀鋒視窗中，按一下 [複製應用程式]。
   
    ![][1]
   
   > [!NOTE]
   > 如果 Web 應用程式尚未處於 [進階] 模式，您將會收到訊息，指出支援應用程式複製的模式。 此時，您可以選取 [升級] 。
   > 
   > 
3. 在 [複製應用程式]  刀鋒視窗中，提供新 Web 應用程式的名稱、資源群組和 App Service 方案。 使用者也可以選擇是否複製多個來源 Web 應用程式設定。
   
    ![][2]
4. 按一下 [建立]  之後，平台會開始建立來源 Web 應用程式的複製。

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a>複製現有應用程式至 App Service 環境
在 [複製應用程式]  刀鋒視窗中，客戶可以在現有 App Service 環境中選擇應用程式集區。

## <a name="current-restrictions"></a>目前的限制
這項功能目前僅供預覽，我們正努力在日後加入新功能，以下是 Azure 入口網站中目前應用程式複製支援的已知限制：

* 不會複製 Azure 流量管理員設定
* 不會複製自動調整設定
* 不會複製備份排程設定
* 不會複製 VNET 設定
* 未自動在目的地 Web 應用程式上設定 App Insights 
* 不會複製簡單驗證設定
* 不會複製 Kudu 延伸模組
* 不會複製 TiP 規則
* 不會複製資料庫內容

### <a name="references"></a>參考
* [使用 PowerShell 複製 Web 應用程式](app-service-web-app-cloning.md)
* [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)
* [如何建立 App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)
* [在 App Service 環境中建立 Web 應用程式](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [App Service 環境簡介](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
