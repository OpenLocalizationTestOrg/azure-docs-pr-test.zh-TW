---
title: "Azure Active Directory 中的 aaaAssign 授權 tooa 群組 |Microsoft 文件"
description: "Tooassign 如何授權 toousers 透過 Azure Active Directory 群組授權"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>指派授權 toousers 由 Azure Active Directory 中的群組成員資格

這篇文章會逐步引導您指派的使用者在 Azure Active Directory (Azure AD) 中的產品授權 tooa 群組，然後確認 他們要正確授權。

在此範例中，hello 租用戶包含安全性群組**人力資源部門皆**。 此群組包含 hello 人力資源部門 （約 1,000 位使用者） 的所有成員。 您想 tooassign Office 365 Enterprise E3 授權 toohello 整個部門。 hello 部門之前準備好使用它的 toostart hello Yammer 企業服務包含在 hello 產品中，必須暫時停用。 您也想 toodeploy 企業行動力 + 安全性授權 toohello 相同的使用者群組。

> [!NOTE]
> 並非所有位置都可使用某些 Microsoft 服務。 Tooa 使用者可以指派授權之前，hello 系統管理員會對使用者 hello toospecify hello Usage 位置屬性。

> 取得群組的授權指派，指定使用位置沒有任何使用者將會繼承 hello hello 目錄位置。 如果您有多個位置中的使用者，我們建議您一律將使用位置做為您的使用者建立流程的一部分 （例如透過 AAD Connect 組態）-可確保授權指派的 hello 結果永遠正確，且使用者未收到的 Azure AD 中不允許的位置中的服務。

## <a name="step-1-assign-hello-required-licenses"></a>步驟 1： 指派所需的 hello 授權

