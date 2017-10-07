---
title: "aaaConfigure 驗證 Amazon Web Services |Microsoft 文件"
description: "本文說明如何 toocreate 及驗證 runbook 在 Azure 自動化中管理 AWS 資源 AWS 認證。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "aws 驗證, 設定 aws"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/11/2016
ms.author: magoedte
ms.openlocfilehash: 6edaa000c1b206d80fe64b18c729dac124849070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a><span data-ttu-id="2622c-104">使用 Amazon Web Services 驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="2622c-104">Authenticate Runbooks with Amazon Web Services</span></span>
<span data-ttu-id="2622c-105">使用 Amazon Web Services (AWS) 中的資源自動執行常見工作可透過 Azure 中的自動化 Runbook 來完成。</span><span class="sxs-lookup"><span data-stu-id="2622c-105">Automating common tasks with resources in Amazon Web Services (AWS) can be accomplished with Automation runbooks in Azure.</span></span>  <span data-ttu-id="2622c-106">您可以和使用 Azure 中的資源一樣，在 AWS 中使用自動化 Runbook 自動執行許多工作。</span><span class="sxs-lookup"><span data-stu-id="2622c-106">You can automate many tasks in AWS using Automation runbooks just like you can with resources in Azure.</span></span>  <span data-ttu-id="2622c-107">所需具備的只有兩項條件︰</span><span class="sxs-lookup"><span data-stu-id="2622c-107">All that is required are two things:</span></span>

* <span data-ttu-id="2622c-108">AWS 訂用帳戶和一組認證。</span><span class="sxs-lookup"><span data-stu-id="2622c-108">An AWS subscription and a set of credentials.</span></span>  <span data-ttu-id="2622c-109">具體而言就是您的 AWS 存取金鑰和秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2622c-109">Specifically your AWS Access Key and Secret Key.</span></span>  <span data-ttu-id="2622c-110">如需詳細資訊，請檢閱 hello 文章[使用 AWS 認證](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html)。</span><span class="sxs-lookup"><span data-stu-id="2622c-110">For more information, please review hello article [Using AWS Credentials](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).</span></span>
* <span data-ttu-id="2622c-111">Azure 訂用帳戶和自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="2622c-111">An Azure subscription and Automation account.</span></span>  <span data-ttu-id="2622c-112">如需設定 Azure 自動化帳戶的詳細資訊，請檢閱 hello 文章[設定 Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。</span><span class="sxs-lookup"><span data-stu-id="2622c-112">For more information on setting up an Azure Automation account, please review hello article [Configure Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>  

<span data-ttu-id="2622c-113">與 AWS tooauthenticate，您必須指定一組 AWS 認證 tooauthenticate 執行來自 Azure 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="2622c-113">tooauthenticate with AWS, you must specify a set of AWS credentials tooauthenticate your runbooks running from Azure Automation.</span></span> <span data-ttu-id="2622c-114">如果您已經建立的自動化帳戶而且想 toouse AWS 與該 tooauthenticate，您可以依照 hello 之後 > 一節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="2622c-114">If you already have an Automation account created and you want toouse that tooauthenticate with AWS, you can follow hello steps in hello following section.</span></span>  <span data-ttu-id="2622c-115">如果您想 toodedicated 帳戶的 runbook 以 AWS 資源時，您應該先建立新[自動化執行身分帳戶](automation-sec-configure-azure-runas-account.md)（略過 hello 選項 toocreate 服務主體），然後遵循下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="2622c-115">If you want toodedicated an account for runbooks targetting AWS resources, you should first create a new [Automation Run As account](automation-sec-configure-azure-runas-account.md) (skip hello option toocreate a service principal) and then follow hello steps below.</span></span>

## <a name="configure-automation-account"></a><span data-ttu-id="2622c-116">設定自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="2622c-116">Configure Automation account</span></span>
<span data-ttu-id="2622c-117">AWS 與 Azure 自動化 toocommunicate，您會先需要 tooretrieve AWS 認證並將其儲存在 Azure 自動化中的資產的方式。</span><span class="sxs-lookup"><span data-stu-id="2622c-117">For Azure Automation toocommunicate with AWS, you will first need tooretrieve your AWS credentials and store them as assets in Azure Automation.</span></span>  <span data-ttu-id="2622c-118">執行 hello hello AWS 文件中所述的步驟[AWS 帳戶管理存取金鑰](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)toocreate 存取金鑰並將複製的 hello**存取金鑰識別碼**和**秘密便捷鍵**(選擇性地下載金鑰檔 toostore 它安全)。</span><span class="sxs-lookup"><span data-stu-id="2622c-118">Perform hello following steps documented in hello AWS document [Managing Access Keys for your AWS Account](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate an Access Key and copy hello **Access Key ID** and **Secret Access Key** (optionally download your key file toostore it somewhere safe).</span></span>

<span data-ttu-id="2622c-119">您已建立且複製 AWS 安全性金鑰之後，您將需要 toocreate 與 Azure 自動化帳戶 toosecurely 認證資產儲存，與您的 runbook 中參考它們。</span><span class="sxs-lookup"><span data-stu-id="2622c-119">After you have created and copied your AWS security keys, you will need toocreate a Credential asset with an Azure Automation account toosecurely store them and reference them with your runbooks.</span></span>  <span data-ttu-id="2622c-120">Hello > 一節中的 hello 步驟**建立新的認證資產**在 hello[認證在 Azure 自動化中的資產](automation-credentials.md)發行項，然後輸入 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="2622c-120">Follow hello steps in hello section **Creating a new credential asset** in hello [Credential assets in Azure Automation](automation-credentials.md) article and enter hello following information:</span></span>

1. <span data-ttu-id="2622c-121">在 hello**名稱**方塊中，輸入**AWScred**或適當的值遵循您命名標準。</span><span class="sxs-lookup"><span data-stu-id="2622c-121">In hello **Name** box, enter **AWScred** or an appropriate value following your naming standards.</span></span>  
2. <span data-ttu-id="2622c-122">在 hello**使用者名稱**方塊中，輸入您**存取識別碼**和您**秘密便捷鍵**在 hello**密碼**和**確認密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="2622c-122">In hello **User name** box type your **Access ID** and your **Secret Access Key** in hello **Password** and **Confirm password** box.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="2622c-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2622c-123">Next steps</span></span>
* <span data-ttu-id="2622c-124">Reivew hello 方案文章[自動 Amazon Web Services 中的 VM 部署](automation-scenario-aws-deployment.md)toolearn toocreate runbook tooautomate AWS 中的工作。</span><span class="sxs-lookup"><span data-stu-id="2622c-124">Reivew hello solution article [Automating deployment of a VM in Amazon Web Services](automation-scenario-aws-deployment.md) toolearn how toocreate runbooks tooautomate tasks in AWS.</span></span>

