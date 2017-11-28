---
title: "在 Azure Stack 上部署 App Service 之前 | Microsoft Docs"
description: "在 Azure Stack 上部署 App Service 之前必須完成的步驟"
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
ms.openlocfilehash: 3cba11acc6279f24d0a47af8978610180724c0a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="b66e5-103">開始使用 Azure Stack 上的 App Service 之前</span><span class="sxs-lookup"><span data-stu-id="b66e5-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="b66e5-104">您需要一些項目，才能在 Azure Stack 上安裝 Azure App Service：</span><span class="sxs-lookup"><span data-stu-id="b66e5-104">You need a few items to install Azure App Service on Azure Stack:</span></span>

- <span data-ttu-id="b66e5-105">完成部署 [Azure Stack 開發套件](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="b66e5-105">A completed deployment of the [Azure Stack development kit](azure-stack-run-powershell-script.md).</span></span>
- <span data-ttu-id="b66e5-106">您的 Azure Stack 系統中有足夠空間可供 Azure Stack 上之 App Service 的小型部署使用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="b66e5-107">所需空間大約是 20 GB 的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="b66e5-107">The required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="b66e5-108">當您針對 Azure Stack 上的 App Service 建立虛擬機器時要使用的 Windows Server VM 映像。</span><span class="sxs-lookup"><span data-stu-id="b66e5-108">A Windows Server VM image for use when you create virtual machines for App Service on Azure Stack.</span></span>
- <span data-ttu-id="b66e5-109">[執行 SQL Server 的伺服器](#SQL-Server)。</span><span class="sxs-lookup"><span data-stu-id="b66e5-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="b66e5-110">下列步驟*全*都會在 Azure Stack 主機電腦上進行。</span><span class="sxs-lookup"><span data-stu-id="b66e5-110">The following steps *all* take place on the Azure Stack host machine.</span></span>

<span data-ttu-id="b66e5-111">若要部署資源提供者，您必須以系統管理員身分執行 PowerShell 整合式指令碼環境 (ISE)。</span><span class="sxs-lookup"><span data-stu-id="b66e5-111">To deploy a resource provider, you must run the PowerShell Integrated Scripting Environment (ISE) as an administrator.</span></span> <span data-ttu-id="b66e5-112">基於這個理由，您需要在用於登入 Azure Active Directory 的 Internet Explorer 設定檔允許 Cookie 和 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="b66e5-112">For this reason, you need to allow cookies and JavaScript in the Internet Explorer profile that you use to sign in to Azure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="b66e5-113">關閉 Internet Explorer 增強式安全性</span><span class="sxs-lookup"><span data-stu-id="b66e5-113">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="b66e5-114">以 **AzureStack/administrator** 身分登入 Azure Stack 開發套件機器，然後開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-114">Sign in to the Azure Stack development kit machine as **AzureStack/administrator**, and then open **Server Manager**.</span></span>

2.  <span data-ttu-id="b66e5-115">針對系統管理員和使用者關閉 [Internet Explorer 增強式安全性設定]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-115">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

3.  <span data-ttu-id="b66e5-116">以系統管理員身分登入 Azure Stack 開發套件機器，然後開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-116">Sign in to the Azure Stack development kit machine as an administrator, and then open **Server Manager**.</span></span>

4.  <span data-ttu-id="b66e5-117">針對系統管理員和使用者關閉 [Internet Explorer 增強式安全性設定]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-117">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="b66e5-118">啟用 Cookie</span><span class="sxs-lookup"><span data-stu-id="b66e5-118">Enable cookies</span></span>

1.  <span data-ttu-id="b66e5-119">選取 [開始] > [所有應用程式] > [Windows 附屬應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-119">Select **Start** > **All apps** > **Windows accessories**.</span></span> <span data-ttu-id="b66e5-120">以滑鼠右鍵按一下 [Internet Explorer] > [更多] > [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-120">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>

2.  <span data-ttu-id="b66e5-121">出現提示時，選取 [使用建議的安全性]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-121">If you're prompted, select **Use recommended security**, and then select **OK**.</span></span>

3.  <span data-ttu-id="b66e5-122">在 Internet Explorer 中，選取 [工具] \(齒輪圖示) > [網際網路選項] > [隱私權] > [進階]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-122">In Internet Explorer, select **Tools** (the gear icon) > **Internet Options** > **Privacy** > **Advanced**.</span></span>

4.  <span data-ttu-id="b66e5-123">選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-123">Select **Advanced**.</span></span> <span data-ttu-id="b66e5-124">確定已選取兩個 [接受] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b66e5-124">Make sure that both **Accept** check boxes are selected.</span></span> <span data-ttu-id="b66e5-125">選取 [確定] 兩次。</span><span class="sxs-lookup"><span data-stu-id="b66e5-125">Select **OK** twice.</span></span>

5.  <span data-ttu-id="b66e5-126">關閉 Internet Explorer，然後以系統管理員身分重新啟動 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="b66e5-126">Close Internet Explorer, and restart the PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="b66e5-127">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="b66e5-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="b66e5-128">若要安裝適用於 Azure Stack 的 PowerShell，請依照[安裝 PowerShell](azure-stack-powershell-install.md) 中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="b66e5-128">To install PowerShell for Azure Stack, follow the steps in [Install PowerShell](azure-stack-powershell-install.md).</span></span>

## <a name="use-visual-studio-with-azure-stack"></a><span data-ttu-id="b66e5-129">搭配 Azure Stack 使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b66e5-129">Use Visual Studio with Azure Stack</span></span>

<span data-ttu-id="b66e5-130">若要搭配 Azure Stack 使用 Visual Studio，請依照[安裝 Visual Studio](azure-stack-install-visual-studio.md) 中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="b66e5-130">To use Visual Studio with Azure Stack, follow the steps in [Install Visual Studio](azure-stack-install-visual-studio.md).</span></span>

## <a name="add-a-windows-server-2016-vm-image-to-azure-stack"></a><span data-ttu-id="b66e5-131">將 Windows Server 2016 VM 映像新增到 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b66e5-131">Add a Windows Server 2016 VM image to Azure Stack</span></span>

<span data-ttu-id="b66e5-132">由於 App Service 會部署一些虛擬機器，因此，它需要 Azure Stack 中的 Windows Server 2016 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="b66e5-132">Because App Service deploys a number of virtual machines, it requires a Windows Server 2016 VM image in Azure Stack.</span></span> <span data-ttu-id="b66e5-133">若要安裝 VM 映像，請依照[新增預設虛擬機器映像](azure-stack-add-default-image.md)中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="b66e5-133">To install a VM image, follow the steps in [Add a default virtual machine image](azure-stack-add-default-image.md).</span></span>

## <span data-ttu-id="b66e5-134"><a name="SQL-Server"></a>SQL Server</span><span class="sxs-lookup"><span data-stu-id="b66e5-134"><a name="SQL-Server"></a>SQL Server</span></span>

<span data-ttu-id="b66e5-135">Azure Stack 上的 App Service 需要存取 SQL Server 執行個體，以建立及裝載兩個資料庫來執行 App Service 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="b66e5-135">App Service on Azure Stack requires access to a SQL Server instance to create and host two databases to run the App Service resource provider.</span></span>  <span data-ttu-id="b66e5-136">如果您選擇在 Azure Stack 上部署 SQL Server VM，則它必須將 SQL 連接性層級設定為 [公用]。</span><span class="sxs-lookup"><span data-stu-id="b66e5-136">Should you choose to deploy a SQL Server VM on Azure Stack it must have the SQL connectivity level set to **Public**.</span></span>  <span data-ttu-id="b66e5-137">您可以選擇在完成 Azure Stack 上之 App Service 安裝程式中的選項時要使用的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b66e5-137">You can choose the SQL Server instance to use when you complete the options in the App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b66e5-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b66e5-138">Next steps</span></span>

- <span data-ttu-id="b66e5-139">[安裝 App Service 資源提供者](azure-stack-app-service-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="b66e5-139">[Install the App Service resource provider](azure-stack-app-service-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
