---
title: "在傳統的 Azure VM 上 aaaRun Java 應用程式伺服器 |Microsoft 文件"
description: "本教學課程使用資源以 hello 傳統部署模型，並且示範如何建立 toocreate Windows 虛擬機器，並將它設定 toorun Apache Tomcat 應用程式伺服器。"
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="140df-103">如何 toorun Java 應用程式伺服器的虛擬機器上建立 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="140df-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="140df-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="140df-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="140df-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="140df-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="140df-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="140df-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="140df-107">資源管理員範本 toodeploy Java 8 與 Tomcat webapp，請參閱[這裡](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/)。</span><span class="sxs-lookup"><span data-stu-id="140df-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="140df-108">有了 Azure，您可以使用虛擬機器 tooprovide 伺服器功能。</span><span class="sxs-lookup"><span data-stu-id="140df-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="140df-109">例如，在 Azure 上執行的虛擬機器可以設定的 toohost Java 應用程式伺服器，例如 Apache Tomcat。</span><span class="sxs-lookup"><span data-stu-id="140df-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="140df-110">完成本指南之後, 您必須了解如何 toocreate 虛擬機器在 Azure 上執行，並將它設定 toorun Java 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="140df-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="140df-111">您會了解，並執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="140df-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="140df-112">如何 toocreate 的虛擬機器，都有 Java Development Kit (JDK) 已安裝。</span><span class="sxs-lookup"><span data-stu-id="140df-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="140df-113">Tooremotely 登入方式 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="140df-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="140df-114">如何 tooinstall Java 應用程式伺服器--Apache Tomcat-虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="140df-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="140df-115">如何 toocreate 虛擬機器的端點。</span><span class="sxs-lookup"><span data-stu-id="140df-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="140df-116">如何 tooopen hello 中的連接埠的應用程式伺服器防火牆。</span><span class="sxs-lookup"><span data-stu-id="140df-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="140df-117">hello 完成安裝在 Tomcat 中虛擬機器上執行的結果。</span><span class="sxs-lookup"><span data-stu-id="140df-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![執行 Apache Tomcat 的虛擬機器][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="140df-119">toocreate 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="140df-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="140df-120">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="140df-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="140df-121">按一下**新增**，按一下 **計算**，然後按一下**查看所有**在 hello**熱門應用程式**。</span><span class="sxs-lookup"><span data-stu-id="140df-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="140df-122">按一下**JDK**，按一下  **JDK 8**在 hello **JDK**窗格。</span><span class="sxs-lookup"><span data-stu-id="140df-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="140df-123">虛擬機器映像支援**JDK 6**和**JDK 7**可用，如果您有未準備好 toorun JDK 8 中的舊版應用程式。</span><span class="sxs-lookup"><span data-stu-id="140df-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="140df-124">在 hello JDK 8 窗格中，選取 **傳統**，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="140df-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="140df-125">在 hello**基本概念**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="140df-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="140df-126">指定 hello 虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="140df-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="140df-127">輸入 hello 系統管理員的名稱在 hello**使用者名**欄位。</span><span class="sxs-lookup"><span data-stu-id="140df-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="140df-128">請記住這個名稱，而且 hello 稍後 hello 下一個欄位的相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="140df-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="140df-129">您需要在您從遠端登入 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="140df-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="140df-130">輸入密碼，hello**新密碼**欄位，並重新輸入在 hello**確認密碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="140df-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="140df-131">此密碼是 hello 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="140df-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="140df-132">選取適當的 hello**訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="140df-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="140df-133">Hello**資源群組**，按一下 **建立新**，然後輸入 hello 是新的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="140df-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="140df-134">或者，按一下**使用現有**並選取其中一個 hello 可用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="140df-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="140df-135">選取的位置 hello 虛擬機器所在的位置，例如**美國中南部**。</span><span class="sxs-lookup"><span data-stu-id="140df-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="140df-136">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="140df-136">Click **Next**.</span></span>
7. <span data-ttu-id="140df-137">在 hello**虛擬機器映像大小**刀鋒視窗中，選取**標準 A1**或另一個適當的映像。</span><span class="sxs-lookup"><span data-stu-id="140df-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="140df-138">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="140df-138">Click **Select**.</span></span>

9. <span data-ttu-id="140df-139">在 hello**設定**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="140df-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="140df-140">您可以使用 Azure 所提供的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="140df-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="140df-141">在 hello**摘要**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="140df-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="140df-142">tooremotely tooyour 虛擬機器中的符號</span><span class="sxs-lookup"><span data-stu-id="140df-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="140df-143">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="140df-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="140df-144">按一下 [虛擬機器 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="140df-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="140df-145">如有需要按一下**更多服務**在 hello 左下角 hello 服務類別之下。</span><span class="sxs-lookup"><span data-stu-id="140df-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="140df-146">hello**虛擬機器 （傳統）**項目會列在 hello**計算**群組。</span><span class="sxs-lookup"><span data-stu-id="140df-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="140df-147">按一下您要 toosign 中的 hello 虛擬機器的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="140df-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="140df-148">Hello 虛擬機器啟動之後，在 hello hello 窗格頂端的功能表允許連線。</span><span class="sxs-lookup"><span data-stu-id="140df-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="140df-149">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="140df-149">Click **Connect**.</span></span>
6. <span data-ttu-id="140df-150">回應 toohello 提示做為所需的 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="140df-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="140df-151">一般而言，您儲存或開啟包含 hello 連接詳細資料的 hello.rdp 檔案。</span><span class="sxs-lookup"><span data-stu-id="140df-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="140df-152">您可能會有 toocopy hello url： 連接埠為 hello 最後一部分 hello hello.rdp 檔案第一行，並將它貼入遠端登入應用程式中。</span><span class="sxs-lookup"><span data-stu-id="140df-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="140df-153">tooinstall 虛擬機器上的 Java 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="140df-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="140df-154">您可以複製 Java 應用程式伺服器 tooyour 虛擬機器，或您可透過安裝程式在 Java 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="140df-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="140df-155">本教學課程會使用為 hello Java 應用程式伺服器 tooinstall Tomcat。</span><span class="sxs-lookup"><span data-stu-id="140df-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="140df-156">當您登入 tooyour 虛擬機器時，開啟瀏覽器工作階段過[Apache Tomcat](http://tomcat.apache.org/download-80.cgi)。</span><span class="sxs-lookup"><span data-stu-id="140df-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="140df-157">按兩下 hello 連結**32 位元/64 位元 Windows 服務的安裝程式**。</span><span class="sxs-lookup"><span data-stu-id="140df-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="140df-158">利用此技術，Tomcat 將以 Windows 服務形式進行安裝。</span><span class="sxs-lookup"><span data-stu-id="140df-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="140df-159">出現提示時，選擇 toorun hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="140df-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="140df-160">在 hello **Apache Tomcat 安裝**精靈，後續 hello 提示 tooinstall Tomcat。</span><span class="sxs-lookup"><span data-stu-id="140df-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="140df-161">基於 hello 本教學課程中，接受 hello 預設值是正常的。</span><span class="sxs-lookup"><span data-stu-id="140df-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="140df-162">當您來到 hello **Apache Tomcat 安裝精靈的正在完成 hello**對話方塊中，您可以選擇性地檢查**執行 Apache Tomcat** toohave 現在 Tomcat 開始。</span><span class="sxs-lookup"><span data-stu-id="140df-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="140df-163">按一下**完成**toocomplete hello Tomcat 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="140df-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="140df-164">toostart Tomcat</span><span class="sxs-lookup"><span data-stu-id="140df-164">toostart Tomcat</span></span>

<span data-ttu-id="140df-165">開啟您的虛擬機器和執行 hello 命令上的命令提示字元，您可以手動啟動 Tomcat **net&nbsp;啟動&nbsp;Tomcat8**。</span><span class="sxs-lookup"><span data-stu-id="140df-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="140df-166">Tomcat 開始執行之後，您可以輸入 hello URL 來存取 Tomcat <http://localhost:8080/<> hello 虛擬機器的瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="140df-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="140df-167">toosee Tomcat 外部機器中執行，您需要 toocreate 端點，並開啟連接埠。</span><span class="sxs-lookup"><span data-stu-id="140df-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="140df-168">toocreate 虛擬機器的端點</span><span class="sxs-lookup"><span data-stu-id="140df-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="140df-169">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="140df-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="140df-170">按一下 [虛擬機器 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="140df-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="140df-171">按一下 hello hello 執行您的 Java 應用程式伺服器的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="140df-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="140df-172">按一下 [端點] 。</span><span class="sxs-lookup"><span data-stu-id="140df-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="140df-173">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="140df-173">Click **Add**.</span></span>
6. <span data-ttu-id="140df-174">在 hello**加入端點**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="140df-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="140df-175">指定 hello 端點; 的名稱例如， **HttpIn**。</span><span class="sxs-lookup"><span data-stu-id="140df-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="140df-176">選取**TCP** hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="140df-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="140df-177">指定**80** hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="140df-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="140df-178">指定**8080** hello 私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="140df-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="140df-179">選取**已停用**hello 浮動 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="140df-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="140df-180">將保留原狀 hello 存取控制清單。</span><span class="sxs-lookup"><span data-stu-id="140df-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="140df-181">按一下 hello**確定**按鈕 tooclose hello 對話方塊，並建立 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="140df-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="140df-182">tooopen hello 防火牆中針對您的虛擬機器中的連接埠</span><span class="sxs-lookup"><span data-stu-id="140df-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="140df-183">登入 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="140df-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="140df-184">按一下 Windows [開始] 。</span><span class="sxs-lookup"><span data-stu-id="140df-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="140df-185">按一下 [控制台] 。</span><span class="sxs-lookup"><span data-stu-id="140df-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="140df-186">依序按一下 [系統及安全性]、[Windows 防火牆] 及 [進階設定]。</span><span class="sxs-lookup"><span data-stu-id="140df-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="140df-187">按一下 輸入規則，然後按一下新增規則。</span><span class="sxs-lookup"><span data-stu-id="140df-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="140df-188">![新增輸入規則][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="140df-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="140df-189">Hello**規則類型**，選取**連接埠**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="140df-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="140df-190">![新增輸入規則連接埠][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="140df-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="140df-191">在 hello**通訊協定和連接埠**畫面上，選取**TCP**，指定**8080**為 hello**特定本機連接埠**，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="140df-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="140df-192">![新增輸入規則][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="140df-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="140df-193">在 [hello**動作**畫面上，選取**允許 hello 連線**，然後按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="140df-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="140df-194">![新增輸入規則動作][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="140df-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="140df-195">在 [hello**設定檔**畫面上，確認**網域**，**私用**，和**公用**已選取，然後再按一下**下一步]**.</span><span class="sxs-lookup"><span data-stu-id="140df-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="140df-196">![新增輸入規則設定檔][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="140df-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="140df-197">在 hello**名稱**畫面上，指定 hello 規則的名稱，例如**HttpIn** （hello 規則名稱不是必要的 toomatch hello 端點名稱，不過），然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="140df-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="140df-198">![新增輸入規則名稱][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="140df-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="140df-199">此時，應該能從外部瀏覽器檢視您的 Tomcat 網站。</span><span class="sxs-lookup"><span data-stu-id="140df-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="140df-200">在 hello 瀏覽器的位址視窗中，輸入 hello 表單的 URL  **http://*您\_DNS\_名稱*。 cloudapp.net**，其中***您\_DNS\_名稱***是 hello hello 虛擬機器的建立時指定的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="140df-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="140df-201">應用程式生命週期考量</span><span class="sxs-lookup"><span data-stu-id="140df-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="140df-202">您無法建立您自己的 web 應用程式封存檔 (WAR)，並將它加入 toohello **webapps**資料夾。</span><span class="sxs-lookup"><span data-stu-id="140df-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="140df-203">例如，建立基本的 Java Service Page (JSP) 動態 Web 專案，並將它匯出為 WAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="140df-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="140df-204">接下來，複製 hello WAR toohello Apache Tomcat **webapps** hello 虛擬機器，然後在瀏覽器中執行上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="140df-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="140df-205">依預設安裝 hello Tomcat 服務時，它是 toostart 手動設定。</span><span class="sxs-lookup"><span data-stu-id="140df-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="140df-206">您可以切換它 toostart 自動使用 hello 服務 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="140df-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="140df-207">啟動 hello 服務 嵌入式管理單元，依序按一下**Windows 啟動**，**系統管理工具**，然後**服務**。</span><span class="sxs-lookup"><span data-stu-id="140df-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="140df-208">按兩下 hello **Apache Tomcat**服務和設定**啟動類型**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="140df-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![自動設定服務 toostart][service_automatic_startup]

    <span data-ttu-id="140df-210">hello 的好處有自動啟動 Tomcat 是，它就會開始執行 hello 虛擬機器重新開機 （例如之後需要重新開機的軟體更新已安裝）, 時。</span><span class="sxs-lookup"><span data-stu-id="140df-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="140df-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="140df-211">Next steps</span></span>
<span data-ttu-id="140df-212">您可以了解其他服務 （例如 Azure 儲存體、 服務匯流排和 SQL Database），您可能會想 tooinclude Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="140df-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="140df-213">檢視可用的 hello 資訊在 hello [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="140df-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
