---
title: "aaaCreate Azure Traffic Manager 設定檔 |Microsoft 文件"
description: "本文說明如何 toocreate Traffic Manager 設定檔"
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
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>建立流量管理員設定檔

本文說明如何使用設定檔**優先順序**tooroute 使用者 tootwo Azure Web 應用程式端點可以建立路由類型。 使用 hello**優先順序**路由類型，所有流量都是路由的 toohello 第一個端點而第二個 hello 將保留做為備份。 如此一來，使用者可以是路由的 toohello 第二個端點，如果 hello 第一個端點會變為狀況不良。

在本文中，兩個先前建立的 Azure Web 應用程式端點會是新建立的關聯的 toothis Traffic Manager 設定檔。 深入了解如何 toolearn toocreate Azure Web 應用程式端點，請瀏覽 hello [Azure Web 應用程式的文件頁面](https://docs.microsoft.com/azure/app-service-web/)。 您可以加入任何端點具有 DNS 名稱，並可透過連線 hello 公用網際網路，我們使用 Azure Web 應用程式端點做為範例。

### <a name="create-a-traffic-manager-profile"></a>建立流量管理員設定檔
1. 從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。 
2. 在 hello**中樞**功能表上，按一下**新增** > **網路** > **查看所有**，按一下**流量管理員**設定檔 tooopen hello**建立 Traffic Manager 設定檔**刀鋒視窗中，然後按一下**建立**。
3. 在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中，完成，如下所示：
    1. 在 [名稱]中，提供設定檔的名稱。 此名稱必須 toobe hello trafficmanager.net 區域內的唯一和 hello DNS 名稱會導致<name>，也就是使用的 tooaccess trafficmanager.net 您的 Traffic Manager 設定檔。
    2. 在**路由方法**，選取 hello**優先順序**路由方法。
    3. 在**訂用帳戶**，選取您想在此設定檔 toocreate hello 訂用帳戶
    4. 在**資源群組**，建立新的資源群組 tooplace 下的這個設定檔。
    5. 在**資源群組位置**，選取 hello hello 資源群組的位置。 此設定是指 toohello hello 資源群組、 位置及 hello 將全域部署的流量管理員設定檔沒有任何影響。
    6. 按一下 [建立] 。
    7. Hello 全域部署，您的 Traffic Manager 設定檔完成時，它是個別資源群組中顯示為 hello 資源的其中一個。

    ![建立流量管理員設定檔](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>新增流量管理員端點

1. 在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**在 hello hello 中前一節，然後按一下 hello 流量管理員設定檔中所建立的名稱會顯示該 hello。
2. 在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。
3. 在 hello**端點**刀鋒視窗，其中會顯示按一下**新增**。
4. 在 hello**加入端點**刀鋒視窗中，完成，如下所示：
    1. 在 [類型] 中，按一下 [Azure 端點]。
    2. 提供**名稱**要 toorecognize 此端點。
    3. 在 [目標資源類型] 中，按一下 [App Service]。
    4. 如**目標資源**，按一下 **選擇 app service** tooshow hello 清單下 hello hello Web 應用程式的相同訂用帳戶。 在 hello**資源**刀鋒視窗，其中會顯示，挑選 hello 您想 tooadd，如 hello 第一個端點的應用程式服務。
    5. 在 [優先順序] 中，選取 [1]。 這會導致所有流量 toothis 端點是否狀況良好。
    6. 維持不勾選 [新增為已停用]。
    7. 按一下 [檔案] &gt; [新增] &gt; [專案] 
5.  重複步驟 3 和 4 hello 下一個 Azure Web 應用程式端點。 請確定 tooadd 使用其**優先順序**在設定值**2**。
6.  這兩個端點的 hello 加法完成時，它們會顯示在 hello **Traffic Manager 設定檔**刀鋒視窗，以及其監視的狀態為**線上**。

    ![新增流量管理員端點](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>使用 hello Traffic Manager 設定檔
1.  在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**在 hello 前面一節中所建立的名稱。 在顯示 hello 結果中，按一下 hello 流量管理員設定檔。
2. 在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下 **概觀**。
3. hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。 這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。 在此情況下，所有要求會路由的 toohello 第一個端點，並且如果 Traffic Manager 偵測到它處於狀況不良狀態，hello 流量自動容錯移轉 toohello 下一個端點。

## <a name="delete-hello-traffic-manager-profile"></a>刪除 hello Traffic Manager 設定檔
當不再需要請刪除 hello 資源群組和您所建立的 hello Traffic Manager 設定檔。 因此，從 hello 選取 hello 資源群組的 toodo **Traffic Manager 設定檔**刀鋒視窗，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

- 深入了解[路由類型](traffic-manager-routing-methods.md)。
- 深入了解端點類型[端點類型](traffic-manager-endpoint-types.md)。
- 深入了解[端點監視](traffic-manager-monitoring.md)。



