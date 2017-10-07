---
title: "aaaTransfer Azure 訂用帳戶擁有權 tooanother 帳戶 |Microsoft 文件"
description: "描述如何 tootransfer Azure 訂用帳戶 tooanother 使用者，而某些常見問題集 (FAQ) 有關 hello 程序"
keywords: "azure 訂用帳戶，azure 轉移訂用帳戶傳輸，移動 azure 訂用帳戶 tooanother 帳戶、 azure 變更訂閱擁有者、 傳輸 azure 訂用帳戶 tooanother 帳戶"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2d9f5d9ccd34738701493e5f31c2f83a02f5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-ownership-of-an-azure-subscription-tooanother-account"></a>Azure 訂用帳戶 tooanother 帳戶的擁有權轉移

您可以傳輸您的訂用帳戶 tooanother 使用者隨用隨付、 Visual Studio、 動作組件或 BizSpark 中針對訂閱 hello 帳戶中心。 我們支援 Azure 外部的服務，這些訂用帳戶類型的 hello 的傳輸。 

您可能想 tootransfer 擁有權的 Azure 訂用帳戶，當您：

* 需要 toohand 的其他您 Azure 訂用帳戶 toosomeone 帳單擁有權。
* 想要使用 Azure 進行 toosign 的 toochange hello 帳戶。 也許您會使用您的 Microsoft 帳戶，而改為為了 toouse 工作或學校帳戶。
* 想 toomove 從一個目錄 tooanother 您 Azure 訂用帳戶。
* 在不同的租用戶中具有 Azure 和 Office 365，而且想 tooconsolidate。

toochange 提供您的訂用帳戶 tooa 不同，請參閱[切換您的 Azure 訂用帳戶 tooanother 優惠](billing-how-to-switch-azure-offer.md)。 

## <a name="transfer-ownership-of-an-azure-subscription"></a>轉移 Azure 訂用帳戶的擁有權
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. 登入 <https://account.windowsazure.com/Subscriptions>。 您有 toobe hello 帳戶管理員 tooperform 擁有權轉移。 toofind 負責 hello 帳戶 hello 訂用帳戶管理員，請參閱 hello[常見問題集](#faq)。

2. 選取 hello 訂用帳戶 tootransfer。

