---
title: "Azure AD Connect 同步： 變更 hello 預設組態 |Microsoft 文件"
description: "提供變更 hello 的 Azure AD Connect 同步處理的預設組態的最佳作法。"
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
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a><span data-ttu-id="4dae8-103">Azure AD Connect 同步： 變更 hello 預設組態的最佳做法</span><span class="sxs-lookup"><span data-stu-id="4dae8-103">Azure AD Connect sync: Best practices for changing hello default configuration</span></span>
<span data-ttu-id="4dae8-104">本主題的 hello 目的是 toodescribe 支援和不支援變更 tooAzure AD Connect 同步處理。</span><span class="sxs-lookup"><span data-stu-id="4dae8-104">hello purpose of this topic is toodescribe supported and unsupported changes tooAzure AD Connect sync.</span></span>

<span data-ttu-id="4dae8-105">建立 Azure AD connect 的 hello 組態適用於 「 現狀 」 同步處理內部部署 Active Directory 與 Azure AD 的大多數環境。</span><span class="sxs-lookup"><span data-stu-id="4dae8-105">hello configuration created by Azure AD Connect works “as is” for most environments that synchronize on-premises Active Directory with Azure AD.</span></span> <span data-ttu-id="4dae8-106">不過，在某些情況下，它是必要的 tooapply 需要某些變更 tooa 組態 toosatisfy 特定或需求。</span><span class="sxs-lookup"><span data-stu-id="4dae8-106">However, in some cases, it is necessary tooapply some changes tooa configuration toosatisfy a particular need or requirement.</span></span>

## <a name="changes-toohello-service-account"></a><span data-ttu-id="4dae8-107">變更 toohello 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="4dae8-107">Changes toohello service account</span></span>
<span data-ttu-id="4dae8-108">Azure AD Connect 同步 hello 安裝精靈所建立的服務帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="4dae8-108">Azure AD Connect sync is running under a service account created by hello installation wizard.</span></span> <span data-ttu-id="4dae8-109">此服務帳戶會保留 hello 加密金鑰 toohello 資料庫同步處理所使用。它使用 127 個字元長的密碼建立和設定 toonot hello 密碼到期。</span><span class="sxs-lookup"><span data-stu-id="4dae8-109">This service account holds hello encryption keys toohello database used by sync. It is created with a 127 characters long password and hello password is set toonot expire.</span></span>

* <span data-ttu-id="4dae8-110">它是**不支援**hello 服務帳戶的 toochange 或重設的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="4dae8-110">It is **unsupported** toochange or reset hello password of hello service account.</span></span> <span data-ttu-id="4dae8-111">這樣會終結 hello 加密金鑰並且 hello 服務不能 tooaccess hello 資料庫，且不能 toostart。</span><span class="sxs-lookup"><span data-stu-id="4dae8-111">Doing so destroys hello encryption keys and hello service is not able tooaccess hello database and is not able toostart.</span></span>

## <a name="changes-toohello-scheduler"></a><span data-ttu-id="4dae8-112">變更 toohello 排程器</span><span class="sxs-lookup"><span data-stu-id="4dae8-112">Changes toohello scheduler</span></span>
<span data-ttu-id="4dae8-113">開頭為從組建 1.1 的 hello 版本 (年 2 月 2016)，您可以設定 hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)toohave 不同的同步處理循環比 hello 預設 30 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4dae8-113">Starting with hello releases from build 1.1 (February 2016) you can configure hello [scheduler](active-directory-aadconnectsync-feature-scheduler.md) toohave a different sync cycle than hello default 30 minutes.</span></span>

## <a name="changes-toosynchronization-rules"></a><span data-ttu-id="4dae8-114">變更 tooSynchronization 規則</span><span class="sxs-lookup"><span data-stu-id="4dae8-114">Changes tooSynchronization Rules</span></span>
<span data-ttu-id="4dae8-115">hello 安裝精靈提供了應該 toowork hello 最常見案例的組態。</span><span class="sxs-lookup"><span data-stu-id="4dae8-115">hello installation wizard provides a configuration that is supposed toowork for hello most common scenarios.</span></span> <span data-ttu-id="4dae8-116">萬一您需要 toomake 變更 toohello 組態，您必須遵循這些規則 toostill 具有支援的組態。</span><span class="sxs-lookup"><span data-stu-id="4dae8-116">In case you need toomake changes toohello configuration, then you must follow these rules toostill have a supported configuration.</span></span>

