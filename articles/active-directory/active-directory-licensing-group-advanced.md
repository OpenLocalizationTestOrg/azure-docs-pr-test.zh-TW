---
title: "以群組為基礎來授權其他案例的 Active Directory aaaAzure |Microsoft 文件"
description: "Azure Active Directory 群組型授權的更多案例"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a><span data-ttu-id="3d539-104">案例、 限制和使用 Azure Active Directory 中的群組 toomanage 授權的已知的問題</span><span class="sxs-lookup"><span data-stu-id="3d539-104">Scenarios, limitations, and known issues using groups toomanage licensing in Azure Active Directory</span></span>

<span data-ttu-id="3d539-105">使用下列資訊和範例 toogain 進一步了解 Azure Active Directory (Azure AD) 以群組為基礎授權的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d539-105">Use hello following information and examples toogain a more advanced understanding of Azure Active Directory (Azure AD) group-based licensing.</span></span>

## <a name="usage-location"></a><span data-ttu-id="3d539-106">使用位置</span><span class="sxs-lookup"><span data-stu-id="3d539-106">Usage location</span></span>

<span data-ttu-id="3d539-107">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="3d539-107">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="3d539-108">Hello 管理員 tooa 使用者可以指派授權之前，已 toospecify hello**使用位置**hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="3d539-108">Before a license can be assigned tooa user, hello administrator has toospecify hello **Usage location** property on hello user.</span></span> <span data-ttu-id="3d539-109">在[hello Azure 入口網站](https://portal.azure.com)，您可以指定在**使用者** &gt; **設定檔** &gt; **設定**。</span><span class="sxs-lookup"><span data-stu-id="3d539-109">In [hello Azure portal](https://portal.azure.com), you can specify in **User** &gt; **Profile** &gt; **Settings**.</span></span>

<span data-ttu-id="3d539-110">取得群組的授權指派，指定使用位置沒有任何使用者將會繼承 hello hello 目錄位置。</span><span class="sxs-lookup"><span data-stu-id="3d539-110">For group license assignment, any users without a usage location specified will inherit hello location of hello directory.</span></span> <span data-ttu-id="3d539-111">如果您有多個位置中的使用者，請確定 tooreflect 正確使用者物件中新增並授權使用者 toogroups 之前。</span><span class="sxs-lookup"><span data-stu-id="3d539-111">If you have users in multiple locations, make sure tooreflect that correctly in your user objects before adding users toogroups with licenses.</span></span>

> [!NOTE]
> <span data-ttu-id="3d539-112">群組授權指派永遠不會修改使用者現有的使用位置值。</span><span class="sxs-lookup"><span data-stu-id="3d539-112">Group license assignment will never modify an existing usage location value on a user.</span></span> <span data-ttu-id="3d539-113">我們建議您一律將使用位置做為您的使用者建立流程的一部分 （例如透過 AAD Connect 組態）-可確保的授權指派的 hello 結果一定是正確的且使用者不會收到服務不的位置中的 Azure AD 中允許的。</span><span class="sxs-lookup"><span data-stu-id="3d539-113">We recommend that you always set usage location as part of your user creation flow in Azure AD (e.g. via AAD Connect configuration) - that will ensure hello result of license assignment is always correct, and users do not receive services in locations that are not allowed.</span></span>

## <a name="use-group-based-licensing-with-dynamic-groups"></a><span data-ttu-id="3d539-114">對動態群組使用群組型授權</span><span class="sxs-lookup"><span data-stu-id="3d539-114">Use group-based licensing with dynamic groups</span></span>

<span data-ttu-id="3d539-115">您可以對任何安全性群組使用群組型授權，這表示可與 Azure AD 動態群組結合。</span><span class="sxs-lookup"><span data-stu-id="3d539-115">You can use group-based licensing with any security group, which means it can be combined with Azure AD dynamic groups.</span></span> <span data-ttu-id="3d539-116">加入對使用者物件屬性 tooautomatically 執行規則的動態群組，並從群組移除使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-116">Dynamic groups run rules against user object attributes tooautomatically add and remove users from groups.</span></span>

<span data-ttu-id="3d539-117">例如，您可以建立動態群組想 tooassign toousers 某些產品集。</span><span class="sxs-lookup"><span data-stu-id="3d539-117">For example, you can create a dynamic group for some set of products you want tooassign toousers.</span></span> <span data-ttu-id="3d539-118">每個群組會擴展其屬性，新增使用者的規則，且每個群組是您想讓 tooreceive hello 分派的授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-118">Each group is populated by a rule adding users by their attributes, and each group is assigned hello licenses that you want them tooreceive.</span></span> <span data-ttu-id="3d539-119">可以指派 hello 屬性在內部部署以及與 Azure AD 同步處理，或者您可以管理直接在 hello 雲端中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d539-119">You can assign hello attribute on-premises and sync it with Azure AD, or you can manage hello attribute directly in hello cloud.</span></span>

<span data-ttu-id="3d539-120">授權就會加入 toohello 群組後不久指派 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-120">Licenses are assigned toohello user shortly after they are added toohello group.</span></span> <span data-ttu-id="3d539-121">Hello 屬性變更時，hello 使用者離開 hello 群組，並移除 hello 授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-121">When hello attribute is changed, hello user leaves hello groups and hello licenses are removed.</span></span>

### <a name="example"></a><span data-ttu-id="3d539-122">範例</span><span class="sxs-lookup"><span data-stu-id="3d539-122">Example</span></span>

<span data-ttu-id="3d539-123">請考慮在內部部署身分識別管理解決方案，決定哪些使用者應該可以存取 tooMicrosoft web 服務的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="3d539-123">Consider hello example of an on-premises identity management solution that decides which users should have access tooMicrosoft web services.</span></span> <span data-ttu-id="3d539-124">它會使用**extensionAttribute1** toostore 的字串值 hello 使用者應該具有代表 hello 授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-124">It uses **extensionAttribute1** toostore a string value representing hello licenses hello user should have.</span></span> <span data-ttu-id="3d539-125">Azure AD Connect 會將它與 Azure AD 同步。</span><span class="sxs-lookup"><span data-stu-id="3d539-125">Azure AD Connect syncs it with Azure AD.</span></span>

<span data-ttu-id="3d539-126">使用者可能需要其中一個授權，也可能需要兩個授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-126">Users might need one license but not another, or might need both.</span></span> <span data-ttu-id="3d539-127">以下是的範例，在其中您所發佈 Office 365 企業版 E5 和企業行動力 + 安全性 (EMS) 授權 toousers 群組中：</span><span class="sxs-lookup"><span data-stu-id="3d539-127">Here's an example, in which you are distributing Office 365 Enterprise E5 and Enterprise Mobility + Security (EMS) licenses toousers in groups:</span></span>

#### <a name="office-365-enterprise-e5-base-services"></a><span data-ttu-id="3d539-128">Office 365 企業版 E5︰基本服務</span><span class="sxs-lookup"><span data-stu-id="3d539-128">Office 365 Enterprise E5: base services</span></span>

![Office 365 企業版 E5 基本服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a><span data-ttu-id="3d539-130">Enterprise Mobility + Security︰授權的使用者</span><span class="sxs-lookup"><span data-stu-id="3d539-130">Enterprise Mobility + Security: licensed users</span></span>

![Enterprise Mobility + Security 授權的使用者螢幕擷取畫面](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

<span data-ttu-id="3d539-132">此範例中，修改一位使用者以及設定其 extensionAttribute1 toohello 值`EMS;E5_baseservices;`如果您想 hello 使用者 toohave 兩個授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-132">For this example, modify one user and set their extensionAttribute1 toohello value of `EMS;E5_baseservices;` if you want hello user toohave both licenses.</span></span> <span data-ttu-id="3d539-133">您可以在內部部署做此修改。</span><span class="sxs-lookup"><span data-stu-id="3d539-133">You can make this modification on-premises.</span></span> <span data-ttu-id="3d539-134">Hello 之後變更與 hello 雲端同步、 hello 使用者會自動加入 tooboth 群組及指派授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-134">After hello change syncs with hello cloud, hello user is automatically added tooboth groups, and licenses are assigned.</span></span>

![顯示如何 tooset hello extensionAttribute1 使用者的螢幕擷取畫面](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> <span data-ttu-id="3d539-136">修改現有群組的成員資格規則時請小心。</span><span class="sxs-lookup"><span data-stu-id="3d539-136">Use caution when modifying an existing group’s membership rule.</span></span> <span data-ttu-id="3d539-137">當變更規則、 hello hello 群組成員資格將會重新評估和不再符合使用者 hello 新規則將會移除 （仍需符合 hello 新規則的使用者將不會影響在此程序）。</span><span class="sxs-lookup"><span data-stu-id="3d539-137">When a rule is changed, hello membership of hello group will be re-evaluated and users who no longer match hello new rule will be removed (users who still match hello new rule will not be affected during this process).</span></span> <span data-ttu-id="3d539-138">那些使用者就能在 hello 程序中無法使用服務，或在某些情況下，可能會導致資料遺失期間移除其授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-138">Those users will have their licenses removed during hello process which may result in loss of service, or in some cases, loss of data.</span></span>

> <span data-ttu-id="3d539-139">如果您有大型的動態群組，視授權指派，請考慮驗證較小的測試群組上進行重大變更，再將它們套用 toohello 主要群組。</span><span class="sxs-lookup"><span data-stu-id="3d539-139">If you have a large dynamic group you depend on for license assignment, consider validating any major changes on a smaller test group before applying them toohello main group.</span></span>

## <a name="multiple-groups-and-multiple-licenses"></a><span data-ttu-id="3d539-140">多個群組和多個授權</span><span class="sxs-lookup"><span data-stu-id="3d539-140">Multiple groups and multiple licenses</span></span>

<span data-ttu-id="3d539-141">使用者可以是多個具有授權之群組的成員。</span><span class="sxs-lookup"><span data-stu-id="3d539-141">A user can be a member of multiple groups with licenses.</span></span> <span data-ttu-id="3d539-142">以下是一些事情 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="3d539-142">Here are some things tooconsider:</span></span>

- <span data-ttu-id="3d539-143">多個授權 hello 相同的產品可以重疊，而且它們會讓所有啟用服務正在套用的 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-143">Multiple licenses for hello same product can overlap, and they result in all enabled services being applied toohello user.</span></span> <span data-ttu-id="3d539-144">hello 下列範例顯示兩個授權群組： *E3 基本服務*包含 hello foundation 服務 toodeploy 第一次，tooall 使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-144">hello following example shows two licensing groups: *E3 base services* contains hello foundation services toodeploy first, tooall users.</span></span> <span data-ttu-id="3d539-145">和*E3 擴充服務*包含其他服務 （Sway 和規劃） toodeploy 只有 toosome 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-145">And *E3 extended services* contains additional services (Sway and Planner) toodeploy only toosome users.</span></span> <span data-ttu-id="3d539-146">在此範例中，hello 使用者加入 tooboth 群組：</span><span class="sxs-lookup"><span data-stu-id="3d539-146">In this example, hello user was added tooboth groups:</span></span>

  ![已啟用服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  <span data-ttu-id="3d539-148">如此一來，hello 使用者有 7 個 hello 12 服務在 hello 產品啟用，同時使用這項產品只能有一個授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-148">As a result, hello user has 7 of hello 12 services in hello product enabled, while using only one license for this product.</span></span>

- <span data-ttu-id="3d539-149">選取 hello *E3*授權顯示更多詳細資料，包括哪些群組會造成 hello 使用者啟用何種服務 toobe 的資訊。</span><span class="sxs-lookup"><span data-stu-id="3d539-149">Selecting hello *E3* license shows more details, including information about which groups caused what services toobe enabled for hello user.</span></span>

  ![依群組啟用服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a><span data-ttu-id="3d539-151">直接授權與群組授權共存</span><span class="sxs-lookup"><span data-stu-id="3d539-151">Direct licenses coexist with group licenses</span></span>

<span data-ttu-id="3d539-152">當使用者從群組繼承授權時，無法直接移除，或修改該 hello 使用者內容中的授權指派。</span><span class="sxs-lookup"><span data-stu-id="3d539-152">When a user inherits a license from a group, you can't directly remove or modify that license assignment in hello user's properties.</span></span> <span data-ttu-id="3d539-153">變更 hello 群組中必須進行，然後再傳播 tooall 使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-153">Changes must be made in hello group and then propagated tooall users.</span></span>

<span data-ttu-id="3d539-154">它，直接在加法 toohello toohello 使用者繼承授權 tooassign 但是 hello 相同的產品授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-154">It is possible, however, tooassign hello same product license directly toohello user, in addition toohello inherited license.</span></span> <span data-ttu-id="3d539-155">您可以啟用其他服務從 hello 產品，只針對一個使用者，而不會影響其他使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-155">You can enable additional services from hello product just for one user, without affecting other users.</span></span>

<span data-ttu-id="3d539-156">可以移除直接指派的授權，而不會影響繼承的授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-156">Directly assigned licenses can be removed, and don’t affect inherited licenses.</span></span> <span data-ttu-id="3d539-157">請考慮 hello，使用者會繼承有 Office 365 Enterprise E3 的授權群組。</span><span class="sxs-lookup"><span data-stu-id="3d539-157">Consider hello user who inherits an Office 365 Enterprise E3 license from a group.</span></span>

1. <span data-ttu-id="3d539-158">Hello 使用者一開始，只會從 hello 繼承 hello 授權*E3 基本服務*群組，讓您的四個的服務方案，如所示：</span><span class="sxs-lookup"><span data-stu-id="3d539-158">Initially, hello user inherits hello license only from hello *E3 basic services* group, which enables four service plans, as shown:</span></span>

  ![E3 群組啟用的服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. <span data-ttu-id="3d539-160">您可以選取**指派**toodirectly E3 授權 toohello 將使用者指派。</span><span class="sxs-lookup"><span data-stu-id="3d539-160">You can select **Assign** toodirectly assign an E3 license toohello user.</span></span> <span data-ttu-id="3d539-161">在此情況下，您將的 toodisable Yammer 企業以外的所有服務計都劃：</span><span class="sxs-lookup"><span data-stu-id="3d539-161">In this case, you are going toodisable all service plans except Yammer Enterprise:</span></span>

  ![如何的螢幕擷取畫面 tooassign 授權直接 tooa 使用者](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. <span data-ttu-id="3d539-163">如此一來，hello 使用者仍會使用一個 hello E3 產品的授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-163">As a result, hello user still uses only one license of hello E3 product.</span></span> <span data-ttu-id="3d539-164">但 hello 直接指派可讓 hello Yammer 企業服務只會為該使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-164">But hello direct assignment enables hello Yammer Enterprise service for that user only.</span></span> <span data-ttu-id="3d539-165">您可以看到哪些服務為啟用 hello 與 hello 直接指派的群組成員資格：</span><span class="sxs-lookup"><span data-stu-id="3d539-165">You can see which services are enabled by hello group membership versus hello direct assignment:</span></span>

  ![繼承和直接指派的螢幕擷取畫面](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. <span data-ttu-id="3d539-167">當您使用直接指派時，允許下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="3d539-167">When you use direct assignment, hello following operations are allowed:</span></span>

  - <span data-ttu-id="3d539-168">Yammer 企業可以關閉 hello 使用者物件上直接。</span><span class="sxs-lookup"><span data-stu-id="3d539-168">Yammer Enterprise can be turned off on hello user object directly.</span></span> <span data-ttu-id="3d539-169">hello**開/關**切換 hello 圖中的已啟用這項服務，但不要 toohello 其他服務切換。</span><span class="sxs-lookup"><span data-stu-id="3d539-169">hello **On/Off** toggle in hello illustration was enabled for this service, as opposed toohello other service toggles.</span></span> <span data-ttu-id="3d539-170">因為在 hello 使用者上直接啟用 hello 服務時，您可以進行修改。</span><span class="sxs-lookup"><span data-stu-id="3d539-170">Because hello service is enabled directly on hello user, it can be modified.</span></span>
  - <span data-ttu-id="3d539-171">其他服務可以直接將授權指派給 hello 的一部分，啟用。</span><span class="sxs-lookup"><span data-stu-id="3d539-171">Additional services can be enabled as well, as part of hello directly assigned license.</span></span>
  - <span data-ttu-id="3d539-172">hello**移除**按鈕可以使用的 tooremove hello 直接授權的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-172">hello **Remove** button can be used tooremove hello direct license from hello user.</span></span> <span data-ttu-id="3d539-173">您可以看到 hello 使用者現在僅有 hello 繼承的群組授權，而且 hello 原始服務保持啟用：</span><span class="sxs-lookup"><span data-stu-id="3d539-173">You can see that hello user now only has hello inherited group license and only hello original services remain enabled:</span></span>

    ![顯示如何 tooremove 直接指派螢幕擷取畫面](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a><span data-ttu-id="3d539-175">管理新的服務加入 tooproducts</span><span class="sxs-lookup"><span data-stu-id="3d539-175">Managing new services added tooproducts</span></span>
<span data-ttu-id="3d539-176">當 Microsoft 將新的服務 tooa 產品時，將會啟用預設會在您已指派的所有群組 toowhich hello 產品授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-176">When Microsoft adds a new service tooa product, it will be enabled by default in all groups toowhich you have assigned hello product license.</span></span> <span data-ttu-id="3d539-177">在您的租用戶會訂閱的 toonotifications 產品變更的相關的使用者都會收到電子郵件，事先 hello 服務即將新增功能的相關通知。</span><span class="sxs-lookup"><span data-stu-id="3d539-177">Users in your tenant who are subscribed toonotifications about product changes will receive emails ahead of time notifying them about hello upcoming service additions.</span></span>

<span data-ttu-id="3d539-178">身為管理員，您可以檢閱 hello 變更影響的所有群組，並採取動作，例如停用每個群組中的 hello 新服務。</span><span class="sxs-lookup"><span data-stu-id="3d539-178">As an administrator, you can review all groups affected by hello change and take action, such as disabling hello new service in each group.</span></span> <span data-ttu-id="3d539-179">例如，如果您建立的群組只要以用於部署的特定服務為目標，您可以返回這些群組，並確定已停用所有新增的服務。</span><span class="sxs-lookup"><span data-stu-id="3d539-179">For example, if you created groups targeting only specific services for deployment, you can revisit those groups and make sure that any newly added services are disabled.</span></span>

<span data-ttu-id="3d539-180">此程序可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="3d539-180">Here is an example of what this process may look like:</span></span>

1. <span data-ttu-id="3d539-181">您一開始指派 hello *Office 365 企業版 E5*產品 tooseveral 群組。</span><span class="sxs-lookup"><span data-stu-id="3d539-181">Originally, you assigned hello *Office 365 Enterprise E5* product tooseveral groups.</span></span> <span data-ttu-id="3d539-182">其中一個群組，稱為*O365 E5-僅適用於 Exchange*已設計的 tooenable 只有 hello *Exchange Online (計劃 2)*服務為其成員。</span><span class="sxs-lookup"><span data-stu-id="3d539-182">One of those groups, called *O365 E5 - Exchange only* was designed tooenable only hello *Exchange Online (Plan 2)* service for its members.</span></span>

2. <span data-ttu-id="3d539-183">通知收到 hello 的 E5 將以新的服務-擴充產品的 Microsoft *Microsoft 資料流*。</span><span class="sxs-lookup"><span data-stu-id="3d539-183">You received a notification from Microsoft that hello E5 product will be extended with a new service - *Microsoft Stream*.</span></span> <span data-ttu-id="3d539-184">在您的租用戶可以使用 hello 服務時，您可以執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3d539-184">When hello service becomes available in your tenant, you can do hello following:</span></span>

3. <span data-ttu-id="3d539-185">移 toohello [ **Azure Active Directory > 授權 > 所有產品**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products)刀鋒視窗，然後選取*Office 365 企業版 E5*，然後選取**授權群組** tooview 該產品的所有群組的清單。</span><span class="sxs-lookup"><span data-stu-id="3d539-185">Go toohello [**Azure Active Directory > Licenses > All products**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) blade and select *Office 365 Enterprise E5*, then select **Licensed Groups** tooview a list of all groups with that product.</span></span>

4. <span data-ttu-id="3d539-186">按一下您想 tooreview hello 群組 (在此情況下， *O365 E5-僅適用於 Exchange*)。</span><span class="sxs-lookup"><span data-stu-id="3d539-186">Click on hello group you want tooreview (in this case, *O365 E5 - Exchange only*).</span></span> <span data-ttu-id="3d539-187">這會開啟 hello**授權** 索引標籤。按一下 hello E5 授權會開啟刀鋒視窗中列出所有已啟用的服務。</span><span class="sxs-lookup"><span data-stu-id="3d539-187">This will open hello **Licenses** tab. Clicking on hello E5 license will open a blade listing all enabled services.</span></span>
> [!NOTE]
> <span data-ttu-id="3d539-188">hello *Microsoft 資料流*服務已自動新增並啟用在此群組中，在加法 toohello *Exchange Online*服務：</span><span class="sxs-lookup"><span data-stu-id="3d539-188">hello *Microsoft Stream* service has been automatically added and enabled in this group, in addition toohello *Exchange Online* service:</span></span>

  ![新服務的螢幕擷取畫面加入 tooa 群組授權](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. <span data-ttu-id="3d539-190">如果您想要 toodisable hello 新服務在此群組中的，按一下 hello**開/關**切換 下一步 toohello 服務，然後按一下 hello**儲存**按鈕 tooconfirm hello 變更。</span><span class="sxs-lookup"><span data-stu-id="3d539-190">If you want toodisable hello new service in this group, click hello **On/Off** toggle next toohello service and click hello **Save** button tooconfirm hello change.</span></span> <span data-ttu-id="3d539-191">Azure AD 將會立即處理 hello 群組 tooapply hello 變更; 中的所有使用者新增任何使用者 toohello 群組將沒有 hello *Microsoft 資料流*啟用服務。</span><span class="sxs-lookup"><span data-stu-id="3d539-191">Azure AD will now process all users in hello group tooapply hello change; any new users added toohello group will not have hello *Microsoft Stream* service enabled.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3d539-192">使用者可能仍有某些其他授權指派 （另一個群組的成員，或直接授權指派） 透過啟用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="3d539-192">Users may still have hello service enabled through some other license assignment (another group they are members of or a direct license assignment).</span></span>

6. <span data-ttu-id="3d539-193">如有需要請執行的 hello 指派相同的步驟，使用這項產品的其他群組。</span><span class="sxs-lookup"><span data-stu-id="3d539-193">If needed, perform hello same steps for other groups with this product assigned.</span></span>

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a><span data-ttu-id="3d539-194">使用 PowerShell toosee 繼承權限，並直接授權</span><span class="sxs-lookup"><span data-stu-id="3d539-194">Use PowerShell toosee who has inherited and direct licenses</span></span>
<span data-ttu-id="3d539-195">如果使用者有直接指派或繼承自群組的授權，您可以使用 PowerShell 指令碼 toocheck。</span><span class="sxs-lookup"><span data-stu-id="3d539-195">You can use a PowerShell script toocheck if users have a license assigned directly or inherited from a group.</span></span>

1. <span data-ttu-id="3d539-196">執行 hello `connect-msolservice` cmdlet tooauthenticate 並連接 tooyour 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3d539-196">Run hello `connect-msolservice` cmdlet tooauthenticate and connect tooyour tenant.</span></span>

2. <span data-ttu-id="3d539-197">`Get-MsolAccountSku`可以是使用的 toodiscover hello 租用戶中的所有已佈建的產品授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-197">`Get-MsolAccountSku` can be used toodiscover all provisioned product licenses in hello tenant.</span></span>

  ![Hello Get-msolaccountsku cmdlet 的螢幕擷取畫面](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. <span data-ttu-id="3d539-199">使用 hello *AccountSkuId* hello 的授權，您有興趣使用中的值[這個 PowerShell 指令碼](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group)。</span><span class="sxs-lookup"><span data-stu-id="3d539-199">Use hello *AccountSkuId* value for hello license you are interested in with [this PowerShell script](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group).</span></span> <span data-ttu-id="3d539-200">這會產生具有 hello 資訊 hello 授權如何指派此授權的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="3d539-200">This will produce a list of users who have this license with hello information about how hello license is assigned.</span></span>

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a><span data-ttu-id="3d539-201">使用稽核記錄 toomonitor 群組為基礎的授權活動</span><span class="sxs-lookup"><span data-stu-id="3d539-201">Use Audit logs toomonitor group-based licensing activity</span></span>

<span data-ttu-id="3d539-202">您可以使用[Azure AD 稽核記錄檔](./active-directory-reporting-activity-audit-logs.md#audit-logs)toosee toogroup 授權，包括相關的所有活動：</span><span class="sxs-lookup"><span data-stu-id="3d539-202">You can use [Azure AD audit logs](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee all activity related toogroup-based licensing, including:</span></span>
- <span data-ttu-id="3d539-203">哪些人變更了群組的授權</span><span class="sxs-lookup"><span data-stu-id="3d539-203">who changed licenses on groups</span></span>
- <span data-ttu-id="3d539-204">當 hello 系統已開始處理群組授權變更，以及當它完成</span><span class="sxs-lookup"><span data-stu-id="3d539-204">when hello system started processing a group license change, and when it finished</span></span>
- <span data-ttu-id="3d539-205">哪些授權變更 tooa 使用者群組的授權指派的結果。</span><span class="sxs-lookup"><span data-stu-id="3d539-205">what license changes were made tooa user as a result of a group license assignment.</span></span>

>[!NOTE]
> <span data-ttu-id="3d539-206">在 hello Azure Active Directory 區段的 hello 入口網站中的大部分刀鋒視窗上使用稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3d539-206">Audit logs are available on most blades in hello Azure Active Directory section of hello portal.</span></span> <span data-ttu-id="3d539-207">根據您在其中存取它們，篩選可能會預先套用的 tooonly hello 刀鋒視窗的顯示活動相關 toohello 內容。</span><span class="sxs-lookup"><span data-stu-id="3d539-207">Depending on where you access them, filters may be pre-applied tooonly show activity relevant toohello context of hello blade.</span></span> <span data-ttu-id="3d539-208">如果您沒有看到預期的 hello 結果，請檢查[篩選選項的 hello](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs)或存取進行篩選的 hello 稽核記錄檔下[ **Azure Active Directory > 活動 > 稽核記錄檔**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).</span><span class="sxs-lookup"><span data-stu-id="3d539-208">If you are not seeing hello results you expect, examine [hello filtering options](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) or access hello unfiltered audit logs under [**Azure Active Directory > Activity > Audit logs**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).</span></span>

### <a name="find-out-who-modified-a-group-license"></a><span data-ttu-id="3d539-209">了解哪些人修改了群組授權</span><span class="sxs-lookup"><span data-stu-id="3d539-209">Find out who modified a group license</span></span>

1. <span data-ttu-id="3d539-210">設定 hello**活動**太篩選*組群組授權*按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="3d539-210">Set hello **Activity** filter too*Set group license* and click **Apply**.</span></span>
2. <span data-ttu-id="3d539-211">hello 結果包含授權要設定或修改群組的所有的案例。</span><span class="sxs-lookup"><span data-stu-id="3d539-211">hello results include all cases of licenses being set or modified on groups.</span></span>
>[!TIP]
> <span data-ttu-id="3d539-212">您也可以輸入 hello hello 群組名稱在 hello*目標*篩選 tooscope hello 結果。</span><span class="sxs-lookup"><span data-stu-id="3d539-212">You can also type hello name of hello group in hello *Target* filter tooscope hello results.</span></span>

3. <span data-ttu-id="3d539-213">按一下 hello 清單檢視 toosee hello 詳細資料中的項目，變更的內容。</span><span class="sxs-lookup"><span data-stu-id="3d539-213">Click an item in hello list view toosee hello details of what has changed.</span></span> <span data-ttu-id="3d539-214">在下*Modified 屬性*列出 hello 授權指派的舊的和新值。</span><span class="sxs-lookup"><span data-stu-id="3d539-214">Under *Modified Properties* both old and new values for hello license assignment are listed.</span></span>

<span data-ttu-id="3d539-215">下列範例顯示最近的群組授權變更，並提供詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3d539-215">Here is an example of recent group license changes, with details:</span></span>

![群組授權變更的螢幕擷取畫面](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a><span data-ttu-id="3d539-217">了解群組變更何時開始和完成處理</span><span class="sxs-lookup"><span data-stu-id="3d539-217">Find out when group changes started and finished processing</span></span>

<span data-ttu-id="3d539-218">當授權變更群組時，Azure AD 將會開始套用 hello 變更 tooall 使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-218">When a license changes on a group, Azure AD will start applying hello changes tooall users.</span></span>

1. <span data-ttu-id="3d539-219">群組可讓您開始處理，當 toosee 設定 hello**活動**太篩選*開始套用群組的基礎授權 toousers*。</span><span class="sxs-lookup"><span data-stu-id="3d539-219">toosee when groups started processing, set hello **Activity** filter too*Start applying group based license toousers*.</span></span> <span data-ttu-id="3d539-220">請注意該 hello 執行者 hello 作業*Microsoft Azure AD 以群組為基礎的授權*-系統帳戶，是使用的 tooexecute 所有群組授權變更。</span><span class="sxs-lookup"><span data-stu-id="3d539-220">Note that hello actor for hello operation is *Microsoft Azure AD Group-Based Licensing* - a system account that is used tooexecute all group license changes.</span></span>
>[!TIP]
> <span data-ttu-id="3d539-221">按一下項目在 hello 清單 toosee hello *Modified 屬性*欄位-它會顯示已挑選要處理的 hello 授權變更。</span><span class="sxs-lookup"><span data-stu-id="3d539-221">Click an item in hello list toosee hello *Modified Properties* field - it shows hello license changes that were picked up for processing.</span></span> <span data-ttu-id="3d539-222">如果您進行多個變更 tooa 群組，而且您不確定哪一個已處理，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="3d539-222">This is useful if you made multiple changes tooa group and you are not sure which one was processed.</span></span>

2. <span data-ttu-id="3d539-223">同樣地，toosee 群組完成處理時，使用 hello 篩選值*結束套用群組的基礎授權 toousers*。</span><span class="sxs-lookup"><span data-stu-id="3d539-223">Similarly, toosee when groups finished processing, use hello filter value *Finish applying group based license toousers*.</span></span>
>[!TIP]
> <span data-ttu-id="3d539-224">在此情況下，hello *Modified 屬性*欄位包含 hello 結果的摘要-這是有用的 tooquickly 檢查，如果發生任何錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="3d539-224">In this case, hello *Modified Properties* field contains a summary of hello results - this is useful tooquickly check if processing resulted in any errors.</span></span> <span data-ttu-id="3d539-225">範例輸出：</span><span class="sxs-lookup"><span data-stu-id="3d539-225">Sample output:</span></span>
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. <span data-ttu-id="3d539-226">toosee hello 完成記錄檔以取得如何群組處理的時間、 所有使用者變更，包括設定 hello 下列篩選：</span><span class="sxs-lookup"><span data-stu-id="3d539-226">toosee hello complete log for how a group was processed, including all user changes, set hello following filters:</span></span>
  - <span data-ttu-id="3d539-227">**啟動者 (執行者)**：「Microsoft Azure AD 群組型授權」</span><span class="sxs-lookup"><span data-stu-id="3d539-227">**Initiated By (Actor)**: "Microsoft Azure AD Group-Based Licensing"</span></span>
  - <span data-ttu-id="3d539-228">**日期範圍** (選用)：特定群組開始和完成處理時間的自訂範圍</span><span class="sxs-lookup"><span data-stu-id="3d539-228">**Date Range** (optional): custom range for when you know a specific group started and finished processing</span></span>

<span data-ttu-id="3d539-229">此範例輸出顯示 hello 開始處理，所有產生的使用者變更與 hello 完成的處理。</span><span class="sxs-lookup"><span data-stu-id="3d539-229">This sample output shows hello start of processing, all resulting user changes, and hello finish of processing.</span></span>

![群組授權變更的螢幕擷取畫面](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> <span data-ttu-id="3d539-231">按一下項目相關太*變更使用者的授權*會顯示授權套用變更 tooeach 個別使用者的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3d539-231">Clicking items related too*Change user license* will show details for license changes applied tooeach individual user.</span></span>

## <a name="limitations-and-known-issues"></a><span data-ttu-id="3d539-232">限制與已知問題</span><span class="sxs-lookup"><span data-stu-id="3d539-232">Limitations and known issues</span></span>

<span data-ttu-id="3d539-233">如果您使用以群組為基礎的授權，它是個不錯的主意 toofamiliarize 自己具有 hello 遵循的限制與已知的問題清單。</span><span class="sxs-lookup"><span data-stu-id="3d539-233">If you use group-based licensing, it's a good idea toofamiliarize yourself with hello following list of limitations and known issues.</span></span>

- <span data-ttu-id="3d539-234">群組型授權目前不支援包含其他群組的群組 (巢狀群組)。</span><span class="sxs-lookup"><span data-stu-id="3d539-234">Group-based licensing currently does not support groups that contain other groups (nested groups).</span></span> <span data-ttu-id="3d539-235">如果您套用授權 tooa 巢狀的群組時，只有 hello 使用者立即回應的第一層級群組的成員 hello 擁有 hello 授權套用。</span><span class="sxs-lookup"><span data-stu-id="3d539-235">If you apply a license tooa nested group, only hello immediate first-level user members of hello group have hello licenses applied.</span></span>

- <span data-ttu-id="3d539-236">hello 功能僅使用安全性群組。</span><span class="sxs-lookup"><span data-stu-id="3d539-236">hello feature can only be used with security groups.</span></span> <span data-ttu-id="3d539-237">目前不支援 office 群組，而且您不會無法 toouse hello 授權指派程序中。</span><span class="sxs-lookup"><span data-stu-id="3d539-237">Office groups are currently not supported and you will not be able toouse them in hello license assignment process.</span></span>

- <span data-ttu-id="3d539-238">hello [Office 365 系統管理入口網站](https://portal.office.com )目前不支援以群組為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-238">hello [Office 365 admin portal](https://portal.office.com ) does not currently support group-based licensing.</span></span> <span data-ttu-id="3d539-239">如果使用者會繼承自群組的授權，本授權條款會顯示在 hello Office 管理入口網站中為一般使用者授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-239">If a user inherits a license from a group, this license appears in hello Office admin portal as a regular user license.</span></span> <span data-ttu-id="3d539-240">如果您嘗試的授權，或嘗試 tooremove hello 授權 toomodify，hello 入口網站會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="3d539-240">If you try toomodify that license or try tooremove hello license, hello portal returns an error message.</span></span> <span data-ttu-id="3d539-241">無法直接修改使用者繼承的群組授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-241">Inherited group licenses cannot be modified directly on a user.</span></span>

- <span data-ttu-id="3d539-242">當使用者從群組中移除，並失去 hello 授權時，hello 從該授權 (例如 SharePoint Online) 的服務方案設定 tooa **Suspended**狀態。</span><span class="sxs-lookup"><span data-stu-id="3d539-242">When a user is removed from a group and loses hello license, hello service plans from that license (for example, SharePoint Online) are set tooa **Suspended** state.</span></span> <span data-ttu-id="3d539-243">hello 服務方案未設定 tooa 最終，停用狀態。</span><span class="sxs-lookup"><span data-stu-id="3d539-243">hello service plans are not set tooa final, disabled state.</span></span> <span data-ttu-id="3d539-244">此預防措施可避免系統管理員在群組成員資格管理時犯錯，而意外移除使用者資料。</span><span class="sxs-lookup"><span data-stu-id="3d539-244">This precaution can avoid accidental removal of user data, if an admin makes a mistake in group membership management.</span></span>

- <span data-ttu-id="3d539-245">當指派或修改大型群組 (例如 100,000 個使用者) 的授權時，可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="3d539-245">When licenses are assigned or modified for a large group (for example, 100,000 users), it could impact performance.</span></span> <span data-ttu-id="3d539-246">具體來說，hello 磁碟區的 Azure AD 自動化所產生的變更可能效能產生負面影響 hello 的 Azure AD 之間的目錄同步作業和在內部部署系統。</span><span class="sxs-lookup"><span data-stu-id="3d539-246">Specifically, hello volume of changes generated by Azure AD automation might negatively impact hello performance of your directory synchronization between Azure AD and on-premises systems.</span></span>

- <span data-ttu-id="3d539-247">授權管理自動化不自動反應 tooall hello 環境中的變更類型。</span><span class="sxs-lookup"><span data-stu-id="3d539-247">License management automation does not automatically react tooall types of changes in hello environment.</span></span> <span data-ttu-id="3d539-248">例如，您可能已用盡授權，導致某些使用者 toobe 處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="3d539-248">For example, you might have run out of licenses, causing some users toobe in an error state.</span></span> <span data-ttu-id="3d539-249">總 hello 可用基座計數 toofree，您可以從其他使用者移除部分直接指派的授權。</span><span class="sxs-lookup"><span data-stu-id="3d539-249">toofree up hello available seat count, you can remove some directly assigned licenses from other users.</span></span> <span data-ttu-id="3d539-250">不過，hello 系統不會自動回應 toothis 變更，以及修正該錯誤狀態中的使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-250">However, hello system does not automatically react toothis change and fix users in that error state.</span></span>

  <span data-ttu-id="3d539-251">做為因應措施 toothese 類型的限制，您可以移 toohello**群組**刀鋒視窗，在 Azure AD 中，按一下 **重新處理**。</span><span class="sxs-lookup"><span data-stu-id="3d539-251">As a workaround toothese types of limitations, you can go toohello **Group** blade in Azure AD, and click **Reprocess**.</span></span> <span data-ttu-id="3d539-252">此命令會處理該群組中的所有使用者，並解析 hello 錯誤狀態，如果可能的話。</span><span class="sxs-lookup"><span data-stu-id="3d539-252">This command processes all users in that group and resolves hello error states, if possible.</span></span>

- <span data-ttu-id="3d539-253">群組為基礎的授權不會記錄錯誤時無法指派授權 tooa 使用者因為 tooa 重複 proxy 位址設定 Exchange Online。在授權指派期間略過這類使用者。</span><span class="sxs-lookup"><span data-stu-id="3d539-253">Group-based licensing does not record errors when a license could not be assigned tooa user due tooa duplicate proxy address configuration in Exchange Online; such users are skipped during license assignment.</span></span> <span data-ttu-id="3d539-254">如需有關如何 tooidentify 和解決這個問題，請參閱[本節](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online)。</span><span class="sxs-lookup"><span data-stu-id="3d539-254">For more information about how tooidentify and solve this problem, see [this section](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d539-255">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d539-255">Next steps</span></span>

<span data-ttu-id="3d539-256">toolearn 有關透過群組為基礎授權的授權管理的其他案例的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="3d539-256">toolearn more about other scenarios for license management through group-based licensing, see:</span></span>

* [<span data-ttu-id="3d539-257">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="3d539-257">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="3d539-258">Azure Active Directory 中指派的授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="3d539-258">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="3d539-259">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="3d539-259">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="3d539-260">如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者</span><span class="sxs-lookup"><span data-stu-id="3d539-260">How toomigrate individual licensed users toogroup-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
