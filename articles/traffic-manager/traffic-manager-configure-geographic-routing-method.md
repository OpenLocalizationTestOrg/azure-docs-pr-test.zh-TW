---
title: "地理 aaaConfigure 流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooconfigure hello 地理流量路由方式使用 Azure Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>設定使用 Traffic Manager hello 地理流量路由方法

hello 地理流量路由方法可讓您 toodirect 流量 toospecific hello hello 要求產生的位置的地理位置為基礎的端點。 本教學課程示範如何 toocreate Traffic Manager 設定檔與此路由的方法，並設定 hello 端點 tooreceive 流量從特定地理位置。

## <a name="create-a-traffic-manager-profile"></a>建立流量管理員設定檔

1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。
2. 在 hello 中樞功能表中，按一下 **新增** > **網路** > **查看所有**，然後按一下 **Traffic Manager 設定檔**tooopen hello**建立 Traffic Manager 設定檔**刀鋒視窗。
3. 在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中：
    1. 提供設定檔的名稱。 此名稱必須 toobe hello trafficmanager.net 區域內的唯一，而且會導致 hello DNS 名稱<profilename>，trafficmanager.net 將會使用的 tooaccess 您的 Traffic Manager 設定檔。
    2. 選取 hello**地理**路由方法。
    3. 選取您想在此設定檔 toocreate hello 訂用帳戶。
    4. 使用現有的資源群組或建立新的資源群組 tooplace 底下的這個設定檔。 如果您選擇 toocreate 新的資源群組，使用 hello**資源群組位置**hello 資源群組的下拉式清單中 toospecify hello 位置。 此設定是指 toohello hello 資源群組、 位置及 hello 將全域部署的 Traffic Manager 設定檔沒有任何影響。
    5. 按一下 [建立] 之後，就會建立流量管理員設定檔並部署到全球。

![建立流量管理員設定檔](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>新增端點

1. 搜尋您剛才建立 hello 入口網站的 [搜尋] 列中的 hello Traffic Manager 設定檔名稱，其顯示時按一下 hello 結果。
2. 瀏覽過**設定** -> **端點**hello Traffic Manager 刀鋒視窗中。
3. 按一下**新增**tooshow hello**加入端點**刀鋒視窗。
3. 在 hello**端點**刀鋒視窗中，按一下**新增**在 hello**加入端點**刀鋒視窗，其中會顯示完成，如下所示：
4. 選取**類型**取決於您要加入的端點的 hello 型別而定。 針對生產環境中使用的地理路由設定檔，我們強烈建議使用巢狀端點類型，而且包含的子設定檔中有多個端點。 如需詳細資訊，請參閱[地理流量路由方法的常見問題集](traffic-manager-FAQs.md)。
5. 提供**名稱**要 toorecognize 此端點。
6. 此刀鋒視窗中的某些欄位，取決於您要加入的端點 hello 類型：
    1. 如果您要新增的 Azure 端點，請選取 hello**目標資源類型**和 hello**目標**hello 資源為基礎您想讓 toodirect 流量
    2. 如果您要新增**外部**端點，提供 hello**完整網域名稱 (FQDN)**端點。
    3. 如果您要新增**巢狀端點**，選取 hello**目標資源**對應 toohello 子系設定檔 toouse 並指定 hello**最少子端點計數**.
7. Hello 地理對應區段中，使用 hello 下拉式功能表中與您想要的流量傳送 toobe toothis 端點 tooadd hello 區域。 您必須新增至少一個區域，而且可以對應多個區域。
8. 重複此步驟之所有端點您想要在此設定檔之下 tooadd

![新增流量管理員端點](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>使用 hello Traffic Manager 設定檔
1.  在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**名稱在 hello 前面一節中所建立，並按一下 hello 中的 hello 流量管理員設定檔結果顯示該 hello。
2. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下 **概觀**。
3. hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。 這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。  在地理路由的 hello 情況下，Traffic Manager 會查看 hello 連入要求的 hello 來源 IP，並判斷它從中產生 hello 區域。 如果該地區對應的 tooan 端點，則流量是路由的 toothere。 如果此區域不是對應的 tooan 端點，Traffic Manager 會傳回為 NODATA 查詢回應。

## <a name="next-steps"></a>後續步驟

- 深入了解[地理流量路由方法](traffic-manager-routing-methods.md#geographic)。
- 了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。
