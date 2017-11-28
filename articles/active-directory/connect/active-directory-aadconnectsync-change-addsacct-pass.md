---
title: "Azure AD Connect 同步： 變更 hello AD DS 帳戶密碼 |Microsoft 文件"
description: "此主題說明如何變更 tooupdate 之後 hello hello AD DS 帳戶密碼的 Azure AD Connect。"
services: active-directory
keywords: "AD DS 帳戶, Active Directory 帳戶, 密碼"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="295a9-104">變更 hello AD DS 帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="295a9-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="295a9-105">hello AD DS 帳戶指的是使用內部部署 Active Directory 與 Azure AD Connect toocommunicate toohello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="295a9-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="295a9-106">如果您變更 hello 的 hello AD DS 帳戶的密碼，您必須更新 Azure AD Connect 同步處理服務與 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="295a9-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="295a9-107">否則，同步處理可以不再正確同步處理以 hello hello 內部部署 Active Directory，您將會遇到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="295a9-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="295a9-108">在 hello 與同步處理服務管理員、 匯入或匯出作業在內部部署 AD 失敗，並**無開始認證**錯誤。</span><span class="sxs-lookup"><span data-stu-id="295a9-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="295a9-109">在 Windows 事件檢視器，hello 應用程式事件記錄檔包含與錯誤**事件識別碼 6000**和訊息**'hello 管理代理程式"contoso.com"hello 認證無效，因為無法 toorun'**.</span><span class="sxs-lookup"><span data-stu-id="295a9-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="295a9-110">如何 tooupdate hello 與 AD DS 帳戶的新密碼的同步處理服務</span><span class="sxs-lookup"><span data-stu-id="295a9-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="295a9-111">使用新密碼的 hello tooupdate hello 同步服務：</span><span class="sxs-lookup"><span data-stu-id="295a9-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="295a9-112">啟動 hello Synchronization Service Manager （開始 → 同步處理服務）。</span><span class="sxs-lookup"><span data-stu-id="295a9-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="295a9-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="295a9-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="295a9-114">移 toohello**連接器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="295a9-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="295a9-115">選取 hello **AD 連接器**對應已變更其密碼的 toohello AD DS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="295a9-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="295a9-116">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="295a9-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="295a9-117">在 hello 快顯對話方塊中，選取 **連接 tooActive Directory 樹系**:</span><span class="sxs-lookup"><span data-stu-id="295a9-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="295a9-118">輸入 hello hello hello AD DS 帳戶新密碼**密碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="295a9-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="295a9-119">按一下**確定**toosave hello 新密碼] 和 [關閉 hello 快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="295a9-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="295a9-120">重新啟動 hello Azure AD Connect 同步處理服務在 Windows 服務控制管理員。</span><span class="sxs-lookup"><span data-stu-id="295a9-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="295a9-121">這是 tooensure hello 記憶體快取中已移除任何參照 toohello 舊密碼。</span><span class="sxs-lookup"><span data-stu-id="295a9-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="295a9-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="295a9-122">Next steps</span></span>
<span data-ttu-id="295a9-123">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="295a9-123">**Overview topics**</span></span>

* [<span data-ttu-id="295a9-124">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="295a9-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="295a9-125">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="295a9-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
