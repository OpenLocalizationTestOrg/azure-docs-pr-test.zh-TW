---
title: "使用 Azure MFA 和 AD FS aaaSecure 雲端資源 |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA 和 AD FS hello 雲端中的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>使用 Azure Multi-Factor Authentication 與 AD FS 保護雲端資源
如果您的組織會與 Azure Active Directory 同盟，使用 Azure Multi-factor Authentication 或 Active Directory Federation Services (AD FS) toosecure 資源存取的 Azure AD。 使用下列程序 toosecure Azure Active Directory 資源與 Azure Multi-factor Authentication 或 Active Directory Federation Services 的 hello。

## <a name="secure-azure-ad-resources-using-ad-fs"></a>使用 AD FS 保護 Azure AD 資源
toosecure 您雲端的資源，設定宣告規則，讓使用者執行雙步驟驗證成功時，Active Directory Federation Services 會發出 hello multipleauthn 宣告。 這個宣告會傳遞 tooAzure AD 上。 請遵循此程序 toowalk，透過 hello 步驟：


1. 開啟 [AD FS 管理]。
2. Hello 左側選取**信賴憑證者信任**。
3. 以滑鼠右鍵按一下 [Microsoft Office 365 身分識別平台]，然後選取 [編輯宣告規則]。

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. 在 [發佈轉換規則] 上，按一下 [新增規則]。

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. 在 hello 新增轉換宣告規則精靈中，選取**傳遞或篩選傳入宣告**從 hello 下拉式清單，然後按一下 **下一步**。

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. 指定規則的名稱。 
7. 選取**驗證方法參考**為 hello 傳入宣告類型。
8. 選取 [傳遞所有宣告值]。
    ![新增轉換宣告規則精靈](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. 按一下 [完成] 。 關閉 hello AD FS 管理主控台。

## <a name="trusted-ips-for-federated-users"></a>同盟使用者的可信任 IP
信任的 Ip 可讓系統管理員 tooby 傳遞雙步驟驗證特定的 IP 位址，或具有源自其自己內部網路要求的同盟使用者。 hello 下列各節說明如何 tooconfigure Azure 多重要素驗證信任 Ip 和同盟的使用者，當要求源自同盟的使用者內部網路時略過雙步驟驗證。 這是設定來達成的 AD FS toouse 傳遞或篩選內送宣告範本以 hello 公司網路內部的宣告類型。

此範例使用 Office 365 做為信賴憑證者信任。

### <a name="configure-hello-ad-fs-claims-rules"></a>設定 hello AD FS 宣告規則
我們需要 toodo hello 第一件事是 tooconfigure hello AD FS 宣告。 建立兩個宣告規則，一個用於 hello 公司網路內部宣告類型和另一個，適用於維持使用者登入。

1. 開啟 [AD FS 管理]。
2. Hello 左側選取**信賴憑證者信任**。
3. 以滑鼠右鍵按一下**[Microsoft Office 365 身分識別平台]**，然後選取 **[編輯宣告規則...]**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. 在 [發佈轉換規則] 上，按一下 **[新增規則]**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. 在 hello 新增轉換宣告規則精靈中，選取**傳遞或篩選傳入宣告**從 hello 下拉式清單，然後按一下 **下一步**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. 在 [hello] 方塊下一步 tooClaim 規則名稱命名您的規則。 例如：InsideCorpNet。
7. Hello 下拉式清單中，從 下一步 tooIncoming 宣告類型，則選取**公司網路內部**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. 按一下 [完成] 。
9. 在 [發佈轉換規則] 上，按一下 [新增規則]。
10. 在 hello 新增轉換宣告規則精靈中，選取**使用自訂規則傳送宣告**從 hello 下拉式清單，然後按一下 **下一步**。
11. 在 宣告規則名稱底下的 hello 方塊： 輸入*維持使用者登入*。
12. 在 [hello 自訂規則] 方塊中輸入：

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. 按一下 [完成] 。
14. 按一下 [Apply (套用)] 。
15. 按一下 [ **確定**]。
16. 關閉 [AD FS 管理]。

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>搭配同盟使用者設定 Azure Multi-Factor Authentication 信任的 IP
既然 hello 宣告已備妥，我們可以設定信任的 Ip。

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左側，按一下  **Active Directory**。
3. 在 [目錄] 選取您要設定信任的 Ip tooset 的 hello 目錄。
4. 在 hello 您選取的目錄中，按一下 **設定**。
5. 在 hello 多因素驗證 區段中，按一下 **管理服務設定**。
6. 在 [hello 服務設定] 頁面上，在受信任 Ip 時，選取**從同盟使用者略過多 multi-factor-authentication 要求，我的內部網路上**。  

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. 按一下 [儲存] 。
8. 一旦套用 hello 更新之後，按一下 **關閉**。

這樣就大功告成了！ 此時，Office 365 同盟的使用者應該只有 toouse MFA 時宣告來自外部的 hello 公司內部網路。
