---
title: "Azure AD Connect：選取安裝類型 | Microsoft Docs"
description: "本主題將逐步解說如何選取要用於 Azure AD Connect 的安裝類型"
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
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="9d879-103">選取要用於 Azure AD Connect 的安裝類型</span><span class="sxs-lookup"><span data-stu-id="9d879-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="9d879-104">Azure AD Connect 針對新安裝提供兩種安裝類型：快速和自訂。</span><span class="sxs-lookup"><span data-stu-id="9d879-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="9d879-105">本主題將協助您決定安裝時要使用的選項。</span><span class="sxs-lookup"><span data-stu-id="9d879-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="9d879-106">Express</span><span class="sxs-lookup"><span data-stu-id="9d879-106">Express</span></span>
<span data-ttu-id="9d879-107">[快速] 是最常見的選項，大約 90% 的全新安裝是使用此選項。</span><span class="sxs-lookup"><span data-stu-id="9d879-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="9d879-108">其設計目的是要提供適用於最常見客戶案例的組態。</span><span class="sxs-lookup"><span data-stu-id="9d879-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="9d879-109">此選項假設：</span><span class="sxs-lookup"><span data-stu-id="9d879-109">It assumes:</span></span>

- <span data-ttu-id="9d879-110">您有內部部署的單一 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="9d879-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="9d879-111">您有可用來進行安裝的企業系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="9d879-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="9d879-112">您內部部署 Active Directory 中的物件少於 10 萬個。</span><span class="sxs-lookup"><span data-stu-id="9d879-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="9d879-113">您會獲得：</span><span class="sxs-lookup"><span data-stu-id="9d879-113">You get:</span></span>

- <span data-ttu-id="9d879-114">從內部部署到 Azure AD 的[密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)，用於進行單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d879-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="9d879-115">同步處理[使用者、群組、連絡人及 Windows 10 電腦](active-directory-aadconnectsync-understanding-default-configuration.md)的組態。</span><span class="sxs-lookup"><span data-stu-id="9d879-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="9d879-116">所有網域和所有 OU 中所有合格物件的同步處理。</span><span class="sxs-lookup"><span data-stu-id="9d879-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="9d879-117">[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)會啟用以確保您一律使用最新的可用版本。</span><span class="sxs-lookup"><span data-stu-id="9d879-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="9d879-118">在下列情況下，您仍然可以選擇使用 [快速]：</span><span class="sxs-lookup"><span data-stu-id="9d879-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="9d879-119">如果您不想要同步處理所有 OU，您仍然可以使用 [快速]，然後在最後一頁取消選取 [開始同步處理程序]*。</span><span class="sxs-lookup"><span data-stu-id="9d879-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="9d879-120">接著，再次執行安裝精靈並變更[組態選項](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)中的 OU，然後啟用排定的同步處理。</span><span class="sxs-lookup"><span data-stu-id="9d879-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="9d879-121">您想要啟用 Azure AD Premium 的其中一個功能，例如密碼回寫。</span><span class="sxs-lookup"><span data-stu-id="9d879-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="9d879-122">請先透過快速安裝來完成初始安裝。</span><span class="sxs-lookup"><span data-stu-id="9d879-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="9d879-123">接著，再次執行安裝精靈並變更[組態選項](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)。</span><span class="sxs-lookup"><span data-stu-id="9d879-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="9d879-124">自訂</span><span class="sxs-lookup"><span data-stu-id="9d879-124">Custom</span></span>
<span data-ttu-id="9d879-125">自訂路徑所允許的選項比快速安裝多更多。</span><span class="sxs-lookup"><span data-stu-id="9d879-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="9d879-126">在上一節所述的快速組態無法代表您組織情況的所有案例中，都應該使用自訂路徑。</span><span class="sxs-lookup"><span data-stu-id="9d879-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="9d879-127">使用時機：</span><span class="sxs-lookup"><span data-stu-id="9d879-127">Use when:</span></span>

- <span data-ttu-id="9d879-128">您無法存取 Active Directory 中的企業管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="9d879-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="9d879-129">您有多個樹系，或是您未來打算同步處理多個樹系。</span><span class="sxs-lookup"><span data-stu-id="9d879-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="9d879-130">您樹系中有無法從 Connect 伺服器連線的網域。</span><span class="sxs-lookup"><span data-stu-id="9d879-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="9d879-131">您打算使用同盟或傳遞驗證來進行使用者登入。</span><span class="sxs-lookup"><span data-stu-id="9d879-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="9d879-132">您擁有的物件超過 10 萬個，並且需要使用完整的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="9d879-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="9d879-133">您打算使用群組型篩選，而不只是網域型或 OU 型篩選。</span><span class="sxs-lookup"><span data-stu-id="9d879-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="9d879-134">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="9d879-134">Upgrade from DirSync</span></span>
<span data-ttu-id="9d879-135">如果您目前使用的是 DirSync，則請依照[從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md)中的步驟來升級您現有的組態。</span><span class="sxs-lookup"><span data-stu-id="9d879-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="9d879-136">有兩個不同的升級選項：</span><span class="sxs-lookup"><span data-stu-id="9d879-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="9d879-137">就地升級：將 Connect 安裝在相同伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9d879-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="9d879-138">平行部署：將 Connect 安裝在新伺服器上，但現有 DirSync 伺服器仍可運作。</span><span class="sxs-lookup"><span data-stu-id="9d879-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="9d879-139">從 Azure AD Sync 升級</span><span class="sxs-lookup"><span data-stu-id="9d879-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="9d879-140">如果您目前使用的是 Azure AD Sync，則可以依照從一個 Connect 版本升級到更新版本時的[相同步驟](active-directory-aadconnect-upgrade-previous-version.md)操作。</span><span class="sxs-lookup"><span data-stu-id="9d879-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="9d879-141">有兩個不同的升級選項：</span><span class="sxs-lookup"><span data-stu-id="9d879-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="9d879-142">就地升級：將 Connect 安裝在相同伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9d879-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="9d879-143">搖擺移轉：將 Connect 安裝在新伺服器上，但現有 Azure AD Sync 伺服器仍可運作。</span><span class="sxs-lookup"><span data-stu-id="9d879-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="9d879-144">從 FIM2010 或 MIM2016 移轉</span><span class="sxs-lookup"><span data-stu-id="9d879-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="9d879-145">如果您目前使用的是 Forefront Identity Manager 2010 或 Microsoft Identity Manager 2016 搭配 Azure AD Connector，則您的唯一選項是移轉。</span><span class="sxs-lookup"><span data-stu-id="9d879-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="9d879-146">請依照[搖擺移轉](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)所述的步驟操作。</span><span class="sxs-lookup"><span data-stu-id="9d879-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="9d879-147">在步驟中，請將所有提到 Azure AD Sync 的地方取代成 FIM2010/MIM2016。</span><span class="sxs-lookup"><span data-stu-id="9d879-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d879-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d879-148">Next steps</span></span>
<span data-ttu-id="9d879-149">請依據您所選取要使用的選項，使用左邊的目錄來尋找含有詳細步驟的文章。</span><span class="sxs-lookup"><span data-stu-id="9d879-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
