---
title: "aaaYou 無法取得那里以下 hello Azure 入口網站，從 Windows 裝置 |Microsoft 文件"
description: "了解，您不能那里從這裡來自的 get 和什麼您可以檢查 tooavoid 執行此對話方塊。"
services: active-directory
keywords: "裝置型條件式存取、裝置註冊、啟用裝置註冊、裝置註冊和 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>您無法在 Windows 裝置上從這裡前往該處

例如，在嘗試存取貴組織的 SharePoint Online 內部網路期間，您可能會碰到一個頁面指出「您無法從這裡前往該處」。 您會看到此頁面上，因為您的系統管理員已設定讓存取 tooyour 組織的資源，在某些情況下的條件式存取原則。 雖然這可能需要 toocontact 技術服務人員或您的系統管理員 tooget 解決這個問題，有幾件事，您可以試用您自己，第一次。

如果您使用**Windows**裝置，您應該檢查下列 hello:

- 您使用支援的瀏覽器？

- 您在裝置上執行支援的 Windows 版本？

- 您的裝置是否符合規範？






## <a name="supported-browser"></a>支援的瀏覽器

如果您的系統管理員已設定條件式存取原則，您只可以使用支援的瀏覽器來存取貴組織的資源。 在 Windows 裝置上，只支援 **Internet Explorer** 和 **Edge**。

您可以輕鬆地識別是否您無法存取的資源，因為 tooan 不支援的瀏覽器查看 hello hello 錯誤頁面的詳細資料 區段：

![不受支援的瀏覽器會收到「您無法從這裡前往該處」訊息](./media/active-directory-conditional-access-device-remediation/02.png "例")

hello 只有補救是 toouse hello 應用程式對您的裝置平台所支援的瀏覽器。 如需支援的瀏覽器完整清單，請參閱[支援的瀏覽器](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies)。  


## <a name="supported-versions-of-windows"></a>支援的 Windows 版本

hello 下列條件必須為 true hello Windows 作業系統，您的裝置上的相關： 

- 如果您 Windows 桌面作業系統上執行您的裝置，它會需要 toobe Windows 7 或更新版本。
- 如果您在裝置上執行 Windows server 作業系統，它需要 toobe Windows Server 2008 R2 或更新版本。 


## <a name="compliant-device"></a>符合規範的裝置

您的系統管理員可能已經設定的條件式存取原則允許存取 tooyour 組織的資源，只會從相容的裝置。 符合標準，您的裝置必須是其中一個聯結的 tooyour toobe 在內部部署 Active Directory 或是已加入 tooyour Azure Active Directory。

您可以輕鬆地識別您無法存取到期，藉由查看 hello 詳細資料區段的 hello 錯誤網頁不相容的 tooa 裝置資源是否：
 
![未註冊的裝置會收到「您無法從這裡前往該處」訊息](./media/active-directory-conditional-access-device-remediation/01.png "案例")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>是聯結的裝置 tooan 內部部署 Active Directory？

**如果您的裝置加入 tooan 內部部署 Active Directory 組織中：**

1. 請確定您使用工作帳戶 （您的 Active Directory 帳戶） 登入 tooWindows。
2. 透過虛擬私人網路 (VPN) 或 DirectAccess tooyour 公司網路連線。
3. 您連接之後，請按 hello Windows 標誌鍵 + hello L 金鑰 toolock Windows 工作階段。
4. 輸入您的工作帳戶認證，以將 Windows 工作階段解除鎖定。
5. 等候數分鐘，然後再試 tooaccess hello 應用程式或服務。
6. 如果您看到 hello 相同頁面上，按一下 hello**詳細**連結，然後再連絡管理員，並 hello 詳細資料。


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>是您的裝置未加入 tooan 內部部署 Active Directory？

如果您的裝置未加入 tooan 在內部部署 Active Directory 及執行 Windows 10 時，有兩個選項：

* 執行 Azure AD Join
* 加入您的工作或學校帳戶 tooWindows

如需這些選項有何差異的相關資訊，請參閱[在您的工作場所中使用 Windows 10 裝置](active-directory-azureadjoin-windows10-devices.md)。  
如果您的裝置：

- 所屬 tooyour 組織，您應該執行 Azure AD Join。
- 個人裝置或 Windows phone，您應該加入您的工作或學校帳戶 tooWindows 



#### <a name="azure-ad-join-on-windows-10"></a>Windows 10 上的 Azure AD Join

hello 步驟 toojoin 您裝置 tooAzure AD 是繫結 hello 您正在執行的 Windows 10 版本。 toodetermine hello 版本的 Windows 10 作業系統，執行 hello **winver**命令： 

![Windows 版本](./media/active-directory-conditional-access-device-remediation/03.png )


**Windows 10 年度更新 (版本 1607)：**

1. 開啟 hello**設定**應用程式。
2. 按一下 [帳戶] > [存取工作或學校]。
3. 按一下 [ **連接**]。
4. 按一下**加入此裝置 tooAzure AD**。
5. 完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。
6. 登出，然後使用您的工作帳戶登入。
7. 再試一次 tooaccess hello 應用程式。

**Windows 10 2015 年 11 月更新 (版本 1511)：**

1. 開啟 hello**設定**應用程式。
2. 按一下 [系統] > [關於]。
3. 按一下 [加入 Azure AD] 。
4. 完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。
5. 登出，然後使用您的工作帳戶 (Azure AD 帳戶) 登入。
6. 再試一次 tooaccess hello 應用程式。


#### <a name="workplace-join-on-windows-81"></a>在 Windows 8.1 上的 Workplace Join

如果您的裝置未加入網域和執行 Windows 8.1，toodo 工作地點加入，且在 Microsoft Intune 中註冊，下列步驟 hello:

1. 開啟 [電腦設定] 。
2. 按一下 [網路] > [工作場所]。
3. 按一下 [ **加入**]。
4. 完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。
5. 按一下 [開啟] 。
6. 再試一次 tooaccess hello 應用程式。



#### <a name="add-your-work-or-school-account-toowindows"></a>加入您的工作或學校帳戶 tooWindows 


**Windows 10 年度更新 (版本 1607)：**

1. 開啟 hello**設定**應用程式。
2. 按一下 [帳戶] > [存取工作或學校]。
3. 按一下 [ **連接**]。
4. 完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。
5. 再試一次 tooaccess hello 應用程式。


**Windows 10 2015 年 11 月更新 (版本 1511)：**

1. 開啟 hello**設定**應用程式。
2. 按一下 [帳戶] > [您的帳戶]。
3. 按一下 [新增工作或學校帳戶] 。
4. 完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。
5. 再試一次 tooaccess hello 應用程式。





## <a name="next-steps"></a>後續步驟
[Azure Active Directory 條件式存取](active-directory-conditional-access.md)

