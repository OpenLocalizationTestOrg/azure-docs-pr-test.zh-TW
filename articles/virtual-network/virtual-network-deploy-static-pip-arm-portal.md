---
title: "aaaCreate VM 使用靜態公用 IP 位址-Azure 入口網站 |Microsoft 文件"
description: "了解如何 toocreate 具有靜態公用 IP 位址使用的 VM hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>使用靜態公用 IP 位址使用 hello Azure 入口網站建立 VM

> [!div class="op_single_selector"]
> * [Azure 入口網站](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [範本](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (傳統)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>使用靜態公用 IP 建立 VM

toocreate 中 hello Azure 入口網站中，完成下列步驟的 hello VM 的靜態公用 IP 位址：

1. 從瀏覽器中，瀏覽 toohello [Azure 入口網站](https://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。
2. Hello hello 入口網站的最上層的左下角，按一下**新增**>>**計算**>**Windows Server 2012 R2 Datacenter**。
3. 在 hello**選取部署模型**清單中，選取**資源管理員**按一下**建立**。
4. 在 hello**基本概念**刀鋒視窗中，輸入 hello VM 資訊，如下所示，然後按一下**確定**。
   
    ![Azure 入口網站 - 基本](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. 在 hello**大小選擇 「**刀鋒視窗中，按一下 **標準 A1**如下所示，然後按一下**選取**。
   
    ![Azure 入口網站 - 選擇大小](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. 在 hello**設定**刀鋒視窗中，按一下 **公用 IP 位址**，然後在 hello**建立公用 IP 位址**刀鋒視窗底下**指派**，按一下**靜態**如下所示。 然後按一下 [確定] 。
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. 在 hello**設定**刀鋒視窗中，按一下 **確定**。
8. 檢閱 hello**摘要**刀鋒視窗，如下所示，然後按一下**確定**。
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. 請注意您的儀表板中的 hello 新磚。
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. 一旦建立 hello VM，hello**設定**刀鋒視窗會顯示，如下所示
    
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

