---
title: "aaaManage 網路安全性群組流程記錄檔與 Azure 網路監看員 |Microsoft 文件"
description: "此頁面說明 toomanage 網路安全性小組流程如何登入 Azure 網路監看員"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>管理網路安全性群組資料流程中的記錄檔 hello Azure 入口網站

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

網路安全性群組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。 這些流量記錄是以 JSON 格式寫入，並提供重要資訊，包括： 

- 每個規則的輸出和輸入流量。
- hello NIC hello 流程，適用於。
- 5 個 tuple hello 資料流程來源/目的地 IP、 來源/目的地連接埠 （通訊協定） 資訊。
- 流量被允許或拒絕的資訊。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員執行個體](network-watcher-create.md)。 hello 案例也會假設您有有效的虛擬機器的資源群組。

## <a name="register-insights-provider"></a>註冊 Insights 提供者

流程記錄 toowork 成功，hello **Microsoft.Insights**必須註冊提供者。 tooregister hello 提供者，採取下列步驟的 hello: 

1. 跳過**訂閱**，然後選取您想要的 tooenable 流程記錄檔的 hello 訂用帳戶。 
2. 在 hello**訂用帳戶**刀鋒視窗中，選取**資源提供者**。 
3. 查看 hello 提供者清單，並確認該 hello **microsoft.insights**註冊提供者。 如果沒有，則選取 [註冊]。

![檢視提供者][providers]

## <a name="enable-flow-logs"></a>啟用流量記錄

這些步驟會引導您啟用網路安全性群組上的流量記錄檔的 hello 程序。

### <a name="step-1"></a>步驟 1

移 tooa 網路監看員執行個體，然後再選取**NSG 流程記錄**。

![流量記錄概觀][1]

### <a name="step-2"></a>步驟 2

從 hello 清單中選取網路安全性群組。

![流量記錄概觀][2]

### <a name="step-3"></a>步驟 3 

在 hello**流程記錄設定**刀鋒視窗中，設定 hello 狀態太**上**，然後設定儲存體帳戶。  完成後，選取 [確定]。 然後選取 [儲存]。

![流量記錄概觀][3]

## <a name="download-flow-logs"></a>下載流量記錄

流量記錄會儲存在儲存體帳戶中。 下載您的流程記錄 tooview 它們。

### <a name="step-1"></a>步驟 1

toodownload 流程記錄檔中，選取**您可以從設定的儲存體帳戶下載流程記錄**。 此步驟會帶您 tooa 儲存體帳戶檢視，您可以選擇哪些記錄檔 toodownload。

![流量記錄設定][4]

### <a name="step-2"></a>步驟 2

移 toohello 正確的儲存體帳戶。 然後選取 [容器] > [insights-log-networksecuritygroupflowevent]。

![流量記錄設定][5]

### <a name="step-3"></a>步驟 3

移 toohello hello 流程記錄檔位置，選取它，並選取**下載**。

![流量記錄設定][6]

Hello 結構 hello 記錄檔的相關資訊，請造訪[網路安全性群組流程記錄概觀](network-watcher-nsg-flow-logging-overview.md)。

## <a name="next-steps"></a>後續步驟

了解如何太[視覺化 NSG 流程記錄與 PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)。

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
