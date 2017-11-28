---
title: "疑難排解： 建立和連線 tooa Machine Learning 工作區 |Microsoft 文件"
description: "建立及連接 tooan Azure Machine Learning 工作區中常見的問題的解決方案"
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
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="aa84c-103">疑難排解指南： 建立和連線 tooan Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="aa84c-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="aa84c-104">本指南針對一些在設定 Azure Machine Learning 工作區時常發生的問題，提供解決方案。</span><span class="sxs-lookup"><span data-stu-id="aa84c-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="aa84c-105">工作區擁有者</span><span class="sxs-lookup"><span data-stu-id="aa84c-105">Workspace owner</span></span>
<span data-ttu-id="aa84c-106">tooopen Machine Learning Studio 中的工作區，您必須在 toohello Microsoft 帳戶登入使用 toocreate hello 工作區中，或者您需要 tooreceive 從 hello 擁有者 toojoin hello 工作區的邀請。</span><span class="sxs-lookup"><span data-stu-id="aa84c-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="aa84c-107">從 hello Azure 入口網站中，您可以管理 hello 工作區，其中包括 hello 能力 tooconfigure 存取。</span><span class="sxs-lookup"><span data-stu-id="aa84c-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="aa84c-108">如需管理工作區的詳細資訊，請參閱 [管理 Azure Machine Learning 工作區]。</span><span class="sxs-lookup"><span data-stu-id="aa84c-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[管理 Azure Machine Learning 工作區]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="aa84c-110">允許區域</span><span class="sxs-lookup"><span data-stu-id="aa84c-110">Allowed regions</span></span>
<span data-ttu-id="aa84c-111">機器學習服務目前可用於數量有限的區域。</span><span class="sxs-lookup"><span data-stu-id="aa84c-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="aa84c-112">如果您的訂用帳戶不包含的其中一個這些區域，您可能會看見 hello 錯誤訊息，「 您有任何訂用帳戶中允許區域的 hello。 」</span><span class="sxs-lookup"><span data-stu-id="aa84c-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="aa84c-113">toorequest 區域是加入 tooyour 訂用帳戶，從 hello Azure 入口網站建立新的 Microsoft 支援要求，選擇**計費**為 hello 問題類型，然後遵循 hello 會提示 toosubmit 您的要求。</span><span class="sxs-lookup"><span data-stu-id="aa84c-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="aa84c-114">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="aa84c-114">Storage account</span></span>
<span data-ttu-id="aa84c-115">hello 機器學習服務需要儲存體帳戶 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="aa84c-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="aa84c-116">您可以使用現有的儲存體帳戶，或當您建立 hello 新 Machine Learning 工作區 （如果有配額 toocreate 新的儲存體帳戶） 時，您可以建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa84c-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="aa84c-117">Hello 新 Machine Learning 工作區建立之後，您可以使用您用 toocreate hello 工作區中的 hello Microsoft 帳戶登入 tooMachine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="aa84c-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="aa84c-118">如果您遇到 hello 錯誤訊息，「 工作區中找不到 」 (類似 toohello 下列螢幕擷取畫面)，請使用下列步驟 toodelete hello 瀏覽器 cookie。</span><span class="sxs-lookup"><span data-stu-id="aa84c-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![找不到工作區][screen3]

<span data-ttu-id="aa84c-120">**toodelete 瀏覽器 cookie**</span><span class="sxs-lookup"><span data-stu-id="aa84c-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="aa84c-121">如果您使用 Internet Explorer，請按一下 hello**工具**hello 右上角的按鈕，然後選取**網際網路選項**。</span><span class="sxs-lookup"><span data-stu-id="aa84c-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![網際網路選項][screen4]

2. <span data-ttu-id="aa84c-123">在 hello**一般**索引標籤上，按一下 **刪除...**</span><span class="sxs-lookup"><span data-stu-id="aa84c-123">Under hello **General** tab, click **Delete…**</span></span>

![[一般] 索引標籤][screen5]

3. <span data-ttu-id="aa84c-125">在 hello**刪除瀏覽歷程記錄**對話方塊方塊中，請確定**Cookie 和網站資料**已選取，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="aa84c-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![刪除 cookie][screen6]

<span data-ttu-id="aa84c-127">刪除 hello cookie 之後，重新啟動 hello 瀏覽器並前往 toohello [Microsoft Azure Machine Learning](https://studio.azureml.net)頁面。</span><span class="sxs-lookup"><span data-stu-id="aa84c-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="aa84c-128">當系統提示您輸入使用者名稱和密碼，hello 用 toocreate hello 工作區相同的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa84c-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="aa84c-129">註解</span><span class="sxs-lookup"><span data-stu-id="aa84c-129">Comments</span></span>

<span data-ttu-id="aa84c-130">我們的目標是 toomake hello 的緊密性越好的機器學習經驗。</span><span class="sxs-lookup"><span data-stu-id="aa84c-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="aa84c-131">請將任何註解和問題張貼在 hello [Azure Machine Learning 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)toohelp 我們提供的服務更好。</span><span class="sxs-lookup"><span data-stu-id="aa84c-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
