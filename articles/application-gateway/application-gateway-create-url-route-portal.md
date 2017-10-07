---
title: "將路徑架構的 aaaCreate 規則-Azure 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate 應用程式閘道使用的路徑規則 hello 入口網站"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>透過 hello 入口網站建立應用程式閘道的路徑規則

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

路徑為基礎的路由 URL 可讓您 tooassociate 路由根據 hello 的 Http 要求的 URL 路徑。 它會檢查是否為 hello 應用程式閘道中所列的 hello URL 設定路由 tooa 後端集區，並將傳送 hello 網路流量 toohello 定義後端集區。 URL 為基礎的路由的常見用法是不同的內容類型 toodifferent 後端伺服器集區的 tooload 平衡要求。

URL 為基礎的路由導入了新的規則類型 tooapplication 閘道。 應用程式閘道具有兩種規則類型：基本和路徑型規則。 hello 基本規則類型，並提供循環配置資源服務的 hello 後端集區的路徑為基礎的規則時此外 tooround 環散佈，也會考量 hello 要求 URL 的路徑模式並選擇 hello 適當的後端集區。

## <a name="scenario"></a>案例

hello 下列案例會經歷在現有的應用程式閘道中建立路徑為基礎的規則。
hello 案例假設您已經有太遵循 hello 步驟[建立應用程式閘道](application-gateway-create-gateway-portal.md)。

![URL 路由][scenario]

## <a name="createrule"></a>建立 hello 路徑型規則

路徑為基礎的規則建立 hello 規則確定您有可用的接聽程式 toouse 的 tooverify 之前需要它自己的接聽程式。

### <a name="step-1"></a>步驟 1

瀏覽 toohello [Azure 入口網站](http://portal.azure.com)選取現有的應用程式閘道。 按一下 [規則] 

![應用程式閘道概觀][1]

### <a name="step-2"></a>步驟 2

按一下**路徑基礎**按鈕 tooadd 新路徑為基礎的規則。

### <a name="step-3"></a>步驟 3

hello**加入路徑為基礎的規則**分頁有兩個區段。 hello 第一個區段是定義 hello 接聽程式、 hello 名稱 hello 規則以及 hello 預設路徑設定位置。 hello 預設路徑設定為未落在 hello 自訂路徑型路由的路由。 hello 第二個區段的 hello**加入路徑為基礎的規則**刀鋒視窗是您在其中定義 hello 路徑為基礎的規則本身。

**基本設定**

* **名稱**-此值為 hello 入口網站中存取的易記名稱 toohello 規則。
* **接聽程式**-這個值是用於 hello 規則 hello 接聽程式。
* **預設 後端集區**-此設定是定義 hello 用於 hello 預設規則的後端 toobe hello 設定
* **預設的 HTTP 設定**-此設定是定義 hello hello 預設規則使用的 HTTP 設定 toobe hello 設定。

**路徑型規則**

* **名稱**-這個值是易記的名稱 toopath 型規則。
* **路徑**-此設定可定義 hello 路徑 hello 規則會搜尋時將流量轉送
* **後端集區**-此設定是定義 hello 後端 toobe hello 規則使用的 hello 設定
* **HTTP 設定**-此設定是定義 hello hello 規則使用的 HTTP 設定 toobe hello 設定。

> [!IMPORTANT]
> 路徑模式 toomatch 路徑： hello 清單。 每個開頭必須是 / 和 hello 唯一地方"\*」 允許 hello 結尾會。 有效範例包括 /xyz、/xyz* 或 /xyz/*。  

![已填入資訊的新增路徑型規則刀鋒視窗][2]

新增路徑為基礎的規則 tooan 現有應用程式閘道會是簡單的程序，透過 hello 入口網站。 建立路徑規則之後，它可以編輯的 tooadd 其他規則。 

![新增其他路徑型規則][3]

此步驟會設定路徑型路由。 要求不會重寫的重要 toounderstand，因為要求來自於應用程式閘道會檢查 hello 要求和 basic hello url 模式傳送嗨要求 toohello 適當後端上。

## <a name="next-steps"></a>後續步驟

如何 tooconfigure SSL 卸載，以及 Azure 應用程式閘道，請參閱的 toolearn[設定 SSL 卸載](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
