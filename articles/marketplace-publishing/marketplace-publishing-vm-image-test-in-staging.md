---
title: "您的 VM 提供 hello Marketplace aaaTest |Microsoft 文件"
description: "了解如何 tootest VM 的映像 hello Azure Marketplace。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>在預備環境中測試您的 VM 優惠 hello Azure Marketplace
預備部署您的 「 沙箱 」 可測試及驗證其功能，再將其部署 toohello Marketplace 的私用的 SKU 的方式。 hello SKU 會出現在暫存就像是 tooa 客戶已經部署。 您的 VM 映像必須是推入的認證的 toobe toostaging。

## <a name="step-1-push-your-offer-toostaging"></a>步驟 1： 推入的供應項目 toostaging
1. 在 hello**發行**索引標籤上，按一下 **推送 tooStaging**。
   
    ![繪圖](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. 如果 hello 發佈入口網站會通知您的任何錯誤，更正它們。
3. 在 hello**誰可以存取您提供執行的服務？**對話方塊方塊中，輸入 Azure 訂用帳戶，您將使用 toopreview 您提供的服務中 hello hello 清單[Azure preview 入口網站](https://portal.azure.com)。
   
   > [!NOTE]
   > 如果是「虛擬機器」和「方案」範本，請 **不要** 將 CSP、DreamSpark 或 Azure in Open 類型的訂用帳戶加入允許清單。
   > 
   > 

    > 發生虛擬機器，當您按一下 [hello] 5d; 按鈕**發送 tooSTAGING**，hello 步驟會執行背後 hello 場景。 您將會無法 tooview hello 進度 hello hello 發行 索引標籤底下的每個步驟的發佈入口網站。 您必須檢查這個頁面在定期間隔 （直到 hello 狀態顯示分段） 需要從您的 end 更正任何失敗資訊。

    > - 一開始您執行的要求會驗證 hello vhd toohello 憑證小組。 不過，如果您的要求有只有行銷變更，然後 hello 憑證會略過步驟。
    > - Hello 憑證完成之後，複寫的 hello 供應項目開始，所有 hello Azure 資料中心。 它通常會採用 24-48hours hello 複寫 toocomplete 的但可能佔用 tooa 週 hello hello vhd 大小而定。 不過，如果您的要求有只有行銷變更，hello 複寫會更快。
    > - Hello 複寫完成時，則 hello 供應項目會提供在 hello [Azure 入口網站](http:/portal.azure.com)。 在該時間 hello 狀態變成暫置在 hello 中發佈入口網站。 階段式供應項目會顯示在 hello [Azure 入口網站](http:/portal.azure.com)只能使用 hello 與 hello 接移的 hello 與優惠的訂用帳戶相關聯的電子郵件識別碼。

1. 登入 toohello [Azure preview 入口網站](https://portal.azure.com)使用其中一種 hello Azure 訂用帳戶中所列 hello 上一個步驟。
2. 尋找您的供應項目，並驗證您的 VM 映像點：
   
   * 請確定在行銷內容可正確顯示 hello Marketplace 中。
   * 端對端部署的 hello VM 映像。
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> 您提供的服務將保留在暫存直到您通知 Microsoft hello 發佈入口網站透過 [**發行** 索引標籤 > hello 5d; 按鈕按一下**」 要求核准 tooPush tooProduction 」**] 您已準備好 toopushtooproduction。 這是小組的理想的時間 toohave，透過在您要列出的優惠準備的所有項目檢查您的所有成員。
> 
> hello 發行者在預覽模式中的測試 hello 供應項目的保護 hello 暫存平台。 我們強烈建議您勿將此平台使用於商業用途。
> 
> 

## <a name="next-steps"></a>後續步驟
既然您提供的服務 「 預備 」，且您已測試其功能與行銷內容，您可以繼續 toohello 最終發行階段中，**步驟 4**:[部署您的優惠 toohello Marketplace](marketplace-publishing-push-to-production.md)。

## <a name="see-also"></a>另請參閱
* [快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)

