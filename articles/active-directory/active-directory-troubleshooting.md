---
title: "疑難排解: 'Active Directory' 項目已遺失或無法使用 |Microsoft 文件"
description: "哪些 toodo 當 Active Directory 功能表項目不會出現在 hello Azure 管理入口網站。"
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="07d6d-103">疑難排解：'Active Directory' 項目遺失或無法使用</span><span class="sxs-lookup"><span data-stu-id="07d6d-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="07d6d-104">許多使用 Azure Active Directory 功能和服務的指示 hello 開頭為 「 移 toohello Azure 管理入口網站，然後按一下**Active Directory**。 」</span><span class="sxs-lookup"><span data-stu-id="07d6d-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="07d6d-105">但該怎麼辦如果 hello Active Directory 延伸模組或功能表項目沒有出現，或其標記為**無法使用**嗎？</span><span class="sxs-lookup"><span data-stu-id="07d6d-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="07d6d-106">本主題是設計的 toohelp。</span><span class="sxs-lookup"><span data-stu-id="07d6d-106">This topic is designed toohelp.</span></span> <span data-ttu-id="07d6d-107">它描述 hello 條件**Active Directory**不會出現或無法使用，並說明如何 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="07d6d-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="07d6d-108">Active Directory 遺失</span><span class="sxs-lookup"><span data-stu-id="07d6d-108">Active Directory is missing</span></span>
<span data-ttu-id="07d6d-109">一般而言， **Active Directory** hello 左的導覽功能表中的項目隨即出現。</span><span class="sxs-lookup"><span data-stu-id="07d6d-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="07d6d-110">Azure Active Directory 程序中的 hello 指示會假設此項目是在檢視中。</span><span class="sxs-lookup"><span data-stu-id="07d6d-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![螢幕擷取畫面：Azure 中的 Active Directory](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="07d6d-112">若任何 hello 下列條件為真，hello Active Directory 項目會出現在 hello 左的導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="07d6d-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="07d6d-113">否則，未顯示 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="07d6d-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="07d6d-114">hello 以 Microsoft 帳戶 （先前稱為 Windows Live ID） 登入目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="07d6d-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="07d6d-115">或</span><span class="sxs-lookup"><span data-stu-id="07d6d-115">OR</span></span>
* <span data-ttu-id="07d6d-116">hello Azure 租用戶具有目錄，而 hello 目前帳戶為目錄管理員。</span><span class="sxs-lookup"><span data-stu-id="07d6d-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="07d6d-117">或</span><span class="sxs-lookup"><span data-stu-id="07d6d-117">OR</span></span>
* <span data-ttu-id="07d6d-118">hello Azure 租用戶具有至少一個 Azure AD 存取控制 (ACS) 命名空間。</span><span class="sxs-lookup"><span data-stu-id="07d6d-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="07d6d-119">如需詳細資訊，請參閱 [存取控制命名空間](https://msdn.microsoft.com/library/azure/gg185908.aspx)。</span><span class="sxs-lookup"><span data-stu-id="07d6d-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="07d6d-120">或</span><span class="sxs-lookup"><span data-stu-id="07d6d-120">OR</span></span>
* <span data-ttu-id="07d6d-121">hello Azure 租用戶具有至少一個 Azure Multi-factor Authentication 提供者。</span><span class="sxs-lookup"><span data-stu-id="07d6d-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="07d6d-122">如需詳細資訊，請參閱 [管理 Azure Multi-Factor Authentication 提供者](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="07d6d-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="07d6d-123">toocreate 存取控制命名空間或為多因素驗證提供者中，按一下**+ 新增** > **應用程式服務** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07d6d-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="07d6d-124">tooget 系統管理權限 tooa 目錄中，有系統管理員指派系統管理員角色 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="07d6d-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="07d6d-125">如需詳細資訊，請參閱 [指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="07d6d-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="07d6d-126">Active Directory 無法使用</span><span class="sxs-lookup"><span data-stu-id="07d6d-126">Active Directory is not available</span></span>
<span data-ttu-id="07d6d-127">當您按一下 [+新增]  >  [應用程式服務] 時，[Active Directory] 項目即會出現。</span><span class="sxs-lookup"><span data-stu-id="07d6d-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="07d6d-128">具體而言，當任何 hello Active Directory 功能，例如目錄、 存取控制或 Multi-factor Auth 提供者，可以使用 toohello 目前的使用者，就會出現 hello Active Directory 項目。</span><span class="sxs-lookup"><span data-stu-id="07d6d-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="07d6d-129">不過，雖然 hello 頁面載入時，hello 項目會呈暗灰色且標示**無法使用**。</span><span class="sxs-lookup"><span data-stu-id="07d6d-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="07d6d-130">這是暫時性狀態。</span><span class="sxs-lookup"><span data-stu-id="07d6d-130">This is a temporary state.</span></span> <span data-ttu-id="07d6d-131">如果您需要等候幾秒鐘的時間，hello 項目會變成可用。</span><span class="sxs-lookup"><span data-stu-id="07d6d-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="07d6d-132">如果 hello 延遲太久，重新整理 hello 網頁通常會解決 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="07d6d-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![螢幕擷取畫面：Active Directory 無法使用](./media/active-directory-troubleshooting/not-available.png)

