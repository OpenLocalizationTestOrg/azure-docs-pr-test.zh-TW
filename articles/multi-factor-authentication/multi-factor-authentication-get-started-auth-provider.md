---
title: "開始使用 Azure Multi-Factor Auth Provider | Microsoft Docs"
description: "了解如何建立 Azure Multi-Factor Auth Provider。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: ed14a5a762bab20a1ccde699504dd21f25009b52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="86fc4-103">開始使用 Azure Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="86fc4-103">Getting started with an Azure Multi-Factor Auth Provider</span></span>
<span data-ttu-id="86fc4-104">依預設，擁有 Azure Active Directory 和 Office 365 使用者的全域管理員可以使用雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="86fc4-104">Two-step verification is available by default for global administrators who have Azure Active Directory, and Office 365 users.</span></span> <span data-ttu-id="86fc4-105">不過，如果您想要充分利用[進階功能](multi-factor-authentication-whats-next.md)，則應該購買完整版的 Azure Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="86fc4-105">However, if you wish to take advantage of [advanced features](multi-factor-authentication-whats-next.md) then you should purchase the full version of Azure Multi-Factor Authentication (MFA).</span></span>

<span data-ttu-id="86fc4-106">Azure Multi-Factor Auth Provider 可用來充分利用完整版 Azure MFA 所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="86fc4-106">An Azure Multi-Factor Auth Provider is used to take advantage of features provided by the full version of Azure MFA.</span></span> <span data-ttu-id="86fc4-107">它的適用對象是**未透過 Azure MFA、Azure AD Premium 或 Enterprise Mobility + Security (EMS) 取得授權**的使用者。</span><span class="sxs-lookup"><span data-stu-id="86fc4-107">It is for users who **do not have licenses through Azure MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS)**.</span></span>  <span data-ttu-id="86fc4-108">Azure MFA、Azure AD Premium 和 EMS 預設會包含完整版 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="86fc4-108">Azure MFA, Azure AD Premium, and EMS include the full version of Azure MFA by default.</span></span> <span data-ttu-id="86fc4-109">如果您有授權，則不需要 Azure Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="86fc4-109">If you have licenses, then you do not need an Azure Multi-Factor Auth Provider.</span></span>

<span data-ttu-id="86fc4-110">下載 SDK 需要 Azure Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="86fc4-110">An Azure Multi-Factor Auth provider is required to download the SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86fc4-111">若要下載 SDK，即使您有 Azure MFA、AAD Premium 或 EMS 授權，還是需要建立 Azure 多因素驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="86fc4-111">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span>  <span data-ttu-id="86fc4-112">如果您針對此用途建立 Azure Multi-Factor Auth Provider，且已有授權，請務必使用**每個啟用的使用者**模型建立提供者。</span><span class="sxs-lookup"><span data-stu-id="86fc4-112">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, be sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="86fc4-113">然後，將提供者連結至包含 Azure MFA、Azure AD Premium 或 EMS 授權的目錄。</span><span class="sxs-lookup"><span data-stu-id="86fc4-113">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="86fc4-114">這個組態可確保您只會在執行雙步驟驗證的唯一使用者超過您所擁有的授權數目時收到帳單。</span><span class="sxs-lookup"><span data-stu-id="86fc4-114">This configuration ensures that you are only billed if you have more unique users performing two-step verification than the number of licenses you own.</span></span>

## <a name="what-is-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="86fc4-115">什麼是 Azure Multi-Factor Auth Provider？</span><span class="sxs-lookup"><span data-stu-id="86fc4-115">What is an Azure Multi-Factor Auth Provider?</span></span>

<span data-ttu-id="86fc4-116">如果您沒有 Azure Multi-factor Authentication 的授權，可以建立驗證提供者，為您的使用者要求雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="86fc4-116">If you don't have licenses for Azure Multi-Factor Authentication, you can create an auth provider to require two-step verification for your users.</span></span> <span data-ttu-id="86fc4-117">如果您要開發自訂應用程式，而且想要啟用 Azure MFA，請建立驗證提供者並[下載 SDK](multi-factor-authentication-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="86fc4-117">If you are developing a custom app and want to enable Azure MFA, create an auth provider and [download the SDK](multi-factor-authentication-sdk.md).</span></span>

<span data-ttu-id="86fc4-118">驗證提供者的類型有兩種，差異在於您 Azure 訂用帳戶的收費方式。</span><span class="sxs-lookup"><span data-stu-id="86fc4-118">There are two types of auth providers, and the distinction is around how your Azure subscription is charged.</span></span> <span data-ttu-id="86fc4-119">每次驗證選項會計算一個月中對您的租用戶執行之驗證數目。</span><span class="sxs-lookup"><span data-stu-id="86fc4-119">The per-authentication option calculates the number of authentications performed against your tenant in a month.</span></span> <span data-ttu-id="86fc4-120">如果您有許多使用者偶爾才會進行驗證，像是如果您要求 MFA 進行自訂應用程式，最好使用此選項。</span><span class="sxs-lookup"><span data-stu-id="86fc4-120">This option is best if you have a number of users authenticating only occasionally, like if you require MFA for a custom application.</span></span> <span data-ttu-id="86fc4-121">每位使用者選項會計算您的租用戶中一個月執行雙步驟驗證之個人數目。</span><span class="sxs-lookup"><span data-stu-id="86fc4-121">The per-user option calculates the number of individuals in your tenant who perform two-step verification in a month.</span></span> <span data-ttu-id="86fc4-122">如果您的某些使用者已擁有授權，但是需要將 MFA 擴充至您授權限制之外的更多使用者，最好使用此選項。</span><span class="sxs-lookup"><span data-stu-id="86fc4-122">This option is best if you have some users with licenses but need to extend MFA to more users beyond your licensing limits.</span></span>

