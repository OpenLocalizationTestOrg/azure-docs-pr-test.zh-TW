---
title: "aaaManage DNS 區域中 Azure DNS-Azure 入口網站 |Microsoft 文件"
description: "您可以管理使用 hello Azure 入口網站的 DNS 區域。 本文說明如何刪除 tooupdate，，和 Azure DNS 上建立 DNS 區域"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>如何在 toomanage DNS 區域 hello Azure 入口網站

> [!div class="op_single_selector"]
> * [入口網站](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

本文章將示範如何 toomanage 您的 DNS 區域使用 hello Azure 入口網站。 您也可以管理您的 DNS 區域使用 hello 跨平台[Azure CLI](dns-operations-dnszones-cli.md)或 hello Azure [PowerShell](dns-operations-dnszones.md)。

## <a name="create-a-dns-zone"></a>建立 DNS 區域

1. 登入 toohello Azure 入口網站
2. 在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。

    ![DNS 區域](./media/dns-operations-dnszones-portal/openzone650.png)

4. 在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:


   | **設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|contoso.com|hello hello DNS 區域名稱|
   |**訂用帳戶**|[您的訂用帳戶]|選取的訂用帳戶 toocreate hello DNS 區域中。|
   |**資源群組**|**建立新的︰**contosoDNSRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。|
   |**位置**|美國西部||

> [!NOTE]
> hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。 hello DNS 區域位置一定是 「 全域 」，而且不會顯示。

## <a name="list-dns-zones"></a>列出 DNS 區域

在 hello Azure 入口網站中瀏覽過**更多服務** > **網路** > **DNS 區域**。 每個 DNS 區域都是它自己的資源，記錄集數目和名稱伺服器數目等資訊皆可在此檢視中檢視。 hello 資料行**名稱伺服器**不在 hello 預設檢視中，tooadd 按一下**資料行**，選取**名稱伺服器**按一下**完成**。

![列出 DNS 區域](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>刪除 DNS 區域

瀏覽 tooa hello 入口網站中的 DNS 區域。 在 hello **DNS 區域**刀鋒視窗中，按一下 **刪除區域**。 您必須提示的 tooconfirm，您會想 toodelete hello DNS 區域。 刪除 DNS 區域時，也會刪除所有包含在 hello 區域的 hello 記錄。

## <a name="next-steps"></a>後續步驟

深入了解如何與您的 DNS 區域記錄造訪 toowork[開始使用 Azure DNS 使用 hello Azure 入口網站](dns-getstarted-portal.md)。
