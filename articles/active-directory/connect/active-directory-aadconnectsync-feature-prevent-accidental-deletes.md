---
title: "Azure AD Connect 同步：防止意外刪除 |Microsoft Docs"
description: "本主題說明 Azure AD Connect 中的防止意外刪除 (可防止意外刪除) 功能。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a33fb729cff5007e40820af696cfec823a3ecfde
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a><span data-ttu-id="8fc94-103">Azure AD Connect 同步處理：防止意外刪除</span><span class="sxs-lookup"><span data-stu-id="8fc94-103">Azure AD Connect sync: Prevent accidental deletes</span></span>
<span data-ttu-id="8fc94-104">本主題說明 Azure AD Connect 中的防止意外刪除 (可防止意外刪除) 功能。</span><span class="sxs-lookup"><span data-stu-id="8fc94-104">This topic describes the prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.</span></span>

<span data-ttu-id="8fc94-105">安裝 Azure AD Connect 時，依預設會啟用防止意外刪除的功能，並設定為不允許超過 500 個刪除項目的匯出。</span><span class="sxs-lookup"><span data-stu-id="8fc94-105">When installing Azure AD Connect, prevent accidental deletes is enabled by default and configured to not allow an export with more than 500 deletes.</span></span> <span data-ttu-id="8fc94-106">這項功能是專門用來保護您免於意外的組態變更及內部部署目錄的變更，因為這會影響許多使用者和其他物件。</span><span class="sxs-lookup"><span data-stu-id="8fc94-106">This feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and other objects.</span></span>

## <a name="what-is-prevent-accidental-deletes"></a><span data-ttu-id="8fc94-107">防止意外刪除是什麼</span><span class="sxs-lookup"><span data-stu-id="8fc94-107">What is prevent accidental deletes</span></span>
<span data-ttu-id="8fc94-108">會看到多項刪除的常見案例包括：</span><span class="sxs-lookup"><span data-stu-id="8fc94-108">Common scenarios when you see many deletes include:</span></span>

