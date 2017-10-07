---
title: "aaaCreate Azure 應用程式閘道-Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用應用程式閘道 toocreate hello Azure CLI 1.0 資源管理員 中"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>使用 Azure CLI hello 建立應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 範本](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Azure 應用程式閘道是第 7 層負載平衡器。 無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。 應用程式閘道有下列應用程式傳遞功能的 hello: HTTP 負載平衡、 cookie 架構工作階段親和性，以及安全通訊端層 (SSL) 卸載自訂健全狀況探查，以及支援多站台。

## <a name="prerequisite-install-hello-azure-cli"></a>必要條件： 安裝 hello Azure CLI

tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](../xplat-cli-install.md) ，而且您需要太[登入 tooAzure](../xplat-cli-connect.md)。 

> [!NOTE]
> 如果您沒有 Azure 帳戶，就需要申請一個。 請 [在此處註冊免費試用](../active-directory/sign-up-organization.md)。

## <a name="scenario"></a>案例

在此案例中，您學會如何應用程式閘道使用 toocreate hello Azure 入口網站。

此案例將會：

* 建立含有兩個執行個體的中型應用程式閘道。
* 建立名為 ContosoVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。
* 建立名為 subnet01 且使用 10.0.0.0/28 作為其 CIDR 區塊的子網路。

> [!NOTE]
> 額外設定 hello 應用程式閘道，包括自訂健全狀況探查，hello 應用程式閘道設定之後，而不會在初始部署設定後端集區位址，以及其他規則。

## <a name="before-you-begin"></a>開始之前

「Azure 應用程式閘道」需要有自己的子網路。 當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。 一旦您部署應用程式閘道 tooa 子網路時，唯一的額外應用程式閘道就能 toobe 加入 toohello 子網路。

## <a name="log-in-tooazure"></a>登入 tooAzure

開啟 hello **Microsoft Azure 命令提示字元**，並登入。 

```azurecli-interactive
azure login
```

一旦您輸入 hello 前面範例中，將程式碼。 瀏覽 toohttps://aka.ms/devicelogin 瀏覽器 toocontinue hello 登入處理序。

![顯示裝置登入的 cmd][1]

在 hello 瀏覽器中，輸入您收到 hello 程式碼。 您已重新導向的 tooa 登入頁面。

![瀏覽器 tooenter 程式碼][2]

一旦輸入 hello 程式碼後您登入，關閉 hello 瀏覽器 toocontinue 與 hello 案例。

![已順利登入][3]

## <a name="switch-tooresource-manager-mode"></a>切換 tooResource 管理員模式

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

建立 hello 應用程式閘道之前, 建立 toocontain hello 應用程式閘道資源群組。 hello 下列範例示範 hello 命令。

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>建立虛擬網路

一旦建立 hello 資源群組時，虛擬網路被建立 hello 應用程式閘道。  在下列範例的 hello，hello 位址空間是為 10.0.0.0/16 hello 上述案例附註中定義。

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>建立子網路

Hello 虛擬網路建立之後，會將子網路加入 hello 應用程式閘道。  如果您計劃 toouse 應用程式閘道與 web 應用程式裝載於 hello 相同虛擬網路與 hello 應用程式閘道，可確定 tooleave 足夠空間供另一個子網路。

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>建立 hello 應用程式閘道

一旦建立 hello 虛擬網路和子網路，hello hello 應用程式閘道的必要元件都已完成。 此外還需要下列步驟的 hello hello 憑證的先前匯出的.pfx 憑證和 hello 密碼： hello 用於 hello 後端的 IP 位址是 hello 的後端伺服器的 IP 位址。 這些值可以是任一個私用 Ip hello 虛擬網路、 公用 ip 時或針對後端伺服器的完整的網域名稱。

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> 如需清單，可以執行下列命令的 hello 建立期間提供的參數： **azure 網路的應用程式閘道建立-協助**。

這個範例會建立基本應用程式閘道 hello 接聽程式、 後端集區、 後端 http 設定和規則的預設設定。 可以修改這些設定 toosuit 部署一旦 hello 佈建成功。
如果您已經使用在先前步驟中，一旦建立，hello hello 後端集區定義的 web 應用程式負載平衡開始。

## <a name="next-steps"></a>後續步驟

了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)

了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
