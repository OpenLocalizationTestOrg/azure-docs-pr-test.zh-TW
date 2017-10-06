---
title: "連接埠和 Url toowhitelist 的 Azure RemoteApp 部署客戶虛擬網路中的 aaaList |Microsoft 文件"
description: "了解哪些連接埠及所需的通訊透過 Azure RemoteApp tooconfigure 的 Url。"
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>清單中的連接埠和 Url toopermit 存取的 Azure RemoteApp 部署客戶虛擬網路中
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

如果您要部署的虛擬網路 (VNET) 中的 Azure RemoteApp 雲端或混合式集合，請檢閱下列連接埠資訊的 hello。 如需虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。 如果您已經建立網路安全性群組 (NSG) 限制您的集合中的流量 toohello 虛擬網路資源，請確定下列連接埠的 hello 可存取、 允許透過 hello hello 虛擬網路上的安全性原則。 如需網路安全性群組的詳細資訊，請參閱[什麼是網路安全性群組？(NSG)？](../virtual-network/virtual-networks-nsg.md)。

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Azure RemoteApp 的子網路必須存取 toothese 端點和 Url:
* *.servicebus.windows.net
* *.servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* 輸出：TCP：443、9351、9352、10101-10175 
* 選用 – UDP：10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Azure RemoteApp 用戶端需要存取 toothese 端點和 Url:
我是說 hello 等該人員的桌面裝置的用戶端使用 tooconnect toohello 應用程式部署在 hello Azure RemoteApp 集合。

* https://telemetry.remoteapp.windowsazure.com  
* https://*.remoteapp.windowsazure.com （此位址是 hello 選擇性 UDP 連接埠） 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* 輸出：TCP：443  
* 選用 - UDP：3391 

