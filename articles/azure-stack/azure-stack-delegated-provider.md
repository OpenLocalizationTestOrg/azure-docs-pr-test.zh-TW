---
title: "Azure 堆疊中提供 aaaDelegating |Microsoft 文件"
description: "深入了解如何 tooput 其他人負責建立提供項目和註冊為您的使用者。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: d539cac3ed56f342338c830d95fbec7e93175929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delegating-offers-in-azure-stack"></a>在 Azure Stack 中委派提供項目

Hello Azure 堆疊雲端操作員，您通常要 tooput 其他人負責建立提供項目和註冊為您的使用者。 比方說，如果您是服務提供者，而且您想要向上客戶轉銷商 toosign 和代替您管理它們。 它也可以發生在企業中，如果您是一個中央 IT 群組的成員，而且想部門或分公司 toosign 使用者不需要您介入。

委派，協助您完成這些工作，可幫助您 tooreach 和管理多個使用者與您能 toodo 直接。 hello 下圖顯示一個層級的委派，但 Azure 堆疊支援多個層級。 委派的提供者接著可以委派 tooother 提供者，向上 toofive 層級。

![](media/azure-stack-delegated-provider/image1.png)

Azure 堆疊雲端操作員可以委派 hello 建立優惠和租用戶 tooother 使用者藉由使用 hello 委派功能。

## <a name="roles-and-steps-in-delegation"></a>委派中的角色和步驟
請記住，有三種角色涉及的 toounderstand 委派：

* hello**雲端操作員**管理 hello Azure 堆疊基礎結構、 建立提供項目範本，並委派給其他人提供它 tootheir 使用者。
* hello 委派的雲端系統管理員稱為**委派提供者**。 它們只能隸屬於 tooother 組織 （例如其他 Azure Active Directory 租用戶）。
* **使用者**申請 hello 優惠，用於管理其工作負載、 建立 Vm、 儲存的資料等。

Hello 下列圖片所示，有兩個步驟中設定委派。

1. **識別委派的 hello 提供者**訂閱它們 tooan 優惠根據包含 hello 訂用帳戶服務的計劃。
   訂閱 toothis 優惠的使用者取得部份 hello 雲端系統管理員的功能，包括 hello 能力 tooextend 優惠和符號使用者註冊它們。
2. **委派優惠 toohello 委派提供者**，這項優惠做為範本的可以提供什麼 hello 委派的提供者。 hello 委派的提供者就能 tootake hello 供應項目、 選擇的名稱 （但不是會變更其服務和配額），並提供它 toocustomers。

![](media/azure-stack-delegated-provider/image2.png)

tooact 作為委派的提供者，使用者需要 tooestablish 關聯性與 hello 主要提供者。也就是說，它們需要 toocreate 訂用帳戶。 在此案例中，此訂用帳戶識別為具有 hello 右 toopresent 代表 hello 主要提供者所提供的委派提供者。

一旦建立此關聯性，hello 雲端操作員可以委派提供 toohello 委派提供者。 hello 委派的提供者就能 tootake hello 供應項目、 將它重新命名 （但不是會變更其內容），並提供它 tooits 客戶。

hello 下列各節說明如何 tooestablish 委派的提供者，委派提供項目，並確認使用者可以註冊其。

## <a name="set-up-roles"></a>設定角色

toosee 於工作的委派提供者，您需要新增 tooyour 雲端操作員帳戶中的其他 Azure Active Directory 帳戶。 如果您沒有它們，請建立 hello 兩個帳戶。 hello 帳戶只能隸屬於 tooany AAD 租用戶。 我們會參考 toothem，如 hello 委派提供者 (DP) 和 hello 使用者。

| **角色** | **組織的權限** |
| --- | --- |
| 委派的提供者 |User |
| User |User |

## <a name="identify-hello-delegated-providers"></a>識別委派的 hello 提供者
1. 以雲端操作員身分登入。
2. 建立 hello 供應項目可讓使用者委派 toobecome 提供者。 這需要您根據它建立方案和供應項目：
   
   a.  [建立方案](azure-stack-create-plan.md)。
       這個計畫應該包括 hello 訂閱服務。 在本文章中，我們會使用名為 PlanForDelegation 的方案。
   
   b.  根據此方案[建立供應項目](azure-stack-create-offer.md)。 在本文章中，我們會使用名為 OfferToDP 的供應項目。
   
   c.  Hello 優惠 hello 建立完成之後，請加入 hello 委派提供者做訂閱者 toothis 供應項目，即可**訂閱** &gt; **新增** &gt; **新增租用戶訂用帳戶**。
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> 因為所有 Azure 堆疊優惠，您都需要 hello 選項製作 hello 優惠公用，讓使用者註冊，或讓它維持在私用，而且都擁有 hello 雲端操作員管理 hello 註冊。 委派的提供者通常是一小群，而且您想 toocontrol 人員就會准許 tooit，所以在大部分情況下保留這項優惠私人意義。
> 
> 

