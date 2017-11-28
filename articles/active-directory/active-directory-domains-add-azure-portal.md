---
title: "您的自訂網域名稱 tooAzure Active Directory 的 aaaAdd |Microsoft 文件"
description: "如何 tooadd 貴公司的網域名稱 tooAzure Active Directory 中，並 tooverify hello 網域名稱的方式。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a><span data-ttu-id="70968-103">新增自訂網域名稱 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70968-103">Add a custom domain name tooAzure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70968-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="70968-104">Azure portal</span></span>](active-directory-domains-add-azure-portal.md)
> * [<span data-ttu-id="70968-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="70968-105">Azure classic portal</span></span>](active-directory-add-domain.md)
> 

<span data-ttu-id="70968-106">使用 Azure Active Directory (Azure AD)，您可以新增您公司網域名稱 tooAzure AD 以及。</span><span class="sxs-lookup"><span data-stu-id="70968-106">Using Azure Active Directory (Azure AD), you can add your corporate domain name tooAzure AD as well.</span></span> <span data-ttu-id="70968-107">該您的組織使用 toodo 商務和使用者使用公司網域名稱登入，您可能必須是網域名稱。</span><span class="sxs-lookup"><span data-stu-id="70968-107">You might have a domain names that you organization uses toodo business, and users who sign in using your corporate domain name.</span></span> <span data-ttu-id="70968-108">加入 hello 網域名稱 tooAzure AD 可讓您在 hello 目錄 tooassign 使用者名稱，是很熟悉 tooyour 的使用者，例如 'alice@contoso.com。 '</span><span class="sxs-lookup"><span data-stu-id="70968-108">Adding hello domain name tooAzure AD allows you tooassign user names in hello directory that are familiar tooyour users, such as ‘alice@contoso.com.’</span></span> <span data-ttu-id="70968-109">hello 程序很簡單：</span><span class="sxs-lookup"><span data-stu-id="70968-109">hello process is simple:</span></span>

1. <span data-ttu-id="70968-110">新增 hello 自訂網域名稱 tooyour 目錄</span><span class="sxs-lookup"><span data-stu-id="70968-110">Add hello custom domain name tooyour directory</span></span>
2. <span data-ttu-id="70968-111">在 hello 網域名稱註冊機構新增 hello 網域名稱的 DNS 項目</span><span class="sxs-lookup"><span data-stu-id="70968-111">Add a DNS entry for hello domain name at hello domain name registrar</span></span>
3. <span data-ttu-id="70968-112">在 Azure AD 中驗證 hello 自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="70968-112">Verify hello custom domain name in Azure AD</span></span>

## <a name="how-do-i-add-a-domain-name"></a><span data-ttu-id="70968-113">如何新增網域名稱？</span><span class="sxs-lookup"><span data-stu-id="70968-113">How do I add a domain name?</span></span>
1. <span data-ttu-id="70968-114">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="70968-114">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="70968-115">選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="70968-115">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="70968-117">在 hello***目錄名稱***刀鋒視窗中，選取**網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="70968-117">On hello ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="70968-118">在 hello ***目錄名稱*-網域名稱**刀鋒視窗中，選取 hello**新增**命令。</span><span class="sxs-lookup"><span data-stu-id="70968-118">On hello ***directory-name* - Domain names** blade, select hello **Add** command.</span></span>
   
   ![選取 hello Add 命令](./media/active-directory-domains-add-azure-portal/add-command.png)
5. <span data-ttu-id="70968-120">在 hello**網域名稱**刀鋒視窗中，在 hello 方塊中，例如 'contoso.com'，輸入 hello 您的自訂網域名稱，然後選取**新增網域**。</span><span class="sxs-lookup"><span data-stu-id="70968-120">On hello **Domain name** blade, enter hello name of your custom domain in hello box, such as 'contoso.com', and then select **Add Domain**.</span></span> <span data-ttu-id="70968-121">為確定 tooinclude hello.com、.net 或其他最上層的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="70968-121">Be sure tooinclude hello .com, .net, or other top-level extension.</span></span>
6. <span data-ttu-id="70968-122">在 hello ***domainname***刀鋒視窗 （也就是 hello 刀鋒視窗中開啟 hello 標題中具有新的網域名稱），取得 Azure AD 會將您的組織擁有 hello 自訂網域名稱的 tooverify hello DNS 項目資訊。</span><span class="sxs-lookup"><span data-stu-id="70968-122">On hello ***domainname*** blade (that is, hello blade that opens that has your new domain name in hello title), get hello DNS entry information that Azure AD will use tooverify that your organization owns hello custom domain name.</span></span>
   
   ![取得 DNS 項目資訊](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

<span data-ttu-id="70968-124">既然您已經加入 hello 網域名稱，Azure AD 必須確認您的組織擁有 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="70968-124">Now that you've added hello domain name, Azure AD must verify that your organization owns hello domain name.</span></span> <span data-ttu-id="70968-125">Azure AD 執行這項驗證之前，您必須在 hello hello 網域名稱的 DNS 區域檔案中新增 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="70968-125">Before Azure AD can perform this verification, you must add a DNS entry in hello DNS zone file for hello domain name.</span></span> <span data-ttu-id="70968-126">Hello hello 網域名稱的網域名稱註冊機構的網站上執行此工作。</span><span class="sxs-lookup"><span data-stu-id="70968-126">This task is performed at hello website for domain name registrar for hello domain name.</span></span>

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a><span data-ttu-id="70968-127">在 hello hello 網域的網域名稱註冊機構新增 hello DNS 項目</span><span class="sxs-lookup"><span data-stu-id="70968-127">Add hello DNS entry at hello domain name registrar for hello domain</span></span>
<span data-ttu-id="70968-128">hello 您的自訂網域名稱與 Azure AD 下一個步驟 toouse 是 tooupdate hello DNS 區域檔案中的 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="70968-128">hello next step toouse your custom domain name with Azure AD is tooupdate hello DNS zone file for hello domain.</span></span> <span data-ttu-id="70968-129">這可讓 Azure AD tooverify 貴組織擁有 hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="70968-129">This enables Azure AD tooverify that your organization owns hello custom domain name.</span></span>

1. <span data-ttu-id="70968-130">登入 toohello hello 網域的網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="70968-130">Sign in toohello domain name registrar for hello domain.</span></span> <span data-ttu-id="70968-131">如果您沒有存取 tooupdate hello DNS 項目，請要求 hello 個人或團隊具有此存取 toocomplete 步驟 2 和 toolet 您知道它完成時。</span><span class="sxs-lookup"><span data-stu-id="70968-131">If you don't have access tooupdate hello DNS entry, ask hello person or team who has this access toocomplete step 2 and toolet you know when it is completed.</span></span>
2. <span data-ttu-id="70968-132">加入 Azure ad 的 hello DNS 項目提供 tooyou，以更新 hello hello 網域的 DNS 區域檔案。</span><span class="sxs-lookup"><span data-stu-id="70968-132">Update hello DNS zone file for hello domain by adding hello DNS entry provided tooyou by Azure AD.</span></span> <span data-ttu-id="70968-133">這個 DNS 項目可讓 Azure AD tooverify hello 網域您擁有權。</span><span class="sxs-lookup"><span data-stu-id="70968-133">This DNS entry enables Azure AD tooverify your ownership of hello domain.</span></span> <span data-ttu-id="70968-134">hello DNS 項目不會變更任何行為，例如郵件路由或 web 裝載。</span><span class="sxs-lookup"><span data-stu-id="70968-134">hello DNS entry doesn't change any behaviors such as mail routing or web hosting.</span></span>

<span data-ttu-id="70968-135">這個新增的 hello DNS 項目說明，請參閱[指示在常用的 DNS 註冊機構加入 DNS 項目](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)</span><span class="sxs-lookup"><span data-stu-id="70968-135">For help with this adding hello DNS entry, read [Instructions for adding a DNS entry at popular DNS registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)</span></span>

## <a name="verify-hello-domain-name-with-azure-ad"></a><span data-ttu-id="70968-136">驗證 Azure AD 與 hello 網域名稱</span><span class="sxs-lookup"><span data-stu-id="70968-136">Verify hello domain name with Azure AD</span></span>
<span data-ttu-id="70968-137">一旦您加入 hello DNS 項目，您已準備好 tooverify hello 網域名稱與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="70968-137">Once you have added hello DNS entry, you are ready tooverify hello domain name with Azure AD.</span></span>

<span data-ttu-id="70968-138">Hello DNS 記錄都已傳播後，才可以驗證網域名稱。</span><span class="sxs-lookup"><span data-stu-id="70968-138">A domain name can be verified only after hello DNS records have propagated.</span></span> <span data-ttu-id="70968-139">通常此傳播只需要幾秒鐘，但有時可能需要一個小時以上。</span><span class="sxs-lookup"><span data-stu-id="70968-139">This propagation often takes only seconds, but it can sometimes take an hour or more.</span></span> <span data-ttu-id="70968-140">如果驗證無法運作 hello 第一次，再試一次。</span><span class="sxs-lookup"><span data-stu-id="70968-140">If verification doesn’t work hello first time, try again later.</span></span>

1. <span data-ttu-id="70968-141">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="70968-141">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="70968-142">選取**瀏覽**，在 [hello] 文字方塊中，輸入使用者管理，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="70968-142">Select **Browse**, enter User Management in hello text box, and then select **Enter**.</span></span>
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="70968-144">在 hello**使用者管理的網域名稱**刀鋒視窗中，您想 tooverify 選取 hello 未經驗證的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="70968-144">On hello **User management - Domain names** blade, select hello unverified domain name that you want tooverify.</span></span>
4. <span data-ttu-id="70968-145">在 hello ***domainname***刀鋒視窗 （也就是 hello 刀鋒視窗中開啟 hello 標題中具有新的網域名稱），選取**確認**toocomplete hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="70968-145">On hello ***domainname*** blade (that is, hello blade that opens that has your new domain name in hello title), select **Verify** toocomplete hello verification.</span></span>

<span data-ttu-id="70968-146">現在您可以[指派包含自訂網域名稱的使用者名稱](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="70968-146">Now you can [assign user names that include your custom domain name](active-directory-users-create-azure-portal.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="70968-147">疑難排解</span><span class="sxs-lookup"><span data-stu-id="70968-147">Troubleshooting</span></span>
<span data-ttu-id="70968-148">如果您無法驗證自訂網域名稱，請嘗試下列 hello。</span><span class="sxs-lookup"><span data-stu-id="70968-148">If you can't verify a custom domain name, try hello following.</span></span> <span data-ttu-id="70968-149">我們將開始 hello 最常見且向 toohello 最常見工作。</span><span class="sxs-lookup"><span data-stu-id="70968-149">We'll start with hello most common and work down toohello least common.</span></span>

1. <span data-ttu-id="70968-150">**等候一小時**。</span><span class="sxs-lookup"><span data-stu-id="70968-150">**Wait an hour**.</span></span> <span data-ttu-id="70968-151">Azure AD 驗證 hello 網域之前 toopropagate 需要 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="70968-151">DNS records need toopropagate before Azure AD can verify hello domain.</span></span> <span data-ttu-id="70968-152">這可能需要一個小時以上。</span><span class="sxs-lookup"><span data-stu-id="70968-152">This can take an hour or more.</span></span>
2. <span data-ttu-id="70968-153">**確定的 hello 輸入 DNS 記錄，並確認它是否正確**。</span><span class="sxs-lookup"><span data-stu-id="70968-153">**Ensure hello DNS record was entered, and that it is correct**.</span></span> <span data-ttu-id="70968-154">完成此步驟在 hello hello hello 網域的網域名稱註冊機構的網站。</span><span class="sxs-lookup"><span data-stu-id="70968-154">Complete this step at hello website for hello domain name registrar for hello domain.</span></span> <span data-ttu-id="70968-155">Azure AD 無法驗證 hello 網域名稱，如果 hello DNS 項目不存在於 hello DNS 區域檔案，或如果不是完全相符 hello DNS 項目與 Azure AD 提供給您。</span><span class="sxs-lookup"><span data-stu-id="70968-155">Azure AD cannot verify hello domain name if hello DNS entry is not present in hello DNS zone file, or if it is not an exact match with hello DNS entry that Azure AD provided you.</span></span> <span data-ttu-id="70968-156">如果您沒有在 hello 網域名稱註冊機構的 hello 網域存取 tooupdate DNS 記錄，與 hello 人員或小組在您組織內具有此存取權，共用 hello DNS 項目，並要求他們 tooadd hello DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="70968-156">If you do not have access tooupdate DNS records for hello domain at hello domain name registrar, share hello DNS entry with hello person or team at your organization who has this access, and ask them tooadd hello DNS entry.</span></span>
3. <span data-ttu-id="70968-157">**從另一個目錄中刪除 hello 網域名稱，在 Azure AD 中**。</span><span class="sxs-lookup"><span data-stu-id="70968-157">**Delete hello domain name from another directory in Azure AD**.</span></span> <span data-ttu-id="70968-158">網域名稱只能在單一目錄中確認。</span><span class="sxs-lookup"><span data-stu-id="70968-158">A domain name can be verified in only a single directory.</span></span> <span data-ttu-id="70968-159">如果網域名稱先前在另一個目錄中確認過，則必須先在那裡將其刪除後，才可在新的目錄中確認。</span><span class="sxs-lookup"><span data-stu-id="70968-159">If a domain name was previously verified in another directory, it must be deleted there before it can be verified in your new directory.</span></span> <span data-ttu-id="70968-160">刪除網域名稱的相關 toolearn 讀取[管理自訂網域名稱](active-directory-domains-manage-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="70968-160">toolearn about deleting domain names, read [Manage custom domain names](active-directory-domains-manage-azure-portal.md).</span></span>    

## <a name="add-more-custom-domain-names"></a><span data-ttu-id="70968-161">新增更多的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="70968-161">Add more custom domain names</span></span>
<span data-ttu-id="70968-162">如果您的組織使用多個自訂網域名稱，例如 'contoso.com' 和 'contosobank.com'，您可以將其加入 tooa 最大值為 900 的網域名稱註冊。</span><span class="sxs-lookup"><span data-stu-id="70968-162">If your organization uses multiple custom domain names, such as ‘contoso.com’ and ‘contosobank.com’, you can add them up tooa maximum of 900 domain names.</span></span> <span data-ttu-id="70968-163">使用的 hello 這個發行項 tooadd 每個網域名稱中的相同步驟。</span><span class="sxs-lookup"><span data-stu-id="70968-163">Use hello same steps in this article tooadd each of your domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70968-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70968-164">Next steps</span></span>
[<span data-ttu-id="70968-165">管理自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="70968-165">Manage custom domain names</span></span>](active-directory-domains-manage-azure-portal.md)

