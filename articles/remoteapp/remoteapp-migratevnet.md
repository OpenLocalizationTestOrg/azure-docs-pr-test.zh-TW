---
title: "從 RemoteApp VNET tooan Azure VNET aaaHow toomigrate |Microsoft 文件"
description: "深入了解如何從 Azure VNET 的 RemoteApp VNET tooan toomigrate"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>如何 toomigrate RemoteApp VNET tooan Azure VNET 中的混合式集合
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

好消息！ 我們已啟用您直接將您現有的 Azure 虛擬網路 (Vnet) 而不是建立特定的 RemoteApp Vnet toodeploy 混合式 RemoteApp 集合。 這可讓您充分利用 hello 的最新的 VNET 功能 （例如 ExpressRoute)，並提供您的混合式集合直接網路存取 tooother Azure 服務和虛擬機器部署 toothat VNET。  (這與 VNET 對 VNET 組態相較之下，可讓您擁有更佳的效能和更簡單的設定)。

假設，您已經建立稱為「OriginalCollection」的混合式 RemoteApp 集合與稱為「RemoteAppVNET」的 RemoteApp VNET。 以下是 hello 步驟 toomigrate 它呼叫新的 Azure VNET 的 tooa *AzureVNET*。

1. Hello 上**網路** 索引標籤中 hello[管理入口網站](http://manage.windowsazure.com/)，建立 VNET 呼叫*AzureVNET*，並使用 （適用於至少一個 hello 相同的位置、 DNS 設定及位址空間hello *AzureVNET*子網路) 與您用於*RemoteAppVNET*。
2. 設定*AzureVNET* tooeither 裝載，或是有網路連線 toohello Active Directory 部署， *OriginalCollection*網域加入。
3. 在 hello **Remoteapp**索引標籤上，建立新的 RemoteApp 集合，稱為*新集合*。 (使用 hello**使用 VNET 建立**選項，不**快速建立**。)
4. 設定*NewCollection* toobe 部署中的子網路 tooa *AzureVNET*。
5. 設定*NewCollection* toouse hello 相同的映像和網域聯結資訊與您用於*OriginalCollection*。
6. 在幾個小時後， *NewCollection* 會顯示在集合清單中，且狀態為 [作用中]。

現在，如果您不需要 toomigrate hello 原始集合 toohello 新集合中的任何使用者資訊，執行下列步驟下一步：

1. 刪除 *OriginalCollection*。
2. 刪除 *RemoteAppVNET*。

大功告成！

或者，如果您需要將使用者資訊 toomigrate hello 原始集合 toohello 新集合中的，執行下列步驟下一步：

1. 傳送電子郵件太[remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration)以您的 Azure 訂用帳戶 ID，請在 hello 您的原始集合的名稱和新的集合，hello 名稱，並要求他們 toomigrate 您的使用者資訊。
2. 2 個工作天內 hello RemoteApp 小組會移動 hello 使用者存取清單和所有使用者文件和使用者設定從 hello 原始集合 toohello 新集合。
3. 刪除 *OriginalCollection*。
4. 刪除 *RemoteAppVNET*。

現在，大功告成！

如果您有任何疑問或需要特殊協助，請將電子郵件寄到 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help)的 RemoteApp VNET。

