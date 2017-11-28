---
title: "Azure AD Connect：選取安裝類型 | Microsoft Docs"
description: "本主題引導您 tooselect hello 安裝的 Azure AD Connect 所輸入的 toouse"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="d83ee-103">選取 Azure AD Connect 的安裝類型 toouse</span><span class="sxs-lookup"><span data-stu-id="d83ee-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="d83ee-104">Azure AD Connect 針對新安裝提供兩種安裝類型：快速和自訂。</span><span class="sxs-lookup"><span data-stu-id="d83ee-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="d83ee-105">本主題可協助您在安裝期間選項 toouse toodecide。</span><span class="sxs-lookup"><span data-stu-id="d83ee-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="d83ee-106">Express</span><span class="sxs-lookup"><span data-stu-id="d83ee-106">Express</span></span>
<span data-ttu-id="d83ee-107">Express 是 hello 最常見的選項，並正由 90%的所有新的安裝。</span><span class="sxs-lookup"><span data-stu-id="d83ee-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="d83ee-108">它是設計的 tooprovide hello 最常見的客戶案例的運作方式的設定。</span><span class="sxs-lookup"><span data-stu-id="d83ee-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="d83ee-109">此選項假設：</span><span class="sxs-lookup"><span data-stu-id="d83ee-109">It assumes:</span></span>

- <span data-ttu-id="d83ee-110">您有內部部署的單一 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="d83ee-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="d83ee-111">您擁有 hello 安裝，您可以使用企業系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d83ee-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="d83ee-112">您內部部署 Active Directory 中的物件少於 10 萬個。</span><span class="sxs-lookup"><span data-stu-id="d83ee-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="d83ee-113">您會獲得：</span><span class="sxs-lookup"><span data-stu-id="d83ee-113">You get:</span></span>

- <span data-ttu-id="d83ee-114">[密碼同步化](active-directory-aadconnectsync-implement-password-synchronization.md)從內部部署 tooAzure AD 進行單一登入。</span><span class="sxs-lookup"><span data-stu-id="d83ee-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="d83ee-115">同步處理[使用者、群組、連絡人及 Windows 10 電腦](active-directory-aadconnectsync-understanding-default-configuration.md)的組態。</span><span class="sxs-lookup"><span data-stu-id="d83ee-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="d83ee-116">所有網域和所有 OU 中所有合格物件的同步處理。</span><span class="sxs-lookup"><span data-stu-id="d83ee-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="d83ee-117">[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)是啟用的 toomake 確定您一律使用 hello 最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="d83ee-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="d83ee-118">在下列情況下，您仍然可以選擇使用 [快速]：</span><span class="sxs-lookup"><span data-stu-id="d83ee-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="d83ee-119">如果您不想 toosynchronize 所有 Ou，您仍然可以使用快速並在 hello 最後一個頁面上，取消選取**啟動 hello 同步處理程序...***.</span><span class="sxs-lookup"><span data-stu-id="d83ee-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="d83ee-120">然後再次執行 hello 安裝精靈，並變更中的 hello Ou[組態選項](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)並啟用排程的同步處理。</span><span class="sxs-lookup"><span data-stu-id="d83ee-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="d83ee-121">您想例如密碼回寫 tooenable 其中一項在 Azure AD Premium，hello 功能。</span><span class="sxs-lookup"><span data-stu-id="d83ee-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="d83ee-122">先經過 express tooget hello 初始安裝已完成。</span><span class="sxs-lookup"><span data-stu-id="d83ee-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="d83ee-123">然後再次執行 hello 安裝精靈，並變更 hello[組態選項](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)。</span><span class="sxs-lookup"><span data-stu-id="d83ee-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="d83ee-124">自訂</span><span class="sxs-lookup"><span data-stu-id="d83ee-124">Custom</span></span>
<span data-ttu-id="d83ee-125">hello 自訂的路徑可讓您比 express 更多選擇。</span><span class="sxs-lookup"><span data-stu-id="d83ee-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="d83ee-126">它應在所有情況下，快速的上一節中所述的 hello 設定不代表貴組織。</span><span class="sxs-lookup"><span data-stu-id="d83ee-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="d83ee-127">使用時機：</span><span class="sxs-lookup"><span data-stu-id="d83ee-127">Use when:</span></span>

