---
title: "aaaHost 與 Azure 應用程式閘道的多個站台 |Microsoft 文件"
description: "此頁面會提供指示 tooconfigure 現有的 Azure 應用程式閘道器裝載 hello 上的多個 web 應用程式相同的閘道器以 hello Azure 入口網站。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>設定現有應用程式閘道來裝載多個 Web 應用程式

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

多個站台裝載可讓您以上一個 web 應用程式的 toodeploy hello 上相同的應用程式閘道。 它依賴在 hello 的傳入 HTTP 要求，而 toodetermine 的接聽程式將會收到流量的主機標頭存在。 hello 接聽程式，然後指示流量 tooappropriate 後端集區中的 hello 閘道 hello 規則定義的設定。 在啟用 SSL 的 web 應用程式，應用程式閘道依賴 hello 伺服器名稱指示 (SNI) 延伸模組 toochoose hello 正確接聽程式 hello 網路流量。 多個站台裝載的常見用法是不同的網頁網域 toodifferent 後端伺服器集區的 tooload 平衡要求。 同樣的多個相同的根網域也無法裝載在 hello 的子網域 hello 相同的應用程式閘道。

## <a name="scenario"></a>案例

在下列範例的 hello，應用程式閘道為 contoso.com 和 fabrikam.com 的流量提供兩個後端伺服器集區： contoso 伺服器集區及 fabrikam 伺服器集區。 類似的安裝程式可能使用的 toohost 子網域，例如 app.contoso.com 和 blog.contoso.com。

![多網站案例][multisite]

## <a name="before-you-begin"></a>開始之前

這個案例會新增多站台支援 tooan 現有應用程式閘道。 toocomplete 此案例中，現有的應用程式閘道需要 toobe 可用 tooconfigure。 請瀏覽[透過 hello 入口網站建立應用程式閘道](application-gateway-create-gateway-portal.md)toolearn 如何 toocreate hello 入口網站中的基本應用程式閘道。

hello 以下是需要 tooupdate hello 應用程式閘道 hello 步驟：

1. 建立每個站台的後端集區 toouse。
2. 建立每個網站應用程式閘道都支援的接聽程式。
3. 建立 hello 適當後端規則 toomap 每個接聽程式。

## <a name="requirements"></a>需求

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。 您也可以使用 FQDN。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。 針對啟用多站台功能的應用程式閘道，會一併新增主機名稱和 SNI 指示器。
* **規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。 規則會在處理 hello 排列順序，而且將會導向流量，透過 hello 比對，不論明確性比較的第一個規則。 比方說，如果您有使用基本的接聽程式的規則和規則，使用多站台接聽程式同時在相同連接埠，與 hello 規則 hello hello 多站台接聽程式必須列出 hello 規則之前為 hello 多站台規則 toofunction 順序中的 hello 基本接聽程式預期的。 
* **憑證︰**每個接聽程式需要唯一的憑證，在此範例中針對多網站建立 2 個接聽程式。 兩個.pfx 憑證和它們的 hello 密碼需要 toobe 建立。

## <a name="create-back-end-pools-for-each-site"></a>建立每個網站的後端集區

需要應用程式閘道支援之每個網站的後端集區，在此案例中會建立 2 個，一個用於 contoso11.com，另一個用於 fabrikam11.com。

### <a name="step-1"></a>步驟 1

瀏覽 tooan 現有應用程式閘道 hello Azure 入口網站 (https://portal.azure.com) 中。 選取 [後端集區]，按一下 [新增]

![新增後端集區][7]

### <a name="step-2"></a>步驟 2

填寫 hello 後端集區的 hello 資訊**pool1**，新增 hello 後端伺服器 hello ip 位址或 Fqdn，然後按一下**[確定]**

![後端集區 pool1 設定][8]

### <a name="step-3"></a>步驟 3

在 [hello 後端集區] 刀鋒視窗上按一下**新增**tooadd 額外的後端集區**pool2**，新增 hello 後端伺服器 hello ip 位址或 FQDN，然後按一下**[確定]**

![後端集區 pool2 設定][9]

## <a name="create-listeners-for-each-back-end"></a>建立每個後端的接聽程式

應用程式閘道依賴 HTTP 1.1 以上某個網站上的主機標頭 toohost hello 相同的公開 IP 位址和連接埠。 hello 基本接聽程式 hello 入口網站中建立不包含這個屬性。

### <a name="step-1"></a>步驟 1

按一下**接聽程式**hello 現有應用程式閘道且按一下**多站台**tooadd hello 第一個接聽程式。

![接聽程式概觀刀鋒視窗][1]

### <a name="step-2"></a>步驟 2

填寫 hello hello 接聽程式的資訊。 在此範例中，會設定 SSL 終止，建立新的前端連接埠。 上傳 hello.pfx 憑證 toobe 用於 SSL 終止。 hello 這個刀鋒視窗中比較 toohello 標準基本的接聽程式 刀鋒視窗的唯一差異是 hello 主機名稱。

![接聽程式屬性刀鋒視窗][2]

### <a name="step-3"></a>步驟 3

按一下**多站台**和 hello hello 第二個網站的上一個步驟中所述，建立其他接聽程式。 請確定 toouse hello 第二個接聽程式的不同憑證。 hello 這個刀鋒視窗中比較 toohello 標準基本的接聽程式 刀鋒視窗的唯一差異是 hello 主機名稱。 填寫 hello hello 接聽程式的資訊，然後按一下**確定**。

![接聽程式屬性刀鋒視窗][3]

> [!NOTE]
> 建立 hello 應用程式閘道的 Azure 入口網站中的接聽程式已長時間執行的工作，它可能需要一些時間 toocreate hello 兩個接聽程式在此案例中。 當完成 hello 接聽程式中顯示 hello 入口網站 hello 下列影像所示：

![接聽程式概觀][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>建立規則 toomap 接聽程式 toobackend 集區

### <a name="step-1"></a>步驟 1

瀏覽 tooan 現有應用程式閘道 hello Azure 入口網站 (https://portal.azure.com) 中。 選取**規則**選擇現有預設規則 hello **rule1**按一下**編輯**。

### <a name="step-2"></a>步驟 2

Hello 下列影像中所見，請填寫 hello 規則刀鋒視窗。 選擇第一個接聽程式 hello 和第一個集區，然後按一下**儲存**時完成。

![編輯現有的規則][6]

### <a name="step-3"></a>步驟 3

按一下**基本規則**toocreate hello 第二個規則。 填寫 hello 表單與 hello 第二個接聽程式，第二個後端集區，然後按一下**確定**toosave。

![新增基本規則刀鋒視窗][10]

這種情況下完成使用多站台支援透過 hello Azure 入口網站中設定現有的應用程式閘道。

## <a name="next-steps"></a>後續步驟

深入了解如何 tooprotect 與網站[應用程式閘道的 Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
