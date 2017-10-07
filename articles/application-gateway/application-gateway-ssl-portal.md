---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "本頁面提供的指示 toocreate 使用 hello 入口網站的應用程式閘道以 SSL 卸載"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>使用 hello 入口網站設定 SSL 卸載的應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。 Hello 前端伺服器安裝並管理 hello web 應用程式，也可以簡化 SSL 卸載。

## <a name="scenario"></a>案例

下列案例中的 hello 經歷設定 SSL 卸載上現有的應用程式閘道。 hello 案例假設您已經有太遵循 hello 步驟[建立應用程式閘道](application-gateway-create-gateway-portal.md)。

## <a name="before-you-begin"></a>開始之前

與應用程式閘道 tooconfigure SSL 卸載，需要憑證。 此憑證會載入上 hello 應用程式閘道和使用 tooencrypt 和解密透過 SSL 傳送嗨流量。 hello 憑證必須 toobe 個人資訊交換 (pfx) 格式。 這種檔案格式允許 hello 私用金鑰 toobe 匯出所需的流量 hello 應用程式閘道 tooperform hello 加密和解密。

## <a name="add-an-https-listener"></a>新增 HTTPS 接聽程式

hello HTTPS 接聽程式會尋找其組態為基礎的流量，並協助路由 hello 流量 toohello 後端集區。

### <a name="step-1"></a>步驟 1

瀏覽 toohello Azure 入口網站並選取現有的應用程式閘道

### <a name="step-2"></a>步驟 2

按一下接聽程式，然後按一下 hello 新增按鈕 tooadd 接聽程式。

![[應用程式閘道概觀] 刀鋒視窗][1]

### <a name="step-3"></a>步驟 3

填寫 hello hello 接聽程式所需的資訊並上傳 hello.pfx 憑證，完成時，請按一下 [確定]。

**名稱**-此值為 hello 接聽程式的易記名稱。

**前端 IP 組態**-這個值是用於 hello 接聽程式的 hello 前端 IP 組態。

**前端連接埠 （名稱/連接埠）** -hello hello 前端 hello 應用程式閘道和使用 hello 實際通訊埠上使用的連接埠的易記名稱。

**通訊協定**-交換器 toodetermine 如果 hello 前端使用 https 或 http。

**憑證 (名稱/密碼)** - 如果使用 SSL 卸載，此設定就需要 .pfx 憑證，並且需要易記名稱和密碼。

![[加入接聽程式] 刀鋒視窗][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>建立規則，並將它關聯 toohello 接聽程式

現在已建立 hello 接聽程式。 它是時間 toocreate hello 接聽程式的規則 toohandle hello 流量。 規則定義流量的多個組態設定，包括是否使用 cookie 架構工作階段親和性、 通訊協定、 連接埠和健全狀況探查為基礎的路由的 toohello 後端集區的方式。

### <a name="step-1"></a>步驟 1

按一下 hello**規則**的 hello 應用程式閘道，然後按一下新增。

![[應用程式閘道規則] 刀鋒視窗][3]

### <a name="step-2"></a>步驟 2

在 hello**加入基本規則**刀鋒視窗中，輸入 hello 規則 hello 易記名稱，然後選擇 hello hello 先前步驟中建立的接聽程式。 選擇 hello 適當的後端集區和設定的 http，然後按一下**[確定]**

![[https 設定] 視窗][4]

hello 設定現在會儲存 toohello 應用程式閘道。 hello 儲存這些設定的程序可能需要一些時間，才可使用 tooview 透過 hello 入口網站或 PowerShell。 儲存之後 hello 應用程式閘道處理 hello 加密和解密的流量。 透過 http 處理 hello 應用程式閘道與 hello 後端 web 伺服器之間的所有流量。 如果透過 https 起始任何通訊回復 toohello 用戶端將會傳回 toohello 加密的用戶端。

## <a name="next-steps"></a>後續步驟

toolearn 如何 tooconfigure 自訂健全狀況探查與 Azure 應用程式閘道，請參閱[建立自訂的健全狀況探查](application-gateway-create-gateway-portal.md)。

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
