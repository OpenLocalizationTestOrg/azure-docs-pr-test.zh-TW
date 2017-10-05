---
title: "啟用 Azure 雲端服務中角色的遠端桌面連線 | Microsoft Docs"
description: "如何設定的 Azure 雲端服務應用程式以允許遠端桌面連線"
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="9747d-103">啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="9747d-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9747d-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9747d-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="9747d-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="9747d-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="9747d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9747d-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="9747d-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9747d-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="9747d-108">遠端桌面可讓您存取 Azure 內執行中角色的桌面。</span><span class="sxs-lookup"><span data-stu-id="9747d-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="9747d-109">您可以使用遠端桌面連線來疑難排解和診斷執行中應用程式的問題。</span><span class="sxs-lookup"><span data-stu-id="9747d-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="9747d-110">您可以在開發期間藉由在服務定義中包含遠端桌面模組啟用遠端桌面連線，也可以選擇透過遠端桌面延伸模組啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="9747d-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="9747d-111">慣用的方法是使用遠端桌面延伸模組，因為即使在部署應用程式之後，您仍然可以啟用遠端桌面，無需重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9747d-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="9747d-112">從 Azure 入口網站設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="9747d-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="9747d-113">Azure 入口網站會使用遠端桌面延伸模組方法，因此即使在應用程式部署之後，您也可以啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="9747d-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="9747d-114">雲端服務的 [遠端桌面] 刀鋒視窗可讓您啟用遠端桌面，變更用來與虛擬機器連線的本機系統管理員帳戶、驗證中使用的憑證，並設定到期日。</span><span class="sxs-lookup"><span data-stu-id="9747d-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="9747d-115">依序按一下 [雲端服務]、雲端服務的名稱及 [遠端桌面]。</span><span class="sxs-lookup"><span data-stu-id="9747d-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="9747d-117">選擇要針對個別的角色或所有角色啟用遠端桌面，然後將切換器的值變更為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="9747d-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="9747d-118">填入必要的使用者名稱、密碼、到期日及憑證欄位。</span><span class="sxs-lookup"><span data-stu-id="9747d-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="9747d-120">當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9747d-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="9747d-121">若要防止重新啟動，角色上必須安裝用來將密碼加密的憑證。</span><span class="sxs-lookup"><span data-stu-id="9747d-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="9747d-122">若要防止重新啟動，請[上傳雲端服務的憑證](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後再回到這個對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9747d-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="9747d-123">在 [角色] 中，選取想要更新的角色，或選取 [全部] 以更新所有角色。</span><span class="sxs-lookup"><span data-stu-id="9747d-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="9747d-124">完成組態更新時，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9747d-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="9747d-125">在您的角色執行個體準備好接受連線之前，會需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="9747d-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="9747d-126">角色執行個體的遠端存取</span><span class="sxs-lookup"><span data-stu-id="9747d-126">Remote into role instances</span></span>
<span data-ttu-id="9747d-127">針對角色啟用 [遠端桌面] 後，就能直接從 Azure 入口網站初始化連線︰</span><span class="sxs-lookup"><span data-stu-id="9747d-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="9747d-128">按一下 [執行個體] 以開啟 [執行個體] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9747d-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="9747d-129">選取已設定「遠端桌面」的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="9747d-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="9747d-130">按一下 [連接] 下載 RDP 檔案的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="9747d-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="9747d-132">按一下 [開啟]，然後按一下 [連接] 以啟動遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="9747d-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="9747d-133">如果您的雲端服務設置在 NSG 後方，您可能需要建立規則以允許連接埠 **3389** 和 **20000** 上的流量。</span><span class="sxs-lookup"><span data-stu-id="9747d-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="9747d-134">遠端桌面使用者連接埠 **3389**。</span><span class="sxs-lookup"><span data-stu-id="9747d-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="9747d-135">系統已為雲端服務執行個體進行負載平衡，因此您無法直接控制要連線的執行個體。</span><span class="sxs-lookup"><span data-stu-id="9747d-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="9747d-136">*RemoteForwarder* 與 *RemoteAccess* 代理程式會管理 RDP 流量，並允許用戶端傳送 RDP Cookie 並指定要連線的個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="9747d-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="9747d-137">*RemoteForwarder* 與 *RemoteAccess* 代理程式要求您必須開啟連接埠 **20000***，這在您使用 NSG 的情況下可能是封鎖的。</span><span class="sxs-lookup"><span data-stu-id="9747d-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9747d-138">其他資源</span><span class="sxs-lookup"><span data-stu-id="9747d-138">Additional resources</span></span>

<span data-ttu-id="9747d-139">[如何設定雲端服務](cloud-services-how-to-configure.md)
[雲端服務常見問題集 - 遠端桌面](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="9747d-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
