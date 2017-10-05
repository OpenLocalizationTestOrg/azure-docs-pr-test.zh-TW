---
title: "如何取得 Azure AD 租用戶 | Microsoft Docs"
description: "如何取得 Azure Active Directory 租用戶，以供註冊及建置應用程式使用。"
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: fe33d490b754e2f793f5c7a13dc55ca038b1b71c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-get-an-azure-active-directory-tenant"></a><span data-ttu-id="d3c74-103">如何取得 Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-103">How to get an Azure Active Directory tenant</span></span>
<span data-ttu-id="d3c74-104">在 Azure Active Directory (Azure AD) 中， [租用戶](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) 代表組織。</span><span class="sxs-lookup"><span data-stu-id="d3c74-104">In Azure Active Directory (Azure AD), a [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) is representative of an organization.</span></span>  <span data-ttu-id="d3c74-105">它是組織在註冊 Microsoft 雲端服務 (例如 Azure、Microsoft Intune 或 Office 365) 時所收到和擁有的專屬 Azure AD 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3c74-105">It is a dedicated instance of the Azure AD service that an organization receives and owns when it signs up for a Microsoft cloud service such as Azure, Microsoft Intune, or Office 365.</span></span>  <span data-ttu-id="d3c74-106">每個 Azure AD 租用戶都不同，並與其他 Azure AD 租用戶分開。</span><span class="sxs-lookup"><span data-stu-id="d3c74-106">Each Azure AD tenant is distinct and separate from other Azure AD tenants.</span></span>  

<span data-ttu-id="d3c74-107">租用戶可裝載公司中的使用者及其相關資訊 (密碼、使用者設定檔資料、權限等)。</span><span class="sxs-lookup"><span data-stu-id="d3c74-107">A tenant houses the users in a company and the information about them - their passwords, user profile data, permissions, and so on.</span></span>  <span data-ttu-id="d3c74-108">它還包含群組、應用程式和關於組織及其安全性的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d3c74-108">It also contains groups, applications, and other information pertaining to an organization and its security.</span></span>

<span data-ttu-id="d3c74-109">若要允許 Azure AD 使用者登入您的應用程式，您必須在您自己的租用戶中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3c74-109">To allow Azure AD users to sign in to your application, you must register your application in a tenant of your own.</span></span>  <span data-ttu-id="d3c74-110">在 Azure AD 租用戶中發佈應用程式 **完全免費**。</span><span class="sxs-lookup"><span data-stu-id="d3c74-110">Publishing an application in an Azure AD tenant is **absolutely free**.</span></span>  <span data-ttu-id="d3c74-111">事實上，大部分的開發人員會建立數個租用戶和應用程式，以供實驗、開發、預備和測試等用途使用。</span><span class="sxs-lookup"><span data-stu-id="d3c74-111">In fact, most developers will create several tenants and applications for experimentation, development, staging and testing purposes.</span></span>  <span data-ttu-id="d3c74-112">如果註冊和使用應用程式的組織想要充分利用進階的目錄功能，他們可以選擇購買授權。</span><span class="sxs-lookup"><span data-stu-id="d3c74-112">Organizations that sign up for and consume your application can optionally choose to purchase licenses if they wish to take advantage of advanced directory features.</span></span>

<span data-ttu-id="d3c74-113">因此，要如何取得 Azure AD 租用戶？</span><span class="sxs-lookup"><span data-stu-id="d3c74-113">So, how do you go about getting an Azure AD tenant?</span></span>  <span data-ttu-id="d3c74-114">此程序可能會有小小的不同，如果您：</span><span class="sxs-lookup"><span data-stu-id="d3c74-114">The process might be a little different if you:</span></span>

