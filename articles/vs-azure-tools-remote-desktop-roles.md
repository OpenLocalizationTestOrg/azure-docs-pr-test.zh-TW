---
title: "透過 Azure 角色的遠端桌面 aaaUsing |Microsoft 文件"
description: "搭配使用遠端桌面與 Azure 角色"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="f8027-103">搭配使用遠端桌面與 Azure 角色</span><span class="sxs-lookup"><span data-stu-id="f8027-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="f8027-104">使用 hello Azure SDK 和遠端桌面服務，您可以存取 Azure 角色和 Azure 託管的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8027-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="f8027-105">在 Visual Studio 中，您可以從 Azure 雲端服務專案設定遠端桌面服務。</span><span class="sxs-lookup"><span data-stu-id="f8027-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="f8027-106">tooenable 遠端桌面服務，您必須建立工作專案包含一個或多個角色，然後將它發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="f8027-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8027-107">您應該只基於疑難排解或開發目的來存取 Azure 角色。</span><span class="sxs-lookup"><span data-stu-id="f8027-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="f8027-108">hello 每個虛擬機器的用途是 toorun Azure 應用程式中，不 toorun 特定角色的其他用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8027-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="f8027-109">如果您想 toouse Azure toohost 可用於任何用途的虛擬機器，請參閱 < 從伺服器總管存取 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8027-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="f8027-110">tooenable 以及 Azure 角色使用遠端桌面</span><span class="sxs-lookup"><span data-stu-id="f8027-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="f8027-111">在 方案總管開啟 hello 雲端服務專案的捷徑功能表，然後選擇 **發行**。</span><span class="sxs-lookup"><span data-stu-id="f8027-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="f8027-112">hello**發行 Azure 應用程式**精靈 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f8027-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![雲端服務專案的發佈命令](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="f8027-114">在 hello 底部**Microsoft Azure 發行設定**精靈頁面的 hello 選取 hello**啟用遠端桌面**所有角色的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f8027-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="f8027-115">hello**遠端桌面組態** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f8027-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="f8027-116">在 hello 底部 hello**遠端桌面組態**對話方塊方塊中，選擇 hello**更多選項** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8027-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="f8027-117">這會顯示下拉式清單方塊，可讓您建立或選擇的憑證，以便您在透過遠端桌面連線時可以加密認證資訊。</span><span class="sxs-lookup"><span data-stu-id="f8027-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="f8027-118">在 hello 下拉式清單中，選擇  **&lt;建立 >**，或選擇現有從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="f8027-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="f8027-119">如果您選擇現有的憑證，請略過下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="f8027-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f8027-120">hello 憑證所需的遠端桌面連線會與不同 hello 憑證用於其他 Azure 作業。</span><span class="sxs-lookup"><span data-stu-id="f8027-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="f8027-121">hello 遠端存取憑證必須具有私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f8027-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="f8027-122">hello **Create Certificate**  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f8027-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="f8027-123">提供新的憑證，hello 的易記名稱，然後選擇 [hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8027-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="f8027-124">hello 新憑證會出現在 hello 下拉式清單方塊中。</span><span class="sxs-lookup"><span data-stu-id="f8027-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="f8027-125">在 hello**遠端桌面組態**對話方塊方塊中，提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f8027-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="f8027-126">您無法使用現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8027-126">You can’t use an existing account.</span></span> <span data-ttu-id="f8027-127">請勿指定系統管理員與 hello hello 新帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f8027-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f8027-128">如果 hello 密碼不符合 hello 複雜性需求下, 一步 toohello 密碼 文字方塊中出現紅色圖示。</span><span class="sxs-lookup"><span data-stu-id="f8027-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="f8027-129">hello 密碼必須包含大寫字母、 小寫字母和數字或符號。</span><span class="sxs-lookup"><span data-stu-id="f8027-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="f8027-130">選擇在哪一個 hello 帳戶逾期和之後，遠端桌面連線將會遭到封鎖的日期。</span><span class="sxs-lookup"><span data-stu-id="f8027-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="f8027-131">提供所有 hello 必要的資訊之後，選擇 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8027-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="f8027-132">啟用遠端存取服務的數個設定會加入 toohello.cscfg 和.csdef 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8027-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="f8027-133">在 hello **Microsoft Azure 發行設定**精靈 中，選擇 hello **確定**按鈕當你準備 toopublish 您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8027-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="f8027-134">如果您不準備 toopublish，請選擇 hello**取消** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8027-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="f8027-135">hello 組態設定會儲存，而且您可以稍後再發行雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8027-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="f8027-136">使用遠端桌面連線 tooan Azure 角色</span><span class="sxs-lookup"><span data-stu-id="f8027-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="f8027-137">發行 Azure 雲端服務之後，您可以使用伺服器總管 toolog hello 虛擬機器到 Azure 託管。</span><span class="sxs-lookup"><span data-stu-id="f8027-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="f8027-138">在 伺服器總管 中，展開 hello **Azure**  節點，然後展開 雲端服務和其角色 toodisplay 執行個體清單的其中一個 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="f8027-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="f8027-139">開啟 hello 一個執行個體節點的捷徑功能表，然後選擇**連接使用的遠端桌面**。</span><span class="sxs-lookup"><span data-stu-id="f8027-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![透過遠端桌面連接](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="f8027-141">輸入 hello 使用者名稱和您先前建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="f8027-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="f8027-142">您現在已登入遠端工作階段。</span><span class="sxs-lookup"><span data-stu-id="f8027-142">You are now logged into your remote session.</span></span>

