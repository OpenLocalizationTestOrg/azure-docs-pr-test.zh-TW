---
title: "aaaCreate Azure 堆疊中提供項目 |Microsoft 文件"
description: "是雲端系統管理員，瞭解如何 toocreate Azure 堆疊中的租用戶優惠。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a>在 Azure Stack 中建立優惠
[提供](azure-stack-key-features.md)是群組的一或多個計劃存在 tootenants toopurchase 該提供者或訂閱。 本文件說明如何 toocreate 優惠，其中包含 hello[您所建立的計劃](azure-stack-create-plan.md)hello 最後一個步驟中。 這項優惠提供 hello 能力 tooprovision 虛擬機器的 「 訂閱者 」。

1. 登入 toohello 堆疊 Azure 管理員入口網站 (https://adminportal.local.azurestack.external) > 按一下**新增** > **租用戶提供 + 計劃** >  **提供**。

   ![](media/azure-stack-create-offer/image01.png)
2. 在 hello**新提供**刀鋒視窗中，填滿**顯示名稱**和**資源名稱**，，然後選取新的或現有**資源群組**。 hello 顯示名稱是 hello 供應項目的易記名稱，並且 hello 時，使用者會看到訂閱 hello 優惠 hello 唯一資訊。 因此，請確定 toouse 直覺式的名稱，可協助 hello 使用者了解隨附 hello 優惠的內容。 只有 hello 管理員可以看到 hello 資源名稱。 它的 hello 名稱，系統管理員 」 搭配 toowork hello 供應項目做為 Azure 資源管理員資源。

   ![](media/azure-stack-create-offer/image01a.png)
3. 按一下**基底計劃**，而在 hello**規劃**刀鋒視窗中，選取 hello 計劃您想要在 hello 優惠 tooinclude，然後按一下**選取**。 按一下**建立**toocreate hello 供應項目。

   ![](media/azure-stack-create-offer/image02.png)
4. 按一下**所有資源**、 新的優惠搜尋、 按一下 hello 新的優惠，然後按一下**狀態變更**，然後按一下**公用**。

   ![](media/azure-stack-create-offer/image03.png)

提供項目必須會公開讓租用戶 tooget hello 完整檢視訂閱時。 供應項目可以是：

* **公用**： 可見 tootenants。
* **私用**： 只顯示 toohello 雲端系統管理員。 有用時草擬階段 hello 計劃或提供的服務，或如果 hello 雲端系統管理員想 tooapprove 每個訂用帳戶。
* **解除委任**： 關閉 toonew 「 訂閱者 」。 hello 雲端系統管理員可以使用已解除委任的 tooprevent 未來的訂閱，但保留目前的訂閱者不變。

變更 toohello 供應項目不會立即看到 toohello 租用戶。 toosee hello 變更，您可能必須 toologout/登入 toosee hello 新訂用帳戶中 hello 」 訂用帳戶選擇器 」 時建立資源/資源群組。

> [!NOTE]
>您也可以使用 PowerShell hello 中所述建立預設優惠、 計劃和配額[Azure 堆疊服務系統管理員讀我檔案](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin)。
>


## <a name="next-steps"></a>後續步驟
[訂閱 tooan 供應項目，然後佈建 VM](azure-stack-subscribe-plan-provision-vm.md)
