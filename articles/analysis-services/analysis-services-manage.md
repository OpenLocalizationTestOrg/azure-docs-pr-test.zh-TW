---
title: "Azure Analysis Services aaaManage |Microsoft 文件"
description: "了解如何 toomanage Analysis Services 在 Azure 中的伺服器。"
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
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="935ae-103">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="935ae-103">Manage Analysis Services</span></span>
<span data-ttu-id="935ae-104">一旦您已在 Azure 中建立 Analysis Services 伺服器，可能有某些管理工作，您需要立即 tooperform 或向下一段時間的 hello 路段圖。</span><span class="sxs-lookup"><span data-stu-id="935ae-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="935ae-105">例如，執行處理 toohello 重新整理資料，控制可以存取您的伺服器上的 hello 模型或監視伺服器之健全狀況。</span><span class="sxs-lookup"><span data-stu-id="935ae-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="935ae-106">有些管理工作只能在 Azure 入口網站中執行，有些只能在 SQL Server Management Studio (SSMS) 中執行，也有些工作可以在這兩個位置中執行。</span><span class="sxs-lookup"><span data-stu-id="935ae-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="935ae-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="935ae-107">Azure portal</span></span>
<span data-ttu-id="935ae-108">[Azure 入口網站](http://portal.azure.com/)是您可以建立和刪除伺服器、 監視伺服器的資源、 變更大小和位置管理誰存取 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="935ae-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="935ae-109">如果您有一些問題，也可以提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="935ae-109">If you're having some problems, you can also submit a support request.</span></span>

![在 Azure 中取得伺服器名稱](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="935ae-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="935ae-111">SQL Server Management Studio</span></span>
<span data-ttu-id="935ae-112">在 Azure 中的 tooyour 伺服器連線，就如同連接 tooa 您組織中的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="935ae-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="935ae-113">從 SSMS，您可以執行許多相同工作，例如處理序資料或建立處理指令碼、 管理角色，以及使用 PowerShell 的 hello。</span><span class="sxs-lookup"><span data-stu-id="935ae-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="935ae-115">下載並安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="935ae-115">Download and install SSMS</span></span>
<span data-ttu-id="935ae-116">tooget 所有 hello 最新的功能和 hello 流暢體驗連接 tooyour Azure Analysis Services 伺服器時，請確定您使用 hello 最新版本的 SSMS。</span><span class="sxs-lookup"><span data-stu-id="935ae-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="935ae-117">[下載 SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="935ae-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="935ae-118">使用 SSMS tooconnect</span><span class="sxs-lookup"><span data-stu-id="935ae-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="935ae-119">當使用 SSMS 連接 tooyour 伺服器 hello 第一次之前，請確定 hello Analysis Services 系統管理員群組中包含您的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="935ae-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="935ae-120">詳細資訊，請參閱 toolearn [Server 系統管理員](#server-administrators)本文稍後。</span><span class="sxs-lookup"><span data-stu-id="935ae-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="935ae-121">在連接之前，您會需要 tooget hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="935ae-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="935ae-122">在**Azure 入口網站**> 伺服器 >**概觀** > **伺服器名稱**，複製 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="935ae-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="935ae-124">在 SSMS > [物件總管] 中，按一下 [連線]  > [分析服務] 。</span><span class="sxs-lookup"><span data-stu-id="935ae-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="935ae-125">在 hello**連接 tooServer**對話方塊中，貼上在 hello 伺服器名稱，然後在**驗證**，選擇其中一個 hello 下列驗證類型：</span><span class="sxs-lookup"><span data-stu-id="935ae-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="935ae-126">**Windows 驗證**toouse 您的 Windows 網域 \ 使用者名稱和密碼認證。</span><span class="sxs-lookup"><span data-stu-id="935ae-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="935ae-127">**Active Directory 密碼驗證**toouse 組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="935ae-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="935ae-128">例如，當從未加入網域的電腦連線時。</span><span class="sxs-lookup"><span data-stu-id="935ae-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="935ae-129">**Active Directory 通用驗證**toouse[非互動式或多重要素驗證](../sql-database/sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="935ae-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![在 SSMS 中連線](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="935ae-131">伺服器管理員和資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="935ae-131">Server administrators and database users</span></span>
<span data-ttu-id="935ae-132">在 Azure Analysis Services 中，有兩種類型的使用者：伺服器管理員和資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="935ae-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="935ae-133">這兩種類型的使用者都必須位於 Azure Active Directory 中，而且必須由組織的電子郵件地址或 UPN 指定。</span><span class="sxs-lookup"><span data-stu-id="935ae-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="935ae-134">詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。</span><span class="sxs-lookup"><span data-stu-id="935ae-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="935ae-135">連接問題的疑難排解</span><span class="sxs-lookup"><span data-stu-id="935ae-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="935ae-136">如果您遇到問題，請使用 SSMS 中的 連線時，您可能需要 tooclear hello 登入快取。</span><span class="sxs-lookup"><span data-stu-id="935ae-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="935ae-137">沒有快取的 toodisc。</span><span class="sxs-lookup"><span data-stu-id="935ae-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="935ae-138">tooclear hello 快取中，關閉並重新啟動 hello 連接處理程序。</span><span class="sxs-lookup"><span data-stu-id="935ae-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="935ae-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="935ae-139">Next steps</span></span>
<span data-ttu-id="935ae-140">如果您未部署表格式模型 tooyour 新的伺服器，現在是很好的時間。</span><span class="sxs-lookup"><span data-stu-id="935ae-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="935ae-141">詳細資訊，請參閱 toolearn[部署 tooAzure Analysis Services](analysis-services-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="935ae-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="935ae-142">如果您已部署模型 tooyour 伺服器，您已準備好 tooconnect tooit 使用用戶端或瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="935ae-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="935ae-143">詳細資訊，請參閱 toolearn[從 Azure Analysis Services 伺服器取得資料](analysis-services-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="935ae-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

