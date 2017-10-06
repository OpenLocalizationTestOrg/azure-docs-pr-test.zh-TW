---
title: "Azure AD Connect： 更新 hello 的 Active Directory Federation Services (AD FS) 伺服陣列的 SSL 憑證 |Microsoft 文件"
description: "此文件詳細資料 hello 步驟 tooupdate hello SSL 憑證 AD FS 伺服器陣列使用 Azure AD Connect。"
services: active-directory
keywords: "azure ad connect, adfs ssl 更新, adfs 憑證更新, 變更 adfs 憑證, 新增 adfs 憑證, adfs 憑證, 更新 adfs ssl 憑證, 更新 ssl 憑證 adfs, 設定 adfs ssl 憑證, adfs, ssl, 憑證, adfs 服務通訊憑證, 更新同盟, 設定同盟, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>更新 Active Directory Federation Services (AD FS) 伺服陣列的 hello SSL 憑證

## <a name="overview"></a>概觀
本文說明如何使用 Azure AD Connect tooupdate hello SSL 憑證，以及在 Active Directory Federation Services (AD FS) 伺服陣列。 即使 hello 使用者登入時選取方法並不是 AD FS，您可以使用 hello Azure AD Connect 工具 tooeasily 更新 hello SSL 憑證的 hello AD FS 伺服器陣列。

您可以執行跨所有同盟和三個簡單步驟中的 Web 應用程式 Proxy (WAP) 伺服器更新 hello AD FS 伺服器陣列的 SSL 憑證的 hello 整個作業：

![三個步驟](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn 進一步了解憑證所使用的 AD FS，請參閱[使用的 AD FS 的了解憑證](https://technet.microsoft.com/library/cc730660.aspx)。

## <a name="prerequisites"></a>必要條件

* **AD FS 伺服器陣列**︰請確定您的 AD FS 伺服器陣列是 Windows Server 2012 R2 型或更新版本。
* **Azure AD Connect**： 請確定該 hello Azure AD Connect 的版本是 1.1.443.0 或更新版本。 您將使用 hello 工作**更新 AD FS SSL 憑證**。

![更新 SSL 工作](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>步驟 1︰提供 AD FS 伺服器陣列資訊

Azure AD Connect 會自動嘗試 tooobtain hello AD FS 伺服器陣列的資訊：
1. 查詢 hello 伺服陣列資訊從 AD FS (Windows Server 2016 或更新版本)。
2. 從儲存在本機使用 Azure AD Connect 中的上一個回合參考 hello 資訊。

您可以修改 hello 清單顯示透過加入或移除 hello 伺服器 tooreflect hello 目前組態 hello AD FS 伺服器陣列的伺服器。 只要提供 hello 伺服器資訊，Azure AD Connect 會顯示 hello 連線和目前的 SSL 憑證狀態。

![AD FS 伺服器資訊](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

如果 hello 清單包含已不再 hello AD FS 伺服器陣列一部分的伺服器，按一下**移除**toodelete hello 伺服器從 AD FS 伺服器陣列中伺服器 hello 清單。

![清單中的離線伺服器](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> 從 hello 清單移除伺服器的 AD FS 伺服器陣列在 Azure AD Connect 是本機作業，並更新 hello hello Azure AD Connect 會在本機維護的 AD FS 伺服器陣列的資訊。 Azure AD Connect 無法修改 AD FS tooreflect hello 變更 hello 組態。    

## <a name="step-2-provide-a-new-ssl-certificate"></a>步驟 2︰提供新的 SSL 憑證

您已確認 AD FS 伺服器陣列伺服器的 hello 資訊之後，會要求 Azure AD Connect hello 新的 SSL 憑證。 提供的密碼保護 PFX 憑證 toocontinue hello 安裝。

![SSL 憑證](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

您提供 hello 憑證之後，Azure AD Connect 會經歷一系列的必要條件。 請確認 hello hello 憑證的憑證 tooensure 是正確的 hello AD FS 伺服器陣列：

-   hello hello 憑證的主體名稱/替代主體名稱為相同 hello 與 hello federation service 名稱，或它是萬用字元憑證。
-   超過 30 天，hello 憑證有效。
-   hello 憑證信賴鏈結是有效的。
-   hello 憑證有密碼保護。

## <a name="step-3-select-servers-for-hello-update"></a>步驟 3： 選取 hello 更新伺服器

在 hello 下一個步驟中，選取需要更新 toohave hello SSL 憑證的 hello 伺服器。 無法針對 hello 更新選取離線的伺服器。

![選取伺服器 tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

您完成 hello 組態之後，Azure AD Connect 會顯示 hello 訊息，指出 hello hello 更新狀態，並提供選項 tooverify hello AD FS 登入。

![組態完成](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>常見問題集

* **應有 hello 憑證主體名稱 hello hello 新的 AD FS SSL 憑證？**

    Azure AD Connect 檢查 hello 憑證 hello 主旨名稱/替代主體名稱是否包含 hello federation service 名稱。 例如，如果您的同盟服務名稱為 fs.contoso.com，hello 主旨名稱/替代主體名稱必須是 fs.contoso.com。也接受萬用字元憑證。

* **為什麼詢問認證再次 hello WAP 伺服器 頁面上？**

    如果您提供 tooAD FS 伺服器的連線的 hello 認證也沒有 hello 權限 toomanage hello WAP 伺服器，Azure AD Connect 會要求在 hello WAP 伺服器上擁有系統管理權限的認證。

* **hello 伺服器顯示為離線。我該怎麼辦？**

    如果 hello 伺服器處於離線狀態，azure AD Connect 無法執行任何作業。 如果 hello 伺服器是 hello AD FS 伺服器陣列的一部分，請檢查 hello 連線 toohello 伺服器。 在解決 hello 問題之後，按 hello 精靈 hello 重新整理圖示 tooupdate hello 狀態。 如果 hello 伺服器是一部分的 hello 伺服器陣列之前，但現在不再存在，請按一下**移除**toodelete 它從 Azure AD Connect 的伺服器 hello 清單會保留。 從 Azure AD Connect 中的 hello 清單移除 hello 伺服器不會改變 hello 本身的 AD FS 設定。 如果您使用 AD FS 在 Windows Server 2016 或更新版本，hello 伺服器仍會留在 hello 組態設定，並會顯示一次 hello 下次 hello 工作會執行。

* **可以更新我的伺服器陣列伺服器子集 hello 新的 SSL 憑證嗎？**

    是。 您可以固定執行 hello 工作**更新 SSL 憑證**再次 tooupdate hello，剩餘的伺服器。 在 hello**選取的伺服器 ssl 憑證更新** 頁面上，您可以依據伺服器 hello 清單**SSL 到期日**不尚未更新的 tooeasily hello 伺服器。

* **我移除 hello 伺服器 hello 先前中的執行，但它仍然正在顯示為離線，列出您在 hello AD FS 伺服器 頁面。我已經將它移除，即使為何仍有 hello 離線的伺服器？**

    從 Azure AD Connect 中的 hello 清單移除 hello 伺服器並不會移除它在 hello AD FS 設定。 Azure AD Connect 參考任何資訊 hello 伺服陣列的 AD 的 FS (Windows Server 2016 或更新版本)。 如果 hello 伺服器仍會出現在 hello AD FS 設定時，將列出在 [hello] 清單。  

## <a name="next-steps"></a>後續步驟

- [Azure AD Connect 和同盟](active-directory-aadconnectfed-whatis.md)
- [使用 Azure AD Connect 管理和自訂 Active Directory Federation Services](active-directory-aadconnect-federation-management.md)
