---
title: "aaaGet 啟動 Azure Multi-factor Auth 提供者 |Microsoft 文件"
description: "深入了解如何 toocreate Azure Multi-factor Auth 提供者。"
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
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="2d7d6-103">開始使用 Azure Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="2d7d6-103">Getting started with an Azure Multi-Factor Auth Provider</span></span>
<span data-ttu-id="2d7d6-104">依預設，擁有 Azure Active Directory 和 Office 365 使用者的全域管理員可以使用雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-104">Two-step verification is available by default for global administrators who have Azure Active Directory, and Office 365 users.</span></span> <span data-ttu-id="2d7d6-105">不過，如果您想利用 tootake[進階功能](multi-factor-authentication-whats-next.md)則您應該購買 hello 完整版本的 Azure Multi-factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-105">However, if you wish tootake advantage of [advanced features](multi-factor-authentication-whats-next.md) then you should purchase hello full version of Azure Multi-Factor Authentication (MFA).</span></span>

<span data-ttu-id="2d7d6-106">使用 Azure Multi-factor Auth 提供者 tootake 利用 hello 完整版本的 Azure MFA 所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-106">An Azure Multi-Factor Auth Provider is used tootake advantage of features provided by hello full version of Azure MFA.</span></span> <span data-ttu-id="2d7d6-107">它的適用對象是**未透過 Azure MFA、Azure AD Premium 或 Enterprise Mobility + Security (EMS) 取得授權**的使用者。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-107">It is for users who **do not have licenses through Azure MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS)**.</span></span>  <span data-ttu-id="2d7d6-108">Azure MFA、 Azure AD Premium 和 EMS 包括 hello 完整版的 Azure MFA 的預設值。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-108">Azure MFA, Azure AD Premium, and EMS include hello full version of Azure MFA by default.</span></span> <span data-ttu-id="2d7d6-109">如果您有授權，則不需要 Azure Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-109">If you have licenses, then you do not need an Azure Multi-Factor Auth Provider.</span></span>

<span data-ttu-id="2d7d6-110">Azure 多因素驗證提供者為必要的 toodownload hello SDK。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-110">An Azure Multi-Factor Auth provider is required toodownload hello SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d7d6-111">toodownload hello SDK，您需要 toocreate Azure Multi-factor Auth 提供者，即使您的 Azure MFA、 AAD Premium 或 EMS 授權數量。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-111">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span>  <span data-ttu-id="2d7d6-112">如果您針對此用途建立 Azure Multi-factor Auth 提供者，且已授權，可確定 toocreate hello 提供者以 hello**每個已啟用的使用者**模型。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-112">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, be sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="2d7d6-113">然後，連結 hello 包含 hello Azure MFA、 Azure AD Premium 或 EMS 授權提供者 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-113">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="2d7d6-114">此組態可確保，您才需要付費如果您有多個唯一的使用者執行雙步驟驗證比 hello 您所擁有的授權數目。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-114">This configuration ensures that you are only billed if you have more unique users performing two-step verification than hello number of licenses you own.</span></span>

## <a name="what-is-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="2d7d6-115">什麼是 Azure Multi-Factor Auth Provider？</span><span class="sxs-lookup"><span data-stu-id="2d7d6-115">What is an Azure Multi-Factor Auth Provider?</span></span>

<span data-ttu-id="2d7d6-116">如果您沒有授權的 Azure Multi-factor Authentication，您可以建立 auth 提供者 toorequire 雙步驟驗證為您的使用者。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-116">If you don't have licenses for Azure Multi-Factor Authentication, you can create an auth provider toorequire two-step verification for your users.</span></span> <span data-ttu-id="2d7d6-117">如果您正在開發自訂應用程式，而且想 tooenable Azure MFA 時，會建立驗證提供者和[下載 hello SDK](multi-factor-authentication-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-117">If you are developing a custom app and want tooenable Azure MFA, create an auth provider and [download hello SDK](multi-factor-authentication-sdk.md).</span></span>

<span data-ttu-id="2d7d6-118">有兩種類型的驗證提供者，且 hello 區別是解決您的 Azure 訂用帳戶收費的方式。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-118">There are two types of auth providers, and hello distinction is around how your Azure subscription is charged.</span></span> <span data-ttu-id="2d7d6-119">hello 驗證每個選項會計算 hello 驗證您的租用戶對執行中之月數。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-119">hello per-authentication option calculates hello number of authentications performed against your tenant in a month.</span></span> <span data-ttu-id="2d7d6-120">如果您有許多使用者偶爾才會進行驗證，像是如果您要求 MFA 進行自訂應用程式，最好使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-120">This option is best if you have a number of users authenticating only occasionally, like if you require MFA for a custom application.</span></span> <span data-ttu-id="2d7d6-121">hello 每位使用者選項計算執行中之月的雙步驟驗證您的租用戶中個人的 hello 的數目。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-121">hello per-user option calculates hello number of individuals in your tenant who perform two-step verification in a month.</span></span> <span data-ttu-id="2d7d6-122">如果您已經擁有授權的某些使用者，但是需要 tooextend MFA toomore 使用者超出您的授權限制，最好使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-122">This option is best if you have some users with licenses but need tooextend MFA toomore users beyond your licensing limits.</span></span>

