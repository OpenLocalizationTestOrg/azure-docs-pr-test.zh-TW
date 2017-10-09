---
title: "aaaConfigure 優先順序流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooconfigure hello 優先順序流量路由方法 Traffic Manager 中"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>在流量管理員中設定優先順序流量路由方法

不論 hello 網站模式，Azure 網站已提供容錯移轉功能，對於資料中心 （也稱為區域） 內的網站。 流量管理員會在不同資料中心為網站提供容錯移轉。

常見的服務容錯移轉模式是 toosend 流量 tooa 主要服務，並提供一組完全相同的備份服務的容錯移轉。 hello 下列步驟說明如何 tooconfigure 這排定優先順序與 Azure 雲端服務和網站的容錯移轉：

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>tooconfigure hello 優先順序流量路由方法

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。 
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**，然後按一下您想要針對 tooconfigure hello 路由方法的 hello 設定檔名稱。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，確認同時 hello 雲端服務，且您想 tooinclude 組態中的網站都存在。
4. 在 hello**設定**區段中，按一下**組態**，在 hello**組態**刀鋒視窗中，完成，如下所示：
    1. 如**流量路由方法設定**，確認 hello 流量路由方式**優先順序**。 如果沒有，請按一下**優先順序**hello 下拉式清單中。
    2. 設定 hello**端點監視設定**所有的每個端點，如下所示的此設定檔內相同：
        1. 選取適當的 hello**通訊協定**，並指定 hello**連接埠**數目。 
        2. 針對 [路徑]，輸入正斜線 */*。 toomonitor 端點，您必須指定路徑和檔案名稱。 A 正斜線"/"hello 相對路徑是有效的項目，表示該 hello 檔案位於 hello 根目錄 （預設值） 中。
        3. 在 hello hello 頁面頂端，按一下**儲存**。
5. 在 hello**設定**區段中，按一下**端點**。
6. 在 hello**端點**刀鋒視窗中，檢閱 hello 優先順序的端點。 當您選取 hello**優先順序**流量路由方式，hello 選取端點的 hello 順序很重要。 請確認 hello 優先順序排列的端點。  hello 主要端點位於最上方。 請仔細檢查 hello 順序顯示。 所有要求將會是路由的 toohello 第一個端點，並且如果 Traffic Manager 偵測到它處於狀況不良狀態，hello 流量自動容錯移轉 toohello 下一個端點。 
7. toochange hello 端點優先順序，請按一下 hello 端點在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**並變更 hello**優先順序**值視. 
8. 按一下**儲存**toosave 變更 hello 端點設定。
9. 完成您的組態變更之後，請按一下**儲存**hello hello 頁底端。
10. 測試 hello 變更您的組態，如下所示：
    1.  在 hello 入口網站搜尋列中，搜尋 hello Traffic Manager 設定檔名稱，然後按一下 hello Traffic Manager 設定檔在 hello 結果中的顯示該 hello。
    2.  在 [hello **Traffic Manager**設定檔] 刀鋒視窗，請按一下**概觀**。
    3.  hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。 這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。 在此情況下的所有要求路由的 toohello 第一個端點，而且如果 Traffic Manager 偵測到它處於狀況不良狀態，hello 流量自動容錯移轉 toohello 下一個端點。
11. 一旦您的 Traffic Manager 設定檔運作正常，編輯 hello DNS 記錄，在您的授權 DNS 伺服器 toopoint 您公司網域名稱 toohello Traffic Manager 網域名稱。

![使用流量管理員設定優先順序流量路由方法][1]

## <a name="next-steps"></a>後續步驟


- 深入了解[加權流量路由方法](traffic-manager-configure-weighted-routing-method.md)。
- 深入了解[效能路由方法](traffic-manager-configure-performance-routing-method.md)。
- 深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。
- 了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png