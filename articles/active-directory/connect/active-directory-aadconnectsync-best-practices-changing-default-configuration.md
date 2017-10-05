---
title: "Azure AD Connect 同步：變更預設組態 | Microsoft Docs"
description: "提供變更 Azure AD Connect 同步處理預設組態的最佳作法。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b723ad800ccc0f3040eb480bb72960943b1fdb16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-the-default-configuration"></a><span data-ttu-id="5d2d5-103">Azure AD Connect 同步處理：變更預設組態的最佳作法</span><span class="sxs-lookup"><span data-stu-id="5d2d5-103">Azure AD Connect sync: Best practices for changing the default configuration</span></span>
<span data-ttu-id="5d2d5-104">本主題的目的旨在說明支援及不支援的 Azure AD Connect 同步處理變更。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-104">The purpose of this topic is to describe supported and unsupported changes to Azure AD Connect sync.</span></span>

<span data-ttu-id="5d2d5-105">Azure AD Connect 所建立的組態適用於大部分同步內部部署 Active Directory 與 Azure AD 的「現狀」環境。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-105">The configuration created by Azure AD Connect works “as is” for most environments that synchronize on-premises Active Directory with Azure AD.</span></span> <span data-ttu-id="5d2d5-106">不過，在某些情況下，組態必須套用某些變更以滿足特定需要或需求。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-106">However, in some cases, it is necessary to apply some changes to a configuration to satisfy a particular need or requirement.</span></span>

## <a name="changes-to-the-service-account"></a><span data-ttu-id="5d2d5-107">服務帳戶的變更</span><span class="sxs-lookup"><span data-stu-id="5d2d5-107">Changes to the service account</span></span>
<span data-ttu-id="5d2d5-108">Azure AD Connect 同步處理會使用安裝精靈所建立的服務帳戶執行。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-108">Azure AD Connect sync is running under a service account created by the installation wizard.</span></span> <span data-ttu-id="5d2d5-109">這個服務帳戶會存放同步處理所使用的資料庫加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-109">This service account holds the encryption keys to the database used by sync.</span></span> <span data-ttu-id="5d2d5-110">它是使用 127 個字元長的密碼所建立的，而且密碼已設定為永不到期。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-110">It is created with a 127 characters long password and the password is set to not expire.</span></span>

* <span data-ttu-id="5d2d5-111">它 **不支援** 變更或重設服務帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-111">It is **unsupported** to change or reset the password of the service account.</span></span> <span data-ttu-id="5d2d5-112">這麼做會損毀加密金鑰，而服務無法存取資料庫且無法啟動。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-112">Doing so destroys the encryption keys and the service is not able to access the database and is not able to start.</span></span>

## <a name="changes-to-the-scheduler"></a><span data-ttu-id="5d2d5-113">排程器的變更</span><span class="sxs-lookup"><span data-stu-id="5d2d5-113">Changes to the scheduler</span></span>
<span data-ttu-id="5d2d5-114">從組建 1.1 (2016 年 2 月) 的版本開始，您可以將 [排程器](active-directory-aadconnectsync-feature-scheduler.md) 的同步處理週期設定為預設值 30 分鐘以外的值。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-114">Starting with the releases from build 1.1 (February 2016) you can configure the [scheduler](active-directory-aadconnectsync-feature-scheduler.md) to have a different sync cycle than the default 30 minutes.</span></span>

## <a name="changes-to-synchronization-rules"></a><span data-ttu-id="5d2d5-115">同步處理規則的變更</span><span class="sxs-lookup"><span data-stu-id="5d2d5-115">Changes to Synchronization Rules</span></span>
<span data-ttu-id="5d2d5-116">安裝精靈所提供的組態應該適用於最常見的案例。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-116">The installation wizard provides a configuration that is supposed to work for the most common scenarios.</span></span> <span data-ttu-id="5d2d5-117">萬一您需要對組態進行變更，則您必須遵循這些規則，以便仍能具備支援的組態。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-117">In case you need to make changes to the configuration, then you must follow these rules to still have a supported configuration.</span></span>

