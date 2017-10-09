---
title: "aaaGet hello 雲端中啟動 Azure MFA |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA hello 雲端中的 hello Microsoft Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="da8c2-103">開始使用 Azure Multi-factor Authentication hello 雲端中</span><span class="sxs-lookup"><span data-stu-id="da8c2-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="da8c2-104">本文逐步 tooget 啟動 hello 雲端中使用 Azure Multi-factor Authentication Server 的方式。</span><span class="sxs-lookup"><span data-stu-id="da8c2-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="da8c2-105">hello 下列文件提供有關如何使用 tooenable 使用者 hello **Azure 傳統入口網站**。</span><span class="sxs-lookup"><span data-stu-id="da8c2-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="da8c2-106">如果您要尋找有關如何設定 Azure Multi-factor Authentication 的 tooset O365 使用者，請參閱[設定 Office 365 的 multi-factor authentication。](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="da8c2-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Hello 雲端中的 MFA](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="da8c2-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="da8c2-108">Prerequisite</span></span>
<span data-ttu-id="da8c2-109">[註冊 Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)-如果您還沒有 Azure 訂用帳戶，您需要 toosign 向上之其中一個。</span><span class="sxs-lookup"><span data-stu-id="da8c2-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="da8c2-110">如果您剛開始使用 Azure MFA，您可以使用試用版訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da8c2-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="da8c2-111">啟用 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="da8c2-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="da8c2-112">只要您的使用者有包含 Azure Multi-factor Authentication Server 的授權，並沒有您需要 Azure MFA 上的 toodo tooturn。</span><span class="sxs-lookup"><span data-stu-id="da8c2-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="da8c2-113">您可以開始要求對個別使用者進行雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="da8c2-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="da8c2-114">啟用 Azure MFA 的 hello 授權是：</span><span class="sxs-lookup"><span data-stu-id="da8c2-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="da8c2-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="da8c2-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="da8c2-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="da8c2-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="da8c2-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="da8c2-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="da8c2-118">如果您還沒有這些三個授權，或是您沒有足夠的授權 toocover 的所有使用者，太的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="da8c2-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="da8c2-119">您只需要 toodo 額外的步驟和[建立 Multi-factor Auth 提供者](multi-factor-authentication-get-started-auth-provider.md)目錄中。</span><span class="sxs-lookup"><span data-stu-id="da8c2-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="da8c2-120">對使用者開啟雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="da8c2-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="da8c2-121">使用其中一個 hello 程序中所列[如何 toorequire 雙步驟驗證的使用者或群組](multi-factor-authentication-get-started-user-states.md)toostart 使用 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="da8c2-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="da8c2-122">您可以選擇 tooenforce 雙步驟驗證的所有登入，或只有當重要 tooyou，您可以建立條件式存取原則 toorequire 雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="da8c2-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da8c2-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da8c2-123">Next Steps</span></span>
<span data-ttu-id="da8c2-124">既然您已經 hello 雲端中設定 Azure Multi-factor Authentication，您可以設定，並設定您的部署。</span><span class="sxs-lookup"><span data-stu-id="da8c2-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="da8c2-125">如需詳細資訊，請參閱[設定 Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)。</span><span class="sxs-lookup"><span data-stu-id="da8c2-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

