---
title: "在 Azure Active Directory 中新增 Azure Stack 租用戶帳戶 | Microsoft Docs"
description: "在部署 Microsoft Azure Stack 開發套件之後，您將需要建立至少一個租用戶使用者帳戶，以便可以瀏覽租用戶入口網站。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 4401de010dec808f080f5460298bb738ddd39312
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="bd32a-103">在 Azure Active Directory 中新增 Azure Stack 租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="bd32a-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="bd32a-104">在[部署 Azure Stack 開發套件](azure-stack-run-powershell-script.md)之後，您將需要租用戶使用者帳戶，以便可以瀏覽租用戶入口網站並測試您的供應項目與方案。</span><span class="sxs-lookup"><span data-stu-id="bd32a-104">After [deploying the Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore the tenant portal and test your offers and plans.</span></span> <span data-ttu-id="bd32a-105">您可以[使用 Azure 入口網站](#create-an-azure-stack-tenant-account-using-the-azure-portal)或[使用 PowerShell](#create-an-azure-stack-tenant-account-using-powershell) 來建立租用戶帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd32a-105">You can create a tenant account by [using the Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-the-azure-portal"></a><span data-ttu-id="bd32a-106">使用 Azure 入口網站建立 Azure Stack 租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="bd32a-106">Create an Azure Stack tenant account using the Azure portal</span></span>
<span data-ttu-id="bd32a-107">您必須擁有 Azure 訂用帳戶，才能使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bd32a-107">You must have an Azure subscription to use the Azure portal.</span></span>

1. <span data-ttu-id="bd32a-108">登入 [Azure](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="bd32a-108">Log in to [Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bd32a-109">在 Microsoft Azure 左側的導覽列中，按一下 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="bd32a-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="bd32a-110">在目錄清單中，按一下您想要用於 Azure Stack 的目錄，或建立一個新的目錄。</span><span class="sxs-lookup"><span data-stu-id="bd32a-110">In the directory list, click the directory that you want to use for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="bd32a-111">在此目錄頁面上，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="bd32a-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="bd32a-112">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="bd32a-112">Click **Add user**.</span></span>
6. <span data-ttu-id="bd32a-113">在 [新增使用者] 精靈的 [使用者類型] 清單中，選擇 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="bd32a-113">In the **Add user** wizard, in the **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="bd32a-114">在 [使用者名稱]  方塊中，輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bd32a-114">In the **User name** box, type a name for the user.</span></span>
8. <span data-ttu-id="bd32a-115">在 [新增使用者精靈] **@** 方塊中，選擇適當的項目。</span><span class="sxs-lookup"><span data-stu-id="bd32a-115">In the **@** box, choose the appropriate entry.</span></span>
9. <span data-ttu-id="bd32a-116">按下一個箭頭。</span><span class="sxs-lookup"><span data-stu-id="bd32a-116">Click the next arrow.</span></span>
10. <span data-ttu-id="bd32a-117">在精靈的 [使用者設定檔]頁面中，輸入**名字**、**姓氏**和**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="bd32a-117">In the **User profile** page of the wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="bd32a-118">在 [角色] 清單中，選擇 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="bd32a-118">In the **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="bd32a-119">按下一個箭頭。</span><span class="sxs-lookup"><span data-stu-id="bd32a-119">Click the next arrow.</span></span>
13. <span data-ttu-id="bd32a-120">在 [取得暫時密碼] 頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="bd32a-120">On the **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="bd32a-121">複製 [新密碼] 。</span><span class="sxs-lookup"><span data-stu-id="bd32a-121">Copy the **New password**.</span></span>
15. <span data-ttu-id="bd32a-122">以新的帳戶登入 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="bd32a-122">Log in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="bd32a-123">在系統提示時變更密碼。</span><span class="sxs-lookup"><span data-stu-id="bd32a-123">Change the password when prompted.</span></span>
16. <span data-ttu-id="bd32a-124">以新的帳戶登入 `https://portal.local.azurestack.external`，查看租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="bd32a-124">Log in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="bd32a-125">使用 PowerShell 建立 Azure Stack 租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="bd32a-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="bd32a-126">如果您沒有 Azure 訂用帳戶，就無法使用 Azure 入口網站來新增租用戶使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd32a-126">If you don't have an Azure subscription, you can't use the Azure portal to add a tenant user account.</span></span> <span data-ttu-id="bd32a-127">在此情況下，您可以改為使用適用於 Windows PowerShell 的 Azure Active Directory 模組。</span><span class="sxs-lookup"><span data-stu-id="bd32a-127">In this case, you can use the Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="bd32a-128">如果您使用 Microsoft 帳戶 (Live ID) 來部署 Azure Stack 開發套件，就無法使用 AAD PowerShell 來建立租用戶帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd32a-128">If you are using Microsoft Account (Live ID) to deploy Azure Stack Development Kit, you can't use AAD PowerShell to create tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="bd32a-129">安裝[適用於 IT 專業人員的 Microsoft Online Services 登入小幫手 RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950)。</span><span class="sxs-lookup"><span data-stu-id="bd32a-129">Install the [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="bd32a-130">安裝[適用於 Windows PowerShell (64 位元版本) 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297) \(英文\)，並將它開啟。</span><span class="sxs-lookup"><span data-stu-id="bd32a-130">Install the [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="bd32a-131">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="bd32a-131">Run the following cmdlets:</span></span>

    ```powershell
    # Provide the AAD credential you use to deploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with the initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="bd32a-132">以新的帳戶登入 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="bd32a-132">Sign in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="bd32a-133">在系統提示時變更密碼。</span><span class="sxs-lookup"><span data-stu-id="bd32a-133">Change the password when prompted.</span></span>
2. <span data-ttu-id="bd32a-134">以新的帳戶登入 `https://portal.local.azurestack.external`，查看租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="bd32a-134">Sign in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

