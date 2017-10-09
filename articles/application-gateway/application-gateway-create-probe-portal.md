---
title: "aaaCreate 自訂探查-Azure 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "了解如何 toocreate 自訂探查應用程式閘道使用 hello 入口網站"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>建立自訂探查使用 hello 入口網站應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure 傳統 PowerShell](application-gateway-create-probe-classic-ps.md)

在本文中，您可以加入自訂探查 tooan 現有應用程式閘道透過 hello Azure 入口網站。 自訂探查適合應用程式的健全狀況檢查 頁面，或未提供成功的回應 hello 預設 web 應用程式的應用程式。

## <a name="before-you-begin"></a>開始之前

如果您還沒有應用程式閘道，請瀏覽[建立應用程式閘道](application-gateway-create-gateway-portal.md)toocreate 應用程式閘道 toowork 與。

## <a name="createprobe"></a>建立 hello 探查

探查的兩步驟程序，透過 hello 入口網站中設定。 hello 第一個步驟是 toocreate hello 探查。 在 hello 第二個步驟中，您可以加入 hello 探查 toohello 後端 http 設定的 hello 應用程式閘道。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 如果您沒有帳戶，可以註冊[免費試用一個月](https://azure.microsoft.com/free)

1. 在 hello Azure 入口網站的 我的最愛 窗格中，按一下 所有資源。 按一下 hello 應用程式閘道 hello 中的所有資源刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入 hello 篩選 partners.contoso.net 依名稱... 方塊 tooeasily 存取 hello 應用程式閘道。

1. 按一下**探查**按一下 hello**新增**按鈕 tooadd 探查。

  ![已填入資訊的 [新增探查] 刀鋒視窗][1]

1. 在 hello**新增健全狀況探查**刀鋒視窗中，填寫必要的 hello 資訊 hello 探查和完成時按一下**確定**。

  |**設定** | **值** | **詳細資料**|
  |---|---|---|
  |**名稱**|customProbe|此值為 hello 入口網站中存取的易記名稱 toohello 探查。|
  |**通訊協定**|HTTP 或 HTTPS | hello 健全狀況探查的 hello 通訊協定使用。|
  |**Host**|亦即 contoso.com|這個值是用於 hello 探查 hello 主機名稱。 只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。 這個值會與 hello VM 主機名稱不同。|
  |**路徑**|/ 或另一個路徑|hello hello 完整 hello 自訂探查 url 的其餘部分。 有效路徑的開頭為 '/'。 只要 http://contoso.com hello 預設路徑使用 '/' |
  |**間隔 (秒)**|30|Hello 探查是的執行頻率 toocheck 健全狀況。 不建議 tooset hello 低於 30 秒。|
  |**逾時 (秒)**|30|逾時之前，等候時間 hello 探查的 hello 數量。使用 hello 逾時時間間隔需求 toobe 高 tooensure hello 後端健全狀況 頁面可以進行 http 呼叫。|
  |**狀況不良臨界值**|3|被視為狀況不良的嘗試 toobe 失敗的次數。 如果健全狀況檢查失敗後端的 hello 決定不良立即 0 表示的臨界值。|

  > [!IMPORTANT]
  > hello 主機名稱不是 hello 做為伺服器名稱相同。 此值為 hello hello hello 應用程式伺服器上執行的虛擬主機名稱。 傳送嗨探查 toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>新增探查 toohello 閘道

既然 hello 探查建立之後，它是時間 tooadd 它 toohello 閘道。 探查設定會設定在 hello 的 hello 應用程式閘道後端 http 設定值。

1. 按一下**HTTP 設定**hello 應用程式在閘道上，toobring hello 組態刀鋒視窗上的按一下 hello 目前後端 http 設定 hello 視窗中列出。

  ![[https 設定] 視窗][2]

1. 在 hello **appGatewayBackEndHttpSettings**設定] 刀鋒視窗中，核取 hello**使用自訂探查**核取方塊，然後選擇 建立 hello 中的 hello 探查[建立 hello 探查](#createprobe)區段在 hello**自訂探查**下拉式清單...
完成後，按**儲存**和 hello 設定會套用。

hello 預設探查檢查 hello 預設存取 toohello web 應用程式。 已建立自訂探查，hello 應用程式閘道會使用針對 hello 後端伺服器 hello 定義的自訂路徑 toomonitor 健全狀況。 根據已定義的 hello 準則，hello 應用程式閘道會檢查 hello hello 探查中指定的路徑。 如果 hello 呼叫 toohost:Port / 路徑不會傳回 HTTP 200 399 狀態回應，hello 伺服器不會採取離輪替循環達到 hello 狀況不良閾值後。 探查時，會繼續在 hello 狀況不良的執行個體 toodetermine 它再度變成狀況良好。 流量 hello 執行個體，加入之後回復 toohealthy 伺服器集區開始再次流動 tooit 以及探查 toohello 執行個體會繼續依使用者指定的間隔，像平常一樣。

## <a name="next-steps"></a>後續步驟

如何 tooconfigure SSL 卸載，以及 Azure 應用程式閘道，請參閱的 toolearn[設定 SSL 卸載](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