## <a name="cloud-operator-creates-hello-delegated-offer"></a>雲端操作員建立 hello 委派的優惠

您現在已建立您的委派提供者。 hello 下一個步驟是建立 hello 計劃，並提供您將 toodelegate，並將會使用您的客戶。 您應該完全依照您想要客戶 toosee 定義這項優惠，因為 hello 委派提供者將無法變更 hello 計劃和它所包含的配額。

1. 身為雲端操作員，請根據它[建立方案](azure-stack-create-plan.md)和[供應項目](azure-stack-create-offer.md)。 在本文章中，我們會使用名為 DelegatedOffer 的供應項目。
   
   > [!NOTE]
   > 這項優惠沒有 toobe 公用。 可以設為公用，如果您選擇，但在大部分情況下，您只要委派提供者 toohave 存取 tooit。 一旦 hello 步驟中所述，您可以委派私人優惠，hello 委派提供者就會具有存取 tooit。
   > 
   > 
1. 委派 hello 供應項目。 移 tooDelegatedOffer，然後在 hello 設定 窗格中，按一下**委派的提供者** &gt; **新增**。
2. 從 [hello] 下拉式清單方塊選取 hello 委派提供者的訂用帳戶，然後按一下**委派**。

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-hello-offer"></a>委派的提供者會自訂 hello 供應項目

登入 toohello**租用戶入口網站**為 hello 委派 提供者，並建立新的優惠使用 hello 委派供應項目做為範本。

1. 按一下 [新增] &gt; [租用戶供應項目 + 方案] &gt; [提供]。

    ![](media/azure-stack-delegated-provider/image5.png)


1. 指派名稱 toohello 供應項目。 這裡我們選擇 ResellerOffer。 它在然後按一下，選取 hello 委派優惠 toobase**建立**。
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > 請注意 hello 差異比較 toooffer 建立為經驗豐富的 hello 雲端操作員。 hello 委派提供者不會建構基底的計劃和附加元件的計畫 hello 提供項目他們可以只選擇已被委派的 toothem，其供應項目，無法進行變更 toothose 優惠。

1. 依序按一下公開提供的 hello**瀏覽** &gt; **提供**、 選取 hello 供應項目，並按一下**狀態變更**。
2. hello 委派提供者會公開這些提供項目透過自己的入口網站 URL。 這些提供項目是只能透過 hello 委派入口網站顯示。 toofind 及變更此 URL:
   
    a.  按一下**瀏覽**&gt; **更多服務**&gt; **訂閱**&gt;選取 hello 委派提供者的訂閱，在我們的案例其*DPSubscription* &gt; **屬性**。
   
    b.  將複製 hello 入口網站 URL tooa 不同的位置，例如 [記事本]。
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   您現在已完成將建立的委派提供 hello 做為委派的提供者。 因為 hello 委派的提供者，請先登出。 關閉已在使用您的 hello 瀏覽器索引標籤。

## <a name="sign-up-for-hello-offer"></a>註冊 hello 優惠
1. 在新的瀏覽器視窗中，移 toohello 委派入口網站在 hello 先前步驟所儲存的 URL。 使用者身分登入 toohello 入口網站。 注意： 使用 hello 委派此步驟中的入口網站。 hello 委派的優惠否則不可見。
2. 在 hello 儀表板中，按一下 **取得訂用帳戶**。 您會看到只 hello 委派提供者所建立的委派 hello 提供會呈現 toohello 使用者：

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

這總結 hello 程序的供應項目委派。 hello 使用者可以立即註冊這項優惠的訂用帳戶取得。

## <a name="multiple-tier-delegation"></a>多層委派

多層式委派可讓委派 hello 提供者 toodelegate 優惠 tooother 實體。 這可讓，比方說，更深入的轉售商通道中的 hello 管理 Azure 堆疊提供者委派優惠 tooa 散發者，後者會委派 tooreseller 人員 hello 建立。
Azure 」 堆疊支援向上 toofive 層級的委派。

toocreate 多個階層提供委派，後者會 hello 委派提供者委派 hello 提供 toohello 下一個提供者。 hello 程序是 hello 相同 hello 委派提供者而 hello 雲端操作員 (請參閱[雲端操作員建立 hello 委派的優惠](#cloud-operator-creates-the-delegated-offer))。

## <a name="next-steps"></a>後續步驟
[佈建 VM](azure-stack-provision-vm.md)

