---
title: "aaaGet 開始使用 Azure DNS 使用 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate DNS 區域與在 Azure DNS 記錄。 這是逐步指南 toocreate 和管理您的第一個 DNS 區域和使用 hello Azure 入口網站的記錄。"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>開始使用 Azure DNS 使用 hello Azure 入口網站

> [!div class="op_single_selector"]
> * [Azure 入口網站](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

這篇文章會引導您透過 hello 步驟 toocreate 您的第一個 DNS 區域和使用 hello Azure 入口網站的記錄。 您也可以使用 Azure PowerShell 執行這些步驟，或 hello 跨平台 Azure CLI。

DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。 toostart 裝載您的網域在 Azure DNS 中，您需要該網域名稱 toocreate DNS 區域。 接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。 最後，toopublish 您的 DNS 區域 toohello 網際網路，您需要 tooconfigure hello 名稱伺服器 hello 網域。 每個步驟所述步驟 hello。

## <a name="create-a-dns-zone"></a>建立 DNS 區域

1. 登入 toohello Azure 入口網站
2. 在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。

    ![DNS 區域](./media/dns-getstarted-portal/openzone650.png)

4. 在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:


   | **設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|contoso.com|hello hello DNS 區域名稱|
   |**訂用帳戶**|[您的訂用帳戶]|選取的訂用帳戶 toocreate hello DNS 區域中。|
   |**資源群組**|**建立新的︰**contosoDNSRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。|
   |**位置**|美國西部||

> [!NOTE]
> hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。 hello DNS 區域位置一定是 「 全域 」，而且不會顯示。

## <a name="create-a-dns-record"></a>建立 DNS 記錄

hello 下列範例會引導您完成建立新的 'A' 記錄 hello 程序。 其他的記錄類型和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。 

1. Hello DNS 區域，在中建立 hello Azure 入口網站**我的最愛**] 窗格中，按一下 [**所有資源**。 按一下 hello **contoso.com** hello 資源刀鋒視窗中所有 DNS 都區域。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**contoso.com**在 hello**依名稱篩選...** 方塊 tooeasily 存取 hello DNS 區域。

1. 頂端的 hello hello **DNS 區域**刀鋒視窗中，選取**+ 記錄集**tooopen hello**加入資料錄集**刀鋒視窗。

1. 在 hello**加入資料錄集**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**。 在此範例中，我們會建立 A 記錄。

   |**設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|www|Hello 記錄名稱|
   |**類型**|A| 類型的 DNS 記錄 toocreate，可接受的值為 A、 AAAA、 CNAME、 MX、 NS、 SRV、 TXT、 和 PTR。  如需記錄類型的詳細資訊，請參閱 [DNS 區域和記錄的概觀](dns-zones-records.md)。|
   |**TTL**|1|-存留時間的 hello DNS 要求。|
   |**TTL 單位**|小時|TTL 值的時間測量。|
   |**IP 位址**|ipAddressValue| 此值為 hello hello DNS 記錄所解析的 IP 位址。|

## <a name="view-records"></a>檢視記錄

在 hello 的 hello DNS 區域刀鋒視窗的下半部，您可以看到 hello hello DNS 區域的記錄。 您應該會看到 hello 預設 DNS 和 SOA 記錄，也就建立在每個區域中加上您建立任何新記錄。

![區域](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>更新名稱伺服器

您可以在該程式的 DNS 區域與記錄已設定正確，您需要 tooconfigure 滿足您的網域名稱 toouse hello Azure DNS 名稱伺服器。 這可讓其他使用者 hello 網際網路 toofind DNS 記錄。

您的區域 hello 名稱伺服器提供 hello Azure 入口網站中：

![區域](./media/dns-getstarted-portal/viewzonens500.png)

這些名稱伺服器應該設有 hello 網域名稱註冊機構 （您購買 hello 網域名稱）。 您的註冊機構提供 hello 選項 tooset hello hello 網域名稱伺服器註冊。 如需詳細資訊，請參閱[委派您網域 tooAzure DNS](dns-domain-delegation.md)。

## <a name="delete-all-resources"></a>刪除所有資源

在本文中完成下列步驟的 hello 建立 toodelete 所有資源：

1. 在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。 按一下 hello **MyResourceGroup** hello 資源刀鋒視窗中所有資源都群組。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**MyResourceGroup**在 hello**依名稱篩選...** 方塊 tooeasily 存取 hello 資源群組。
1. 在 [hello **MyResourceGroup**刀鋒視窗中，按一下 hello**刪除**] 按鈕。
1. hello 入口網站需要您想要 toodelete hello 資源群組 tooconfirm tootype hello 名稱它。 按一下**刪除**，型別*MyResourceGroup* hello 資源群組名稱，然後按一下**刪除**。 刪除資源群組會刪除 hello 資源群組中的所有資源，所以一定會確定 tooconfirm hello 內容的資源群組然後再刪除。 hello 入口網站刪除 hello 的資源群組中包含的所有資源，然後都刪除本身 hello 資源群組。 這個程序需要幾分鐘的時間。


## <a name="next-steps"></a>後續步驟

toolearn 進一步了解 Azure DNS，請參閱[Azure DNS 概觀](dns-overview.md)。

進一步了解管理 Azure DNS 的 DNS 記錄 toolearn 看到[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。