## <a name="create-a-multi-factor-auth-provider"></a><span data-ttu-id="86fc4-123">建立 Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="86fc4-123">Create a Multi-Factor Auth Provider</span></span>
<span data-ttu-id="86fc4-124">使用下列步驟，建立 Azure Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="86fc4-124">Use the following steps to create an Azure Multi-Factor Auth Provider.</span></span> <span data-ttu-id="86fc4-125">只能在 Azure 傳統入口網站中建立 Azure Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="86fc4-125">Azure Multi-Factor Auth Providers can only be created in the Azure classic portal.</span></span> <span data-ttu-id="86fc4-126">如果您無法登入 Azure 傳統入口網站，請確定 Azure AD 租用戶[與 Azure 訂用帳戶相關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="86fc4-126">If you can't sign in to the Azure classic portal, check to make sure that your Azure AD tenant is [associated with an Azure subscription](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span> 

1. <span data-ttu-id="86fc4-127">以系統管理員身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="86fc4-127">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="86fc4-128">選取左邊的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="86fc4-128">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="86fc4-129">在 [Active Directory] 頁面頂端，選取 [Multi-Factor Authentication Provider] 。</span><span class="sxs-lookup"><span data-stu-id="86fc4-129">On the Active Directory page, at the top, select **Multi-Factor Authentication Providers**.</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. <span data-ttu-id="86fc4-131">在底部按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="86fc4-131">At the bottom, click **New**.</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. <span data-ttu-id="86fc4-133">在 [應用程式服務] 之下，選取 [Multi-Factor Auth Provider]</span><span class="sxs-lookup"><span data-stu-id="86fc4-133">Under App Services, select **Multi-Factor Auth Provider**</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. <span data-ttu-id="86fc4-135">選取 [快速建立] 。</span><span class="sxs-lookup"><span data-stu-id="86fc4-135">Select **Quick Create**.</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. <span data-ttu-id="86fc4-137">填寫下列欄位並選取 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="86fc4-137">Fill in the following fields and select **Create**.</span></span>
   1. <span data-ttu-id="86fc4-138">**名稱** – Multi-Factor Auth Provider 的名稱。</span><span class="sxs-lookup"><span data-stu-id="86fc4-138">**Name** – The name of the Multi-Factor Auth Provider.</span></span>
   2. <span data-ttu-id="86fc4-139">**使用量模型** – 選擇兩個選項其中之一：</span><span class="sxs-lookup"><span data-stu-id="86fc4-139">**Usage Model** – Choose one of two options:</span></span>
      * <span data-ttu-id="86fc4-140">每次驗證 – 購買依每次驗證付費的模式。</span><span class="sxs-lookup"><span data-stu-id="86fc4-140">Per Authentication – purchasing model that charges per authentication.</span></span> <span data-ttu-id="86fc4-141">通常用於在取用者導向應用程式中使用 Azure Multi-factor Authentication 的案例。</span><span class="sxs-lookup"><span data-stu-id="86fc4-141">Typically used for scenarios that use Azure Multi-Factor Authentication in a consumer-facing application.</span></span>
      * <span data-ttu-id="86fc4-142">每個啟用的使用者 – 購買依每個啟用使用者付費的模式。</span><span class="sxs-lookup"><span data-stu-id="86fc4-142">Per Enabled User – purchasing model that charges per enabled user.</span></span> <span data-ttu-id="86fc4-143">通常用於員工存取 Office 365 之類的應用程式。</span><span class="sxs-lookup"><span data-stu-id="86fc4-143">Typically used for employee access to applications such as Office 365.</span></span> <span data-ttu-id="86fc4-144">如果某些使用者已擁有 Azure MFA 的授權，請選擇這個選項。</span><span class="sxs-lookup"><span data-stu-id="86fc4-144">Choose this option if you have some users that are already licensed for Azure MFA.</span></span>
   3. <span data-ttu-id="86fc4-145">**目錄** – 與 Multi-Factor Authentication Provider 相關聯的 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="86fc4-145">**Directory** – The Azure Active Directory tenant that the Multi-Factor Authentication Provider is associated with.</span></span> <span data-ttu-id="86fc4-146">請注意以下事項：</span><span class="sxs-lookup"><span data-stu-id="86fc4-146">Be aware of the following:</span></span>
      * <span data-ttu-id="86fc4-147">您不需要 Azure AD 目錄即可建立 Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="86fc4-147">You do not need an Azure AD directory to create a Multi-Factor Auth Provider.</span></span> <span data-ttu-id="86fc4-148">如果您只打算下載 Azure Multi-Factor Authentication Server 或 SDK，請將方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="86fc4-148">Leave this box blank if you are only planning to download the Azure Multi-Factor Authentication Server or SDK.</span></span>
      * <span data-ttu-id="86fc4-149">Multi-Factor Auth Provider 必須與 Azure AD 目錄產生關聯，才能利用進階功能。</span><span class="sxs-lookup"><span data-stu-id="86fc4-149">The Multi-Factor Auth Provider must be associated with an Azure AD directory to take advantage of the advanced features.</span></span>
      * <span data-ttu-id="86fc4-150">只有一個 Multi-Factor Auth Provider 可以與任何一個 Azure AD 目錄相關聯。</span><span class="sxs-lookup"><span data-stu-id="86fc4-150">Only one Multi-Factor Auth Provider can be associated with any one Azure AD directory.</span></span>  
      ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. <span data-ttu-id="86fc4-152">一旦按一下建立，系統便會建立 Multi-Factor Authentication Provider，而且您應該會看到一則指出「已成功建立 Multi-Factor Authentication Provider」 的訊息。</span><span class="sxs-lookup"><span data-stu-id="86fc4-152">Once you click create, the Multi-Factor Authentication Provider is created and you should see a message stating: **Successfully created Multi-Factor Authentication Provider**.</span></span> <span data-ttu-id="86fc4-153">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="86fc4-153">Click **Ok**.</span></span>  
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a><span data-ttu-id="86fc4-155">管理 Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="86fc4-155">Manage your Multi-Factor Auth Provider</span></span>

<span data-ttu-id="86fc4-156">建立 MFA 提供者之後，您就無法變更使用量模型 (依據已啟用的使用者或依據驗證)。</span><span class="sxs-lookup"><span data-stu-id="86fc4-156">You cannot change the usage model (per enabled user or per authentication) after an MFA provider is created.</span></span> <span data-ttu-id="86fc4-157">不過，您可以刪除 MFA 提供者，然後建立一個使用不同使用量模型的 MFA 提供者。</span><span class="sxs-lookup"><span data-stu-id="86fc4-157">However, you can delete the MFA provider and then create one with a different usage model.</span></span>

<span data-ttu-id="86fc4-158">如果目前的 Multi-Factor Auth Provider 與 Azure AD 目錄 (也稱為 Azure AD 租用戶) 相關聯，您就可以安全地將 MFA 提供者刪除，並建立連結至相同 Azure AD 租用戶的 MFA 提供者。</span><span class="sxs-lookup"><span data-stu-id="86fc4-158">If the current Multi-Factor Auth Provider is associated with an Azure AD directory (also known as an Azure AD tenant), you can safely delete the MFA provider and create one that is linked to the same Azure AD tenant.</span></span> <span data-ttu-id="86fc4-159">或者，如果您購買的 MFA、Azure AD Premium 或 Enterprise Mobility + Security (EMS) 授權已足夠讓啟用 MFA 的所有使用者使用，您可以一併刪除 MFA 提供者。</span><span class="sxs-lookup"><span data-stu-id="86fc4-159">Alternatively, if you purchased enough MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS) licenses to cover all users that are enabled for MFA, you can delete the MFA provider altogether.</span></span>

