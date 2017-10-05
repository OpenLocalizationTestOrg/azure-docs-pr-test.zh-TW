---
title: "Azure AD Connect 同步處理：變更 AD DS 帳戶密碼 | Microsoft Docs"
description: "本主題文件說明如何在變更 AD DS 帳戶的密碼後更新 Azure AD Connect。"
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
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="4caec-104">變更 AD DS 帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="4caec-104">Changing the AD DS account password</span></span>
<span data-ttu-id="4caec-105">AD DS 帳戶指的是 Azure AD Connect 用來與內部部署 Active Directory 進行通訊的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4caec-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="4caec-106">如果您變更 AD DS 帳戶的密碼，您必須以新密碼更新 Azure AD Connect 同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="4caec-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="4caec-107">否則，同步處理服務就無法再正確地與內部部署 Active Directory 進行同步處理，而且您會遇到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="4caec-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="4caec-108">在同步處理服務管理員中，使用內部部署 AD 進行的匯入或匯出作業會失敗，並出現 **no-start-credentials** 錯誤。</span><span class="sxs-lookup"><span data-stu-id="4caec-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="4caec-109">Windows 事件檢視器底下的應用程式事件記錄會包含**事件識別碼為 6000** 的錯誤與**「管理代理程式 "contoso.com" 無法執行，因為認證無效」**的訊息。</span><span class="sxs-lookup"><span data-stu-id="4caec-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="4caec-110">如何以新的 AD DS 帳戶密碼更新同步處理服務</span><span class="sxs-lookup"><span data-stu-id="4caec-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="4caec-111">若要以新密碼更新同步處理服務︰</span><span class="sxs-lookup"><span data-stu-id="4caec-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="4caec-112">啟動同步處理服務管理員 ([開始] → [同步處理服務])。</span><span class="sxs-lookup"><span data-stu-id="4caec-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="4caec-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="4caec-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="4caec-114">移至 [連接器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4caec-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="4caec-115">選取密碼已變更之 AD DS 帳戶所對應的 [AD 連接器]。</span><span class="sxs-lookup"><span data-stu-id="4caec-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="4caec-116">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="4caec-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="4caec-117">在快顯對話方塊中，選取 [連線至 Active Directory 樹系]：</span><span class="sxs-lookup"><span data-stu-id="4caec-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="4caec-118">在 [密碼] 文字方塊中輸入 AD DS 帳戶的新密碼。</span><span class="sxs-lookup"><span data-stu-id="4caec-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="4caec-119">按一下 [確定] 以儲存新密碼，然後關閉快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4caec-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="4caec-120">在 Windows 服務控制管理員底下重新啟動 Azure AD Connect 同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="4caec-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="4caec-121">這可確保系統會從記憶體快取中移除舊密碼的任何參考。</span><span class="sxs-lookup"><span data-stu-id="4caec-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4caec-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4caec-122">Next steps</span></span>
<span data-ttu-id="4caec-123">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="4caec-123">**Overview topics**</span></span>

* [<span data-ttu-id="4caec-124">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="4caec-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="4caec-125">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4caec-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
