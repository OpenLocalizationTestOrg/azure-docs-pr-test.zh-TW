---
title: "Azure Active Directory 中的 aaaLicense 使用者 |Microsoft 文件"
description: "深入了解如何 toolicense 自己和您在 Azure Active Directory 中的使用者。"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a><span data-ttu-id="3ca0a-103">快速入門：在 Azure Active Directory 中授權使用者</span><span class="sxs-lookup"><span data-stu-id="3ca0a-103">Quickstart: License users in Azure Active Directory</span></span>
<span data-ttu-id="3ca0a-104">以授權為基礎的 Azure AD 服務的運作方式，是在您的 Azure 租用戶中啟用 Azure Active Directory (Azure AD) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-104">License-based Azure AD services work by activating an Azure Active Directory (Azure AD) subscription in your Azure tenant.</span></span> <span data-ttu-id="3ca0a-105">Hello 訂閱在作用中之後，會由 Azure AD 系統管理員管理服務功能，而且所授權的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-105">After hello subscription is active, service capabilities are managed by Azure AD administrators and used by licensed users.</span></span> <span data-ttu-id="3ca0a-106">當您購買企業行動力 + 安全性、 Azure AD Premium 或 Azure AD Basic，您的租用戶時，會更新與 hello 訂用帳戶，包括其有效期間內，而且預付授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-106">When you purchase Enterprise Mobility + Security, Azure AD Premium, or Azure AD Basic, your tenant is updated with hello subscription, including its validity period and prepaid licenses.</span></span> <span data-ttu-id="3ca0a-107">您的訂用帳戶資訊，包括 hello 分派或可用授權數目是透過 hello Azure 入口網站下**Azure Active Directory**所開啟的 hello**授權**磚。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-107">Your subscription information, including hello number of assigned or available licenses, is available through hello Azure portal under **Azure Active Directory** by opening hello **Licenses** tile.</span></span> <span data-ttu-id="3ca0a-108">hello**授權**刀鋒視窗是也 hello 最佳地方 toomanage 授權指派。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-108">hello **Licenses** blade is also hello best place toomanage your license assignments.</span></span>

<span data-ttu-id="3ca0a-109">取得訂用帳戶是所有您需要付費功能 tooconfigure，雖然您仍需指派使用者授權的付費 Azure AD 的付費功能。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-109">Although obtaining a subscription is all you need tooconfigure paid capabilities, you must still assign user licenses for paid Azure AD paid features.</span></span> <span data-ttu-id="3ca0a-110">應存取 Azure AD 付費功能或者透過 Azure AD 付費功能管理的人員，都必須獲得授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-110">Any user who should have access to, or who is managed through, an Azure AD paid feature must be assigned a license.</span></span> <span data-ttu-id="3ca0a-111">授權指派是一種使用者與購買的服務 (例如 Azure AD Premium、Basic 或 Enterprise Mobility + Security) 之間的對應。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-111">License assignment is a mapping between a user and a purchased service, such as Azure AD Premium, Basic, or Enterprise Mobility + Security.</span></span>

<span data-ttu-id="3ca0a-112">您可以使用[群組為基礎的授權指派](active-directory-licensing-whatis-azure-portal.md)tooset hello 如下的規則：</span><span class="sxs-lookup"><span data-stu-id="3ca0a-112">You can use [group-based license assignment](active-directory-licensing-whatis-azure-portal.md) tooset up rules such as hello following:</span></span>
* <span data-ttu-id="3ca0a-113">目錄中的所有使用者都自動取得授權</span><span class="sxs-lookup"><span data-stu-id="3ca0a-113">All users in your directory automatically get a license</span></span>
* <span data-ttu-id="3ca0a-114">Everyone 具有 hello 適當職稱取得授權</span><span class="sxs-lookup"><span data-stu-id="3ca0a-114">Everyone with hello appropriate job title gets a license</span></span>
* <span data-ttu-id="3ca0a-115">您可以將委派 hello 組織中的 hello 決策 tooother 管理員 (使用[自助群組](active-directory-accessmanagement-self-service-group-management.md))</span><span class="sxs-lookup"><span data-stu-id="3ca0a-115">You can delegate hello decision tooother managers in hello organization (by using [self-service groups](active-directory-accessmanagement-self-service-group-management.md))</span></span>

