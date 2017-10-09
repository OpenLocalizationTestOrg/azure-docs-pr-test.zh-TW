---
title: "部署 Azure 堆疊上的應用程式服務的 aaaBefore |Microsoft 文件"
description: "部署 Azure 堆疊上的應用程式服務之前的步驟 toocomplete"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="207c6-103">開始使用 Azure Stack 上的 App Service 之前</span><span class="sxs-lookup"><span data-stu-id="207c6-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="207c6-104">您需要幾個項目 tooinstall Azure 堆疊上的 Azure 應用程式服務：</span><span class="sxs-lookup"><span data-stu-id="207c6-104">You need a few items tooinstall Azure App Service on Azure Stack:</span></span>

- <span data-ttu-id="207c6-105">已完成的部署的 hello [Azure 堆疊開發套件](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="207c6-105">A completed deployment of hello [Azure Stack development kit](azure-stack-run-powershell-script.md).</span></span>
- <span data-ttu-id="207c6-106">您的 Azure Stack 系統中有足夠空間可供 Azure Stack 上之 App Service 的小型部署使用。</span><span class="sxs-lookup"><span data-stu-id="207c6-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="207c6-107">hello 所需空間大約是 20 GB 的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="207c6-107">hello required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="207c6-108">當您針對 Azure Stack 上的 App Service 建立虛擬機器時要使用的 Windows Server VM 映像。</span><span class="sxs-lookup"><span data-stu-id="207c6-108">A Windows Server VM image for use when you create virtual machines for App Service on Azure Stack.</span></span>
- <span data-ttu-id="207c6-109">[執行 SQL Server 的伺服器](#SQL-Server)。</span><span class="sxs-lookup"><span data-stu-id="207c6-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="207c6-110">下列步驟 hello*所有*hello Azure 堆疊主機電腦上的進行。</span><span class="sxs-lookup"><span data-stu-id="207c6-110">hello following steps *all* take place on hello Azure Stack host machine.</span></span>

<span data-ttu-id="207c6-111">toodeploy 資源提供者，您必須以系統管理員身分執行 hello PowerShell 整合式指令碼環境 (ISE)。</span><span class="sxs-lookup"><span data-stu-id="207c6-111">toodeploy a resource provider, you must run hello PowerShell Integrated Scripting Environment (ISE) as an administrator.</span></span> <span data-ttu-id="207c6-112">基於這個理由，您需要 tooallow cookie 和 JavaScript 中，您會使用 toosign tooAzure Active Directory 中的 hello Internet Explorer 設定檔。</span><span class="sxs-lookup"><span data-stu-id="207c6-112">For this reason, you need tooallow cookies and JavaScript in hello Internet Explorer profile that you use toosign in tooAzure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="207c6-113">關閉 Internet Explorer 增強式安全性</span><span class="sxs-lookup"><span data-stu-id="207c6-113">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="207c6-114">登入 toohello Azure 堆疊開發套件的電腦**AzureStack/系統管理員**，然後開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="207c6-114">Sign in toohello Azure Stack development kit machine as **AzureStack/administrator**, and then open **Server Manager**.</span></span>

2.  <span data-ttu-id="207c6-115">針對系統管理員和使用者關閉 [Internet Explorer 增強式安全性設定]。</span><span class="sxs-lookup"><span data-stu-id="207c6-115">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

3.  <span data-ttu-id="207c6-116">登入 toohello 身為管理員，Azure 堆疊開發套件電腦，然後開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="207c6-116">Sign in toohello Azure Stack development kit machine as an administrator, and then open **Server Manager**.</span></span>

4.  <span data-ttu-id="207c6-117">針對系統管理員和使用者關閉 [Internet Explorer 增強式安全性設定]。</span><span class="sxs-lookup"><span data-stu-id="207c6-117">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="207c6-118">啟用 Cookie</span><span class="sxs-lookup"><span data-stu-id="207c6-118">Enable cookies</span></span>

1.  <span data-ttu-id="207c6-119">選取 [開始] > [所有應用程式] > [Windows 附屬應用程式]。</span><span class="sxs-lookup"><span data-stu-id="207c6-119">Select **Start** > **All apps** > **Windows accessories**.</span></span> <span data-ttu-id="207c6-120">以滑鼠右鍵按一下 [Internet Explorer] > [更多] > [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="207c6-120">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>

2.  <span data-ttu-id="207c6-121">出現提示時，選取 [使用建議的安全性]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="207c6-121">If you're prompted, select **Use recommended security**, and then select **OK**.</span></span>

3.  <span data-ttu-id="207c6-122">在 Internet Explorer 中，選取**工具**（hello 齒輪圖示） >**網際網路選項** > **隱私權** > **進階**.</span><span class="sxs-lookup"><span data-stu-id="207c6-122">In Internet Explorer, select **Tools** (hello gear icon) > **Internet Options** > **Privacy** > **Advanced**.</span></span>

4.  <span data-ttu-id="207c6-123">選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="207c6-123">Select **Advanced**.</span></span> <span data-ttu-id="207c6-124">確定已選取兩個 [接受] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="207c6-124">Make sure that both **Accept** check boxes are selected.</span></span> <span data-ttu-id="207c6-125">選取 [確定] 兩次。</span><span class="sxs-lookup"><span data-stu-id="207c6-125">Select **OK** twice.</span></span>

5.  <span data-ttu-id="207c6-126">關閉 Internet Explorer，然後重新啟動 hello 身為系統管理員的 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="207c6-126">Close Internet Explorer, and restart hello PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="207c6-127">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="207c6-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="207c6-128">tooinstall PowerShell for Azure 堆疊，請依照下列中的 hello 步驟[安裝 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="207c6-128">tooinstall PowerShell for Azure Stack, follow hello steps in [Install PowerShell](azure-stack-powershell-install.md).</span></span>

## <a name="use-visual-studio-with-azure-stack"></a><span data-ttu-id="207c6-129">搭配 Azure Stack 使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="207c6-129">Use Visual Studio with Azure Stack</span></span>

<span data-ttu-id="207c6-130">toouse Visual Studio 和 Azure 堆疊，請依照下列中的 hello 步驟[安裝 Visual Studio](azure-stack-install-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="207c6-130">toouse Visual Studio with Azure Stack, follow hello steps in [Install Visual Studio](azure-stack-install-visual-studio.md).</span></span>

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a><span data-ttu-id="207c6-131">新增 Windows Server 2016 VM 映像 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="207c6-131">Add a Windows Server 2016 VM image tooAzure Stack</span></span>

<span data-ttu-id="207c6-132">由於 App Service 會部署一些虛擬機器，因此，它需要 Azure Stack 中的 Windows Server 2016 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="207c6-132">Because App Service deploys a number of virtual machines, it requires a Windows Server 2016 VM image in Azure Stack.</span></span> <span data-ttu-id="207c6-133">tooinstall VM 映像，請依照下列中的 hello 步驟[新增預設虛擬機器映像](azure-stack-add-default-image.md)。</span><span class="sxs-lookup"><span data-stu-id="207c6-133">tooinstall a VM image, follow hello steps in [Add a default virtual machine image](azure-stack-add-default-image.md).</span></span>

## <span data-ttu-id="207c6-134"><a name="SQL-Server"></a>SQL Server</span><span class="sxs-lookup"><span data-stu-id="207c6-134"><a name="SQL-Server"></a>SQL Server</span></span>

<span data-ttu-id="207c6-135">Azure 堆疊上的應用程式服務需要存取 tooa SQL Server 執行個體 toocreate 和主機兩個資料庫 toorun hello 應用程式服務資源提供者。</span><span class="sxs-lookup"><span data-stu-id="207c6-135">App Service on Azure Stack requires access tooa SQL Server instance toocreate and host two databases toorun hello App Service resource provider.</span></span>  <span data-ttu-id="207c6-136">您應該選擇 toodeploy hello SQL 連線層級設定得必須 Azure 堆疊上的 SQL Server VM**公用**。</span><span class="sxs-lookup"><span data-stu-id="207c6-136">Should you choose toodeploy a SQL Server VM on Azure Stack it must have hello SQL connectivity level set too**Public**.</span></span>  <span data-ttu-id="207c6-137">當您完成 hello 應用程式服務在 Azure 堆疊安裝程式中的 hello 選項時，您可以選擇 hello SQL Server 執行個體 toouse。</span><span class="sxs-lookup"><span data-stu-id="207c6-137">You can choose hello SQL Server instance toouse when you complete hello options in hello App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="207c6-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="207c6-138">Next steps</span></span>

- <span data-ttu-id="207c6-139">[安裝應用程式服務資源提供者 hello](azure-stack-app-service-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="207c6-139">[Install hello App Service resource provider](azure-stack-app-service-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
