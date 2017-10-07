---
title: "使用 Azure RemoteApp aaaValidate hello Azure VNET toouse |Microsoft 文件"
description: "了解如何 toomake 確定 Azure VNET 準備使用 Azure RemoteApp toouse"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>驗證與 Azure RemoteApp 一起 hello Azure VNET toouse
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

您可以使用 Azure VNET 與 Azure RemoteApp 之前，您可能想 toovalidate hello VNET。 這有助於避免發生連線問題。

toovalidate Azure VNET 中，執行下列 hello:

1. 建立 Azure 虛擬機器內的 hello Azure VNET，您想要使用 Azure RemoteApp toouse hello 子網路。
2. 使用 hello 連線 toothat VM**連接**hello 管理入口網站中的選項。
3. 加入 hello 虛擬機器 toohello 您想使用 Azure RemoteApp toouse 相同的網域。 如果您要建立混合式集合 tooyour 在內部部署網路連線，再加入 hello 虛擬機器 tooyour 本機網域。

如果成功，hello Azure VNET 是準備 toouse RemoteApp 使用。

如需 hello 端對端混合式集合工作流程的詳細資訊，請參閱下列文章的 hello:

* [如何 tooplan 的 Azure RemoteApp 虛擬網路](remoteapp-planvnet.md)
* [建立混合式收藏](remoteapp-create-hybrid-deployment.md)
* [部署 Azure RemoteApp 集合 tooyour Azure 虛擬網路 （透過 ExpressRoute 支援）](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

