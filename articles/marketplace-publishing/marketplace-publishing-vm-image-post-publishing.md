---
title: "您的虛擬機器映像中 hello Azure Marketplace aaaManaging |Microsoft 文件"
description: "上如何 toomanage 您的虛擬機器映像 hello Azure Marketplace 中之後初始發行集的詳細的指引"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>虛擬機器後製指南所提供的 hello Azure Marketplace
本文說明如何更新 hello Azure Marketplace 中的即時虛擬機器提供項目。 它會引導您完成新增一或多個新的 Sku tooan 現有的優惠的 hello 程序。 它也會引導您 hello 程序的即時虛擬機器提供項目或 SKU 移除 hello Marketplace。

供應項目/SKU 已經暫置在 hello 之後[Azure 入口網站](http://portal.azure.com)，您無法變更下列文字方塊中的 hello:

* **提供的識別項**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。 然後按一下 [VM 映像] > [供應項目識別碼]。
* **SKU 識別碼**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。 然後按一下 [SKU] > [新增 SKU]。
* **發行者命名空間**: hello 在發行入口網站，太移**虛擬機器** > **逐步解說** > **告訴我們有關您公司**（在 「 步驟 2 註冊您公司 」 下找到） >**發行者命名空間** > **命名空間**。

Hello 優惠/SKU 會列在 hello 之後[Marketplace](http://azure.microsoft.com/marketplace)，您無法變更下列文字方塊中的 hello:

* **提供的識別項**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。 然後按一下 [VM 映像] > [供應項目識別碼]。
* **SKU 識別碼**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。 然後按一下 [SKU] > [新增 SKU]。
* **發行者命名空間**: hello 在發行入口網站，太移**虛擬機器** > **逐步解說** > **告訴我們有關您公司**（找到在 「 步驟 2 註冊 」）**發行者命名空間** > **命名空間**。
* **連接埠**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。 然後按一下 [VM 映像] > [開啟連接埠]。
* **已列出 SKU 的價格變更**
* **已列出 SKU 的計費模式變更**
* **移除已列出 SKU 的計費區域**
* **變更的 hello 資料磁碟計數列出 SKU(s)**

## <a name="update-hello-technical-details-of-a-sku"></a>更新 hello SKU 的技術詳細資料
新的版本 toohello tooadd 列 SKU 和重新發行您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello **VM 映像**] 索引標籤。
4. 在 hello **Sku**區段中，找出您想 tooupdate SKU hello。
5. 加入新的版本號碼的 hello SKU，然後按一下 hello  **+**   按鈕。 hello 新的版本應該採用 X.Y.Z 格式，X、 Y 和 Z 都是整數。 只能以累加方式變更版本。
6. 在 hello **OS VHD URL**方塊、 輸入 hello 共用的存取簽章 URI 建立 hello 作業系統 VHD 和儲存 hello 的變更。

   > [!IMPORTANT]
   > 您無法遞增/遞減 hello 資料磁碟計數列出的 SKU。 在此情況下，您需要 toocreate 新 SKU。 如需詳細指引，請參閱 toohello 區段[加入列出的供應項目底下的新 SKU](#add-a-new-sku-under-a-listed-offer)。
   >
   >
7. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
8. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![VM 映像](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>更新優惠或 SKU 的 hello 非技術性的詳細資料
您可以更新 hello 非技術性 (行銷、 legal 支援類別目錄) 即時優惠或 SKU 的 hello Marketplace 中的詳細資料。

### <a name="update-hello-offer-description-and-logos"></a>更新 hello 供應項目描述和標誌
tooupdate hello 優惠詳細資料和重新發行您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。
4. 按一下 [英文 (美國)]。
5. 按一下 hello**詳細資料** 索引標籤。在 hello**描述**區段中，更新 hello 優惠**標題**，**摘要**，和**長摘要**儲存 hello 的變更。

   > [!NOTE]
   > 當您更新 hello SKU 詳細資料時，請注意這些限制： 
   * 請勿將重複的文字輸入 hello 供應項目描述和 hello SKU 描述。
   * 請勿 hello SKU 標題和 hello 供應項目完整摘要輸入重複的文字。 
   * 請勿為 hello SKU 標題和 hello 供給摘要輸入重複的文字。
   >
   >

    ![詳細資料](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. 在 hello**標誌**區段 hello**詳細資料**索引標籤上，更新 hello 標誌。 請確定 hello 標誌遵循 hello [Azure Marketplace 的指導方針](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。

   > [!NOTE]
   > 主圖圖示是選擇性的。 您可以選擇不 tooupload 英雄圖示。 不過上, 傳英雄圖示之後，沒有任何佈建 toodelete 從 hello 發佈入口網站。 請遵循 hello[英雄圖示指導方針](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。
   >
   >
7. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
8. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![標誌](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>更新 hello SKU 描述
tooupdate hello SKU 詳細資料，並重新發行您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。
4. 按一下 [英文 (美國)]。
5. 按一下 hello**計劃**] 索引標籤。在 [hello **Sku**區段中，更新 hello SKU**標題**，**摘要**，和**描述**儲存 hello 的變更。

   > [!NOTE]
   > 當您更新 hello SKU 詳細資料時，請注意這些限制： 
   * 請勿將重複的文字輸入 hello 供應項目描述和 hello SKU 描述。 
   * 請勿 hello SKU 標題和 hello 供應項目完整摘要輸入重複的文字。 
   * 請勿為 hello SKU 標題和 hello 供給摘要輸入重複的文字。
   >
   >
6. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
7. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![方案](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>變更現有連結或新增連結
toochange 現有連結或加入新的連結，然後重新發佈您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。
4. 按一下 [英文 (美國)]。
5. 按一下 hello**連結** 索引標籤。
6. 新的連結，在 hello tooadd**連結**區段中，按一下**+ 加入連結**。 在 hello**加入連結**對話方塊方塊中，輸入 hello 連結**標題**和**URL**儲存 hello 的變更。 您可以輸入任何包含資訊來協助客戶的連結。
7. tooupdate 或刪除現有連結，請選取 hello 連結，然後按一下 hello**編輯**按鈕或 hello**刪除** 按鈕。

   > [!NOTE]
   > 請確定您已輸入本節中的 hello 連結正常運作，因為這些連結取得驗證您在實際執行要求程序。
   >
   >
8. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
9. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![連結](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![新增連結](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>變更現有範例映像或新增範例映像
現有的範例 toochange 映像或加入新的範例映像，然後重新發佈您的優惠，請遵循下列步驟：

> [!NOTE]
> 只有一個範例影像會顯示在 hello [Azure 入口網站](https://portal.azure.com)。
>
>

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。
4. 按一下 [英文 (美國)]。
5. 按一下 hello**範例影像** 索引標籤。
6. 新範例映像，在 hello tooadd**範例影像**區段中，按一下**上傳新的映像**儲存 hello 的變更。

   > [!NOTE]
   > 包含範例映像是選擇性作業。
   >
7. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
8. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![範例映像](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>更新 hello 合法的內容
tooupdate hello 合法的內容重新發佈您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。
4. 按一下 [英文 (美國)]。
5. 按一下 hello**合法**] 索引標籤。在 [hello**合法**區段中，更新使用您原則/詞彙。 輸入或貼上 hello hello 原則/詞彙**使用條款**方塊，並儲存 hello 變更。
6. 使用 hello 法律規定 hello 字元限制為 1 百萬個字元。
7. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
8. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![法律](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>更新 hello 支援資訊
tooupdate hello 支援資訊並重新發行您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**支援**] 索引標籤。
4. 在 hello**工程連絡**區段中，更新 hello 工程連絡人詳細資料。 這些詳細資料會用於內部通訊 hello 夥伴與 Microsoft 之間只。
5. 在 hello**客戶支援部門**區段中，更新 hello 支援連絡人詳細資料和 hello**支援 URL**。 這些詳細資料會用於內部通訊 hello 夥伴與 Microsoft 之間只。

   > [!NOTE]
   > 如果您想 tooprovide 唯一的電子郵件支援，請輸入空的電話號碼中 hello**客戶支援部門**> 一節。 在此情況下，您提供的 hello 電子郵件改為使用。
   >
   >
6. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
7. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![支援](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>更新 hello 類別
tooupdate hello 類別為您提供的服務區段，然後重新發佈您的優惠，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**類別**] 索引標籤。
4. 在 hello**類別**區段中，更新您的優惠的 hello 分類然後儲存 hello 的變更。 您可以選擇 toofive hello Azure Marketplace 的組件庫的類別。
5. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
6. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![類別](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>在已列出的供應項目下新增 SKU
tooadd 新 SKU 中您的提供即時服務，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello **SKU** ] 索引標籤。然後按一下 [新增 SKU]。 
4. 在 [hello] 對話方塊中，輸入**SKU 識別碼**小寫。 選取 hello**攜帶您自己的授權 (BYOL) 計費模型**核取方塊，如果您想 toopublish hello BYOL 計費的模型使用新的 SKU。 否則，請清除 [hello] 核取方塊。 按一下 hello 刻度記號 toocreate 新 SKU。 如果您未選擇 hello BYOL 計費模型，hello 計費模型會自動設定 toohourly。 如果您想 hello 每小時的計費模型的 hello 30 天免費試用版，請選取**一個月**如**可免費試用版嗎？** 否則，請選取 [無試用]。 (**可免費試用版嗎？**時建立 hello 新 SKU 您尚未選取 BYOL 時，才會出現。)

   > [!IMPORTANT]
   > **因為永遠應該購買方案範本透過隱藏 hello Marketplace 從這個 SKU**應該**是***只*如果核准以發佈方案範本。 否則，這個選項應該永遠都是 [否]。
   >
   >
4. 在左側 hello hello 功能表上，按一下 [hello **VM 映像**] 索引標籤，找出 hello 您已建立的新 SKU。
5. tooset 最多 hello 新 SKU，請參閱[取得憑證的 VM 映像](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image)指導方針。
6. 行銷資料 tooadd hello 新 SKU，請參閱[行銷內容提供 Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。
7. 定價資訊的 tooadd hello 新 SKU，請參閱[設定價格](marketplace-publishing-push-to-staging.md#step-2-set-your-prices)。
8. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
9. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![新增 SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>變更所列的 SKU hello 資料磁碟計數
您無法遞增/遞減 hello 資料磁碟計數列出的 SKU。 在此情況下，您需要 toocreate 新 SKU。 如需詳細指引，請參閱 toohello 區段[加入列出的供應項目底下的新 SKU](#add-a-new-sku-under-a-listed-offer)。

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>列出的優惠刪除 hello Marketplace
各個層面需要 toobe 要求 tooremove 即時優惠 hello 案例處理。 hello 支援小組 tooremove hello Marketplace，列出提供項目從 tooget 指引，請遵循下列步驟：

1. 引發支援票證上 hello[建立事件](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681)頁面。

2. 選取 [管理供應項目] 作為 [問題類型]，然後選取 [修改已在生產中的供應項目和/或 SKU] 作為 [類別]。
3. 送出 hello 要求。

hello 支援小組會引導您完成 hello 優惠/SKU 刪除程序。

> [!NOTE]
> 在 [草稿] 狀態 （但不是預備或生產） 時，隨時都可以刪除 hello 供應項目。 在 hello**記錄**索引標籤上，按一下 **捨棄草稿**。
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>從 hello Marketplace 刪除列出的 SKU
toodelete 列出 SKU 從 hello 服務商場，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。

2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在 hello hello 左側窗格，按一下 hello **SKU**  索引標籤。
4. 選取 hello SKU toodelete，並按一下 hello**刪除** 按鈕。
5. 移 toohello**發行** 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello hello Marketplace 中的供應項目。
6. Hello 供應項目會重新發行在 hello Marketplace 之後，會刪除 hello SKU hello Marketplace 和 hello Azure 入口網站。

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>從 hello Marketplace 刪除 hello 目前版本列出的 SKU
toodelete hello 目前版本列出 SKU 從 hello 服務商場，請遵循下列步驟： 

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。

2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello **VM 映像**] 索引標籤。
4. 選取 hello SKU 的目前版本 toodelete，然後按一下 hello**刪除** 按鈕。
5. 移 toohello**發行** 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello hello Marketplace 中的供應項目。
6. Hello 供應項目取得 hello Marketplace 中發佈之後，hello 的 hello 列出的 SKU 從中 hello Marketplace 和 hello Azure 入口網站的目前版本。 hello SKU 將會回復 tooits 先前的版本。

## <a name="revert-hello-listing-price-tooproduction-values"></a>還原 hello 列出價格 tooproduction 值
toorevert hello 清單價格 tooproduction 值，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。
2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello**定價**] 索引標籤。
4. 選取您想要其價格的地區 tooreset。

    ![價格區域](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. 對於每小時的計費模型的 Sku，重設所有 hello 核心的 hello 價格和它們在 hello 所選區域的生產環境中。 Sku BYOL 計費的模型，請選取 hello SKU 的 hello 核取方塊在 hello hello hello 區域中可用的 SKU **EXTERNALLY-LICENSED (BYOL) SKU 可用性**> 一節。

    ![定價模式](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. 按一下 [依據美國價格自動訂定其他市場價格] 。

   > [!NOTE]
   > hello 按鈕的標籤可能會不同，視您選取的 hello 地區而定。 因為我們選取 美國，所以 hello 按鈕的標籤為**AUTOPRICE 其他市場基礎 ON 價格在美國的狀態**。
   >
   >

    ![自動定價](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. 在 hello Autoprice 精靈的第 1 頁，選擇 hello 基底的市場，然後按 hello**箭號** 按鈕。

    ![基底市場](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. 在第 2 頁，選擇服務計劃和公尺 （核心），然後按 hello**箭號** 按鈕。

    ![服務方案和計量](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. 在第 3 頁，按一下 **切換所有**tooselect 所有區域。 或者，您可以手動選取特定區域的核取方塊。 按一下 hello**箭號** 按鈕。

    ![選擇市場](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. 在頁面 4 檢閱 hello 匯率，並按一下**完成**。 hello 精靈會重設 hello 定價相應 tooyour 選取項目。

11. 在 hello**定價**索引標籤上，按一下 **檢視和變更摘要**。
    對於 [檢視版本]，選取 [草稿]，以及針對 [比較項目]，選取 [生產]。 如果您不看到任何價格差異，hello 定價 toohello 生產環境值成功還原。

    ![摘要檢視和變更](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
13. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

## <a name="revert-hello-billing-model-tooproduction-values"></a>還原 hello 計費模型 tooproduction 值
toorevert hello 計費模型 tooproduction 值，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。

2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello **SKU** ] 索引標籤。
4. 按一下 hello**編輯**按鈕 toorevert hello 計費模型。 在 hello 開啟視窗中，選取或清除 hello**計費和授權由外部 Azure （又稱 「 攜帶您自己授權）**核取方塊。

    ![編輯計費](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. 遵循本文章中的"Revert hello 列出價格 tooproduction 值"hello 步驟進行。
6. 移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。 如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。
7. 測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。 按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>還原列出的 SKU toohello 生產環境值 hello 可見性設定
列出 SKU toohello 實際值，toorevert hello 可見性設定，請遵循下列步驟：

1. 登入 toohello[發佈入口網站](https://publish.windowsazure.com)。

2. 移 toohello**虛擬機器**索引標籤，然後選取您的優惠。
3. 在左側 hello hello 功能表上，按一下 [hello **SKU** ] 索引標籤。
4. 選取您的 SKU，並還原 hello 的 hello SKU toohello 生產環境值的可見性設定。

    ![可見性](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. 您已完成 hello 變更之後，請按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。

## <a name="see-also"></a>另請參閱
* [開始： 發佈供應項目 toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* [了解付款報告](marketplace-publishing-report-payout.md)
* [變更雲端解決方案提供者轉售商獎勵](marketplace-publishing-csp-incentive.md)
* [疑難排解 hello Marketplace 中的一般發佈問題](marketplace-publishing-support-common-issues.md)
* [以發佈者身分取得支援](marketplace-publishing-get-publisher-support.md)
* [建立內部部署 VM 映像](marketplace-publishing-vm-image-creation-on-premise.md)
* [建立執行 Windows hello Azure preview 入口網站中的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
