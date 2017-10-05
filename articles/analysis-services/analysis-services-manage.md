---
title: "管理 Azure Analysis Services | Microsoft Docs"
description: "瞭解如何以 Azure 管理 Analysis Services 伺服器。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="86988-103">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="86988-103">Manage Analysis Services</span></span>
<span data-ttu-id="86988-104">在 Azure 中建立 Analysis Services 伺服器之後，會有一些您必須立即或稍後執行的管理工作。</span><span class="sxs-lookup"><span data-stu-id="86988-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="86988-105">例如：執行資料重新整理處理作業、控制誰能夠存取您伺服器上的模型，或監視伺服器的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="86988-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="86988-106">有些管理工作只能在 Azure 入口網站中執行，有些只能在 SQL Server Management Studio (SSMS) 中執行，也有些工作可以在這兩個位置中執行。</span><span class="sxs-lookup"><span data-stu-id="86988-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="86988-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="86988-107">Azure portal</span></span>
<span data-ttu-id="86988-108">[Azure 入口網站](http://portal.azure.com/)可讓您建立與刪除伺服器、監視伺服器資源、變更大小，以及管理誰能夠存取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="86988-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="86988-109">如果您有一些問題，也可以提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="86988-109">If you're having some problems, you can also submit a support request.</span></span>

![在 Azure 中取得伺服器名稱](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="86988-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="86988-111">SQL Server Management Studio</span></span>
<span data-ttu-id="86988-112">在 Azure 中連線到您的伺服器，就如同連線到您自己組織中的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="86988-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="86988-113">您可從 SSMS 執行許多相同的工作，例如處理資料或建立處理指令碼、管理角色，以及使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="86988-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="86988-115">下載並安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="86988-115">Download and install SSMS</span></span>
<span data-ttu-id="86988-116">若要取得所有最新功能，並在連接到 Azure Analysis Services 伺服器時獲得最順暢的體驗，請確定您使用的是最新版的 SSMS。</span><span class="sxs-lookup"><span data-stu-id="86988-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="86988-117">[下載 SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="86988-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="86988-118">以 SSMS 連線</span><span class="sxs-lookup"><span data-stu-id="86988-118">To connect with SSMS</span></span>
 <span data-ttu-id="86988-119">使用 SSMS 時，請在第一次連線到您伺服器之前，先確定您的使用者名稱包含在「Analysis Services 管理員」群組中。</span><span class="sxs-lookup"><span data-stu-id="86988-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="86988-120">若要深入了解，請參閱本文稍後的[伺服器管理員](#server-administrators)。</span><span class="sxs-lookup"><span data-stu-id="86988-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="86988-121">連線之前，您必須先取得伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="86988-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="86988-122">在 [Azure 入口網站] > 伺服器 > [概觀]  >  [伺服器名稱] 中，複製伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="86988-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="86988-124">在 SSMS > [物件總管] 中，按一下 [連線]  > [分析服務] 。</span><span class="sxs-lookup"><span data-stu-id="86988-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="86988-125">在 [連線至伺服器] 對話方塊中，貼上伺服器名稱，然後在 [驗證] 中，選擇下列其中一種驗證類型：</span><span class="sxs-lookup"><span data-stu-id="86988-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="86988-126">[Windows 驗證] 以使用您的 Windows 網域\使用者名稱和密碼認證。</span><span class="sxs-lookup"><span data-stu-id="86988-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="86988-127">[Active Directory 密碼驗證] 以使用組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="86988-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="86988-128">例如，當從未加入網域的電腦連線時。</span><span class="sxs-lookup"><span data-stu-id="86988-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="86988-129">[Active Directory 通用驗證] 以使用[非互動式或多重要素驗證](../sql-database/sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="86988-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![在 SSMS 中連線](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="86988-131">伺服器管理員和資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="86988-131">Server administrators and database users</span></span>
<span data-ttu-id="86988-132">在 Azure Analysis Services 中，有兩種類型的使用者：伺服器管理員和資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="86988-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="86988-133">這兩種類型的使用者都必須位於 Azure Active Directory 中，而且必須由組織的電子郵件地址或 UPN 指定。</span><span class="sxs-lookup"><span data-stu-id="86988-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="86988-134">若要深入了解，請參閱[驗證和使用者權限](analysis-services-manage-users.md)。</span><span class="sxs-lookup"><span data-stu-id="86988-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="86988-135">連接問題的疑難排解</span><span class="sxs-lookup"><span data-stu-id="86988-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="86988-136">使用 SSMS 進行連線時，如果遇到問題，您可能需要清除登入快取。</span><span class="sxs-lookup"><span data-stu-id="86988-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="86988-137">系統不會將任何資料快取到磁碟。若要清除快取，請將連線程序關閉並重新啟動。</span><span class="sxs-lookup"><span data-stu-id="86988-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="86988-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86988-138">Next steps</span></span>
<span data-ttu-id="86988-139">如果您尚未將表格式模型部署到新伺服器，現在正是時候。</span><span class="sxs-lookup"><span data-stu-id="86988-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="86988-140">若要深入了解，請參閱 [Deploy to Azure Analysis Services](analysis-services-deploy.md) (部署至 Azure Analysis Services)。</span><span class="sxs-lookup"><span data-stu-id="86988-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="86988-141">如果您已將模型部署至您的伺服器，您便可以透過用戶端或瀏覽器與伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="86988-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="86988-142">若要深入了解，請參閱 [Get data from Azure Analysis Services server](analysis-services-connect.md) (從 Azure Analysis Services 伺服器取得資料)。</span><span class="sxs-lookup"><span data-stu-id="86988-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

