---
title: "Azure 堆疊上的 App Service 中的 FTP aaaEnable |Microsoft 文件"
description: "Azure 堆疊上的 App Service 中的步驟 toocomplete tooenable FTP"
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
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a><span data-ttu-id="c9c02-103">在 Azure Stack 上的 App Service 中啟用 FTP</span><span class="sxs-lookup"><span data-stu-id="c9c02-103">Enable FTP in App Service on Azure Stack</span></span>

<span data-ttu-id="c9c02-104">一旦您已成功部署 Azure 堆疊上的應用程式服務如果您想 tooenable FTP 發行，以便您的租用戶可以上傳其應用程式檔案和內容，有一些額外的步驟需要 toobe 完成。</span><span class="sxs-lookup"><span data-stu-id="c9c02-104">Once you have successfully deployed App Service on Azure Stack if you wish tooenable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need toobe completed.</span></span>  <span data-ttu-id="c9c02-105">在未來的版本中，這些步驟將自動執行。</span><span class="sxs-lookup"><span data-stu-id="c9c02-105">In future releases these steps will be automated.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c02-106">這些步驟適用於在 Azure Stack 資源提供者上設定 App Service 的服務或企業系統管理員。</span><span class="sxs-lookup"><span data-stu-id="c9c02-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span></span>

## <a name="enable-ftp"></a><span data-ttu-id="c9c02-107">啟用 FTP</span><span class="sxs-lookup"><span data-stu-id="c9c02-107">Enable FTP</span></span>

1.  <span data-ttu-id="c9c02-108">Hello 服務系統管理員身分登入 toohello 堆疊 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c9c02-108">Log in toohello Azure Stack portal as hello service administrator.</span></span>
2.  <span data-ttu-id="c9c02-109">瀏覽過**網路介面**和選取 hello **FTP NIC**下**資源群組** - **AppService 本機**。</span><span class="sxs-lookup"><span data-stu-id="c9c02-109">Browse too**Network interfaces** and select hello **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span></span> <span data-ttu-id="c9c02-110">![Azure Stack 網路介面][1]</span><span class="sxs-lookup"><span data-stu-id="c9c02-110">![Azure Stack Network Interfaces][1]</span></span>
3.  <span data-ttu-id="c9c02-111">請注意 hello**公用 IP 位址**的 hello **FTP NIC**。</span><span class="sxs-lookup"><span data-stu-id="c9c02-111">Note hello **Public IP Address** of hello **FTP-NIC**.</span></span> 
<span data-ttu-id="c9c02-112">![Azure Stack 網路介面詳細資料][2]</span><span class="sxs-lookup"><span data-stu-id="c9c02-112">![Azure Stack Network Interface Details][2]</span></span>
4.  <span data-ttu-id="c9c02-113">下一步瀏覽過**虛擬機器**和選取 hello **FTP0 VM**。</span><span class="sxs-lookup"><span data-stu-id="c9c02-113">Next Browse too**Virtual Machines** and select hello **FTP0-VM**.</span></span> <span data-ttu-id="c9c02-114">![Azure Stack 虛擬機器][3]</span><span class="sxs-lookup"><span data-stu-id="c9c02-114">![Azure Stack Virtual Machines][3]</span></span>
5.  <span data-ttu-id="c9c02-115">開啟 遠端桌面工作階段 toohello VM 使用 hello**連接**按鈕與登入 toohello 工作階段，使用您在應用程式服務部署期間設定的 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="c9c02-115">Open a remote desktop session toohello VM using hello **Connect** button and login toohello session using hello Administrator credentials you set during App Service deployment.</span></span>  
<span data-ttu-id="c9c02-116">![Azure Stack 虛擬機器詳細資料][4]</span><span class="sxs-lookup"><span data-stu-id="c9c02-116">![Azure Stack Virtual Machine Details][4]</span></span>
6.  <span data-ttu-id="c9c02-117">開啟**網際網路資訊服務 (IIS) 管理員**hello FTP VM (FTP0 VM) 上。</span><span class="sxs-lookup"><span data-stu-id="c9c02-117">Open **Internet Information Service (IIS) Manager** on hello FTP VM (FTP0-VM).</span></span>
7.  <span data-ttu-id="c9c02-118">在 [網站] 下，選取 [裝載 FTP 網站]。</span><span class="sxs-lookup"><span data-stu-id="c9c02-118">Under **Sites** select **Hosting FTP Site**.</span></span>
8.  <span data-ttu-id="c9c02-119">開啟 [FTP 防火牆支援]。</span><span class="sxs-lookup"><span data-stu-id="c9c02-119">Open **FTP Firewall Support**.</span></span> <span data-ttu-id="c9c02-120">![App Service FTP0-VM 上的 IIS Manager][5]</span><span class="sxs-lookup"><span data-stu-id="c9c02-120">![IIS Manager on App Service FTP0-VM][5]</span></span>
9.  <span data-ttu-id="c9c02-121">輸入 hello hello FTP NIC 的公用 IP 位址，然後按一下**套用** ![IIS Manager FTP 防火牆支援][6]</span><span class="sxs-lookup"><span data-stu-id="c9c02-121">Enter hello Public IP Address of hello FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span></span>

