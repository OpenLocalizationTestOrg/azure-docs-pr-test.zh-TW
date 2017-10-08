---
title: "擴充功能應用程式 - Azure AD B2C | Microsoft Docs"
description: "還原 hello b2c-擴充功能-應用程式"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="ee801-103">Azure AD B2C：擴充功能應用程式</span><span class="sxs-lookup"><span data-stu-id="ee801-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="ee801-104">建立 Azure AD B2C 目錄時，應用程式呼叫`b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.`hello 新目錄內會自動建立。</span><span class="sxs-lookup"><span data-stu-id="ee801-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="ee801-105">此應用程式，參照的 tooas hello **b2c 擴充功能-應用程式**，會顯示在*應用程式註冊*。</span><span class="sxs-lookup"><span data-stu-id="ee801-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="ee801-106">它會使用 hello Azure AD B2C 服務 toostore 使用者和資訊的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="ee801-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="ee801-107">如果刪除 hello 應用程式時，Azure AD B2C 將無法正確運作，並會影響您的生產環境。</span><span class="sxs-lookup"><span data-stu-id="ee801-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee801-108">除非您計劃 tooimmediately 刪除您的租用戶，請勿刪除 hello b2c-擴充功能-應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee801-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="ee801-109">若 hello 應用程式維持已刪除超過 30 天，使用者資訊將會永久遺失。</span><span class="sxs-lookup"><span data-stu-id="ee801-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="ee801-110">正在驗證該 hello 擴充功能的應用程式是否存在</span><span class="sxs-lookup"><span data-stu-id="ee801-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="ee801-111">hello b2c 擴充功能-應用程式的 tooverify 存在於：</span><span class="sxs-lookup"><span data-stu-id="ee801-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="ee801-112">在您 Azure AD B2C 租用戶中，按一下 上**更多服務**hello 左側瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="ee801-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="ee801-113">搜尋並開啟 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="ee801-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="ee801-114">尋找以 **b2c-extensions-app** 開頭的應用程式</span><span class="sxs-lookup"><span data-stu-id="ee801-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="ee801-115">復原 hello 擴充功能的應用程式</span><span class="sxs-lookup"><span data-stu-id="ee801-115">Recover hello extensions app</span></span>

<span data-ttu-id="ee801-116">如果您不小心刪除 hello b2c-擴充功能-應用程式，您有 30 天 toorecover 它。</span><span class="sxs-lookup"><span data-stu-id="ee801-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="ee801-117">您可以還原使用 hello Graph API 的 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="ee801-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="ee801-118">瀏覽過[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="ee801-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="ee801-119">您想用於 toorestore hello 刪除應用程式的 hello Azure AD B2C 目錄的全域管理員身分登入 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="ee801-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="ee801-120">發出 HTTP GET 針對 hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api 版本 = 1.6。</span><span class="sxs-lookup"><span data-stu-id="ee801-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="ee801-121">請確定 tooreplace`{tenantName}`以您的租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ee801-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="ee801-122">這項作業會列出所有已刪除在 hello 過去 30 天的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee801-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="ee801-123">其中 hello 名稱開頭為 'b2c 擴充功能-應用程式' 和複製的 hello 清單中尋找 hello 應用程式及其`objectid`屬性值。</span><span class="sxs-lookup"><span data-stu-id="ee801-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="ee801-124">發出 HTTP POST 對 URL hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`。</span><span class="sxs-lookup"><span data-stu-id="ee801-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="ee801-125">取代 hello `{OBJECTID}` hello URL 以 hello 部分`objectid`hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="ee801-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="ee801-126">您現在應該可以太[hello 還原應用程式請參閱 <<c2> ](#verifying-that-the-extensions-app-is-present)  hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ee801-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ee801-127">如果已遭刪除 hello 內過去 30 天內，可以只還原應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee801-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="ee801-128">如果已經超過 30 天，資料將會永久遺失。</span><span class="sxs-lookup"><span data-stu-id="ee801-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="ee801-129">如需協助，請提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="ee801-129">For more assistance, file a support ticket.</span></span>