## <a name="create-a-multi-factor-auth-provider"></a><span data-ttu-id="2d7d6-123">建立 Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="2d7d6-123">Create a Multi-Factor Auth Provider</span></span>
<span data-ttu-id="2d7d6-124">使用下列步驟 toocreate Azure Multi-factor Auth 提供者的 hello。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-124">Use hello following steps toocreate an Azure Multi-Factor Auth Provider.</span></span> <span data-ttu-id="2d7d6-125">只能在 hello Azure 傳統入口網站中建立 azure 的 Multi-factor Auth 提供者。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-125">Azure Multi-Factor Auth Providers can only be created in hello Azure classic portal.</span></span> <span data-ttu-id="2d7d6-126">如果您無法登入 toohello Azure 傳統入口網站，檢查確定您的 Azure AD 租用戶是 toomake[與 Azure 訂用帳戶相關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-126">If you can't sign in toohello Azure classic portal, check toomake sure that your Azure AD tenant is [associated with an Azure subscription](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span> 

1. <span data-ttu-id="2d7d6-127">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-127">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="2d7d6-128">Hello 左側選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-128">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="2d7d6-129">在 [hello Active Directory] 頁面上，在 hello 頂端，選取**Multi-factor Authentication 提供者**。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-129">On hello Active Directory page, at hello top, select **Multi-Factor Authentication Providers**.</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. <span data-ttu-id="2d7d6-131">在 hello 下方，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-131">At hello bottom, click **New**.</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. <span data-ttu-id="2d7d6-133">在 [應用程式服務] 之下，選取 [Multi-Factor Auth Provider]</span><span class="sxs-lookup"><span data-stu-id="2d7d6-133">Under App Services, select **Multi-Factor Auth Provider**</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. <span data-ttu-id="2d7d6-135">選取 [快速建立] 。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-135">Select **Quick Create**.</span></span>
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. <span data-ttu-id="2d7d6-137">填寫下列欄位的 hello，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-137">Fill in hello following fields and select **Create**.</span></span>
   1. <span data-ttu-id="2d7d6-138">**名稱**– hello hello Multi-factor Auth 提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-138">**Name** – hello name of hello Multi-Factor Auth Provider.</span></span>
   2. <span data-ttu-id="2d7d6-139">**使用量模型** – 選擇兩個選項其中之一：</span><span class="sxs-lookup"><span data-stu-id="2d7d6-139">**Usage Model** – Choose one of two options:</span></span>
      * <span data-ttu-id="2d7d6-140">每次驗證 – 購買依每次驗證付費的模式。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-140">Per Authentication – purchasing model that charges per authentication.</span></span> <span data-ttu-id="2d7d6-141">通常用於在取用者導向應用程式中使用 Azure Multi-factor Authentication 的案例。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-141">Typically used for scenarios that use Azure Multi-Factor Authentication in a consumer-facing application.</span></span>
      * <span data-ttu-id="2d7d6-142">每個啟用的使用者 – 購買依每個啟用使用者付費的模式。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-142">Per Enabled User – purchasing model that charges per enabled user.</span></span> <span data-ttu-id="2d7d6-143">通常用於例如 Office 365 的員工存取 tooapplications。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-143">Typically used for employee access tooapplications such as Office 365.</span></span> <span data-ttu-id="2d7d6-144">如果某些使用者已擁有 Azure MFA 的授權，請選擇這個選項。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-144">Choose this option if you have some users that are already licensed for Azure MFA.</span></span>
   3. <span data-ttu-id="2d7d6-145">**目錄**– hello Azure Active Directory 租用戶的多因素驗證提供者是與相關聯的 hello。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-145">**Directory** – hello Azure Active Directory tenant that hello Multi-Factor Authentication Provider is associated with.</span></span> <span data-ttu-id="2d7d6-146">請注意下列 hello:</span><span class="sxs-lookup"><span data-stu-id="2d7d6-146">Be aware of hello following:</span></span>
      * <span data-ttu-id="2d7d6-147">您不需要 Azure AD 目錄 toocreate Multi-factor Auth 提供者。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-147">You do not need an Azure AD directory toocreate a Multi-Factor Auth Provider.</span></span> <span data-ttu-id="2d7d6-148">這個方塊保留空白，如果您計劃只 toodownload hello Azure Multi-factor Authentication Server 或 SDK。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-148">Leave this box blank if you are only planning toodownload hello Azure Multi-Factor Authentication Server or SDK.</span></span>
      * <span data-ttu-id="2d7d6-149">hello Multi-factor Auth 提供者必須是 hello 的 Azure AD 目錄 tootake 優點的進階功能與相關聯。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-149">hello Multi-Factor Auth Provider must be associated with an Azure AD directory tootake advantage of hello advanced features.</span></span>
      * <span data-ttu-id="2d7d6-150">只有一個 Multi-Factor Auth Provider 可以與任何一個 Azure AD 目錄相關聯。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-150">Only one Multi-Factor Auth Provider can be associated with any one Azure AD directory.</span></span>  
      ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. <span data-ttu-id="2d7d6-152">一旦您按一下 建立，請建立多因素驗證提供者的 hello 和您應該會看到訊息指出：**已成功建立 Multi-factor Authentication 提供者**。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-152">Once you click create, hello Multi-Factor Authentication Provider is created and you should see a message stating: **Successfully created Multi-Factor Authentication Provider**.</span></span> <span data-ttu-id="2d7d6-153">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-153">Click **Ok**.</span></span>  
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a><span data-ttu-id="2d7d6-155">管理 Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="2d7d6-155">Manage your Multi-Factor Auth Provider</span></span>

<span data-ttu-id="2d7d6-156">您無法變更 hello 使用量的 MFA 提供者建立之後，模型 （每個已啟用的使用者或驗證）。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-156">You cannot change hello usage model (per enabled user or per authentication) after an MFA provider is created.</span></span> <span data-ttu-id="2d7d6-157">不過，您可以刪除 hello MFA 提供者，然後建立一個具有不同的使用方式模型。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-157">However, you can delete hello MFA provider and then create one with a different usage model.</span></span>

<span data-ttu-id="2d7d6-158">如果 hello 目前 Multi-factor Auth 提供者與相關聯的 Azure AD 目錄 （也稱為 Azure AD 租用戶），您就可以安全地刪除 hello MFA 提供者，並建立一個是連結的 toohello 相同的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-158">If hello current Multi-Factor Auth Provider is associated with an Azure AD directory (also known as an Azure AD tenant), you can safely delete hello MFA provider and create one that is linked toohello same Azure AD tenant.</span></span> <span data-ttu-id="2d7d6-159">或者，如果您購買足夠 MFA、 Azure AD Premium，或企業行動力 + 安全性 (EMS) 授權 toocover 所有使用者啟用 MFA，您可以完全刪除 hello MFA 提供者。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-159">Alternatively, if you purchased enough MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS) licenses toocover all users that are enabled for MFA, you can delete hello MFA provider altogether.</span></span>