> [!TIP]
> <span data-ttu-id="3ca0a-116">如需授權指派 toogroups 詳細討論，包括進階的案例和 Office 365 授權的情況下，請參閱[指派授權 Azure Active Directory 中的群組成員資格 toousers](active-directory-licensing-group-assignment-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-116">For a detailed discussion of license assignment toogroups, including advanced scenarios and Office 365 licensing scenarios, see [Assign licenses toousers by group membership in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

## <a name="assign-licenses-toousers-and-groups"></a><span data-ttu-id="3ca0a-117">指派授權 toousers 和群組</span><span class="sxs-lookup"><span data-stu-id="3ca0a-117">Assign licenses toousers and groups</span></span>
<span data-ttu-id="3ca0a-118">使用有效的訂用帳戶，應該先指派授權 tooyourself 並重新整理您的瀏覽器 tooensure，您會看到所有包含的 hello 預期功能與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-118">Using an active subscription, you should first assign a license tooyourself and refresh your browser tooensure that you see all of hello expected features included with your subscription.</span></span> <span data-ttu-id="3ca0a-119">hello 下一個步驟是 tooassign 授權 toohello 使用者需要存取 toopaid Azure AD 功能。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-119">hello next step is tooassign licenses toohello users who need access toopaid Azure AD features.</span></span> <span data-ttu-id="3ca0a-120">輕鬆 tooassign 授權是使用者，而非 tooindividuals tooassign 授權 toogroups。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-120">An easy way tooassign licenses is tooassign licenses toogroups of users rather than tooindividuals.</span></span> <span data-ttu-id="3ca0a-121">當您指派授權 tooa 群組時，所有群組成員已都獲得授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-121">When you assign licenses tooa group, all group members are assigned a license.</span></span> <span data-ttu-id="3ca0a-122">加入或從 hello 群組中移除使用者時，會自動會指派或移除 hello 適當授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-122">If users are added or removed from hello group, hello appropriate license is automatically assigned or removed.</span></span> 

> [!NOTE]
> <span data-ttu-id="3ca0a-123">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-123">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="3ca0a-124">Hello 管理員 tooa 使用者可以指派授權之前，必須指定 hello**使用位置**hello 使用者的屬性。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-124">Before a license can be assigned tooa user, hello administrator must specify hello **Usage location** property for hello user.</span></span> <span data-ttu-id="3ca0a-125">您可以設定此屬性在**使用者** &gt; **設定檔** &gt; **設定**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-125">You can set this property under **User** &gt; **Profile** &gt; **Settings** in hello Azure portal.</span></span> <span data-ttu-id="3ca0a-126">當使用群組授權指派，其使用位置未指定任何使用者會繼承 hello hello 目錄位置。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-126">When using group license assignment, any user whose usage location is not specified inherits hello location of hello directory.</span></span>

<span data-ttu-id="3ca0a-127">tooassign 授權下**Azure Active Directory** &gt; **授權** &gt; **所有產品**，選取一或多個產品，然後選取**指派**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-127">tooassign a license, under **Azure Active Directory** &gt; **Licenses** &gt; **All Products**, select one or more products, and then select **Assign** on hello command bar.</span></span>

![選取授權 tooassign](media/license-users-groups/select-license-to-assign.png)

<span data-ttu-id="3ca0a-129">您可以使用 hello**使用者和群組**刀鋒視窗 toochoose hello 產品中的多個使用者或群組或 toodisable 服務計劃。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-129">You can use hello **Users and groups** blade toochoose multiple users or groups or toodisable service plans in hello product.</span></span> <span data-ttu-id="3ca0a-130">使用上最上層 toosearch hello [搜尋] 方塊，使用者和群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-130">Use hello search box on top toosearch for user and group names.</span></span>

![選取要指派授權的使用者或群組](media/license-users-groups/select-user-for-license-assignment.png)

<span data-ttu-id="3ca0a-132">當您指派授權 tooa 群組時，可能需要一些時間才所有使用者都會都繼承 hello 授權 hello 群組 hello 大小而定。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-132">When you assign licenses tooa group, it can take some time before all users inherit hello license depending on hello size of hello group.</span></span> <span data-ttu-id="3ca0a-133">您可以檢查處理狀態 hello hello**群組**刀鋒視窗中的，在 hello**授權**磚。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-133">You can check hello processing status on hello **Group** blade, under hello **Licenses** tile.</span></span>

![授權指派狀態](media/license-users-groups/license-assignment-status.png)

<span data-ttu-id="3ca0a-135">在 Azure AD 授權指派期間，可能會發生指派錯誤，但在管理 Azure AD 和 Enterprise Mobility + Security 產品時則相對較少發生。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-135">Assignment errors can occur during Azure AD license assignment but are relatively rare when managing Azure AD and Enterprise Mobility + Security products.</span></span> <span data-ttu-id="3ca0a-136">可能發生的指派錯誤僅限於：</span><span class="sxs-lookup"><span data-stu-id="3ca0a-136">Potential assignment errors are limited to:</span></span>
- <span data-ttu-id="3ca0a-137">指派衝突： 在使用者先前已指派與 hello 目前的授權不相容的授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-137">Assignment conflict: When a user was previously assigned a license that is incompatible with hello current license.</span></span> <span data-ttu-id="3ca0a-138">在此情況下，hello 新授權指派，需要移除目前 hello。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-138">In this case, assigning hello new license requires removing hello current one.</span></span>
- <span data-ttu-id="3ca0a-139">超過可用的授權： hello 分派群組中的使用者數目超過 hello 可用的授權，使用者的指派狀態會反映失敗 tooassign toomissing 授權到期。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-139">Exceeded available licenses: When hello number of users in assigned groups exceeds hello available licenses, a user's assignment status reflects a failure tooassign due toomissing licenses.</span></span>

### <a name="azure-ad-b2b-collaboration-licensing"></a><span data-ttu-id="3ca0a-140">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="3ca0a-140">Azure AD B2B collaboration licensing</span></span>

<span data-ttu-id="3ca0a-141">B2B 共同作業可讓您 tooinvite guest 使用者到 Azure AD 租用戶 tooprovide 存取 tooAzure AD 服務和您將提供任何 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-141">B2B collaboration allows you tooinvite guest users into your Azure AD tenant tooprovide access tooAzure AD services and any Azure resources you make available.</span></span>  

<span data-ttu-id="3ca0a-142">沒有邀請 B2B 使用者並指派它們 tooan 在 Azure AD 中的應用程式需付費。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-142">There is no charge for inviting B2B users and assigning them tooan application in Azure AD.</span></span> <span data-ttu-id="3ca0a-143">針對每個來賓 too10 應用程式設定使用者和 3 的基本報告也是 B2B 共同作業的使用者可以免費。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-143">Up too10 apps per guest user and 3 basic reports are also free for B2B collaboration users.</span></span> <span data-ttu-id="3ca0a-144">如果 guest 使用者有任何適當的授權指派 hello 夥伴的 Azure AD 租用戶中，它們將會用您以及授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-144">If your guest user has any appropriate licenses assigned in hello partner's Azure AD tenant, they'll be licensed in yours as well.</span></span>

<span data-ttu-id="3ca0a-145">它不是必要，但如果您想 tooprovide 存取 toopaid Azure AD 功能，這些 B2B 來賓使用者必須獲得授權與適當的 Azure AD 授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-145">It's not required, but if you want tooprovide access toopaid Azure AD features, those B2B guest users must be licensed with appropriate Azure AD licenses.</span></span> <span data-ttu-id="3ca0a-146">邀請其他租用戶與 Azure AD 的付費授權可以指派 B2B 共同作業的使用者權限受邀 tooan 額外的五個來賓使用者 toohello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-146">An inviting tenant with an Azure AD paid license can assign B2B collaboration user rights tooan additional five guest users invited toohello tenant.</span></span> <span data-ttu-id="3ca0a-147">如需這方面的案例和資訊，請參閱 [B2B 共同作業授權指引](active-directory-b2b-licensing.md)。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-147">For scenarios and information, see [B2B collaboration licensing guidance](active-directory-b2b-licensing.md).</span></span>

## <a name="view-assigned-licenses"></a><span data-ttu-id="3ca0a-148">檢視已指派的授權</span><span class="sxs-lookup"><span data-stu-id="3ca0a-148">View assigned licenses</span></span>

<span data-ttu-id="3ca0a-149">已指派授權和可用授權的摘要檢視會顯示在 [Azure Active Directory] &gt; [授權] &gt; [所有產品] 下。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-149">A summary view of assigned and available licenses is displayed under **Azure Active Directory** &gt; **Licenses** &gt; **All products**.</span></span>

![檢視授權摘要](media/license-users-groups/view-license-summary.png)

<span data-ttu-id="3ca0a-151">選取特定產品時，會顯示可用的已指派使用者和群組的詳細清單。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-151">A detailed list of assigned users and groups is available when selecting a specific product.</span></span> <span data-ttu-id="3ca0a-152">hello**授權使用者**清單會顯示目前耗用一個授權和是否 hello 授權已直接指派 toohello 使用者，或如果它繼承自群組的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-152">hello **Licensed Users** list shows all users currently consuming a license and whether hello license was assigned directly toohello user or if it is inherited from a group.</span></span>

![檢視授權詳細資料](media/license-users-groups/view-license-detail.png)

<span data-ttu-id="3ca0a-154">同樣地，hello**授權群組**清單會顯示所有群組已指派給 toowhich 授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-154">Similarly, hello **Licensed Groups** list shows all groups toowhich licenses have been assigned.</span></span> <span data-ttu-id="3ca0a-155">選取使用者或群組的 tooopen hello**授權**刀鋒視窗中，會顯示所有授權指派給 toothat 物件。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-155">Select a user or group tooopen hello **Licenses** blade, which shows all licenses assigned toothat object.</span></span>

## <a name="remove-a-license"></a><span data-ttu-id="3ca0a-156">移除授權</span><span class="sxs-lookup"><span data-stu-id="3ca0a-156">Remove a license</span></span>

<span data-ttu-id="3ca0a-157">tooremove 授權，請移 toohello 使用者或群組，並開啟 hello**授權**磚。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-157">tooremove a license, go toohello user or group, and open hello **Licenses** tile.</span></span> <span data-ttu-id="3ca0a-158">選取 hello 授權，然後按一下 **移除**。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-158">Select hello license, and click **Remove**.</span></span>

![移除授權](media/license-users-groups/remove-license.png)

<span data-ttu-id="3ca0a-160">無法直接移除繼承自群組的 hello 使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-160">Licenses inherited by hello user from a group cannot be removed directly.</span></span> <span data-ttu-id="3ca0a-161">相反地，移除 hello 使用者從他們從中繼承 hello 授權 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-161">Instead, remove hello user from hello group from which they are inheriting hello license.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ca0a-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ca0a-162">Next steps</span></span>
<span data-ttu-id="3ca0a-163">本快速入門中，您學到如何 tooassign 授權 toousers 和 Azure AD 目錄中的群組。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-163">In this quickstart, you’ve learned how tooassign licenses toousers and groups in Azure AD directory.</span></span> 

<span data-ttu-id="3ca0a-164">您可以使用 hello hello Azure 入口網站中的下列 Azure AD 中的連結 tooconfigure 訂用帳戶授權指派。</span><span class="sxs-lookup"><span data-stu-id="3ca0a-164">You can use hello following link tooconfigure subscription license assignments in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ca0a-165">指派 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="3ca0a-165">Assign Azure AD licenses</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 