---
title: "如何從 RemoteApp VNET 移轉至 Azure VNET | Microsoft Docs"
description: "了解如何從 RemoteApp VNET 移轉至 Azure VNET"
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
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a>如何將混合式集合從 RemoteApp VNET 移轉至 Azure VNET
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

好消息！ 我們已讓您將混合式 RemoteApp 集合直接部署到現有 Azure 虛擬網路 (VNET)，而未建立 RemoteApp 特定 VNET。 這可讓您利用最新的 VNET 功能 (如 ExpressRoute)，並將部署至該 VNET 之其他 Azure 服務和虛擬機器的直接網路存取權提供給混合式集合   (這與 VNET 對 VNET 組態相較之下，可讓您擁有更佳的效能和更簡單的設定)。

假設，您已經建立稱為「OriginalCollection」的混合式 RemoteApp 集合與稱為「RemoteAppVNET」的 RemoteApp VNET。 以下是將它移轉至稱為 *AzureVNET*之新 Azure VNET 的步驟。

1. 在[管理入口網站](http://manage.windowsazure.com/)的 [網路] 索引標籤上，使用與用於 RemoteAppVNET 相同的位置、DNS 組態和位址空間 (針對至少其中一個 AzureVNET 子網路) 建立稱為 AzureVNET 的 VNET。
2. 設定 AzureVNET 裝載或透過網路連接到 OriginalCollection 加入網域的 Active Directory 部署。
3. 在 [RemoteApp] 索引標籤上，建立稱為「新集合」的新 RemoteApp 集合  (使用 [使用 VNET 建立] 選項，而不是 [快速建立])。
4. 設定要部署到 AzureVNET 中子網路的 NewCollection。
5. 設定 NewCollection 使用與您用於 OriginalCollection 相同的映像和網域加入資訊。
6. 在幾個小時後， *NewCollection* 會顯示在集合清單中，且狀態為 [作用中]。

現在，如果您不需要將任何使用者資訊從原始集合移轉到新的集合，請接著執行下列步驟：

1. 刪除 *OriginalCollection*。
2. 刪除 *RemoteAppVNET*。

大功告成！

或者，如果您需要將使用者資訊從原始集合移轉到新的集合，請接著執行下列步驟：

1. 使用 Azure 訂用帳戶識別碼、原始集合名稱以及新集合名稱，將電子郵件傳送給 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) ，並要求他們移轉您的使用者資訊。
2. 在 2 個工作日內，RemoteApp 小組會將使用者存取清單以及所有使用者文件和使用者設定從原始集合移至新的集合。
3. 刪除 *OriginalCollection*。
4. 刪除 *RemoteAppVNET*。

現在，大功告成！

如果您有任何疑問或需要特殊協助，請將電子郵件寄到 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help)的 RemoteApp VNET。

