---
title: "aaaAzure Active Directory 裝置管理常見問題集 |Microsoft 文件"
description: "Azure Active Directory 裝置管理常見問題集。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a>Azure Active Directory 裝置管理常見問題集

**問： 我最近註冊 hello 裝置。為什麼在 我的使用者資訊 hello Azure 入口網站中看不到 hello 裝置？**

**答：**與自動裝置註冊加入網域的 Windows 10 裝置不會出現在 hello 使用者資訊。
您需要 toouse PowerShell toosee 所有裝置。 

只有 hello 下列裝置列在 hello 使用者資訊：

- 所有未加入企業的個人裝置 
- 所有非 Windows 10/Windows Server 2016 裝置 
- 所有非 Windows 裝置 

---

**問： 為什麼不看到 hello Azure 入口網站中註冊 Azure Active Directory 中的所有 hello 裝置？** 

**答：**目前沒有任何方式 toosee 所有已註冊的裝置 hello Azure 入口網站中。 您可以使用 Azure PowerShell toofind 所有裝置。 如需詳細資訊，請參閱 hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet。

--- 

**問： 如何知道哪些 hello 裝置登錄狀態的 hello 用戶端是否？**

**答：** hello 裝置登錄狀態而定：

- 哪些 hello 裝置
- 裝置的註冊方式 
- Tooit 相關任何詳細資料。 
 

---

**問： 為何我已刪除的裝置在 hello Azure 入口網站或使用 Windows PowerShell 仍然列為註冊嗎？**

**答：**原先的設計就是如此。 hello 裝置不會存取 tooresources hello 雲端中。 如果您想 tooremove hello 裝置並重新登錄，手動動作必須 toobe 採取 hello 裝置上。 

針對已加入內部部署 AD 網域的 Windows 10 與 Windows Server 2016：

1.  系統管理員身分開啟命令提示字元中 hello。

2.  輸入 `dsregcmd.exe /debug /leave`

3.  登出再登入 tootrigger hello 排定的工作，重新登錄裝置 hello。 

針對其他已加入內部部署 AD 網域的 Windows 平台：

1.  系統管理員身分開啟命令提示字元中 hello。
2.  輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`。
3.  輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`。

---

**問：為什麼我在 Azure 入口網站中看到重複的裝置項目？**

**答：**

-   針對 Windows 10 和 Windows Server 2016 中，會重複的嘗試 toounjoin 並重新聯結 hello 相同的裝置，可能會有重複的項目。 

-   如果您已經使用新增工作或學校帳戶，每個 windows 使用者使用新增工作或學校帳戶的人員會建立新的裝置記錄 hello 與同一個裝置名稱。

-   其他 Windows 的平台在內部部署 AD 加入網域使用自動註冊將會建立新的裝置記錄 hello 與相同的網域使用者之登入 hello 裝置的裝置名稱。 

-   一經抹除，AADJ 機器重新安裝並重新加入 hello 與相同名稱，會顯示以 hello 的另一筆記錄為相同的裝置名稱。

---

**問： 為什麼使用者仍然可以存取資源從我有 hello Azure 入口網站中停用的裝置？**

**答：**就可以在套用 revoke toobe tooan 小時。

>[!Note] 
>對於遺失裝置，我們建議抹除 hello 裝置 tooensure 使用者無法存取 hello 裝置。 如需更多詳細資料，請參閱[註冊裝置以在 Intune 中管理](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。 


---

**問：為什麼我的使用者會看到「您無法從這裡前往該處」？**

**答：**如果您已設定特定的條件式存取規則 toorequire 特定裝置狀態，且 hello 裝置不符合 hello 準則，使用者會封鎖，並看到此訊息。 請評估 hello 規則，並確認該 hello 裝置是無法 toomeet hello 準則 tooavoid 這則訊息。

---


**問： 我看到 hello 下 hello hello Azure 入口網站中的使用者資訊的裝置記錄，並且可以看到 hello 狀態，hello 用戶端上註冊。我是否已針對使用條件式存取進行正確設定？**

**答：** hello 裝置記錄 (deviceID) 和 hello Azure 入口網站上的狀態必須符合 hello 用戶端，並符合條件式存取的任何評估準則。 如需更多詳細資料，請參閱[開始使用 Azure Active Directory 裝置註冊](active-directory-device-registration.md)。

---

**問： 為什麼取得 「 使用者名稱或密碼不正確 」 訊息裝置我剛加入 tooAzure AD？**

**答：**此情況的常見原因如下：

- 您的使用者認證已經無效。

- 您的電腦位於與 Azure Active Directory 無法 toocommunicate。 請檢查是否有任何網路連線問題。

- 不符合 hello Azure AD Join 的必要元件。 請確定您已遵循的步驟 hello[擴充雲端功能 tooWindows 10 裝置透過 Azure Active Directory Join](active-directory-azureadjoin-overview.md)。  

- 同盟登入需要您的同盟伺服器 toosupport Ws-trust 作用中的端點。 

---

**問： 為什麼看 hello"...糟糕，發生錯誤 ！ 」 對話方塊時請勿加入我的電腦？**

**答：**這是使用 Intune 來設定 Azure Active Directory 註冊的結果。 如需更多詳細資料，請參閱[設定 Windows 裝置管理](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment)。  

---

**問： 為什麼我的電腦失敗雖然未出現任何錯誤資訊的嘗試 toojoin 嗎？**

**答：**可能的原因是該的 hello 使用者已登入 toohello 裝置使用 hello 內建的 administrator 帳戶。 請使用 Azure Active Directory Join toocomplete hello 安裝程式之前，建立不同的本機帳戶。 

---

**問： 哪裡可以找到指示 hello 安裝程式的自動裝置註冊？**

**答：**詳細指示，請參閱[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**問： 哪裡可以找到疑難排解 hello 自動裝置註冊相關資訊？**

**答：**如需疑難排解資訊，請參閱：

- [疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [疑難排解自動登錄的網域加入 Windows 下層用戶端電腦 tooAzure AD](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

