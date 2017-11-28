---
title: "aaaManage Azure 自動化帳戶 |Microsoft 文件"
description: "本文說明如何 toomanage hello 您的自動化帳戶，例如憑證更新、 刪除和設定不正確的設定。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="b9c7a-103">管理 Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="b9c7a-103">Manage Azure Automation account</span></span>
<span data-ttu-id="b9c7a-104">在某個時間點您的自動化帳戶到期前，您將需要 toorenew hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="b9c7a-105">如果您認為該 hello 執行身分帳戶已遭洩漏，您可以刪除並重新建立它。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="b9c7a-106">本章節將討論如何 tooperform 這些作業。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="b9c7a-107">自我簽署憑證更新</span><span class="sxs-lookup"><span data-stu-id="b9c7a-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="b9c7a-108">hello hello 執行身分帳戶建立的自我簽署的憑證到期從建立 hello 日期起一年。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="b9c7a-109">您可以在該憑證到期前隨時更新憑證。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="b9c7a-110">當您更新它時，hello 目前有效的憑證會保留的 tooensure 任何 runbook 的執行中或正在執行，會進入佇列，並可向 hello 執行身分帳戶，不會產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="b9c7a-111">hello 憑證到期日前就持續有效。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="b9c7a-112">如果您已設定您自動化執行身分帳戶 toouse 您企業憑證授權單位所核發的憑證，且您使用此選項，將會自我簽署憑證所取代 hello 企業憑證。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="b9c7a-113">toorenew hello 憑證，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="b9c7a-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="b9c7a-114">在 hello Azure 入口網站，開啟 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="b9c7a-115">在 hello**自動化帳戶**刀鋒視窗中的，在 hello**帳戶屬性**窗格下**帳戶設定**，選取**執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![自動化帳戶的屬性窗格](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="b9c7a-117">在 hello**執行身分帳戶**屬性刀鋒視窗中，選取任一 hello 執行身分帳戶或 hello 傳統執行身分帳戶，您想要 toorenew hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="b9c7a-118">在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**更新憑證**。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![更新執行身分帳戶的憑證](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="b9c7a-120">當更新 hello 憑證後時，您可以追蹤下的 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="b9c7a-121">刪除執行身分或傳統執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="b9c7a-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="b9c7a-122">本章節描述如何 toodelete 並重新建立執行身分或傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="b9c7a-123">當您執行此動作時，會保留 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="b9c7a-124">刪除執行身分或傳統執行身分帳戶後，您可以在 hello Azure 入口網站中重新建立它。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="b9c7a-125">在 hello Azure 入口網站，開啟 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="b9c7a-126">在 [hello**自動化帳戶**刀鋒視窗中的，hello 帳戶屬性] 窗格中，選取**執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="b9c7a-127">在 hello**執行身分帳戶**想 toodelete 屬性刀鋒視窗中，選取任一 hello 執行身分帳戶 」 或 「 傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="b9c7a-128">然後，在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![刪除執行身分帳戶](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="b9c7a-130">正在刪除 hello 帳戶，而您可以追蹤下的 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="b9c7a-131">Hello 帳戶已被刪除後，您可以重新建立它在 hello**執行身分帳戶**屬性刀鋒視窗中的選取 hello 建立選項**Azure 執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![重新建立 hello 自動化執行身分帳戶](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="b9c7a-133">設定錯誤</span><span class="sxs-lookup"><span data-stu-id="b9c7a-133">Misconfiguration</span></span>
<span data-ttu-id="b9c7a-134">某些組態項目所需的 hello 執行身分或傳統執行身分帳戶 toofunction 正確可能已刪除或在初始安裝期間，建立方式不正確。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="b9c7a-135">hello 項目包括：</span><span class="sxs-lookup"><span data-stu-id="b9c7a-135">hello items include:</span></span>

* <span data-ttu-id="b9c7a-136">憑證資產</span><span class="sxs-lookup"><span data-stu-id="b9c7a-136">Certificate asset</span></span>
* <span data-ttu-id="b9c7a-137">連線資產</span><span class="sxs-lookup"><span data-stu-id="b9c7a-137">Connection asset</span></span>
* <span data-ttu-id="b9c7a-138">已從 hello 參與者角色移除執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="b9c7a-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="b9c7a-139">Azure AD 中的服務主體或應用程式</span><span class="sxs-lookup"><span data-stu-id="b9c7a-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="b9c7a-140">在上述的 hello 和設定錯誤的其他執行個體，hello 自動化帳戶會偵測 hello 變更，並顯示狀態為*完整*上 hello**執行身分帳戶**hello 的屬性刀鋒視窗帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![不完整的執行身分帳戶設定狀態](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="b9c7a-142">當您選取執行身分帳戶 hello 時，hello 帳戶**屬性** 窗格會顯示下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="b9c7a-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![不完整的執行身分設定警告訊息](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="b9c7a-144">.</span><span class="sxs-lookup"><span data-stu-id="b9c7a-144">.</span></span>

<span data-ttu-id="b9c7a-145">您可以快速解決這些執行身分帳戶的問題，藉由刪除並重新建立 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9c7a-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9c7a-146">Next steps</span></span>
* <span data-ttu-id="b9c7a-147">如需有關服務主體的詳細資訊，請參閱太[應用程式與服務主體物件](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="b9c7a-148">如需有關在 Azure 自動化中的 角色型存取控制的詳細資訊，請參閱太[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="b9c7a-149">如需有關憑證和 Azure 服務的詳細資訊，請參閱太[Azure 雲端服務憑證概觀](../cloud-services/cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="b9c7a-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
