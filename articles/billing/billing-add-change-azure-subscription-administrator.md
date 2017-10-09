---
title: "aaaAdd 或變更管理 Azure 訂用帳戶角色 |Microsoft 文件"
description: "描述如何 tooadd 或變更 Azure 共同管理員、 服務管理員及帳戶管理員"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>新增或變更管理 hello 訂用帳戶或服務的 Azure 系統管理員角色
您可以變更 hello Azure 系統管理員管理您的 Azure 訂用帳戶或管理 hello Azure 訂用帳戶中使用的服務。 tooview Azure 帳單資訊和管理訂用帳戶，您必須登入 toohello[帳戶中心](https://account.windowsazure.com/Home/Index)為 hello 帳戶系統管理員。 

## <a name="add-an-admin-for-a-subscription"></a>新增訂用帳戶的管理員
在 hello Azure 入口網站或 hello Azure 傳統入口網站中，您可以加入 Azure 系統管理員。

**Azure 入口網站**

tooadd 某人身為系統管理員的訂用帳戶 hello Azure 入口網站中，您可以讓 hello 擁有者角色。 hello 擁有者角色只能管理您所指派的 hello 訂用帳戶中的 hello 資源。 沒有存取權限 tooother 訂用帳戶。 hello hello 透過您加入的擁有者[Azure 入口網站](https://portal.azure.com)無法管理資源在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，選取 **訂用帳戶** > *hello 訂用帳戶的 hello admin tooaccess*。

    ![顯示已選取訂用帳戶選項的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. 在 hello 訂用帳戶 刀鋒視窗中，選取 **存取控制 (IAM)**。
4. 選取 [新增] > [角色] > [擁有者]。 輸入您想 tooadd 做為擁有者，選取 hello 使用者，然後選取 hello 使用者 hello 電子郵件地址**儲存**。

    ![顯示選取的 hello 擁有者角色的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. 如果您想 tooadd hello 擁有者帳戶為共同管理員，在 hello**存取控制 (IAM)**頁面上，以滑鼠右鍵按一下 hello 使用者，然後選取**加入為共同管理員**。 [Azure 預覽入口網站](https://preview.portal.azure.com/)現提供此功能。 

     ![新增共同管理員的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >如果，則需要 tooadd hello 「 擁有者 」 使用者共同系統管理員身分 hello 使用者需要 toomanage hello 的 Azure 服務[Azure 傳統入口網站](https://manage.windowsazure.com/)。

    tooremove hello 共同系統管理員權限，以滑鼠右鍵按一下 hello 「 共同系統管理員 」 使用者，然後選取**移除共同管理員**。

    ![移除共同管理員的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Azure 傳統入口網站**

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)。
2. 在 hello 瀏覽窗格中，選取**設定**> **管理員**> **新增**。 </br>

    ![顯示 tooget toohello 將按鈕加入的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. 類型 hello 電子郵件地址 hello 人員想 tooadd 共同系統管理員身分，，然後選取您想 hello 共同管理員 tooaccess hello 訂用帳戶。</br>

    ![顯示已選取訂用帳戶選項的螢幕擷取畫面 ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

遵循電子郵件地址的 hello 可新增為共同管理員：

* **Microsoft 帳戶** (先前的 Windows Live ID) </br>
  您可以使用 Microsoft 帳戶 toosign tooall 消費者導向 Microsoft 產品和雲端服務，例如 Outlook (Hotmail)、 Skype (MSN)、 OneDrive、 Windows Phone 和 Xbox LIVE。
* **Organizational account**</br>
  組織帳戶是建立在 Azure Active Directory 之下的帳戶。 hello 組織帳戶地址格式如下：

    使用者@&lt;您的網域&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>變更訂用帳戶的服務管理員
Hello 帳戶系統管理員可以變更 hello 服務系統管理員的訂用帳戶。

1. 登入太[Azure 帳戶中心](https://account.windowsazure.com/subscriptions)使用 hello 帳戶系統管理員。
2. 選取您想要 toochange hello 訂用帳戶。
3. 在 hello 右邊，選取**編輯訂用帳戶**詳細資料。 </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. 在 hello**服務系統管理員**方塊中，輸入 hello hello 電子郵件地址新增服務系統管理員。 </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>變更 hello 帳戶管理員
tootransfer 擁有權的 hello Azure 帳戶 tooanother 帳戶，請參閱[傳輸的 Azure 訂用帳戶的擁有權](billing-subscription-transfer.md)。

我們強烈建議您不要刪除或重新命名 hello 帳戶系統管理員的電子郵件地址。 您可能會看到非預期且不想要的行為，以 hello Azure 帳戶。 您不能與該帳戶的無法登入 tooAzure、 toohello 帳戶進行變更或管理該帳戶的資源。 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>核取 hello hello 訂用帳戶的帳戶管理員
如果您不確定 hello 帳戶系統管理員是訂用帳戶，使用下列步驟 toofind 出 hello。

  1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
  2. 在 hello 中樞功能表中，選取 **訂用帳戶**。
  3. 選取您想 toocheck，，然後再查看底下的 hello 訂用帳戶**設定**。
  4. 選取 [屬性] 。 hello hello 訂用帳戶的帳戶管理員會顯示在 hello**帳戶管理員**方塊。  

## <a name="types-of-azure-admin-accounts"></a>Azure 管理帳戶的類型
 帳戶系統管理員、 服務管理員和共同管理員是 hello 三種類型的 Microsoft Azure 中的系統管理員角色。 hello 下表描述這三個系統管理角色的 hello 差異。

| 管理角色 | 限制 | 說明 |
| --- | --- | --- |
| 帳戶管理員 (AA) |每個 Azure 帳戶 1 名 |這是 hello 人員註冊或購買 Azure 訂用帳戶，並為授權的 tooaccess hello[帳戶中心](https://account.windowsazure.com/Home/Index)並執行各項管理工作。 這些包括能夠 toocreate 訂閱、 取消訂用帳戶、 變更 hello 計費訂用帳戶，及變更 hello 服務系統管理員。 |
| 服務管理員 (SA) |每個 Azure 訂用帳戶 1 名 |這個角色是在 hello 授權的 toomanage 服務[Azure 入口網站](https://portal.azure.com)。 根據預設，新的訂閱 hello 帳戶系統管理員也是 hello 服務系統管理員。 |
| 共同管理員 (CA)，在 hello [Azure 傳統入口網站](https://manage.windowsazure.com) |每個訂用帳戶 200 名 |這個角色有 hello 相同 hello 服務系統管理員，以存取權限，但無法變更 hello 關聯的訂用帳戶 tooAzure 目錄。 |

Azure Active Directory 角色型存取控制 (RBAC) 可讓使用者 toobe 加入 toomultiple 角色。 如需詳細資訊，請參閱 [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)。

## <a name="limitations-and-restrictions-for-admin-accounts"></a>系統管理員帳戶的限制和約束
* 每個訂用帳戶相關聯的 Azure AD 目錄 (也稱為 hello 預設目錄)。 toofind hello 預設目錄 hello 訂用帳戶都與移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)，選取**設定** > **訂閱**。 請檢查 hello 訂用帳戶 ID toofind hello 預設目錄。
* 如果您登入 Microsoft 帳戶，您只可以共同系統管理員身分來加入其他的 Microsoft 帳戶或 hello 預設目錄中的使用者。
* 如果您以組織帳戶登入，就可以將組織中的其他組織帳戶新增為共同管理員。 舉例來說，abby@contoso.com 可以將 bob@contoso.com 新增為服務管理員或共同管理員，但無法新增 john@notcontoso.com，除非 john@notcontoso.com 在預設目錄中。 登入組織帳戶的使用者可以繼續 tooadd Microsoft 帳戶使用者做為服務管理員或共同管理員。
* 現在，很可能在有組織帳戶 tooAzure toosign，以下是 hello 變更 tooService 系統管理員和共同管理員帳戶需求：

  | 登入方法 | 將 Microsoft 帳戶或預設目錄中的使用者新增為 CA 或 SA？ | 在 hello 中新增組織帳戶做為 CA 或 SA 相同組織嗎？ | 將不同組織中的組織帳戶新增為 CA 或 SA？ |
  | --- | --- | --- | --- |
  |  Microsoft 帳戶 |是 |否 |否 |
  |  組織帳戶 |是 |是 |否 |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>深入了解資源存取控制和 Active Directory
* toolearn 深入了解如何控制資源存取 Microsoft Azure 中，請參閱[了解 Azure 中的資源存取](../active-directory/active-directory-understanding-resource-access.md)。
* 如需有關 Azure Active Directory 的詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)和[指派 Azure Active Directory 中的管理員角色](../active-directory/active-directory-assign-admin-roles.md)。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
