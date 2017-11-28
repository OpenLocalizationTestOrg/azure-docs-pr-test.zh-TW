---
title: "Azure 雲端服務中的角色的遠端桌面連線 aaaEnable |Microsoft 文件"
description: "如何 tooconfigure 您的 azure 雲端服務應用程式 tooallow 遠端桌面連線"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="6d5a9-103">啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="6d5a9-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d5a9-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6d5a9-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="6d5a9-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="6d5a9-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="6d5a9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d5a9-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="6d5a9-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d5a9-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="6d5a9-108">遠端桌面可讓您在 Azure 中執行的角色 tooaccess hello 桌面。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="6d5a9-109">您可以使用遠端桌面連線 tootroubleshoot 後診斷問題的應用程式，在執行時。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="6d5a9-110">您可以啟用遠端桌面連線您的角色在開發期間包含在服務定義中的 hello 遠端桌面模組，或者您可以選擇透過遠端桌面延伸模組 hello tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="6d5a9-111">hello 慣用的方法為 toouse hello 遠端桌面延伸您可以在 hello 應用程式部署而不需要 tooredeploy 您的應用程式時，即使啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="6d5a9-112">從 hello Azure 入口網站中設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="6d5a9-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="6d5a9-113">hello Azure 入口網站會使用 hello 遠端桌面的擴充方法，因此即使在 hello 應用程式部署之後，您可以啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="6d5a9-114">hello**遠端桌面**刀鋒視窗中的為雲端服務可讓您 tooenable 遠端桌面變更 hello 本機系統管理員帳戶使用 tooconnect toohello 虛擬機器、 hello 憑證用於驗證和設定 hello到期日。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="6d5a9-115">按一下**雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**遠端桌面**。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="6d5a9-117">選擇是否 tooenable 遠端桌面針對個別的角色或所有的角色，然後變更 hello 切換器 hello 值太**啟用**。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="6d5a9-118">填寫使用者名稱、 密碼、 到期，以及憑證的 hello 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="6d5a9-120">當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="6d5a9-121">tooprevent hello 憑證使用的 tooencrypt hello 密碼重新開機，必須安裝在 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="6d5a9-122">重新啟動，tooprevent [hello 雲端服務將憑證上傳](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後傳回 toothis 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="6d5a9-123">在**角色**，選取您想要 tooupdate 或選取 hello 角色**所有**所有角色。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="6d5a9-124">完成組態更新時，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="6d5a9-125">它將需要一些時間才能在角色執行個體都是準備 tooreceive 連接。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="6d5a9-126">角色執行個體的遠端存取</span><span class="sxs-lookup"><span data-stu-id="6d5a9-126">Remote into role instances</span></span>
<span data-ttu-id="6d5a9-127">一旦 hello 角色上啟用遠端桌面，您可以起始直接從 hello Azure 入口網站的連接：</span><span class="sxs-lookup"><span data-stu-id="6d5a9-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="6d5a9-128">按一下**執行個體**tooopen hello**執行個體**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="6d5a9-129">選取已設定「遠端桌面」的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="6d5a9-130">按一下**連接**toodownload RDP 檔，以取得 hello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="6d5a9-132">按一下**開啟**然後**連接**toostart hello 遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="6d5a9-133">如果您的雲端服務坐 NSG 後方，您可能需要 toocreate 規則以允許連接埠上的流量**3389**和**20000**。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="6d5a9-134">遠端桌面使用者連接埠 **3389**。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="6d5a9-135">雲端服務執行個體是負載平衡，因此您無法直接控制至哪一個執行個體 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="6d5a9-136">hello *RemoteForwarder*和*RemoteAccess*代理程式管理 RDP 流量，並允許 hello 用戶端 toosend RDP cookie，並指定要個別執行個體 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="6d5a9-137">hello *RemoteForwarder*和*RemoteAccess*代理程式需要該連接埠**20000*** 開啟，如果您有 NSG 可能會封鎖連接。</span><span class="sxs-lookup"><span data-stu-id="6d5a9-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d5a9-138">其他資源</span><span class="sxs-lookup"><span data-stu-id="6d5a9-138">Additional resources</span></span>

<span data-ttu-id="6d5a9-139">[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)
[雲端服務的常見問題集-遠端桌面](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6d5a9-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
