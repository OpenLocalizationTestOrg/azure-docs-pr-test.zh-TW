---
title: "疑難排解：建立及連接至機器學習工作區 | Microsoft Docs"
description: "建立及連接 Azure Machine Learning 工作區之常見問題的解決方法"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="1d0cd-103">疑難排解指南：建立及連接至機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="1d0cd-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="1d0cd-104">本指南針對一些在設定 Azure Machine Learning 工作區時常發生的問題，提供解決方案。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="1d0cd-105">工作區擁有者</span><span class="sxs-lookup"><span data-stu-id="1d0cd-105">Workspace owner</span></span>
<span data-ttu-id="1d0cd-106">若要在 Machine Learning Studio 中開啟工作區，您必須使用建立工作區的 Microsoft 帳戶登入，或需要收到來自擁有者的邀請，才能加入工作區。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="1d0cd-107">您可以從 Azure 入口網站管理工作區，其中包括設定存取的能力。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="1d0cd-108">如需管理工作區的詳細資訊，請參閱 [管理 Azure Machine Learning 工作區]。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="1d0cd-109">[管理 Azure Machine Learning 工作區]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="1d0cd-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="1d0cd-110">允許區域</span><span class="sxs-lookup"><span data-stu-id="1d0cd-110">Allowed regions</span></span>
<span data-ttu-id="1d0cd-111">機器學習服務目前可用於數量有限的區域。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="1d0cd-112">如果您的訂用帳戶並未包含這其中一個區域，您可能會看見錯誤訊息「您在允許的區域中沒有任何訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="1d0cd-113">為了要求將區域新增至您的訂用帳戶，請從 Azure 入口網站中建立新的 Microsoft 支援要求，選取 [計費] 做為問題類型，並遵照提示來提交您的要求。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="1d0cd-114">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1d0cd-114">Storage account</span></span>
<span data-ttu-id="1d0cd-115">機器學習服務需要儲存體帳戶來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="1d0cd-116">您可以使用現有的儲存體帳戶，或是在建立新的機器學習服務工作區時建立新的儲存體帳戶 (如果您有建立新儲存體帳戶的配額)。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="1d0cd-117">新的 Machine Learning 工作區建立完成後，您可以使用建立工作區的 Microsoft 帳戶登入 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="1d0cd-118">如果您遇到錯誤訊息「找不到工作區」(類似於下列螢幕擷取畫面)，請使用下列步驟來刪除您的瀏覽器 Cookie。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![找不到工作區][screen3]

<span data-ttu-id="1d0cd-120">**刪除瀏覽器 Cookie**</span><span class="sxs-lookup"><span data-stu-id="1d0cd-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="1d0cd-121">如果您是使用 Internet Explorer，請按一下右上角的 [工具] 按鈕，然後選取 [網際網路選項]。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![網際網路選項][screen4]

2. <span data-ttu-id="1d0cd-123">在 [一般] 索引標籤下，按一下 [刪除...]</span><span class="sxs-lookup"><span data-stu-id="1d0cd-123">Under the **General** tab, click **Delete…**</span></span>

![[一般] 索引標籤][screen5]

3. <span data-ttu-id="1d0cd-125">在 [刪除瀏覽歷程記錄] 對話方塊中，確定已選取 [Cookie 與網站資料]，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![刪除 cookie][screen6]

<span data-ttu-id="1d0cd-127">刪除 Cookie 之後，請重新啟動瀏覽器，然後前往 [Microsoft Azure Machine Learning](https://studio.azureml.net) 頁面。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="1d0cd-128">出現輸入使用者名稱和密碼的提示時，請輸入建立工作區所使用的同一個 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="1d0cd-129">註解</span><span class="sxs-lookup"><span data-stu-id="1d0cd-129">Comments</span></span>

<span data-ttu-id="1d0cd-130">我們的目標是讓機器學習服務經驗盡可能完美。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="1d0cd-131">請將任何建議或問題貼在 [Azure Machine Learning 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) 中，以協助我們為您提供更好的服務。</span><span class="sxs-lookup"><span data-stu-id="1d0cd-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