- <span data-ttu-id="d83ee-128">您沒有在 Active Directory 中存取 tooan 企業系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d83ee-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="d83ee-129">您有多個樹系，或您計劃 toosynchronize hello 未來中的多個樹系。</span><span class="sxs-lookup"><span data-stu-id="d83ee-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="d83ee-130">您無法連線到從 hello 連接伺服器的樹系中有網域。</span><span class="sxs-lookup"><span data-stu-id="d83ee-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="d83ee-131">您計劃 toouse 同盟或傳遞驗證的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="d83ee-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="d83ee-132">您有 100,000 個以上的物件，而且需要 toouse 完整的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="d83ee-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="d83ee-133">您計劃 toouse 群組為基礎的篩選和不僅網域或組織單位型篩選。</span><span class="sxs-lookup"><span data-stu-id="d83ee-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="d83ee-134">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="d83ee-134">Upgrade from DirSync</span></span>
<span data-ttu-id="d83ee-135">如果您目前使用 DirSync，然後依照中的 hello 步驟[從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md)tooupgrade 您現有的組態。</span><span class="sxs-lookup"><span data-stu-id="d83ee-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="d83ee-136">有兩個不同的升級選項：</span><span class="sxs-lookup"><span data-stu-id="d83ee-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="d83ee-137">就地升級 tooinstall 連接上 hello 相同伺服器。</span><span class="sxs-lookup"><span data-stu-id="d83ee-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="d83ee-138">Hello 現有的 DirSync 伺服器仍可運作時，平行部署 tooinstall 連接新的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="d83ee-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="d83ee-139">從 Azure AD Sync 升級</span><span class="sxs-lookup"><span data-stu-id="d83ee-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="d83ee-140">如果您目前使用 Azure AD Sync，則您可以依照 hello[相同的步驟](active-directory-aadconnect-upgrade-previous-version.md)做為您從一個連接版本 tooa 較新的升級時。</span><span class="sxs-lookup"><span data-stu-id="d83ee-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="d83ee-141">有兩個不同的升級選項：</span><span class="sxs-lookup"><span data-stu-id="d83ee-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="d83ee-142">就地升級 tooinstall 連接上 hello 相同伺服器。</span><span class="sxs-lookup"><span data-stu-id="d83ee-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="d83ee-143">迴旋移轉 tooinstall 連接新的伺服器時 hello 現有 Azure AD 同步伺服器上時仍可運作。</span><span class="sxs-lookup"><span data-stu-id="d83ee-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="d83ee-144">從 FIM2010 或 MIM2016 移轉</span><span class="sxs-lookup"><span data-stu-id="d83ee-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="d83ee-145">如果您目前以 hello Azure AD 連接器使用 Forefront Identity Manager 2010 或 Microsoft Identity Manager 2016，唯一的選項是移轉。</span><span class="sxs-lookup"><span data-stu-id="d83ee-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="d83ee-146">中所述步驟 hello[迴旋移轉](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)。</span><span class="sxs-lookup"><span data-stu-id="d83ee-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="d83ee-147">在 hello 步驟中，取代 FIM2010/MIM2016 中任何提及 Azure AD Sync。</span><span class="sxs-lookup"><span data-stu-id="d83ee-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d83ee-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d83ee-148">Next steps</span></span>
<span data-ttu-id="d83ee-149">根據 hello 選項而定，您已選取 toouse，請使用 hello 資料表的內容 toohello 左 toofind 您文件以 hello 詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="d83ee-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
