---
title: "aaaCreate 內部負載平衡器-Azure 入口網站 |Microsoft 文件"
description: "了解如何 toocreate 內部負載平衡器資源管理員 中使用 hello Azure 入口網站"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立內部負載平衡器

> [!div class="op_single_selector"]
> * [Azure 入口網站](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>開始使用 Azure 入口網站建立內部負載平衡器

使用 hello hello Azure 入口網站中的下列步驟 toocreate 內部負載平衡器。

1. 開啟瀏覽器，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)，並以您的 Azure 帳戶登入。
2. Hello 囉 」 畫面的左上方，按一下 **新增** > **網路** > **負載平衡器**。
3. 在 hello**建立負載平衡器**刀鋒視窗中，輸入**名稱**您的負載平衡器。
4. 在 [配置] 中，按一下 [內部]。
5. 按一下**虛擬網路**，，然後選取 hello 想 toocreate hello 負載平衡器的虛擬網路。

   > [!NOTE]
   > 如果看不到您想要 toouse hello 虛擬網路，請檢查 hello**位置**您正在使用 hello 負載平衡器，並據此變更它。

6. 按一下**子網路**，然後選取您想要 toocreate hello 負載平衡器的 hello 子網路。
7. 在下**IP 位址指派**，按一下 **動態**或**靜態**，取決於您是否想 hello IP 位址的 hello 負載平衡器 toobe 固定 （靜態） 或不。

   > [!NOTE]
   > 如果您選取 toouse 靜態 IP 位址，您將擁有 tooprovide hello 負載平衡器位址。

8. 在下**資源群組**請指定新的資源群組的 hello 名稱 hello 負載平衡器，或按一下**選取現有**選取現有的資源群組。
9. 按一下 [建立] 。

## <a name="configure-load-balancing-rules"></a>設定負載平衡規則

之後 hello 負載平衡器建立、 瀏覽 toohello 負載平衡器資源 tooconfigure 它。
您需要 tooconfigure 第一次的後端位址集區和一個探查設定負載平衡規則之前。

### <a name="step-1-configure-a-back-end-pool"></a>步驟 1：設定後端集區

1. 在 hello Azure 入口網站，按一下 **瀏覽** > **負載平衡器**，然後按一下先前建立的 hello 負載平衡器。
2. 在 hello**設定**刀鋒視窗中，按一下 **後端集區**。
3. 在 hello**後端位址集區**刀鋒視窗中，按一下 **新增**。
4. 在 hello**新增後端集區**刀鋒視窗中，輸入**名稱**為 hello 後端集區，然後按一下**確定**。

### <a name="step-2-configure-a-probe"></a>步驟 2：設定探查

1. 在 hello Azure 入口網站，按一下 **瀏覽** > **負載平衡器**，然後按一下先前建立的 hello 負載平衡器。
2. 在 hello**設定**刀鋒視窗中，按一下 **探查**。
3. 在 hello**探查**刀鋒視窗中，按一下 **新增**。
4. 在 hello**新增探查**刀鋒視窗中，輸入**名稱**hello 探查。
5. 在 [通訊協定] 下，選取 [HTTP]\(適用於網站) 或 [TCP] \(適用於其他 TCP 型應用程式)。
6. 在下**連接埠**，存取 hello 探查時，指定 hello 連接埠 toouse。
7. 在下**路徑**（適用於 HTTP 探查只），指定 hello 路徑 toouse 探查。
8. 在下**間隔**指定 tooprobe hello 應用程式的頻率。
9. 在下**狀況不良閾值**，指定 hello 後端的虛擬機器標示為狀況不良之前失敗嘗試次數。
10. 按一下**確定**toocreate 探查。

### <a name="step-3-configure-load-balancing-rules"></a>步驟 3：設定負載平衡規則

1. 在 hello Azure 入口網站，按一下 **瀏覽** > **負載平衡器**，然後按一下先前建立的 hello 負載平衡器。
2. 在 hello**設定**刀鋒視窗中，按一下 **負載平衡規則**。
3. 在 hello**負載平衡規則**刀鋒視窗中，按一下 **新增**。
4. 在 hello**新增負載平衡規則**刀鋒視窗中，輸入**名稱**hello 規則。
5. 在 [通訊協定] 下，選取 [HTTP]\(適用於網站) 或 [TCP] \(適用於其他 TCP 型應用程式)。
6. 在下**連接埠**，指定 hello 連接埠的用戶端連接 tooin hello 負載平衡器。
7. 在下**後端連接埠**，指定 hello hello 後端集區中使用的連接埠 toobe (通常 hello 負載平衡器通訊埠和 hello 後端連接埠是 hello 相同)。
8. 在下**後端集區**，選取 hello 後端集區，您在上面建立。
9. 在下**工作階段持續性**，選取您想要的工作階段 toopersist 的方式。
10. 在下**閒置逾時 （分鐘）**，指定 hello 閒置逾時。
11. 在 [浮動 IP (伺服器直接回傳)] 下，按一下 [停用] 或 [啟用]。
12. 按一下 [確定] 。

## <a name="next-steps"></a>後續步驟

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)

