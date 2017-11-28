---
title: "Azure Active Directory 中的新 Azure 堆疊租用戶帳戶 aaaAdd |Microsoft 文件"
description: "部署 Microsoft Azure 堆疊開發套件之後, 您必須至少一個 toocreate 租用戶的使用者帳戶，好讓您可以瀏覽 hello 租用戶入口網站。"
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
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="0f2ef-103">在 Azure Active Directory 中新增 Azure Stack 租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="0f2ef-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="0f2ef-104">之後[部署 hello Azure 堆疊開發套件](azure-stack-run-powershell-script.md)，讓您可以瀏覽 hello 租用戶入口網站，並測試您的優惠和方案，您將需要租用戶的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-104">After [deploying hello Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore hello tenant portal and test your offers and plans.</span></span> <span data-ttu-id="0f2ef-105">您可以建立租用戶帳戶[使用 hello Azure 入口網站](#create-an-azure-stack-tenant-account-using-the-azure-portal)或[使用 PowerShell](#create-an-azure-stack-tenant-account-using-powershell)。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-105">You can create a tenant account by [using hello Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a><span data-ttu-id="0f2ef-106">建立 Azure 堆疊租用戶帳戶使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0f2ef-106">Create an Azure Stack tenant account using hello Azure portal</span></span>
<span data-ttu-id="0f2ef-107">您必須擁有 Azure 訂用帳戶 toouse hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-107">You must have an Azure subscription toouse hello Azure portal.</span></span>

1. <span data-ttu-id="0f2ef-108">登入太[Azure](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-108">Log in too[Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0f2ef-109">在 Microsoft Azure 左側的導覽列中，按一下 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="0f2ef-110">在 hello 目錄清單中，按一下您想要 Azure 堆疊 toouse 或建立一個新的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-110">In hello directory list, click hello directory that you want toouse for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="0f2ef-111">在此目錄頁面上，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="0f2ef-112">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-112">Click **Add user**.</span></span>
6. <span data-ttu-id="0f2ef-113">在 hello**新增使用者**精靈，hello**使用者類型**清單中，選擇**您組織中的新使用者**。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-113">In hello **Add user** wizard, in hello **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="0f2ef-114">在 hello**使用者名**方塊中，輸入 hello 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-114">In hello **User name** box, type a name for hello user.</span></span>
8. <span data-ttu-id="0f2ef-115">在 hello  **@** 方塊中，選擇 hello 適當的項目。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-115">In hello **@** box, choose hello appropriate entry.</span></span>
9. <span data-ttu-id="0f2ef-116">按一下 下一步箭號 hello。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-116">Click hello next arrow.</span></span>
10. <span data-ttu-id="0f2ef-117">在 [hello**使用者設定檔**hello 精靈] 頁面輸入**名字**，**姓氏**，和**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-117">In hello **User profile** page of hello wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="0f2ef-118">在 hello**角色**清單中，選擇**使用者**。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-118">In hello **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="0f2ef-119">按一下 下一步箭號 hello。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-119">Click hello next arrow.</span></span>
13. <span data-ttu-id="0f2ef-120">在 hello**取得暫時密碼**頁面上，按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-120">On hello **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="0f2ef-121">複製 hello**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-121">Copy hello **New password**.</span></span>
15. <span data-ttu-id="0f2ef-122">登入 tooMicrosoft Azure hello 新帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-122">Log in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="0f2ef-123">變更 hello 密碼提示。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-123">Change hello password when prompted.</span></span>
16. <span data-ttu-id="0f2ef-124">登入太`https://portal.local.azurestack.external`與 hello 新帳戶 toosee hello 租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-124">Log in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="0f2ef-125">使用 PowerShell 建立 Azure Stack 租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="0f2ef-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="0f2ef-126">如果您沒有 Azure 訂用帳戶，您無法使用 hello Azure 入口網站 tooadd 租用戶的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-126">If you don't have an Azure subscription, you can't use hello Azure portal tooadd a tenant user account.</span></span> <span data-ttu-id="0f2ef-127">在此情況下，您可以改為使用 hello Azure Active Directory 的 Windows PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-127">In this case, you can use hello Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2ef-128">如果您使用 Microsoft 帳戶 (Live ID) toodeploy Azure 堆疊開發套件，您無法使用 AAD PowerShell toocreate 租用戶帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-128">If you are using Microsoft Account (Live ID) toodeploy Azure Stack Development Kit, you can't use AAD PowerShell toocreate tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="0f2ef-129">安裝 hello [Microsoft Online Services 登入小幫手的 IT 專業人員 RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950)。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-129">Install hello [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="0f2ef-130">安裝 hello [Azure Active Directory 的 Windows PowerShell 模組 （64 位元版本）](http://go.microsoft.com/fwlink/p/?linkid=236297)並開啟它。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-130">Install hello [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="0f2ef-131">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f2ef-131">Run hello following cmdlets:</span></span>

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="0f2ef-132">登入 tooMicrosoft Azure hello 新帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-132">Sign in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="0f2ef-133">變更 hello 密碼提示。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-133">Change hello password when prompted.</span></span>
2. <span data-ttu-id="0f2ef-134">登入太`https://portal.local.azurestack.external`與 hello 新帳戶 toosee hello 租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f2ef-134">Sign in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