* <span data-ttu-id="4dae8-117">您可以[變更屬性流程](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes)如果 hello 預設直接屬性流程不是適用於您的組織。</span><span class="sxs-lookup"><span data-stu-id="4dae8-117">You can [change attribute flows](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) if hello default direct attribute flows are not suitable for your organization.</span></span>
* <span data-ttu-id="4dae8-118">如果您想太[流動屬性](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute)並移除任何現有的屬性值在 Azure AD 中，則您在此案例需要 toocreate 規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-118">If you want too[not flow an attribute](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) and remove any existing attribute values in Azure AD, then you need toocreate a rule for this scenario.</span></span>
* <span data-ttu-id="4dae8-119">[停用不必要的同步處理規則](#disable-an-unwanted-sync-rule) 而非加以刪除。</span><span class="sxs-lookup"><span data-stu-id="4dae8-119">[Disable an unwanted Sync Rule](#disable-an-unwanted-sync-rule) rather than deleting it.</span></span> <span data-ttu-id="4dae8-120">升級期間會重新建立已刪除的規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-120">A deleted rule is recreated during an upgrade.</span></span>
* <span data-ttu-id="4dae8-121">太[變更鶈蜪規則](#change-an-out-of-box-rule)，您應該複製一份 hello 原始規則並停用 hello 鶈蜪規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-121">too[change an out-of-box rule](#change-an-out-of-box-rule), you should make a copy of hello original rule and disable hello out-of-box rule.</span></span> <span data-ttu-id="4dae8-122">hello 同步處理規則編輯器會提示，並協助您。</span><span class="sxs-lookup"><span data-stu-id="4dae8-122">hello Sync Rule Editor prompts and helps you.</span></span>
* <span data-ttu-id="4dae8-123">匯出自訂同步處理規則使用 hello 同步處理規則編輯器。</span><span class="sxs-lookup"><span data-stu-id="4dae8-123">Export your custom synchronization rules using hello Synchronization Rules Editor.</span></span> <span data-ttu-id="4dae8-124">hello 編輯器會提供您一個 PowerShell 指令碼，您可以使用 tooeasily 重新建立它們的災害復原案例中。</span><span class="sxs-lookup"><span data-stu-id="4dae8-124">hello editor provides you with a PowerShell script you can use tooeasily recreate them in a disaster recovery scenario.</span></span>

> [!WARNING]
> <span data-ttu-id="4dae8-125">hello 現成的同步處理規則有憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="4dae8-125">hello out-of-box sync rules have a thumbprint.</span></span> <span data-ttu-id="4dae8-126">如果 toothese 規則進行變更，不再符合 hello 指紋。</span><span class="sxs-lookup"><span data-stu-id="4dae8-126">If you make a change toothese rules, hello thumbprint is no longer matching.</span></span> <span data-ttu-id="4dae8-127">當您嘗試 tooapply Azure AD Connect 的新版本時，可能會在未來的 hello 發生問題。</span><span class="sxs-lookup"><span data-stu-id="4dae8-127">You might have problems in hello future when you try tooapply a new release of Azure AD Connect.</span></span> <span data-ttu-id="4dae8-128">在本文中，只提供變更 hello 方式描述。</span><span class="sxs-lookup"><span data-stu-id="4dae8-128">Only make changes hello way it is described in this article.</span></span>

### <a name="disable-an-unwanted-sync-rule"></a><span data-ttu-id="4dae8-129">停用不必要的同步處理規則</span><span class="sxs-lookup"><span data-stu-id="4dae8-129">Disable an unwanted Sync Rule</span></span>
<span data-ttu-id="4dae8-130">請勿刪除現成可用的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-130">Do not delete an out-of-box sync rule.</span></span> <span data-ttu-id="4dae8-131">升級期間會重新建立此規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-131">It is recreated during next upgrade.</span></span>

<span data-ttu-id="4dae8-132">在某些情況下，hello 安裝精靈所產生的組態，您的拓撲無法作用。</span><span class="sxs-lookup"><span data-stu-id="4dae8-132">In some cases, hello installation wizard has produced a configuration that is not working for your topology.</span></span> <span data-ttu-id="4dae8-133">例如，如果您有帳戶資源樹系拓撲，但您有擴充的 hello 結構描述與 hello Exchange 結構描述的 hello 帳戶樹系中，規則適用於 Exchange 會建立 hello 帳戶樹系和 hello 資源樹系。</span><span class="sxs-lookup"><span data-stu-id="4dae8-133">For example, if you have an account-resource forest topology but you have extended hello schema in hello account forest with hello Exchange schema, then rules for Exchange are created for hello account forest and hello resource forest.</span></span> <span data-ttu-id="4dae8-134">在此情況下，您需要適用於 Exchange toodisable hello 的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-134">In this case, you need toodisable hello Sync Rule for Exchange.</span></span>

![已停用同步處理規則](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

<span data-ttu-id="4dae8-136">在上述的 hello 圖片，hello 安裝精靈已找到 hello 帳戶樹系中的舊的 Exchange 2003 結構描述。</span><span class="sxs-lookup"><span data-stu-id="4dae8-136">In hello picture above, hello installation wizard has found an old Exchange 2003 schema in hello account forest.</span></span> <span data-ttu-id="4dae8-137">Fabrikam 的環境中導入 hello 資源樹系之前，已加入此結構描述延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4dae8-137">This schema extension was added before hello resource forest was introduced in Fabrikam's environment.</span></span> <span data-ttu-id="4dae8-138">tooensure 同步 hello 舊 Exchange 實作沒有屬性，應停用 hello 同步處理規則，如所示。</span><span class="sxs-lookup"><span data-stu-id="4dae8-138">tooensure no attributes from hello old Exchange implementation are synchronized, hello sync rule should be disabled as shown.</span></span>

### <a name="change-an-out-of-box-rule"></a><span data-ttu-id="4dae8-139">變更現成可用的規則</span><span class="sxs-lookup"><span data-stu-id="4dae8-139">Change an out-of-box rule</span></span>
<span data-ttu-id="4dae8-140">hello 唯一的時候，您應該變更預設的規則時，您需要 toochange hello 聯結規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-140">hello only time you should change an out-of-box rule is when you need toochange hello join rule.</span></span> <span data-ttu-id="4dae8-141">如果您需要 toochange 屬性流程，則您應該建立同步處理規則的優先順序高於 hello 鶈蜪規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-141">If you need toochange an attribute flow, then you should create a sync rule with higher precedence than hello out-of-box rules.</span></span> <span data-ttu-id="4dae8-142">只有您幾乎需要 tooclone 規則是 hello hello**中 from AD-User Join**。</span><span class="sxs-lookup"><span data-stu-id="4dae8-142">hello only rule you practically need tooclone is hello rule **In from AD - User Join**.</span></span> <span data-ttu-id="4dae8-143">您可以使用具有較高優先順序的規則來覆寫所有其他規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-143">You can override all other rules with a higher precedence rule.</span></span>

<span data-ttu-id="4dae8-144">如果您需要 toomake 變更 tooan 鶈蜪規則，然後應該複製一份 hello 鶈蜪規則並停用 hello 原始規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-144">If you need toomake changes tooan out-of-box rule, then you should make a copy of hello out-of-box rule and disable hello original rule.</span></span> <span data-ttu-id="4dae8-145">然後請 hello 變更 toohello 複製的規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-145">Then make hello changes toohello cloned rule.</span></span> <span data-ttu-id="4dae8-146">hello 同步處理規則編輯器會協助您進行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="4dae8-146">hello Sync Rule Editor is helping you with those steps.</span></span> <span data-ttu-id="4dae8-147">當您開啟現成可用的規則時，即會顯示此對話方塊：</span><span class="sxs-lookup"><span data-stu-id="4dae8-147">When you open an out-of-box rule, you are presented with this dialog box:</span></span>  
![對現成可用的規則發出警告](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

<span data-ttu-id="4dae8-149">選取**是**toocreate hello 規則的複本。</span><span class="sxs-lookup"><span data-stu-id="4dae8-149">Select **Yes** toocreate a copy of hello rule.</span></span> <span data-ttu-id="4dae8-150">然後開啟 hello 複製的規則。</span><span class="sxs-lookup"><span data-stu-id="4dae8-150">hello cloned rule is then opened.</span></span>  
<span data-ttu-id="4dae8-151">![複製的規則](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)</span><span class="sxs-lookup"><span data-stu-id="4dae8-151">![Cloned rule](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)</span></span>

<span data-ttu-id="4dae8-152">在此複製的規則，進行任何必要的變更 tooscope、 聯結和轉換。</span><span class="sxs-lookup"><span data-stu-id="4dae8-152">On this cloned rule, make any necessary changes tooscope, join, and transformations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dae8-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4dae8-153">Next steps</span></span>
<span data-ttu-id="4dae8-154">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="4dae8-154">**Overview topics**</span></span>

* [<span data-ttu-id="4dae8-155">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="4dae8-155">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4dae8-156">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dae8-156">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