<span data-ttu-id="86fc4-160">如果您的 MFA 提供者未連結至 Azure AD 租用戶，或是您將新的 MFA 提供者連結至不同 Azure AD 租用戶，則使用者設定和組態選項並不會進行轉移。</span><span class="sxs-lookup"><span data-stu-id="86fc4-160">If your MFA provider is not linked to an Azure AD tenant, or you link the new MFA provider to a different Azure AD tenant, user settings and configuration options are not transferred.</span></span> <span data-ttu-id="86fc4-161">此外，現有 Azure MFA 伺服器也需要使用新 MFA 提供者產生的啟用認證重新啟動。</span><span class="sxs-lookup"><span data-stu-id="86fc4-161">Also, existing Azure MFA Servers need to be reactivated using activation credentials generated through the new MFA Provider.</span></span> <span data-ttu-id="86fc4-162">重新啟用 MFA 伺服器以將其連結至新的 MFA 提供者，並不會影響電話和簡訊驗證，但所有使用者的行動裝置應用程式通知將會停止運作，直到他們重新啟動行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="86fc4-162">Reactivating the MFA Servers to link them to the new MFA Provider doesn't impact phone call and text message authentication, but mobile app notifications will stop working for all users until they reactivate the mobile app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86fc4-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86fc4-163">Next steps</span></span>

[<span data-ttu-id="86fc4-164">下載 Multi-Factor Authentication SDK</span><span class="sxs-lookup"><span data-stu-id="86fc4-164">Download the Multi-Factor Authentication SDK</span></span>](multi-factor-authentication-sdk.md)

[<span data-ttu-id="86fc4-165">進行 Multi-Factor Authentication 設定</span><span class="sxs-lookup"><span data-stu-id="86fc4-165">Configure Multi-Factor Authentication settings</span></span>](multi-factor-authentication-whats-next.md)