1. 登入 toohello [ **Azure 入口網站**](https://portal.azure.com)以系統管理員帳戶。 toomanage 授權，hello 帳戶必須是全域管理員角色或使用者帳戶管理員。

2. 選取**更多服務**在 hello 左側瀏覽窗格，然後選取  **Azure Active Directory**。 您可以新增此刀鋒視窗 tooFavorites，或將其釘選 toohello 入口網站儀表板。

3. 在 hello **Azure Active Directory**刀鋒視窗中，選取**授權**。 這會開啟刀鋒視窗，您可以在此檢視並管理 hello 租用戶中的所有授權產品。

4. 在下**所有產品**，選取 Office 365 Enterprise E3 和 Enterprise Mobility + Security 選取 hello 產品名稱。 toostart hello 分派，選取**指派**在 hello hello 刀鋒視窗最上方。

   ![所有產品、指派授權](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. 在 hello**指派授權**刀鋒視窗中，按一下 **使用者和群組**tooopen hello**使用者和群組**刀鋒視窗。 Hello 群組名稱的搜尋*人力資源部門皆*選取 hello 群組，然後依序按一下要確定 tooconfirm**選取**在 hello hello 刀鋒視窗的底部。

   ![選取群組](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. 在 hello**指派授權**刀鋒視窗中，按一下 **指派選項 （選擇性）**，其中顯示所有服務方案包含在 hello 我們先前選取的兩個產品。 尋找**Yammer 企業**並使其**關閉**toodisable 從 hello 產品授權服務。 按一下以確認**確定**底部的 hello**指派選項**。

   ![指派選項](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. hello 上的 toocomplete hello 指派**指派授權**刀鋒視窗中，按一下 **指派**在 hello hello 刀鋒視窗的底部。

8. Hello 右上角，其中顯示 hello 狀態和 hello 程序結果中會顯示通知。 如果 hello 分派 toohello 群組無法完成 （例如，由於 hello 群組中的現有預先授權） 中，按一下 hello hello 失敗的通知 tooview 詳細資料。

我們現在已經指定 hello 人力資源部門皆群組的授權範本。 在 Azure AD 中的背景處理序已啟動的 tooprocess 該群組的所有現有的成員。 這項初始作業可能需要一些時間，視 hello hello 群組目前大小而定。 在 hello 下一個步驟中，我們將說明如何 tooverify hello 程序已完成，並判斷是否需要的 tooresolve 問題進一步注意。

> [!NOTE]
> 您可以啟動 hello 從替代位置的同一個指派：**使用者和群組**在 Azure AD 中。 跳過**Azure Active Directory** > **使用者和群組** > **所有群組**。 然後尋找 hello 群組、 選取它，並移 toohello**授權** 索引標籤 hello**指派**hello 刀鋒視窗頂端的按鈕會開啟 hello 授權指派 刀鋒視窗。

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>步驟 2： 驗證 hello 初始作業已完成

1. 跳過**Azure Active Directory** > **使用者和群組** > **所有群組**。 然後尋找 hello**人力資源部門皆**授權指派給群組。

2. 在 hello**人力資源部門皆**群組刀鋒視窗中，選取**授權**。 這可讓您快速確認授權已獲完全指派 toousers，而且如果有需要 toolook 到任何錯誤。 使用位於 hello 下列資訊：

   - 目前的產品授權清單指派 toohello 群組。 選取項目 tooshow hello 特定服務已啟用，並 toomake 變更。

   - Hello 最新授權所做的變更 toohello 群組 （如果正在處理 hello 變更，或處理已完成的所有使用者的成員） 的狀態。

   - 處於錯誤狀態，因為 toothem 無法指派授權的使用者的相關資訊。

   ![指派選項](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. 如需授權處理的詳細資訊，請參閱 [Azure Active Directory] > [使用者和群組] > 群組名稱 > [稽核記錄]。 請注意下列活動的 hello:

   - 活動：**開始套用群組的基礎授權 toousers**。 這會記錄 hello 系統拾取 hello hello 群組和啟動時將它套用 tooall 使用者成員上的授權指派變更時。 它包含 hello 所做變更的相關資訊。

   - 活動：**結束套用群組的基礎授權 toousers**。 這會記錄當 hello 系統完成處理 hello 群組中的所有使用者。 它包含已成功處理的使用者人數和無法獲得群組授權指派的使用者人數之摘要。

   [閱讀本節](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity)toolearn 深入了解如何稽核記錄檔可能會使用的 tooanalyze 變更群組為基礎的授權。

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>步驟 3︰檢查授權問題及解決這些問題

1. 跳過**Azure Active Directory** > **使用者和群組** > **所有群組**，並尋找 hello**人力資源部門皆**授權指派給群組。
2. 在 hello**人力資源部門皆**群組刀鋒視窗中，選取**授權**。 在 [hello] 刀鋒視窗頂端的 hello 通知顯示無法指派授權給 10 個使用者。 按一下通知，隨即開啟一份此群組為授權錯誤狀態的所有使用者。
3. hello**無法指派**資料行告訴我們這兩個產品的授權，無法指派 toohello 使用者。 hello**排名最前面的失敗原因**資料行包含 hello hello 失敗原因。 在此案例中為 [衝突的服務方案]。

   ![失敗的指派](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. 選取使用者 tooopen hello**授權**刀鋒視窗。 此刀鋒視窗會顯示所有目前已指派 toohello 使用者的授權。 在此範例中，hello 使用者具有繼承自 hello 的 hello Office 365 Enterprise E1 授權**Kiosk 使用者**群組。 這與 hello 系統嘗試 tooapply 從 hello 的 hello E3 授權衝突**人力資源部門皆**群組。 如此一來，無該群組中的 hello 授權已被指派 toohello 使用者。

   ![檢視使用者的授權](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve 這項衝突，移除 hello 使用者從 hello **Kiosk 使用者**群組。 Azure AD 處理 hello 變更之後，hello**人力資源部門皆**正確指派授權。

   ![已正確指派的授權](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>後續步驟

toolearn hello 功能有關的詳細資訊設定的授權管理透過群組，請參閱下列文章的 hello:

* [什麼是 Azure Active Directory 中以群組為基礎的授權？](active-directory-licensing-whatis-azure-portal.md)
* [識別及解決 Azure Active Directory 中群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory 群組型授權其他案例 (英文)](active-directory-licensing-group-advanced.md)
