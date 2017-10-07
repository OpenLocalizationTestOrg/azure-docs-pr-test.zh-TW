---
title: "aaaManage 端點在 Azure Traffic Manager |Microsoft 文件"
description: "本文將協助您從 Azure 流量管理員加入、移除、啟用和停用端點。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>新增、停用、啟用或刪除端點

Azure App Service 中的 hello Web 應用程式功能已提供容錯移轉和循環配置資源流量路由功能的網站內的資料中心，無論 hello 網站模式為何。 Azure Traffic Manager 可讓您 toospecify 容錯移轉和循環配置資源的流量路由的不同資料中心內的網站和雲端服務。 hello 第一個步驟所需 tooprovide 功能是 tooadd hello 雲端服務或網站端點 tooTraffic 管理員。

您也可以停用屬於流量管理員設定檔一部分的個別端點。 停用端點會讓它 hello 設定檔的一部分，但是 hello 設定檔行為會如同 hello 端點並未包含在內般。 此動作對於暫時移除處於維護模式、或被重新部署的端點而言很有用。 Hello 端點一旦再次啟動並執行，它可以啟用它。

> [!NOTE]
> 停用端點會執行任何動作 toodo 與 Azure 中的部署狀態。 狀況良好的端點保持為最新，而且要能 tooreceive 流量，即使停用 Traffic Manager 中。 此外，在一個設定檔中停用端點並不會影響它在另一個設定檔中的狀態。

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd 雲端服務或應用程式服務端點 tooa Traffic Manager 設定檔

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。
4. 在 hello**端點**刀鋒視窗，其中會顯示按一下**新增**。
5. 在 hello**加入端點**刀鋒視窗中，完成，如下所示：
    1. 在 [類型] 中，按一下 [Azure 端點]。
    2. 提供**名稱**要 toorecognize 此端點。
    3. 如**目標資源類型**、 從 hello 下拉式清單中，選擇 hello 適當的資源類型。
    4. 如**目標資源**、 從 hello 下拉式清單中，選擇適當的目標資源，hello tooshow hello 清單下的資源 hello 相同的訂用帳戶中 hello**資源刀鋒視窗**。 在 hello**資源**刀鋒視窗，其中會顯示您想 tooadd，如 hello 第一個端點挑選 hello 服務。
    5. 在 [優先順序] 中，選取 [1]。 這會導致所有流量 toothis 端點是否狀況良好。
    6. 維持不勾選 [新增為已停用]。
    7. 按一下 [檔案] &gt; [新增] &gt; [專案] 
6.  重複步驟 4 和 5 tooadd hello 下一個 Azure 端點。 請確定 tooadd 使用其**優先順序**在設定值**2**。
7.  這兩個端點的 hello 加法完成時，它們會顯示在 hello **Traffic Manager 設定檔**刀鋒視窗，以及其監視的狀態為**線上**。

> [!NOTE]
> 在新增或移除端點，從使用 hello 設定檔之後*容錯移轉*流量路由方法、 hello 容錯移轉優先順序清單可能無法排序它們您想要的方式。 您可以調整 hello hello 組態 頁面上的 hello 容錯移轉優先順序清單順序。 如需詳細資訊，請參閱 [設定容錯移轉流量路由](traffic-manager-configure-failover-routing-method.md)。

## <a name="toodisable-an-endpoint"></a>toodisable 端點

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下顯示 hello 結果 hello Traffic Manager 設定檔的名稱。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。 
4. 按一下您想 toodisable，hello 端點，然後在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**。
5. 在 hello**端點**刀鋒視窗中，也變更 hello 端點狀態**已停用**，然後按一下**儲存**。
6. 用戶端會繼續 toosend 流量 toohello 端點 hello 持續時間內的存留時間 (TTL)。 您可以變更 hello TTL hello 的 hello Traffic Manager 設定檔設定 頁面上。

## <a name="tooenable-an-endpoint"></a>tooenable 端點

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下顯示 hello 結果 hello Traffic Manager 設定檔的名稱。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。 
4. 按一下您想 toodisable，hello 端點，然後在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**。
5. 在 hello**端點**刀鋒視窗中，也變更 hello 端點狀態**啟用**，然後按一下**儲存**。
6. 用戶端會繼續 toosend 流量 toohello 端點 hello 持續時間內的存留時間 (TTL)。 您可以變更 hello TTL hello 的 hello Traffic Manager 設定檔設定 頁面上。

## <a name="toodelete-an-endpoint"></a>toodelete 端點

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下顯示 hello 結果 hello Traffic Manager 設定檔的名稱。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。 
4. 按一下您想 toodisable，hello 端點，然後在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**。
5. 在 hello**端點**刀鋒視窗中，也變更 hello 端點狀態**啟用**，然後按一下**儲存**。


## <a name="next-steps"></a>後續步驟

* [管理流量管理員設定檔](traffic-manager-manage-profiles.md)
* [設定路由方法](traffic-manager-configure-routing-method.md)
* [疑難排解流量管理員的已降級狀態](traffic-manager-troubleshooting-degraded.md)
* [流量管理員的效能考量](traffic-manager-performance-considerations.md)
* [流量管理員的相關作業 (REST API 參考)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