* <span data-ttu-id="5d2d5-118">如果預設的直接屬性流程不適合您的組織使用，您可以 [變更屬性流程](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) 。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-118">You can [change attribute flows](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) if the default direct attribute flows are not suitable for your organization.</span></span>
* <span data-ttu-id="5d2d5-119">如果您想要 [不傳送屬性](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) 並移除 Azure AD 中任何現有的屬性值，則必須為此案例建立規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-119">If you want to [not flow an attribute](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) and remove any existing attribute values in Azure AD, then you need to create a rule for this scenario.</span></span>
* <span data-ttu-id="5d2d5-120">[停用不必要的同步處理規則](#disable-an-unwanted-sync-rule) 而非加以刪除。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-120">[Disable an unwanted Sync Rule](#disable-an-unwanted-sync-rule) rather than deleting it.</span></span> <span data-ttu-id="5d2d5-121">升級期間會重新建立已刪除的規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-121">A deleted rule is recreated during an upgrade.</span></span>
* <span data-ttu-id="5d2d5-122">若要 [變更現成可用的規則](#change-an-out-of-box-rule)，您應該複製原始規則並停用現成可用的規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-122">To [change an out-of-box rule](#change-an-out-of-box-rule), you should make a copy of the original rule and disable the out-of-box rule.</span></span> <span data-ttu-id="5d2d5-123">同步處理規則編輯器會提示並協助您。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-123">The Sync Rule Editor prompts and helps you.</span></span>
* <span data-ttu-id="5d2d5-124">使用同步處理規則編輯器，匯出您的自訂同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-124">Export your custom synchronization rules using the Synchronization Rules Editor.</span></span> <span data-ttu-id="5d2d5-125">此編輯器會提供可用來在災害復原情況下輕鬆重建它們的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-125">The editor provides you with a PowerShell script you can use to easily recreate them in a disaster recovery scenario.</span></span>

> [!WARNING]
> <span data-ttu-id="5d2d5-126">現成可用的同步處理規則具有憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-126">The out-of-box sync rules have a thumbprint.</span></span> <span data-ttu-id="5d2d5-127">如果您變更這些規則，將不再符合憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-127">If you make a change to these rules, the thumbprint is no longer matching.</span></span> <span data-ttu-id="5d2d5-128">未來當您嘗試套用新版的 Azure AD Connect 時可能會遇到問題。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-128">You might have problems in the future when you try to apply a new release of Azure AD Connect.</span></span> <span data-ttu-id="5d2d5-129">僅利用本文所述的方式進行變更。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-129">Only make changes the way it is described in this article.</span></span>

### <a name="disable-an-unwanted-sync-rule"></a><span data-ttu-id="5d2d5-130">停用不必要的同步處理規則</span><span class="sxs-lookup"><span data-stu-id="5d2d5-130">Disable an unwanted Sync Rule</span></span>
<span data-ttu-id="5d2d5-131">請勿刪除現成可用的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-131">Do not delete an out-of-box sync rule.</span></span> <span data-ttu-id="5d2d5-132">升級期間會重新建立此規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-132">It is recreated during next upgrade.</span></span>

<span data-ttu-id="5d2d5-133">在某些情況下，安裝精靈所產生的組態不適用於您的拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-133">In some cases, the installation wizard has produced a configuration that is not working for your topology.</span></span> <span data-ttu-id="5d2d5-134">例如，如果您具備帳戶與資源樹系拓撲，但已在具備 Exchange 結構描述的帳戶樹系中擴充該結構描述，則系統會針對帳戶樹系和資源樹系建立適用於 Exchange 的規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-134">For example, if you have an account-resource forest topology but you have extended the schema in the account forest with the Exchange schema, then rules for Exchange are created for the account forest and the resource forest.</span></span> <span data-ttu-id="5d2d5-135">在此情況下，您需要停用適用於 Exchange 的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-135">In this case, you need to disable the Sync Rule for Exchange.</span></span>

![已停用同步處理規則](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

<span data-ttu-id="5d2d5-137">在上圖中，安裝精靈已在帳戶樹系中找到舊的 Exchange 2003 結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-137">In the picture above, the installation wizard has found an old Exchange 2003 schema in the account forest.</span></span> <span data-ttu-id="5d2d5-138">此結構描述擴充是在 Fabrikam 的環境中引進資源樹系之前新增的。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-138">This schema extension was added before the resource forest was introduced in Fabrikam's environment.</span></span> <span data-ttu-id="5d2d5-139">若要確保不會同步處理任何來自舊的 Exchange 實作的屬性，就必須以所述的方式停用同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-139">To ensure no attributes from the old Exchange implementation are synchronized, the sync rule should be disabled as shown.</span></span>

### <a name="change-an-out-of-box-rule"></a><span data-ttu-id="5d2d5-140">變更現成可用的規則</span><span class="sxs-lookup"><span data-stu-id="5d2d5-140">Change an out-of-box rule</span></span>
<span data-ttu-id="5d2d5-141">只有當您需要變更聯結規則時，才應該變更內建規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-141">The only time you should change an out-of-box rule is when you need to change the join rule.</span></span> <span data-ttu-id="5d2d5-142">如果您需要變更屬性流程，則您應該建立其優先順序高於內建規則的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-142">If you need to change an attribute flow, then you should create a sync rule with higher precedence than the out-of-box rules.</span></span> <span data-ttu-id="5d2d5-143">您實際上唯一需要複製的規則是 **In from AD - User Join** 規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-143">The only rule you practically need to clone is the rule **In from AD - User Join**.</span></span> <span data-ttu-id="5d2d5-144">您可以使用具有較高優先順序的規則來覆寫所有其他規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-144">You can override all other rules with a higher precedence rule.</span></span>

<span data-ttu-id="5d2d5-145">如果您需要對現成可用的規則進行變更，則您應該複製該現成可用的規則，然後停用原始的規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-145">If you need to make changes to an out-of-box rule, then you should make a copy of the out-of-box rule and disable the original rule.</span></span> <span data-ttu-id="5d2d5-146">接著對複製的規則進行變更。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-146">Then make the changes to the cloned rule.</span></span> <span data-ttu-id="5d2d5-147">同步處理規則編輯器會協助您完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-147">The Sync Rule Editor is helping you with those steps.</span></span> <span data-ttu-id="5d2d5-148">當您開啟現成可用的規則時，即會顯示此對話方塊：</span><span class="sxs-lookup"><span data-stu-id="5d2d5-148">When you open an out-of-box rule, you are presented with this dialog box:</span></span>  
![對現成可用的規則發出警告](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

<span data-ttu-id="5d2d5-150">選取 [是]  來建立規則的複本。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-150">Select **Yes** to create a copy of the rule.</span></span> <span data-ttu-id="5d2d5-151">隨即會開啟複製的規則。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-151">The cloned rule is then opened.</span></span>  
<span data-ttu-id="5d2d5-152">![複製的規則](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)</span><span class="sxs-lookup"><span data-stu-id="5d2d5-152">![Cloned rule](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)</span></span>

<span data-ttu-id="5d2d5-153">在這個複製的規則上，對範圍、聯結和轉換進行任何必要變更。</span><span class="sxs-lookup"><span data-stu-id="5d2d5-153">On this cloned rule, make any necessary changes to scope, join, and transformations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d2d5-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d2d5-154">Next steps</span></span>
<span data-ttu-id="5d2d5-155">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="5d2d5-155">**Overview topics**</span></span>

* [<span data-ttu-id="5d2d5-156">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="5d2d5-156">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="5d2d5-157">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d2d5-157">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