* [<span data-ttu-id="d3c74-115">具有現有的 Office 365 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-115">Have an existing Office 365 subscription</span></span>](#use-an-existing-office-365-subscription)
* [<span data-ttu-id="d3c74-116">具有與 Microsoft 帳戶相關聯的現有 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-116">Have an existing Azure subscription associated with a Microsoft Account</span></span>](#use-an-msa-azure-subscription)
* [<span data-ttu-id="d3c74-117">具有與組織帳戶相關聯的現有 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-117">Have an existing Azure subscription associated with an organizational account</span></span>](#use-an-organizational-azure-subscription)
* [<span data-ttu-id="d3c74-118">以上皆無並想要從頭開始</span><span class="sxs-lookup"><span data-stu-id="d3c74-118">Have none of the above & want to start from scratch</span></span>](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a><span data-ttu-id="d3c74-119">使用現有的 Office 365 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-119">Use an existing Office 365 subscription</span></span>
<span data-ttu-id="d3c74-120">如果您擁有現有的 Office 365 訂用帳戶，就已擁有 Azure AD 租用戶！</span><span class="sxs-lookup"><span data-stu-id="d3c74-120">If you have an existing Office 365 subscription, you already have an Azure AD tenant!</span></span> <span data-ttu-id="d3c74-121">您可以使用您的 O365 帳戶登入 [Azure 入口網站](https://portal.azure.com)並開始使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d3c74-121">You can sign in to the [Azure portal](https://portal.azure.com) with your O365 account and start using Azure AD.</span></span>

## <a name="use-an-msa-azure-subscription"></a><span data-ttu-id="d3c74-122">使用 MSA Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-122">Use an MSA Azure subscription</span></span>
<span data-ttu-id="d3c74-123">如果您先前已使用個別的 Microsoft 帳戶註冊 Azure 訂用帳戶，則您已經有一個租用戶！</span><span class="sxs-lookup"><span data-stu-id="d3c74-123">If you have previously signed up for an Azure subscription with your individual Microsoft Account, you already have a tenant!</span></span>  <span data-ttu-id="d3c74-124">當您登入 [Azure 入口網站](https://portal.azure.com)時，會自動登入您的預設租用戶。</span><span class="sxs-lookup"><span data-stu-id="d3c74-124">When you log in to the [Azure Portal](https://portal.azure.com), you will automatically be logged in to your default tenant.</span></span> <span data-ttu-id="d3c74-125">您可以視需要任意使用此租用戶，但您可能會想要建立組織系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3c74-125">You are free to use this tenant as you see fit - but you may want to create an Organizational administrator account.</span></span>

<span data-ttu-id="d3c74-126">若要這樣做，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d3c74-126">To do so, follow these steps.</span></span>  <span data-ttu-id="d3c74-127">或者，您可能會想要建立新的租用戶，並按照類似的程序在該租用戶中建立系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d3c74-127">Alternatively, you may wish to create a new tenant and create an administrator in that tenant following a similar process.</span></span>

1. <span data-ttu-id="d3c74-128">使用您的個別帳戶登入 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d3c74-128">Log into the [Azure Portal](https://portal.azure.com) with your individual account</span></span>
2. <span data-ttu-id="d3c74-129">瀏覽至入口網站的 [Azure Active Directory] 區段 (您可在左側瀏覽列的**更多服務**下找到)</span><span class="sxs-lookup"><span data-stu-id="d3c74-129">Navigate to the “Azure Active Directory” section of the portal (found in the left nav bar, under **More Services**)</span></span>
3. <span data-ttu-id="d3c74-130">您應該會自動登入「預設目錄」，如果未自動登入，您可以按一下右上角的帳戶名稱切換目錄。</span><span class="sxs-lookup"><span data-stu-id="d3c74-130">You should automatically be signed in to the "Default Directory", if not you can switch directories by clicking on your account name in the top right corner.</span></span>
4. <span data-ttu-id="d3c74-131">從 [快速工作] 區段中，選擇 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="d3c74-131">From the **Quick Tasks** section, choose **Add a user**.</span></span>
5. <span data-ttu-id="d3c74-132">在 [新增使用者表單] 中，請提供下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d3c74-132">In the Add User Form, provide the following details:</span></span>

   * <span data-ttu-id="d3c74-133">名稱：(選擇適當的值)</span><span class="sxs-lookup"><span data-stu-id="d3c74-133">Name: (choose an appropriate value)</span></span>
   * <span data-ttu-id="d3c74-134">使用者名稱：(為此系統管理員選擇一個使用者名稱)</span><span class="sxs-lookup"><span data-stu-id="d3c74-134">User name: (choose a user name for this administrator)</span></span>
   * <span data-ttu-id="d3c74-135">設定檔：(在名字、姓氏、職稱和部門中填入適當的值)</span><span class="sxs-lookup"><span data-stu-id="d3c74-135">Profile: (fill in the appropriate values for First name, Last name, Job title and Department)</span></span>
   * <span data-ttu-id="d3c74-136">角色：全域系統管理員</span><span class="sxs-lookup"><span data-stu-id="d3c74-136">Role: Global Administrator</span></span>
6. <span data-ttu-id="d3c74-137">當您完成新增使用者表單，並收到新系統管理使用者的暫時密碼時，請務必記錄此密碼，因為您必須以此新使用者身分登入，才能變更密碼。</span><span class="sxs-lookup"><span data-stu-id="d3c74-137">When you have completed the Add User Form, and receive the temporary password for the new administrative user, be sure to record this password as you will need to login with this new user in order to change the password.</span></span> <span data-ttu-id="d3c74-138">您也可以使用替代電子郵件，直接將密碼傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="d3c74-138">You can also send the password directly to the user, using an alternative e-mail.</span></span>
7. <span data-ttu-id="d3c74-139">按一下 [建立] 來建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d3c74-139">Click on **Create** to create the new user.</span></span>
8. <span data-ttu-id="d3c74-140">若要變更暫時密碼，請使用這個新使用者帳戶登入 [https://login.microsoftonline.com](https://login.microsoftonline.com)變更密碼。</span><span class="sxs-lookup"><span data-stu-id="d3c74-140">To change the temporary password, log into [https://login.microsoftonline.com](https://login.microsoftonline.com) with this new user account and change the password when requested.</span></span>

## <a name="use-an-organizational-azure-subscription"></a><span data-ttu-id="d3c74-141">使用組織的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3c74-141">Use an organizational Azure subscription</span></span>
<span data-ttu-id="d3c74-142">如果您先前已使用組織帳戶註冊 Azure 訂用帳戶，則您已經有一個租用戶！</span><span class="sxs-lookup"><span data-stu-id="d3c74-142">If you have previously signed up for an Azure subscription with your organizational account, you already have a tenant!</span></span>  <span data-ttu-id="d3c74-143">在 [Azure 入口網站](https://portal.azure.com)中，當您瀏覽至 [更多服務] 和 [Azure Active Directory] 時應該會找到租用戶。</span><span class="sxs-lookup"><span data-stu-id="d3c74-143">In the [Azure Portal](https://portal.azure.com), you should find a tenant when you navigate to "More Services" and "Azure Active Directory."</span></span>  <span data-ttu-id="d3c74-144">您可以視需要任意使用此租用戶。</span><span class="sxs-lookup"><span data-stu-id="d3c74-144">You are free to use this tenant as you see fit.</span></span>

## <a name="start-from-scratch"></a><span data-ttu-id="d3c74-145">從頭開始</span><span class="sxs-lookup"><span data-stu-id="d3c74-145">Start from scratch</span></span>
<span data-ttu-id="d3c74-146">如果上述對您沒有太大的意義，別擔心。</span><span class="sxs-lookup"><span data-stu-id="d3c74-146">If all of the above is gibberish to you, don't worry.</span></span>  <span data-ttu-id="d3c74-147">您只需造訪 [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) ，並以新的組織身分註冊 Azure。</span><span class="sxs-lookup"><span data-stu-id="d3c74-147">Simply visit [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) to sign up for Azure with a new organization.</span></span>  <span data-ttu-id="d3c74-148">完成此程序時，您將會有自己專屬的 Azure AD 租用戶，並且它會有您在註冊時選擇的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d3c74-148">Once you've completed the process, you will have your very own Azure AD tenant with the domain name you chose during sign up.</span></span>  <span data-ttu-id="d3c74-149">在 [Azure 入口網站](https://portal.azure.com)中，您可以透過瀏覽至左側導覽中的 [Azure Active Directory] 找到租用戶。</span><span class="sxs-lookup"><span data-stu-id="d3c74-149">In the [Azure Portal](https://portal.azure.com), you can find your tenant by navigating to "Azure Active Directory" in the left hand nav.</span></span>

<span data-ttu-id="d3c74-150">註冊 Azure 的過程中，您將需要提供信用卡的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d3c74-150">As part of the process of signing up for Azure, you will be required to provide credit card details.</span></span>  <span data-ttu-id="d3c74-151">您可以放心繼續執行，您將不會被收取在 Azure AD 中發佈應用程式或建立新租用戶的費用。</span><span class="sxs-lookup"><span data-stu-id="d3c74-151">You can proceed with confidence - you will not be charged for publishing applications in Azure AD or creating new tenants.</span></span>
