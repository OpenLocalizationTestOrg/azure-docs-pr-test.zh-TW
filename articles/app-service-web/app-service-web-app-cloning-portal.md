---
title: "使用 Azure 入口網站的應用程式複製 aaaWeb"
description: "深入了解如何 tooclone 您 Web 應用程式 toonew 使用 Azure 入口網站的 Web 應用程式。"
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>使用 Azure 入口網站的 Azure App Service 應用程式複製
複製功能中的 hello [Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)可讓您輕鬆地複製現有 web 應用程式 tooa 新建立的應用程式或不同的區域中的 hello 相同的區域。 這可讓客戶 toodeploy 的應用程式的數字跨越不同地區，快速且輕鬆地。

應用程式複製目前僅支援 Premium 層 App Service 方案。 新功能使用 hello hello 相同限制 Web 應用程式備份功能，請參閱 <<c0> [ 備份 web 應用程式在 Azure App Service 中](web-sites-backup.md)。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>複製現有的應用程式
hello web 應用程式必須執行在 hello **Premium**順序 toocreate hello web 應用程式的複製模式。

1. 在 [hello [Azure 入口網站](https://portal.azure.com/)，開啟您的 web 應用程式] 刀鋒視窗。
2. 按一下 [工具] 。 然後，在 hello**工具**刀鋒視窗中，按一下 **複製應用程式**。
   
    ![][1]
   
   > [!NOTE]
   > 如果 hello web 應用程式已不在 hello **Premium**模式中，您會收到訊息，指出應用程式複製的 hello 支援模式。 此時，您擁有 hello 選項 tooselect**升級**。
   > 
   > 
3. 在 hello**複製應用程式**刀鋒視窗中提供的 hello 新 web 應用程式、 資源群組和應用程式服務方案的名稱。 也 hello 使用者將能夠 toochoose 是否 tooclone 的來源 web 應用程式設定的數字或不。
   
    ![][2]
4. 按一下後**建立**hello 平台就會開始建立 hello 來源 web 應用程式的複製工作。

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>複製現有的應用程式 tooan App Service 環境
在 hello**複製應用程式**刀鋒視窗 hello 客戶會有 hello 選項 toochoose 現有的 App Service 環境中的應用程式集區。

## <a name="current-restrictions"></a>目前的限制
這項功能目前為預覽狀態，我們目前正在處理 tooadd 新功能經過一段時間，hello 清單後面是 hello hello 目前支援的 Azure 入口網站中複製的應用程式的已知的限制：

* 不會複製 Azure 流量管理員設定
* 不會複製自動調整設定
* 不會複製備份排程設定
* 不會複製 VNET 設定
* App Insights 不會自動上設定 hello 目的地 web 應用程式
* 不會複製簡單驗證設定
* 不會複製 Kudu 延伸模組
* 不會複製 TiP 規則
* 不會複製資料庫內容

### <a name="references"></a>參考
* [使用 PowerShell 複製 Web 應用程式](app-service-web-app-cloning.md)
* [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)
* [如何 tooCreate App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)
* [在 App Service 環境中建立 Web 應用程式](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