3. 按一下 hello**轉移訂用帳戶**選項。 請參閱[常見問題集](#no-button)如果您沒有看見 hello 按鈕。

   ![Azure 帳戶的訂用帳戶索引標籤](./media/billing-subscription-transfer/image1.png)
4. 指定 hello 收件者。

   ![移轉訂用帳戶對話方塊](./media/billing-subscription-transfer/image2.PNG)
5. hello 收件者自動取得含有接受連結的電子郵件。

   ![訂用帳戶傳送電子郵件 toorecipient](./media/billing-subscription-transfer/image3.png)
6. hello 收件者按一下 hello 連結，並遵循 hello 指示，包括輸入其付款資訊。

   ![第一個訂用帳戶移轉網頁](./media/billing-subscription-transfer/image4.png)

   ![第二個訂用帳戶移轉網頁](./media/billing-subscription-transfer/image5.png)
7. 成功！ 現在傳送嗨訂用帳戶。

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a>轉送 Enterprise 合約 (EA) 客戶的訂用帳戶擁有權
hello 企業系統管理員可以傳輸在嘗試註冊訂閱的擁有權。 tooget 啟動，請參閱[傳輸帳戶擁有權](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription)hello EA 入口網站中。

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a>接受訂用帳戶擁有權後的後續步驟
1. 現在您已經準備 hello 帳戶系統管理員。 檢閱並更新 hello 服務系統管理員和共同管理員。 管理系統管理員 」 中 hello [Azure 傳統入口網站](https://manage.windowsazure.com)移 tooSettings。 [深入了解管理員角色](billing-add-change-azure-subscription-administrator.md)。

2. 您也可以針對訂用帳戶和服務使用角色型存取控制 (RBAC)。 請瀏覽 hello [Azure 入口網站](https://portal.azure.com)。 [深入了解 RBAC](../active-directory/role-based-access-control-configure.md)

3. 更新與此訂用帳戶服務相關聯的認證，包括：
   
   * 授與 hello 使用者系統管理員權限 toosubscription 資源的管理憑證。 如需詳細資訊，請參閱 [Create and upload a management certificate for Azure](../cloud-services/cloud-services-certs-create.md)
   
   * 服務 (例如儲存體) 的存取金鑰。 如需詳細資訊，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)
   
   * 服務 (例如 Azure 虛擬機器) 的遠端存取認證。 

4. [更新此訂用帳戶的計費警示](billing-set-up-alerts.md)在 hello [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)。 

5. 如果您使用與合作夥伴，請考慮更新此訂用帳戶的 hello 合作夥伴 ID。 您可以更新在 hello hello 合作夥伴 ID [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)。

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a>常見問題集 (FAQ)
* <a name="whoisaa"></a>**Hello hello 訂用帳戶的帳戶管理員是誰？**

  hello 帳戶系統管理員是 hello 人員註冊或購買 hello Azure 訂用帳戶。 它們是授權的 tooaccess hello[帳戶中心](https://account.windowsazure.com/Home/Index)以及執行各種管理工作，例如建立訂閱、 取消訂用帳戶、 變更 hello 計費訂用帳戶，或變更 hello 服務系統管理員。 如果您不確定 hello 帳戶系統管理員是訂用帳戶，使用下列步驟 toofind 出 hello。

  1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
  2. 在 hello 中樞功能表中，選取 **訂用帳戶**。
  3. 選取您想 toocheck，，然後再查看底下的 hello 訂用帳戶**設定**。
  4. 選取 [屬性] 。 hello hello 訂用帳戶的帳戶管理員會顯示在 hello**帳戶管理員**方塊。  

* **所有項目都會轉送嗎？包括資源群組、VM、磁碟和其他執行中的服務？**

  是，您的資源像是磁碟的 Vm 和網站傳送 toohello 新擁有者。 不過，不會跨不同目錄轉送您所設定的任何[系統管理員角色](billing-add-change-azure-subscription-administrator.md)和[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md) 原則。

* <a id="no-button"></a>**為什麼無法查看 hello 轉移訂用帳戶 按鈕？**

  如果您沒有看見 hello**轉移訂用帳戶**按鈕，則不支援您的優惠訂用帳戶轉移。 [連絡客戶支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。

* **訂用帳戶移轉會造成服務中斷嗎？**

  沒有影響 toohello 服務。 傳送嗨訂用帳戶取消 hello hello 目前帳戶系統管理員的訂用帳戶，並建立 hello 收件者的帳戶下的訂用帳戶。 相關聯的 toohello 基礎的 Azure 服務 hello 新的訂用帳戶。 會維持為訂用帳戶識別碼 hello hello 相同。

* **如何使用這個程序 toochange hello 目錄訂用帳戶中？**

  帳戶系統管理員屬於該 hello 時，是 hello 目錄中建立 Azure 訂用帳戶。 toochange hello 目錄中，傳送嗨訂用帳戶 tooa 使用者帳戶 hello 目標目錄中。 該使用者完成 hello 步驟 tooaccept 傳輸，hello 訂用帳戶時，會自動移動的 toohello 目標目錄。

* **如果我接管來自另一個組織的訂用帳戶的帳單擁有權時，繼續 toohave 存取 toomy 資源它們嗎？**

  如果 hello 訂用帳戶轉移的 tooanother 租用戶，hello 與 hello 先前的租用戶相關聯的使用者失去存取 toohello 訂用帳戶。 即使使用者不是服務管理員或共同管理員，它們仍然可能透過其他安全性機制，包括存取 toohello 訂用帳戶：

  * 授與 hello 使用者系統管理員權限 toosubscription 資源的管理憑證。 如需詳細資訊，請參閱[建立和上傳 Azure 的管理憑證](../cloud-services/cloud-services-certs-create.md)。
  * 服務 (例如儲存體) 的存取金鑰。 如需詳細資訊，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。
  * 服務 (例如 Azure 虛擬機器) 的遠端存取認證。

 如果 hello 收件者需要 toorestrict 存取 tootheir 資源，它們應該考慮更新任何與 hello 服務相關聯的密碼。 最多資源可以使用下列步驟的 hello 更新：

    1. 移 toohello [Azure 入口網站](https://portal.azure.com)。
    2. 在 hello 中樞功能表中，選取 **所有資源**。
    3. 選取 hello 資源。 
    4. 在 hello 資源刀鋒視窗中，按一下 **設定**。 您可以在這裡檢視並更新現有的密碼。

* **如果我 hello 訂用帳戶傳輸 hello 中間的 hello 帳單週期，並 hello 收件者支付 hello 整個計費循環嗎？**

  hello 寄件者會負責 toohello 點 hello 傳送已完成上回報了任何使用方式的付款。 hello 收件者會負責從傳輸及更新版本的 hello 時間報告的使用方式。 可能有某些使用量是在移轉之前發生，但在之後才報告。 hello 使用隨附於 hello 收件者的帳單。

* **Hello 收件者是否有存取 toousage 和帳單記錄？**

  hello 唯一資訊可用 toohello 收件者 hello 數量 hello 最後一個帳單或如果產生 hello 第一個帳單之前，已傳送 hello 訂用帳戶 hello 餘額。 hello 的 hello 使用量及帳單記錄的其餘部分將不會傳送 hello 訂用帳戶中執行。

* **可在傳輸期間變更 hello 優惠嗎？**

  hello 供應項目必須保持 hello 相同。 toochange 您提供服務，請參閱[切換您的 Azure 訂用帳戶 tooanother 優惠](billing-how-to-switch-azure-offer.md)。

* **可以傳輸在另一個國家/地區的訂用帳戶 tooa 使用者帳戶？**

  否，不支援傳送另一個國家/地區的訂用帳戶 tooa 使用者帳戶。 hello 收件者的使用者帳戶必須是在 hello 相同國家/地區。

* **Hello 收件者可以使用不同的付款方式嗎？**

  是。 但 hello 訂閱計費記錄分成兩個帳戶。  

* **Hello 付款方法被影響之後傳輸 Azure 訂用帳戶？**

  tooaccept 訂用帳戶轉移、 信用卡或類似的付款方式必須提供 toopay hello 訂用帳戶。 例如，如果 Bob 將轉移訂用帳戶 tooJane Jane 接受 hello 傳輸，Jane 必須提供付款方法 toopay hello 訂用帳戶。 Hello 轉移完成之後，會將 Jane 計費 hello 訂用帳戶不 Bob。

* **如何移轉資料和我 Azure 訂用帳戶 toonew 訂用帳戶的服務？**

  如果您無法轉移訂用帳戶的擁有權，則可手動移轉您的資源。 請參閱[移動資源 toonew 資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。



## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。 


