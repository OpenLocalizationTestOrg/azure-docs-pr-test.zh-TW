---
title: "aaaConfigure 加權循環流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooload 平衡流量 Traffic Manager 中使用的循環配置資源方法"
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a>設定 Traffic Manager 中的 hello 加權流量路由方法

常見的流量路由方法模式是一組相同的端點，包括雲端服務和網站，並以循環配置資源方式傳送流量 tooeach tooprovide。 hello 下列步驟概述如何 tooconfigure 這類型的流量路由方法。

> [!NOTE]
> Azure 網站已為資料中心 (也稱為「區域」) 內的網站提供循環配置資源負載平衡功能。 Traffic Manager 可讓您網站的 toospecify 循環配置資源的流量路由方法不同資料中心內。

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a>tooconfigure hello 加權流量路由方法

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。 
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**，然後按一下您想要針對 tooconfigure hello 路由方法的 hello 設定檔名稱。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，確認同時 hello 雲端服務，且您想 tooinclude 組態中的網站都存在。
4. 在 hello**設定**區段中，按一下**組態**，在 hello**組態**刀鋒視窗中，完成，如下所示：
    1. 如**流量路由方法設定**，確認 hello 流量路由方式**加權**。 如果沒有，請按一下**加權**hello 下拉式清單中。
    2. 設定 hello**端點監視設定**所有的每個端點，如下所示的此設定檔內相同：
        1. 選取適當的 hello**通訊協定**，並指定 hello**連接埠**數目。 
        2. 針對 [路徑]，輸入正斜線 */*。 toomonitor 端點，您必須指定路徑和檔案名稱。 A 正斜線"/"hello 相對路徑是有效的項目，表示該 hello 檔案位於 hello 根目錄 （預設值） 中。
        3. 在 hello hello 頁面頂端，按一下**儲存**。
5. 測試 hello 變更您的組態，如下所示：
    1.  在 hello 入口網站搜尋列中，搜尋 hello Traffic Manager 設定檔名稱，然後按一下 hello Traffic Manager 設定檔在 hello 結果中的顯示該 hello。
    2.  在 [hello **Traffic Manager**設定檔] 刀鋒視窗，請按一下**概觀**。
    3.  hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。 這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。 在此情況下，所有要求都會以循環配置資源方式路由到每個端點。
6. 一旦您的 Traffic Manager 設定檔運作正常，編輯 hello DNS 記錄，在您的授權 DNS 伺服器 toopoint 您公司網域名稱 toohello Traffic Manager 網域名稱。

![使用流量管理員設定加權流量路由方法][1]

## <a name="next-steps"></a>後續步驟

- 深入了解[優先順序流量路由方法](traffic-manager-configure-priority-routing-method.md)。
- 深入了解[效能流量路由方法](traffic-manager-configure-performance-routing-method.md)。
- 深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。
- 了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