<span data-ttu-id="2d7d6-160">如果您的 MFA 提供者不是連結的 tooan Azure AD 租用戶，或連結 hello 新 MFA 提供者 tooa 不同的 Azure AD 租用戶、 使用者設定和組態選項不會傳送。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-160">If your MFA provider is not linked tooan Azure AD tenant, or you link hello new MFA provider tooa different Azure AD tenant, user settings and configuration options are not transferred.</span></span> <span data-ttu-id="2d7d6-161">此外，現有的 Azure MFA 伺服器需要重新啟動使用透過產生啟用認證 toobe hello 新的 MFA 提供者。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-161">Also, existing Azure MFA Servers need toobe reactivated using activation credentials generated through hello new MFA Provider.</span></span> <span data-ttu-id="2d7d6-162">重新啟動 hello MFA Server toolink 它們 toohello 新的 MFA 提供者不會影響通話和簡訊驗證，但通知將會停止運作的所有使用者，直到它們重新啟用 hello 行動應用程式的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d7d6-162">Reactivating hello MFA Servers toolink them toohello new MFA Provider doesn't impact phone call and text message authentication, but mobile app notifications will stop working for all users until they reactivate hello mobile app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d7d6-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d7d6-163">Next steps</span></span>

[<span data-ttu-id="2d7d6-164">下載多因素驗證 SDK hello</span><span class="sxs-lookup"><span data-stu-id="2d7d6-164">Download hello Multi-Factor Authentication SDK</span></span>](multi-factor-authentication-sdk.md)

[<span data-ttu-id="2d7d6-165">進行 Multi-Factor Authentication 設定</span><span class="sxs-lookup"><span data-stu-id="2d7d6-165">Configure Multi-Factor Authentication settings</span></span>](multi-factor-authentication-whats-next.md)
