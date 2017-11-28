---
title: "Linux 虛擬機器上的設定 Apache Tomcat aaaSet |Microsoft 文件"
description: "深入了解如何使用 Azure 虛擬機器執行 Linux 向上 Apache Tomcat7 tooset。"
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="4dad9-103">使用 Azure 在 Linux 虛擬機器上設定 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="4dad9-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="4dad9-104">Apache Tomcat （或只是 Tomcat 中，也原名雅加達 Tomcat） 是開放原始碼 web 伺服器及 servlet hello Apache 軟體基礎 (ASF) 所開發的容器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="4dad9-105">Tomcat 實作 hello Java Servlet 和 Sun Microsystems 從 hello JavaServer 頁面 (JSP) 規格。</span><span class="sxs-lookup"><span data-stu-id="4dad9-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="4dad9-106">Tomcat 提供純 Java HTTP web 伺服器環境中哪些 toorun Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4dad9-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="4dad9-107">Tomcat hello 簡單的組態，是單一的作業系統處理序中執行。</span><span class="sxs-lookup"><span data-stu-id="4dad9-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="4dad9-108">此程序會執行 Java 虛擬機器 (JVM)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="4dad9-109">從瀏覽器 tooTomcat 每個 HTTP 要求會處理做為個別的執行緒在 hello Tomcat 程序中。</span><span class="sxs-lookup"><span data-stu-id="4dad9-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="4dad9-110">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="4dad9-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4dad9-111">本文件涵蓋如何 toouse hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4dad9-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="4dad9-112">建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="4dad9-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4dad9-113">toouse 資源管理員範本 toodeploy Ubuntu 具有 VM Open JDK 和 Tomcat，請參閱[本文](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="4dad9-114">在本文中，您將在 Linux 映像上安裝 Tomcat7 並且部署於 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="4dad9-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="4dad9-115">您將了解：</span><span class="sxs-lookup"><span data-stu-id="4dad9-115">You will learn:</span></span>  

* <span data-ttu-id="4dad9-116">如何 toocreate Azure 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="4dad9-117">如何 tooprepare hello Tomcat7 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="4dad9-118">如何 tooinstall Tomcat7。</span><span class="sxs-lookup"><span data-stu-id="4dad9-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="4dad9-119">假設您已經有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4dad9-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="4dad9-120">如果沒有，您可以註冊免費試用版在[hello Azure 網站](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="4dad9-121">如果您擁有 MSDN 訂用帳戶，請參閱 [Microsoft Azure 特價：MSDN、MPN 及 BizSpark 優惠](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="4dad9-122">toolearn 深入了解 Azure 中，請參閱[何謂 Azure？](https://azure.microsoft.com/overview/what-is-azure/)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="4dad9-123">本文假設您有 Tomcat 和 Linux 的基本操作知識。</span><span class="sxs-lookup"><span data-stu-id="4dad9-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="4dad9-124">第 1 階段：建立映像。</span><span class="sxs-lookup"><span data-stu-id="4dad9-124">Phase 1: Create an image</span></span>
<span data-ttu-id="4dad9-125">在這個階段，您將在 Azure 中使用 Linux 映像建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="4dad9-126">步驟 1：產生 SSH 驗證金鑰</span><span class="sxs-lookup"><span data-stu-id="4dad9-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="4dad9-127">SSH 對系統管理員而言是很重要的工具。</span><span class="sxs-lookup"><span data-stu-id="4dad9-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="4dad9-128">不過，不建議根據人為決定的密碼來設定存取安全性。</span><span class="sxs-lookup"><span data-stu-id="4dad9-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="4dad9-129">惡意使用者可以依據使用者名稱和弱式密碼侵入系統。</span><span class="sxs-lookup"><span data-stu-id="4dad9-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="4dad9-130">hello 好消息是 tooleave 遠端存取開啟的而不必擔心密碼。</span><span class="sxs-lookup"><span data-stu-id="4dad9-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="4dad9-131">此方法是由使用非對稱密碼編譯的驗證所組成。</span><span class="sxs-lookup"><span data-stu-id="4dad9-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="4dad9-132">hello 使用者的私密金鑰為 hello 授與 hello 驗證的其中一個。</span><span class="sxs-lookup"><span data-stu-id="4dad9-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="4dad9-133">您甚至可以鎖定 hello 使用者帳戶 toonot 允許密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="4dad9-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="4dad9-134">這個方法的另一個好處是，您不需要不同的密碼 toosign toodifferent 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="4dad9-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="4dad9-135">您可以藉由 hello 個人私密金鑰所有在伺服器上，這可讓您不必 tooremember 數個密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4dad9-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="4dad9-136">請遵循這些步驟 toogenerate hello SSH 驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="4dad9-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="4dad9-137">下載並安裝從下列位置的 hello Ssh-keygen: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="4dad9-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="4dad9-138">執行 Puttygen.exe。</span><span class="sxs-lookup"><span data-stu-id="4dad9-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="4dad9-139">按一下**產生**toogenerate hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4dad9-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="4dad9-140">在 hello 過程中，您可以增加隨機性移動 hello 滑鼠 hello hello 視窗中的空白區域上。</span><span class="sxs-lookup"><span data-stu-id="4dad9-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="4dad9-141">![PuTTY 金鑰產生器螢幕擷取畫面顯示 hello 產生新的索引鍵 按鈕][1]</span><span class="sxs-lookup"><span data-stu-id="4dad9-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="4dad9-142">Hello 產生程序之後，Puttygen.exe 會顯示新的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="4dad9-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![PuTTY 金鑰產生器螢幕擷取畫面顯示 hello 新的公開金鑰與 hello 儲存私用金鑰按鈕][2]
5. <span data-ttu-id="4dad9-144">選取並複製 hello 公開金鑰，並將它儲存在名為 publicKey.pem 的檔案。</span><span class="sxs-lookup"><span data-stu-id="4dad9-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="4dad9-145">不要按**儲存公開金鑰**，因為 hello 儲存公開金鑰的檔案格式是我們想要的 hello 公用金鑰不同。</span><span class="sxs-lookup"><span data-stu-id="4dad9-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="4dad9-146">按一下 [儲存私密金鑰]，並將它儲存在名為 privateKey.ppk 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="4dad9-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="4dad9-147">步驟 2: Hello Azure 入口網站中建立 hello 映像</span><span class="sxs-lookup"><span data-stu-id="4dad9-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="4dad9-148">在 hello[入口網站](https://portal.azure.com/)，按一下**新增**在 hello 工作列 toocreate 映像。</span><span class="sxs-lookup"><span data-stu-id="4dad9-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="4dad9-149">然後選擇 hello Linux 映像，取決於您的需求。</span><span class="sxs-lookup"><span data-stu-id="4dad9-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="4dad9-150">hello 下列範例使用 hello Ubuntu 14.04 映像。</span><span class="sxs-lookup"><span data-stu-id="4dad9-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="4dad9-151">![顯示 hello 新按鈕的 hello 入口網站的螢幕擷取畫面][3]</span><span class="sxs-lookup"><span data-stu-id="4dad9-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="4dad9-152">如**主機名稱**，指定 hello hello URL，您和網際網路用戶端會使用 tooaccess 此虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="4dad9-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="4dad9-153">定義 hello DNS 名稱，例如 tomcatdemo hello 最後一個部分。</span><span class="sxs-lookup"><span data-stu-id="4dad9-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="4dad9-154">Azure 會隨後產生 hello URL 為 tomcatdemo.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="4dad9-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="4dad9-155">如**SSH 驗證金鑰**，從 hello publicKey.pem 檔案，其中包含 hello Ssh-keygen 所產生的公開金鑰複製 hello 索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="4dad9-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="4dad9-156">![方塊 hello 入口網站中的 SSH 驗證金鑰][4]</span><span class="sxs-lookup"><span data-stu-id="4dad9-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="4dad9-157">視需要設定其他設定，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="4dad9-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="4dad9-158">第 2 階段：準備用於 Tomcat7 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4dad9-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="4dad9-159">在這個階段中，您將設定 Tomcat 流量的端點，並再連接 tooyour 新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="4dad9-160">步驟 1： 開啟 hello HTTP 連接埠 tooallow web 存取</span><span class="sxs-lookup"><span data-stu-id="4dad9-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="4dad9-161">Azure 中的端點包含 TCP 或 UDP 通訊協定，以及公用和私人連接埠。</span><span class="sxs-lookup"><span data-stu-id="4dad9-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="4dad9-162">hello 私用連接埠是 hello hello 服務會接聽 tooon hello 虛擬機器的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="4dad9-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="4dad9-163">hello 公用連接埠是 hello Azure 雲端服務的 hello 連接埠會接聽 tooexternally 針對以網際網路為基礎的連入流量。</span><span class="sxs-lookup"><span data-stu-id="4dad9-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="4dad9-164">TCP 連接埠 8080 是 Tomcat 使用 toolisten hello 預設連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="4dad9-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="4dad9-165">如果使用 Azure 端點開啟這個連接埠，您和其他網際網路用戶端即可存取 Tomcat 頁面。</span><span class="sxs-lookup"><span data-stu-id="4dad9-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="4dad9-166">在 hello 入口網站中，按一下 **瀏覽** > **虛擬機器**，然後按一下hello 您所建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="4dad9-167">![Hello Virtual machines 目錄的螢幕擷取畫面][5]</span><span class="sxs-lookup"><span data-stu-id="4dad9-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="4dad9-168">tooadd 端點 tooyour 虛擬機器，按一下 hello**端點**方塊。</span><span class="sxs-lookup"><span data-stu-id="4dad9-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="4dad9-169">![顯示 hello 端點方塊的螢幕擷取畫面][6]</span><span class="sxs-lookup"><span data-stu-id="4dad9-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="4dad9-170">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="4dad9-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="4dad9-171">Hello 端點，請輸入的名稱中的 hello 端點**端點**，然後輸入 80**公用連接埠**。</span><span class="sxs-lookup"><span data-stu-id="4dad9-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="4dad9-172">如果您將它設定 too80，您不需要使用的 tooaccess Tomcat hello URL tooinclude hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="4dad9-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="4dad9-173">例如，http://tomcatdemo.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="4dad9-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="4dad9-174">如果您設定它 tooanother 值，例如 81，您需要 tooadd hello 連接埠號碼 toohello URL tooaccess Tomcat。</span><span class="sxs-lookup"><span data-stu-id="4dad9-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="4dad9-175">例如，http://tomcatdemo.cloudapp.net:81/。</span><span class="sxs-lookup"><span data-stu-id="4dad9-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="4dad9-176">在 [私人連接埠] 中輸入 8080。</span><span class="sxs-lookup"><span data-stu-id="4dad9-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="4dad9-177">Tomcat 預設會接聽 TCP 連接埠 8080。</span><span class="sxs-lookup"><span data-stu-id="4dad9-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="4dad9-178">如果您變更 hello 預設接聽 Tomcat 連接埠，您應該更新**私用連接埠**toobe hello 與 hello Tomcat 接聽連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="4dad9-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="4dad9-179">![UI 的螢幕擷取畫面，其中顯示 [新增] 命令、[公用連接埠] 和 [私人連接埠]][7]</span><span class="sxs-lookup"><span data-stu-id="4dad9-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="4dad9-180">按一下**確定**tooadd hello 端點 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="4dad9-181">步驟 2： 連接 toohello 您所建立的映像</span><span class="sxs-lookup"><span data-stu-id="4dad9-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="4dad9-182">您可以選擇任何 SSH 工具 tooconnect tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="4dad9-183">在此範例中，我們使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4dad9-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="4dad9-184">收到 hello 入口網站中的 hello 的虛擬機器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4dad9-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="4dad9-185">按一下 [瀏覽] > [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="4dad9-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="4dad9-186">選取您的虛擬機器的 hello 名稱，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="4dad9-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="4dad9-187">在 hello**屬性**磚中，查看 hello**網域名稱**方塊 tooget hello DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4dad9-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="4dad9-188">取得從 hello SSH 連線的 hello 連接埠號碼**SSH**方塊。</span><span class="sxs-lookup"><span data-stu-id="4dad9-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="4dad9-189">![顯示 hello SSH 連接埠號碼的螢幕擷取畫面][8]</span><span class="sxs-lookup"><span data-stu-id="4dad9-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="4dad9-190">下載 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="4dad9-191">下載之後，按一下 Putty.exe hello 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="4dad9-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="4dad9-192">在 PuTTY 組態中，設定 hello 基本選項與 hello 主機名稱和連接埠號碼是從虛擬機器的 hello 屬性取得。</span><span class="sxs-lookup"><span data-stu-id="4dad9-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![螢幕擷取畫面會顯示 hello PuTTY 設定主機名稱和連接埠的選項][9]

5. <span data-ttu-id="4dad9-194">Hello 左窗格中，按一下 **連接** > **SSH** > **Auth**，然後按一下**瀏覽**toospecifyhello hello privateKey.ppk 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="4dad9-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="4dad9-195">hello privateKey.ppk 檔案含有 hello 私密金鑰所產生的 Ssh-keygen 稍 hello 」 階段 1： 建立映像 」 一節。</span><span class="sxs-lookup"><span data-stu-id="4dad9-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="4dad9-196">![顯示 hello 連接目錄階層和瀏覽 按鈕的螢幕擷取畫面][10]</span><span class="sxs-lookup"><span data-stu-id="4dad9-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="4dad9-197">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="4dad9-197">Click **Open**.</span></span> <span data-ttu-id="4dad9-198">您可能會收到警告訊息方塊。</span><span class="sxs-lookup"><span data-stu-id="4dad9-198">You might be alerted by a message box.</span></span> <span data-ttu-id="4dad9-199">如果您已設定 hello DNS 名稱，並正確連接埠號碼，請按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="4dad9-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="4dad9-200">![會顯示 hello 通知的螢幕擷取畫面][11]</span><span class="sxs-lookup"><span data-stu-id="4dad9-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="4dad9-201">您會提示的 tooenter 您的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4dad9-201">You are prompted tooenter your username.</span></span>  
![螢幕擷取畫面顯示在哪裡 tooenter 使用者名稱][12]

8. <span data-ttu-id="4dad9-203">輸入 hello hello 用於 toocreate hello 虛擬機器的使用者名稱 」 階段 1： 建立映像 」 稍早在本文中的 > 一節。</span><span class="sxs-lookup"><span data-stu-id="4dad9-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="4dad9-204">您會看到類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4dad9-204">You will see something like hello following:</span></span>  
![顯示 hello authentication 確認的螢幕擷取畫面][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="4dad9-206">第 3 階段：安裝軟體</span><span class="sxs-lookup"><span data-stu-id="4dad9-206">Phase 3: Install software</span></span>
<span data-ttu-id="4dad9-207">在這個階段中，您可以安裝 hello Java runtime environment、 Tomcat7 和其他 Tomcat7 元件。</span><span class="sxs-lookup"><span data-stu-id="4dad9-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="4dad9-208">Java 執行階段環境</span><span class="sxs-lookup"><span data-stu-id="4dad9-208">Java runtime environment</span></span>
<span data-ttu-id="4dad9-209">Tomcat 是以 Java 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="4dad9-209">Tomcat is written in Java.</span></span> <span data-ttu-id="4dad9-210">Java 開發套件 (JDK) 有兩種類型 (OpenJDK 和 Oracle JDK)。</span><span class="sxs-lookup"><span data-stu-id="4dad9-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="4dad9-211">您可以選擇您想要的 hello。</span><span class="sxs-lookup"><span data-stu-id="4dad9-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="4dad9-212">同時 Jdk 有幾乎相同的 hello Java API 中的 hello 類別的程式碼的 hello 但 hello hello 虛擬機器的程式碼都不同。</span><span class="sxs-lookup"><span data-stu-id="4dad9-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="4dad9-213">OpenJDK 傾向 toouse 開啟文件庫，而 Oracle JDK 傾向 toouse 關閉的。</span><span class="sxs-lookup"><span data-stu-id="4dad9-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="4dad9-214">Oracle JDK 有較多的類別和一些已修復的錯誤，而 Oracle JDK 則比 OpenJDK 穩定。</span><span class="sxs-lookup"><span data-stu-id="4dad9-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="4dad9-215">安裝 OpenJDK</span><span class="sxs-lookup"><span data-stu-id="4dad9-215">Install OpenJDK</span></span>  

<span data-ttu-id="4dad9-216">使用下列命令 toodownload OpenJDK hello。</span><span class="sxs-lookup"><span data-stu-id="4dad9-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="4dad9-217">toocreate 目錄 toocontain hello JDK 檔案：</span><span class="sxs-lookup"><span data-stu-id="4dad9-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="4dad9-218">tooextract hello JDK 檔案到 hello/usr/lib/jvm/目錄：</span><span class="sxs-lookup"><span data-stu-id="4dad9-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="4dad9-219">安裝 Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="4dad9-219">Install Oracle JDK</span></span>


<span data-ttu-id="4dad9-220">使用 hello hello Oracle 網站中的下列命令 toodownload Oracle JDK。</span><span class="sxs-lookup"><span data-stu-id="4dad9-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="4dad9-221">toocreate 目錄 toocontain hello JDK 檔案：</span><span class="sxs-lookup"><span data-stu-id="4dad9-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="4dad9-222">tooextract hello JDK 檔案到 hello/usr/lib/jvm/目錄：</span><span class="sxs-lookup"><span data-stu-id="4dad9-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="4dad9-223">tooset hello 預設 Java 虛擬機器的 Oracle JDK:</span><span class="sxs-lookup"><span data-stu-id="4dad9-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="4dad9-224">確認 Java 安裝成功</span><span class="sxs-lookup"><span data-stu-id="4dad9-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="4dad9-225">您可以使用類似下列 tootest，如果已正確安裝 hello Java 執行階段環境的 hello 的命令：</span><span class="sxs-lookup"><span data-stu-id="4dad9-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="4dad9-226">如果您安裝 OpenJDK，您應該會看到類似 hello 下列訊息：![成功 OpenJDK 安裝訊息][14]</span><span class="sxs-lookup"><span data-stu-id="4dad9-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="4dad9-227">如果您已安裝 Oracle JDK，您應該會看到類似 hello 下列訊息：![成功 Oracle JDK 安裝的訊息][15]</span><span class="sxs-lookup"><span data-stu-id="4dad9-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="4dad9-228">安裝 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="4dad9-228">Install Tomcat7</span></span>
<span data-ttu-id="4dad9-229">使用下列命令 tooinstall Tomcat7 hello。</span><span class="sxs-lookup"><span data-stu-id="4dad9-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="4dad9-230">如果您未使用 Tomcat7，使用這個命令的 hello 適當的變體。</span><span class="sxs-lookup"><span data-stu-id="4dad9-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="4dad9-231">確認 Tomcat7 安裝成功</span><span class="sxs-lookup"><span data-stu-id="4dad9-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="4dad9-232">toocheck 如果成功安裝 Tomcat7，瀏覽 tooyour Tomcat 伺服器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4dad9-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="4dad9-233">在本文中，hello 範例 URL 會是 http://tomcatexample.cloudapp.net/。</span><span class="sxs-lookup"><span data-stu-id="4dad9-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="4dad9-234">如果您看到類似下列 hello 訊息，Tomcat7 已正確安裝。</span><span class="sxs-lookup"><span data-stu-id="4dad9-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="4dad9-235">![Tomcat7 安裝成功訊息][16]</span><span class="sxs-lookup"><span data-stu-id="4dad9-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="4dad9-236">安裝其他 Tomcat7 元件</span><span class="sxs-lookup"><span data-stu-id="4dad9-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="4dad9-237">您也可以安裝其他選用 Tomcat 元件。</span><span class="sxs-lookup"><span data-stu-id="4dad9-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="4dad9-238">使用 hello **sudo apt 快取搜尋 tomcat7**命令 toosee 所有 hello 可用的元件。</span><span class="sxs-lookup"><span data-stu-id="4dad9-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="4dad9-239">使用下列命令 tooinstall hello 一些有用的元件。</span><span class="sxs-lookup"><span data-stu-id="4dad9-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="4dad9-240">第 4 階段：設定 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="4dad9-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="4dad9-241">在這個階段，您可以管理 Tomcat。</span><span class="sxs-lookup"><span data-stu-id="4dad9-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="4dad9-242">啟動和停止 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="4dad9-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="4dad9-243">當您安裝它，hello Tomcat7 伺服器會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="4dad9-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="4dad9-244">您也可以啟動它以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4dad9-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="4dad9-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="4dad9-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="4dad9-246">Tomcat7 tooview hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="4dad9-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="4dad9-247">toorestart Tomcat 服務：</span><span class="sxs-lookup"><span data-stu-id="4dad9-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="4dad9-248">Tomcat7 系統管理</span><span class="sxs-lookup"><span data-stu-id="4dad9-248">Tomcat7 administration</span></span>
<span data-ttu-id="4dad9-249">您可以編輯 hello Tomcat 使用者組態檔案 tooset 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4dad9-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="4dad9-250">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4dad9-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="4dad9-251">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="4dad9-251">Here is an example:</span></span>  
![顯示 hello sudo vi 命令輸出的螢幕擷取畫面][17]  

> [!NOTE]
> <span data-ttu-id="4dad9-253">建立 hello 管理員使用者名稱的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="4dad9-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="4dad9-254">編輯這個檔案之後, 應該重新啟動 Tomcat7 服務，以下列命令 tooensure hello 變更生效的 hello:</span><span class="sxs-lookup"><span data-stu-id="4dad9-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="4dad9-255">開啟瀏覽器，並輸入**http://<your tomcat server DNS name>/管理員/html**為 hello URL。</span><span class="sxs-lookup"><span data-stu-id="4dad9-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="4dad9-256">如本文中的 hello 範例，hello URL 是 http://tomcatexample.cloudapp.net/manager/html。</span><span class="sxs-lookup"><span data-stu-id="4dad9-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="4dad9-257">連接之後，您應該會看到類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="4dad9-257">After connecting, you should see something similar toohello following:</span></span>  
![Hello Tomcat Web 應用程式管理員的螢幕擷取畫面][18]

## <a name="common-issues"></a><span data-ttu-id="4dad9-259">常見問題</span><span class="sxs-lookup"><span data-stu-id="4dad9-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="4dad9-260">無法從 hello 網際網路存取與 Tomcat Moodle hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4dad9-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="4dad9-261">徵狀</span><span class="sxs-lookup"><span data-stu-id="4dad9-261">Symptom</span></span>  
  <span data-ttu-id="4dad9-262">Tomcat 正在執行，但是您無法看到 hello Tomcat 預設頁面與您的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4dad9-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="4dad9-263">可能的根本原因</span><span class="sxs-lookup"><span data-stu-id="4dad9-263">Possible root cause</span></span>   

  * <span data-ttu-id="4dad9-264">hello Tomcat 接聽連接埠不是 hello 與 hello Tomcat 流量的虛擬機器的端點的私人連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="4dad9-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="4dad9-265">檢查您的公用連接埠和私用連接埠端點設定，並確定 hello 私用連接埠是 hello 相同 hello Tomcat 接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="4dad9-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="4dad9-266">請參閱本文＜第 1 階段：建立映像＞一節，以取得為虛擬機器設定端點的指示。</span><span class="sxs-lookup"><span data-stu-id="4dad9-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="4dad9-267">toodetermine hello Tomcat 接聽連接埠，請開啟 /etc/httpd/conf/httpd.conf (Red Hat release) 或 /etc/tomcat7/server.xml （Debian 發行）。</span><span class="sxs-lookup"><span data-stu-id="4dad9-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="4dad9-268">根據預設，hello Tomcat 接聽連接埠為 8080。</span><span class="sxs-lookup"><span data-stu-id="4dad9-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="4dad9-269">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="4dad9-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="4dad9-270">如果您使用虛擬機器，Debian 或 Ubuntu 和您想要 toochange hello 預設連接埠的 Tomcat 接聽 (例如 8081) 一樣，您也應該開啟 hello hello 作業系統的連接埠。</span><span class="sxs-lookup"><span data-stu-id="4dad9-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="4dad9-271">首先，開啟 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="4dad9-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="4dad9-272">然後取消註解 hello 最後一行，並變更 「 否 」 太"yes"。</span><span class="sxs-lookup"><span data-stu-id="4dad9-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="4dad9-273">hello 防火牆已停用 hello 接聽連接埠的 Tomcat。</span><span class="sxs-lookup"><span data-stu-id="4dad9-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="4dad9-274">您只能看到 hello 本機主機 hello Tomcat 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="4dad9-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="4dad9-275">hello 問題是最有可能是冀望的 tooby Tomcat，hello 連接埠已被 hello 防火牆封鎖。</span><span class="sxs-lookup"><span data-stu-id="4dad9-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="4dad9-276">您可以使用 hello w3m 工具 toobrowse hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="4dad9-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="4dad9-277">hello 下列命令安裝 w3m 並瀏覽 toohello Tomcat 預設頁面：</span><span class="sxs-lookup"><span data-stu-id="4dad9-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="4dad9-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="4dad9-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="4dad9-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="4dad9-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="4dad9-280">方案</span><span class="sxs-lookup"><span data-stu-id="4dad9-280">Solution</span></span>

  * <span data-ttu-id="4dad9-281">Hello Tomcat 接聽連接埠不是 hello 相同 hello hello 端點的流量 toohello 虛擬機器的私用連接埠為，如果您需要變更 hello 私用連接埠 toobe hello 與 hello Tomcat 接聽連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="4dad9-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="4dad9-282">如果 hello 問題因防火牆/iptables，加入下列行太/等/sysconfig/iptables hello。</span><span class="sxs-lookup"><span data-stu-id="4dad9-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="4dad9-283">https 流量，才需要 hello 第二行：</span><span class="sxs-lookup"><span data-stu-id="4dad9-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="4dad9-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="4dad9-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="4dad9-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="4dad9-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="4dad9-286">請確定 hello 先前行的位置會全域限制存取，例如 hello 下列任何程式碼行上方:-A 輸入-j 拒絕-拒絕與 icmp 主機禁止</span><span class="sxs-lookup"><span data-stu-id="4dad9-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="4dad9-287">tooreload hello iptables，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4dad9-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="4dad9-288">這在 CentOS 6.3 上已經過測試。</span><span class="sxs-lookup"><span data-stu-id="4dad9-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="4dad9-289">權限被拒絕，當您上傳專案檔太/var/lib/tomcat7/webapps /</span><span class="sxs-lookup"><span data-stu-id="4dad9-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="4dad9-290">徵狀</span><span class="sxs-lookup"><span data-stu-id="4dad9-290">Symptom</span></span>
  <span data-ttu-id="4dad9-291">當您使用 SFTP 用戶端 （例如 FileZilla) tooconnect tooyour 虛擬機器，並瀏覽太/var/lib/tomcat7/webapps/toopublish 您的網站，取得錯誤訊息類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="4dad9-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="4dad9-292">可能的根本原因</span><span class="sxs-lookup"><span data-stu-id="4dad9-292">Possible root cause</span></span>
  <span data-ttu-id="4dad9-293">您有任何權限 tooaccess hello /var/lib/tomcat7/webapps 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dad9-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="4dad9-294">方案</span><span class="sxs-lookup"><span data-stu-id="4dad9-294">Solution</span></span>  
  <span data-ttu-id="4dad9-295">您需要 tooget hello 根帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="4dad9-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="4dad9-296">您可以變更該資料夾的 hello 擁有權與您佈建 hello 機器時所使用的根 toohello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4dad9-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="4dad9-297">以下是範例與 hello azureuser 帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="4dad9-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="4dad9-298">使用 hello-R 選項 tooapply hello 權限的目錄內的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="4dad9-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="4dad9-299">此命令也適用於目錄。</span><span class="sxs-lookup"><span data-stu-id="4dad9-299">This command also works for directories.</span></span> <span data-ttu-id="4dad9-300">hello-R 選項變更 hello 所有檔案和目錄 hello 目錄內的權限。</span><span class="sxs-lookup"><span data-stu-id="4dad9-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="4dad9-301">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="4dad9-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="4dad9-302">此命令會變更擁有權 （使用者和群組） 的所有檔案和 hello 目錄內的目錄。</span><span class="sxs-lookup"><span data-stu-id="4dad9-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="4dad9-303">hello 下列命令只會變更 hello 資料夾目錄中的 hello 權的限。</span><span class="sxs-lookup"><span data-stu-id="4dad9-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="4dad9-304">hello 檔案與 hello 目錄內的資料夾不會變更。</span><span class="sxs-lookup"><span data-stu-id="4dad9-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
