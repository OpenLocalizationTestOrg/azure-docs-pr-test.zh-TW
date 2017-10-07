---
title: "aaaManage Azure Traffic Manager 設定檔 |Microsoft 文件"
description: "本文會協助您建立、停用、啟用及刪除 Azure 流量管理員設定檔。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>管理 Azure 流量管理員設定檔

Traffic Manager 設定檔使用流量 tooyour 雲端服務或網站端點的流量路由方法 toocontrol hello 分佈。 這篇文章說明如何 toocreate 和管理這些設定檔。

## <a name="create-a-traffic-manager-profile"></a>建立流量管理員設定檔

您可以使用 hello Azure 入口網站來建立流量管理員設定檔。 建立您的設定檔之後, 您可以在 hello Azure 入口網站中設定端點、 監視和其他設定。 Traffic Manager 支援個 too200 端點，每個設定檔。 不過，大部分的使用案例僅需要少量的端點。

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate Traffic Manager 設定檔

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。 
2. 在 hello**中樞**功能表上，按一下**新增** > **網路** > **查看所有**，按一下**流量管理員**設定檔 tooopen hello**建立 Traffic Manager 設定檔**刀鋒視窗中，然後按一下**建立**。
3. 在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中，完成，如下所示：
    1. 在 [名稱]中，提供設定檔的名稱。 此名稱必須 toobe hello trafficmanager.net 區域內的唯一和 hello DNS 名稱會導致<name>，trafficmanager.net 所使用的 tooaccess 您的 Traffic Manager 設定檔。
    2. 在**路由方法**，選取 hello**優先順序**路由方法。
    3. 在**訂用帳戶**，選取您想在此設定檔 toocreate hello 訂用帳戶
    4. 在**資源群組**，建立新的資源群組 tooplace 下的這個設定檔。
    5. 在**資源群組位置**，選取 hello hello 資源群組的位置。 此設定是指 toohello hello 資源群組、 位置及 hello 將全域部署的流量管理員設定檔沒有任何影響。
    6. 按一下 [建立] 。
    7. Hello 全域部署，您的 Traffic Manager 設定檔完成時，它是個別資源群組中顯示為 hello 資源的其中一個。

## <a name="disable-enable-or-delete-a-profile"></a>停用、啟用或刪除設定檔

您可以停用現有的設定檔，讓 Traffic Manager 不是指使用者要求 toohello 設定端點。 當您停用流量管理員設定檔時，hello 設定檔與 hello hello 設定檔中包含的資訊仍維持不變，可以在 hello Traffic Manager 介面中進行編輯。  當您重新啟用 hello 設定檔，就會繼續轉介。 當您在 hello Azure 入口網站中建立流量管理員設定檔時，它會自動啟用。 如果您決定不再需要某個設定檔，可以將它刪除。

### <a name="toodisable-a-profile"></a>toodisable 設定檔

1. 如果您使用自訂網域名稱，變更您的網際網路 DNS 伺服器上的 hello CNAME 記錄，使它不再指向 tooyour Traffic Manager 設定檔。
2. 流量會停止正在執行導向 toohello hello Traffic Manager 設定檔所設定的端點。
3. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下**概觀**，hello 概觀刀鋒視窗中按一下**停用**，然後確認 toodisable hello Traffic Manager 設定檔。

### <a name="tooenable-a-profile"></a>tooenable 設定檔

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下**概觀**，然後在 hello 概觀刀鋒視窗中按一下**啟用**。
5. 如果您使用自訂網域名稱，請對您網際網路 DNS 伺服器 toopoint toohello 網域名稱 Traffic Manager 設定檔建立的 CNAME 資源記錄。
6. 流量會導向的 toohello 端點的一次。

### <a name="toodelete-a-profile"></a>toodelete 設定檔

1. 請確定您的網際網路 DNS 伺服器上的 hello DNS 資源記錄不會再使用的 CNAME 資源記錄指向 Traffic Manager 設定檔 toohello 網域名稱。
2. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。
3. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下**概觀**，hello 概觀刀鋒視窗中按一下**刪除**，然後確認 toodelete hello Traffic Manager 設定檔。

## <a name="next-steps"></a>後續步驟

* [新增端點。](traffic-manager-endpoints.md)
* [設定優先順序路由方法](traffic-manager-configure-priority-routing-method.md)
* [設定地理路由方法](traffic-manager-configure-geographic-routing-method.md) 
* [設定加權路由方法](traffic-manager-configure-weighted-routing-method.md)
* [設定效能路由方法](traffic-manager-configure-performance-routing-method.md)