* <span data-ttu-id="8fc94-109">變更未選取整個 [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) 或[網域](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering)的[篩選](active-directory-aadconnectsync-configure-filtering.md)。</span><span class="sxs-lookup"><span data-stu-id="8fc94-109">Changes to [filtering](active-directory-aadconnectsync-configure-filtering.md) where an entire [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) or [domain](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is unselected.</span></span>
* <span data-ttu-id="8fc94-110">OU 中的所有物件遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="8fc94-110">All objects in an OU are deleted.</span></span>
* <span data-ttu-id="8fc94-111">重新命名 OU，結果使得其中的所有物件被視為不在同步處理範圍內。</span><span class="sxs-lookup"><span data-stu-id="8fc94-111">An OU is renamed so all objects in it are considered to be out of scope for synchronization.</span></span>

<span data-ttu-id="8fc94-112">可以使用 PowerShell 的 `Enable-ADSyncExportDeletionThreshold`進行變更的預設值是 500 個物件。</span><span class="sxs-lookup"><span data-stu-id="8fc94-112">The default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="8fc94-113">您應該將此值設定為符合您組織的大小。</span><span class="sxs-lookup"><span data-stu-id="8fc94-113">You should configure this value to fit the size of your organization.</span></span> <span data-ttu-id="8fc94-114">由於同步排程器會每隔 30 分鐘執行一次，因此該值是 30 分鐘內看到的刪除數目。</span><span class="sxs-lookup"><span data-stu-id="8fc94-114">Since the sync scheduler runs every 30 minutes, the value is the number of deletes seen within 30 minutes.</span></span>

<span data-ttu-id="8fc94-115">如果有太多刪除預備要匯出到 Azure AD，則匯出會停止，且您會收到如下的電子郵件：</span><span class="sxs-lookup"><span data-stu-id="8fc94-115">If there are too many deletes staged to be exported to Azure AD, then the export stops and you receive an email like this:</span></span>

![防止意外刪除電子郵件](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> <span data-ttu-id="8fc94-117">*Hello (技術連絡人)。有時身分識別同步處理服務偵測到的刪除數目會超過 (組織名稱) 所設定的刪除閾值。本次執行身分識別同步處理時，共傳送 (數目) 個物件進行刪除。這已到達或超過設定的 (數目) 個物件的刪除閾值。您需先確認要刪除這些項目，才可繼續進行。若要深入了解此電子郵件中列出的錯誤，請參見防止意外刪除。*</span><span class="sxs-lookup"><span data-stu-id="8fc94-117">*Hello (technical contact). At (time) the Identity synchronization service detected that the number of deletions exceeded the configured deletion threshold for (organization name). A total of (number) objects were sent for deletion in this Identity synchronization run. This met or exceeded the configured deletion threshold value of (number) objects. We need you to provide confirmation that these deletions should be processed before we will proceed. Please see the preventing accidental deletions for more information about the error listed in this email message.*</span></span>
>
> 

<span data-ttu-id="8fc94-118">當您查看匯出設定檔的 **Synchronization Service Manager** UI，您也會看到狀態 `stopped-deletion-threshold-exceeded`。</span><span class="sxs-lookup"><span data-stu-id="8fc94-118">You can also see the status `stopped-deletion-threshold-exceeded` when you look in the **Synchronization Service Manager** UI for the Export profile.</span></span>
<span data-ttu-id="8fc94-119">![防止意外刪除 Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="8fc94-119">![Prevent Accidental deletes Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span></span>

<span data-ttu-id="8fc94-120">如果這是非預期的結果，請進行調查，並採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="8fc94-120">If this was unexpected, then investigate and take corrective actions.</span></span> <span data-ttu-id="8fc94-121">若要查看哪些物件即將被刪除時，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="8fc94-121">To see which objects are about to be deleted, do the following:</span></span>

1. <span data-ttu-id="8fc94-122">從 [開始] 功能表啟動 [同步處理服務]  。</span><span class="sxs-lookup"><span data-stu-id="8fc94-122">Start **Synchronization Service** from the Start Menu.</span></span>
2. <span data-ttu-id="8fc94-123">移至 [連接器] 。</span><span class="sxs-lookup"><span data-stu-id="8fc94-123">Go to **Connectors**.</span></span>
3. <span data-ttu-id="8fc94-124">選取 **Azure Active Directory**類型的連接器。</span><span class="sxs-lookup"><span data-stu-id="8fc94-124">Select the Connector with type **Azure Active Directory**.</span></span>
4. <span data-ttu-id="8fc94-125">在右側的 [動作] 之下，選取 [搜尋連接器空間]。</span><span class="sxs-lookup"><span data-stu-id="8fc94-125">Under **Actions** to the right, select **Search Connector Space**.</span></span>
5. <span data-ttu-id="8fc94-126">在 [範圍] 下的快顯中，選取 [中斷連線起點]，並選擇一個過去的時間。</span><span class="sxs-lookup"><span data-stu-id="8fc94-126">In the pop-up under **Scope**, select **Disconnected Since** and pick a time in the past.</span></span> <span data-ttu-id="8fc94-127">按一下 [搜尋] 。</span><span class="sxs-lookup"><span data-stu-id="8fc94-127">Click **Search**.</span></span> <span data-ttu-id="8fc94-128">此頁面會顯示所有即將刪除的物件。</span><span class="sxs-lookup"><span data-stu-id="8fc94-128">This page provides a view of all objects about to be deleted.</span></span> <span data-ttu-id="8fc94-129">按一下每個項目，您就可以了解該物件的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="8fc94-129">By clicking each item, you can get additional information about the object.</span></span> <span data-ttu-id="8fc94-130">您也可以按一下 [資料行設定]  ，新增其他屬性以顯示在方格中。</span><span class="sxs-lookup"><span data-stu-id="8fc94-130">You can also click **Column Setting** to add additional attributes to be visible in the grid.</span></span>

![搜尋連接器空間](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

<span data-ttu-id="8fc94-132">如果想要刪除所有項目，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="8fc94-132">If all the deletes are desired, then do the following:</span></span>

1. <span data-ttu-id="8fc94-133">若要擷取目前的刪除閾值，請執行 PowerShell Cmdlet `Get-ADSyncExportDeletionThreshold`。</span><span class="sxs-lookup"><span data-stu-id="8fc94-133">To retrieve the current deletion threshold, run the PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="8fc94-134">提供 Azure AD 全域系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="8fc94-134">Provide an Azure AD Global Administrator account and password.</span></span> <span data-ttu-id="8fc94-135">預設值為 500。</span><span class="sxs-lookup"><span data-stu-id="8fc94-135">The default value is 500.</span></span>
2. <span data-ttu-id="8fc94-136">若要暫時停用此保護功能並刪除這些項目，請執行 PowerShell Cmdlet： `Disable-ADSyncExportDeletionThreshold`。</span><span class="sxs-lookup"><span data-stu-id="8fc94-136">To temporarily disable this protection and let those deletes go through, run the PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="8fc94-137">提供 Azure AD 全域系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="8fc94-137">Provide an Azure AD Global Administrator account and password.</span></span>
   <span data-ttu-id="8fc94-138">![認證](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span><span class="sxs-lookup"><span data-stu-id="8fc94-138">![Credentials](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span></span>
3. <span data-ttu-id="8fc94-139">如果 Azure Active Directory Connector 仍處於選取狀態，請選取 [執行] 動作，再選取 [匯出]。</span><span class="sxs-lookup"><span data-stu-id="8fc94-139">With the Azure Active Directory Connector still selected, select the action **Run** and select **Export**.</span></span>
4. <span data-ttu-id="8fc94-140">若要重新啟用此保護功能，請執行 PowerShell Cmdlet： `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`。</span><span class="sxs-lookup"><span data-stu-id="8fc94-140">To re-enable the protection, run the PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span></span> <span data-ttu-id="8fc94-141">使用您在擷取目前刪除閾值時記下的值來取代 500。</span><span class="sxs-lookup"><span data-stu-id="8fc94-141">Replace 500 with the value you noticed when retrieving the current deletion threshold.</span></span> <span data-ttu-id="8fc94-142">提供 Azure AD 全域系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="8fc94-142">Provide an Azure AD Global Administrator account and password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc94-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fc94-143">Next steps</span></span>
<span data-ttu-id="8fc94-144">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="8fc94-144">**Overview topics**</span></span>

* [<span data-ttu-id="8fc94-145">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="8fc94-145">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="8fc94-146">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fc94-146">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
