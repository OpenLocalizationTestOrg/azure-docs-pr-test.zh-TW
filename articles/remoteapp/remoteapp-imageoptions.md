---
title: "Azure RemoteApp 映像 aaaCreate |Microsoft 文件"
description: "了解可用來建立的 Azure RemoteApp 映像的 hello 選項"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>建立 Azure RemoteApp 映像
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 使用映像 toohold hello 應用程式，您與您的使用者共用。 （我們接受您的映像並使用它 toocreate Vm 層的什麼 hello 當使用者存取他們登入 Azure RemoteApp。）toocreate 與您所選擇的應用程式的 Azure RemoteApp 集合，不論是雲端或混合式，開始您以建立映像與安裝這些應用程式。 接著，建立集合，其中會使用該映像、 將使用者指派 toohello 集合和發佈應用程式 toothose 使用者。

您有幾個選項可建立或使用映像。 基本的 hello[需求](remoteapp-imagereqs.md)的映像的是執行 Windows Server 2012 R2 且已安裝的 hello 遠端桌面工作階段主機 (RDSH) 角色。 如何達成就是有趣的地方。

您有下列選項，當 tooimages hello:

* 您可以匯入和使用 [根據 Azure 虛擬機器的映像](remoteapp-image-on-azurevm.md)。 這適用於需要自訂設定的特定業務應用程式。 您可以自訂 hello 映像 toowork hello 應用程式。
* 您可以 [建立和上傳自訂映像](remoteapp-create-custom-image.md)。 如果您已經有用於內部部署遠端桌面服務部署的映像，則這十分不錯。
* 您可以使用其中一個 hello[範本映像](remoteapp-images.md)納入 RemoteApp 訂用帳戶。 這些映像所建立，且由 hello RemoteApp 團隊負責維護，且包含一些標準應用程式 （例如 hello Office 套件），您可以將可用的 tooyour 使用者。 請注意只有 hello Office 365 Pro Plus 映像可用於生產設定。

不論您用來取得您的映像，或您建立的方式，您需要確定您了解 hello toomake[應用程式需求](remoteapp-appreqs.md)您的應用程式都適用於 RemoteApp 的 tooensure。 接著，hello 下一個步驟就是 toocreate[雲端](remoteapp-create-cloud-deployment.md)或[混合式](remoteapp-create-hybrid-deployment.md)集合。

