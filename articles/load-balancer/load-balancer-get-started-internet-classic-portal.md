---
title: "aaaCreate 網際網路對向負載平衡器-傳統 Azure 入口網站 |Microsoft 文件"
description: "了解如何在模型中使用傳統部署使用網際網路對向負載平衡器 toocreate hello Azure 傳統入口網站"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>開始建立網際網路對向 hello Azure 傳統入口網站中的負載平衡器 （傳統）

> [!div class="op_single_selector"]
> * [Azure 傳統入口網站](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 雲端服務](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> 您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。 在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。 您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。 本文涵蓋 hello 傳統部署模型。 您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>為虛擬機器設定網際網路面向的負載平衡器

在訂單 tooload 平衡網路流量從 hello 網際網路跨 hello 虛擬機器的雲端服務，您必須建立一組負載平衡。 此程序假設您已經建立 hello 虛擬機器，而且必須為所有內 hello 相同雲端服務。

**tooconfigure 一組負載平衡的虛擬機器**

1. 在 hello Azure 傳統入口網站，按一下 **虛擬機器**，然後按一下hello hello 負載平衡集內的虛擬機器的名稱。
2. 選取 端點，然後按一下新增。
3. 在 hello**加入端點 tooa 的虛擬機器**頁面上，按一下向右箭號 hello。
4. 在 hello**指定 hello hello 端點詳細資料**頁面：

   * 在**名稱**，輸入 hello 端點的名稱，或從 hello 預先定義的端點針對常用的通訊協定清單中選取 hello 名稱。
   * 在**通訊協定**，視需要選取 hello hello 類型的端點，TCP 或 UDP，所需的通訊協定。
   * 在**公用連接埠和私用連接埠**，輸入您想要的 hello 虛擬機器 toouse 視 hello 連接埠號碼。 您可以使用 hello 私用連接埠和防火牆規則上 hello 虛擬機器 tooredirect 流量適用於您的應用程式的方式。 hello 私用連接埠可以 hello 與 hello 公用連接埠相同。 比方說，對於 web (HTTP) 流量的端點，您無法將指派連接埠 80 tooboth hello 公用和私用連接埠。

5. 選取**建立負載平衡集**，然後按一下hello 向右箭號。
6. 在 hello**設定 hello 負載平衡集**頁面，輸入 hello 負載平衡集名稱，然後再指派 hello hello Azure 負載平衡器的探查行為值。 hello 負載平衡器使用探查 toodetermine hello hello 負載平衡集內的虛擬機器時可用的 tooreceive 連入流量。
7. 按一下 hello 核取記號 toocreate hello 負載平衡的端點。 您會看到**是**在 hello**負載平衡集名稱**資料行的 hello**端點**hello 虛擬機器的頁面。
8. 在 hello 入口網站中，按一下 **虛擬機器**，按一下 hello hello 負載平衡集內的其他虛擬機器名稱，按一下**端點**，然後按一下**新增**。
9. 在 hello**加入端點 tooa 的虛擬機器**頁面上，按一下**新增端點 tooan 現有負載平衡集**選取 hello hello 負載平衡集名稱，然後按一下hello 向右箭號。
10. 在 hello**指定 hello hello 端點詳細資料**頁面上，輸入 hello 端點的名稱，然後按一下hello 核取記號。

Hello 其他虛擬機器的 hello 負載平衡集內，重複步驟 8-10。

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