## <a name="validate-hello-enabling-of-ftp"></a><span data-ttu-id="c9c02-122">驗證 hello 啟用 FTP 的</span><span class="sxs-lookup"><span data-stu-id="c9c02-122">Validate hello enabling of FTP</span></span>

1.  <span data-ttu-id="c9c02-123">登入 toohello 堆疊 Azure 入口網站為 hello 服務管理員或租用戶身分。</span><span class="sxs-lookup"><span data-stu-id="c9c02-123">Log in toohello Azure Stack portal as either hello service administrator or as a tenant.</span></span>
2.  <span data-ttu-id="c9c02-124">瀏覽過**應用程式服務**並選取 Web、 行動裝置或您已建立的應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9c02-124">Browse too**App Services** and select a Web, Mobile, or API App you have created.</span></span> <span data-ttu-id="c9c02-125">![應用程式服務][7]</span><span class="sxs-lookup"><span data-stu-id="c9c02-125">![App Services][7]</span></span>
3.  <span data-ttu-id="c9c02-126">在 hello 應用程式詳細資料請注意 hello **FTP 主機名稱**和**FTP/部署使用者名稱**。</span><span class="sxs-lookup"><span data-stu-id="c9c02-126">In hello application details note hello **FTP Hostname** and **FTP/deployment username**.</span></span> <span data-ttu-id="c9c02-127">![App Service 應用程式詳細資料][8]</span><span class="sxs-lookup"><span data-stu-id="c9c02-127">![App Service App Details][8]</span></span>
> [!NOTE]
> <span data-ttu-id="c9c02-128">如果看不到下的一個項目**FTP/部署使用者名稱**，您必須先使用 hello tooset hello 部署認證**部署認證**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c9c02-128">If you do not see an entry under **FTP/deployment username**, you need tooset hello Deployment credentials first using hello **Deployment Credentials** Blade.</span></span>

4.  <span data-ttu-id="c9c02-129">開啟 Windows 檔案總管中，輸入 hello 檔案網址列，例如 ftp://ftp.appservice.azurestack.local hello FTP 主機名稱</span><span class="sxs-lookup"><span data-stu-id="c9c02-129">Open Windows Explorer, enter hello FTP hostname into hello file address bar for example, ftp://ftp.appservice.azurestack.local</span></span>
5.  <span data-ttu-id="c9c02-130">出現提示時輸入 hello**部署認證**您記下在步驟 3 中，如果已啟用 hello 功能您會看到 hello 應用程式服務應用程式的內容的目錄清單。</span><span class="sxs-lookup"><span data-stu-id="c9c02-130">When prompted enter hello **Deployment credentials** you noted in step 3, if hello feature has been enabled you will see a directory listing of hello app service application's contents.</span></span> <span data-ttu-id="c9c02-131">![FTP 檔案清單][9]</span><span class="sxs-lookup"><span data-stu-id="c9c02-131">![FTP File Listing][9]</span></span>
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
