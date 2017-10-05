---
title: "將您的自訂網域名稱新增至 Azure Active Directory | Microsoft Docs"
description: "如何在 Azure Active Directory 中新增您公司的網域名稱，以及如何確認網域名稱。"
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
ms.openlocfilehash: ad72f768add7edc1d34a85c27dc2aa1b4e4b3a50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-custom-domain-name-to-azure-active-directory"></a><span data-ttu-id="33395-103">將自訂網域名稱新增至 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33395-103">Add a custom domain name to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33395-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="33395-104">Azure portal</span></span>](active-directory-domains-add-azure-portal.md)
> * [<span data-ttu-id="33395-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="33395-105">Azure classic portal</span></span>](active-directory-add-domain.md)
> 

<span data-ttu-id="33395-106">使用 Azure Active Directory (Azure AD)，您可以將您的公司網域名稱新增到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="33395-106">Using Azure Active Directory (Azure AD), you can add your corporate domain name to Azure AD as well.</span></span> <span data-ttu-id="33395-107">您可能會有貴公司營運所用的網域名稱，以及使用貴公司網域名稱登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="33395-107">You might have a domain names that you organization uses to do business, and users who sign in using your corporate domain name.</span></span> <span data-ttu-id="33395-108">將網域名稱新增到 Azure AD 可讓您在目錄中指派您使用者熟悉的使用者名稱，例如 ‘alice@contoso.com’。</span><span class="sxs-lookup"><span data-stu-id="33395-108">Adding the domain name to Azure AD allows you to assign user names in the directory that are familiar to your users, such as ‘alice@contoso.com.’</span></span> <span data-ttu-id="33395-109">程序佷簡單：</span><span class="sxs-lookup"><span data-stu-id="33395-109">The process is simple:</span></span>

1. <span data-ttu-id="33395-110">在目錄中新增自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="33395-110">Add the custom domain name to your directory</span></span>
2. <span data-ttu-id="33395-111">在網域名稱註冊機構中新增網域名稱的 DNS 項目</span><span class="sxs-lookup"><span data-stu-id="33395-111">Add a DNS entry for the domain name at the domain name registrar</span></span>
3. <span data-ttu-id="33395-112">驗證 Azure AD 中的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="33395-112">Verify the custom domain name in Azure AD</span></span>

## <a name="how-do-i-add-a-domain-name"></a><span data-ttu-id="33395-113">如何新增網域名稱？</span><span class="sxs-lookup"><span data-stu-id="33395-113">How do I add a domain name?</span></span>
1. <span data-ttu-id="33395-114">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="33395-114">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="33395-115">選取 [更多服務]，在文字方塊中輸入 **Azure Active Directory**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="33395-115">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="33395-117">在 [directory-name] 刀鋒視窗上，選取 [網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="33395-117">On the ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="33395-118">在 [*directory-name* - 網域名稱] 刀鋒視窗上，選取 [新增] 命令。</span><span class="sxs-lookup"><span data-stu-id="33395-118">On the ***directory-name* - Domain names** blade, select the **Add** command.</span></span>
   
   ![選取 [新增] 命令](./media/active-directory-domains-add-azure-portal/add-command.png)
5. <span data-ttu-id="33395-120">在 [網域名稱] 刀鋒視窗上，於方塊中輸入您的自訂網域名稱 (例如 'contoso.com')，然後選取 [新增網域]。</span><span class="sxs-lookup"><span data-stu-id="33395-120">On the **Domain name** blade, enter the name of your custom domain in the box, such as 'contoso.com', and then select **Add Domain**.</span></span> <span data-ttu-id="33395-121">請務必包含 .com、.net 或其他最上層的擴充。</span><span class="sxs-lookup"><span data-stu-id="33395-121">Be sure to include the .com, .net, or other top-level extension.</span></span>
6. <span data-ttu-id="33395-122">在 [domainname] 刀鋒視窗 (亦即所開啟且標題中含有新網域名稱的刀鋒視窗) 上，取得 Azure AD 將用來驗證貴組織是否擁有自訂網域名稱的 DNS 項目資訊。</span><span class="sxs-lookup"><span data-stu-id="33395-122">On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), get the DNS entry information that Azure AD will use to verify that your organization owns the custom domain name.</span></span>
   
   ![取得 DNS 項目資訊](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

<span data-ttu-id="33395-124">既然您已新增網域名稱，Azure AD 必須確認您的組織擁有該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-124">Now that you've added the domain name, Azure AD must verify that your organization owns the domain name.</span></span> <span data-ttu-id="33395-125">您必須先在 DNS 區域檔案中新增該網域名稱的 DNS 項目，Azure AD 才可以進行此確認。</span><span class="sxs-lookup"><span data-stu-id="33395-125">Before Azure AD can perform this verification, you must add a DNS entry in the DNS zone file for the domain name.</span></span> <span data-ttu-id="33395-126">這項工作是在該網域名稱的網域名稱註冊機構網站上進行。</span><span class="sxs-lookup"><span data-stu-id="33395-126">This task is performed at the website for domain name registrar for the domain name.</span></span>

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a><span data-ttu-id="33395-127">在網域名稱註冊機構中新增網域的 DNS 項目</span><span class="sxs-lookup"><span data-stu-id="33395-127">Add the DNS entry at the domain name registrar for the domain</span></span>
<span data-ttu-id="33395-128">利用 Azure AD 使用您自訂網域名稱的下一個步驟，就是更新網域的 DNS 區域檔案。</span><span class="sxs-lookup"><span data-stu-id="33395-128">The next step to use your custom domain name with Azure AD is to update the DNS zone file for the domain.</span></span> <span data-ttu-id="33395-129">這可讓 Azure AD 確認您的組織擁有該自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-129">This enables Azure AD to verify that your organization owns the custom domain name.</span></span>

1. <span data-ttu-id="33395-130">登入網域的網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="33395-130">Sign in to the domain name registrar for the domain.</span></span> <span data-ttu-id="33395-131">如果您無法存取以更新 DNS 項目，請要求具有此存取權的人員或小組完成步驟 2 並在完成時通知您。</span><span class="sxs-lookup"><span data-stu-id="33395-131">If you don't have access to update the DNS entry, ask the person or team who has this access to complete step 2 and to let you know when it is completed.</span></span>
2. <span data-ttu-id="33395-132">透過新增 Azure AD 提供給您的 DNS 項目來更新網域的 DNS 區域檔案。</span><span class="sxs-lookup"><span data-stu-id="33395-132">Update the DNS zone file for the domain by adding the DNS entry provided to you by Azure AD.</span></span> <span data-ttu-id="33395-133">此 DNS 項目可讓 Azure AD 確認您擁有網域。</span><span class="sxs-lookup"><span data-stu-id="33395-133">This DNS entry enables Azure AD to verify your ownership of the domain.</span></span> <span data-ttu-id="33395-134">DNS 項目不會變更任何行為，例如郵件路由或 Web 裝載。</span><span class="sxs-lookup"><span data-stu-id="33395-134">The DNS entry doesn't change any behaviors such as mail routing or web hosting.</span></span>

<span data-ttu-id="33395-135">如需新增此 DNS 項目的說明，請參閱 [在常用 DNS 註冊機構新增 DNS 項目的指示](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)</span><span class="sxs-lookup"><span data-stu-id="33395-135">For help with this adding the DNS entry, read [Instructions for adding a DNS entry at popular DNS registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)</span></span>

## <a name="verify-the-domain-name-with-azure-ad"></a><span data-ttu-id="33395-136">使用 Azure AD 確認網域名稱</span><span class="sxs-lookup"><span data-stu-id="33395-136">Verify the domain name with Azure AD</span></span>
<span data-ttu-id="33395-137">一旦新增了 DNS 項目，您就可以使用 Azure AD 確認網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-137">Once you have added the DNS entry, you are ready to verify the domain name with Azure AD.</span></span>

<span data-ttu-id="33395-138">只有在 DNS 記錄傳播完成之後，才能驗證網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-138">A domain name can be verified only after the DNS records have propagated.</span></span> <span data-ttu-id="33395-139">通常此傳播只需要幾秒鐘，但有時可能需要一個小時以上。</span><span class="sxs-lookup"><span data-stu-id="33395-139">This propagation often takes only seconds, but it can sometimes take an hour or more.</span></span> <span data-ttu-id="33395-140">如果驗證第一次不成功，請稍後再試。</span><span class="sxs-lookup"><span data-stu-id="33395-140">If verification doesn’t work the first time, try again later.</span></span>

1. <span data-ttu-id="33395-141">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="33395-141">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="33395-142">選取 [瀏覽]，在文字方塊中輸入「使用者管理」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="33395-142">Select **Browse**, enter User Management in the text box, and then select **Enter**.</span></span>
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="33395-144">在 [使用者管理 - 網域名稱]  刀鋒視窗上，選取您想要驗證的未驗證網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-144">On the **User management - Domain names** blade, select the unverified domain name that you want to verify.</span></span>
4. <span data-ttu-id="33395-145">在 [domainname] 刀鋒視窗 (也就是所開啟且標題中含有新網域名稱的刀鋒視窗) 上，選取 [驗證] 來完成驗證。</span><span class="sxs-lookup"><span data-stu-id="33395-145">On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), select **Verify** to complete the verification.</span></span>

<span data-ttu-id="33395-146">現在您可以[指派包含自訂網域名稱的使用者名稱](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="33395-146">Now you can [assign user names that include your custom domain name](active-directory-users-create-azure-portal.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="33395-147">疑難排解</span><span class="sxs-lookup"><span data-stu-id="33395-147">Troubleshooting</span></span>
<span data-ttu-id="33395-148">如果無法確認自訂網域名稱，請嘗試下列方法。</span><span class="sxs-lookup"><span data-stu-id="33395-148">If you can't verify a custom domain name, try the following.</span></span> <span data-ttu-id="33395-149">我們會從最常見的原因來開始逐一介紹到最不常見的原因。</span><span class="sxs-lookup"><span data-stu-id="33395-149">We'll start with the most common and work down to the least common.</span></span>

1. <span data-ttu-id="33395-150">**等候一小時**。</span><span class="sxs-lookup"><span data-stu-id="33395-150">**Wait an hour**.</span></span> <span data-ttu-id="33395-151">DNS 記錄必須在 Azure AD 確認網域之後傳播。</span><span class="sxs-lookup"><span data-stu-id="33395-151">DNS records need to propagate before Azure AD can verify the domain.</span></span> <span data-ttu-id="33395-152">這可能需要一個小時以上。</span><span class="sxs-lookup"><span data-stu-id="33395-152">This can take an hour or more.</span></span>
2. <span data-ttu-id="33395-153">**確定已輸入正確的 DNS 記錄**。</span><span class="sxs-lookup"><span data-stu-id="33395-153">**Ensure the DNS record was entered, and that it is correct**.</span></span> <span data-ttu-id="33395-154">請在該網域的網域名稱註冊機構網站上完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="33395-154">Complete this step at the website for the domain name registrar for the domain.</span></span> <span data-ttu-id="33395-155">如果 DNS 項目不在 DNS 區域檔案中，或如果與 Azure AD 提供您的 DNS 項目不完全相符，則 Azure AD 無法確認網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-155">Azure AD cannot verify the domain name if the DNS entry is not present in the DNS zone file, or if it is not an exact match with the DNS entry that Azure AD provided you.</span></span> <span data-ttu-id="33395-156">如果您無法在網域名稱註冊機構上存取以更新網域的 DNS 記錄，請與組織內具有此存取權的個人或團隊共用 DNS 項目，並請他們新增 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="33395-156">If you do not have access to update DNS records for the domain at the domain name registrar, share the DNS entry with the person or team at your organization who has this access, and ask them to add the DNS entry.</span></span>
3. <span data-ttu-id="33395-157">**從 Azure AD 中的另一個目錄刪除網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="33395-157">**Delete the domain name from another directory in Azure AD**.</span></span> <span data-ttu-id="33395-158">網域名稱只能在單一目錄中確認。</span><span class="sxs-lookup"><span data-stu-id="33395-158">A domain name can be verified in only a single directory.</span></span> <span data-ttu-id="33395-159">如果網域名稱先前在另一個目錄中確認過，則必須先在那裡將其刪除後，才可在新的目錄中確認。</span><span class="sxs-lookup"><span data-stu-id="33395-159">If a domain name was previously verified in another directory, it must be deleted there before it can be verified in your new directory.</span></span> <span data-ttu-id="33395-160">若要了解如何刪除網域名稱，請參閱 [管理自訂網域名稱](active-directory-domains-manage-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="33395-160">To learn about deleting domain names, read [Manage custom domain names](active-directory-domains-manage-azure-portal.md).</span></span>    

## <a name="add-more-custom-domain-names"></a><span data-ttu-id="33395-161">新增更多的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="33395-161">Add more custom domain names</span></span>
<span data-ttu-id="33395-162">如果您的組織使用多個自訂網域名稱，例如 ‘contoso.com’ 和 ‘contosobank.com’，您最多可以新增 900 個網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-162">If your organization uses multiple custom domain names, such as ‘contoso.com’ and ‘contosobank.com’, you can add them up to a maximum of 900 domain names.</span></span> <span data-ttu-id="33395-163">請使用本文中的相同步驟來新增每個網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33395-163">Use the same steps in this article to add each of your domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33395-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33395-164">Next steps</span></span>
[<span data-ttu-id="33395-165">管理自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="33395-165">Manage custom domain names</span></span>](active-directory-domains-manage-azure-portal.md)

