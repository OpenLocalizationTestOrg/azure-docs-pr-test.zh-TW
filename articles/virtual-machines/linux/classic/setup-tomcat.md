---
title: "在 Linux 虛擬機器上設定 Apache Tomcat | Microsoft Docs"
description: "了解如何使用執行 Linux 的 Azure 虛擬機器設定 Apache Tomcat7。"
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
ms.openlocfilehash: fa30c78a5a5d458ba8845c3c10b87538427786c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="318ed-103">使用 Azure 在 Linux 虛擬機器上設定 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="318ed-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="318ed-104">Apache Tomcat (或直接稱為 Tomcat，以往也稱為 Jakarta Tomcat) 是 Apache Software Foundation (ASF) 開發的開放原始碼 Web 伺服器和 Servlet 容器。</span><span class="sxs-lookup"><span data-stu-id="318ed-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="318ed-105">Tomcat 會實作 Sun Microsystems 提供的 Java Servlet 和 JavaServer Pages (JSP) 規格。</span><span class="sxs-lookup"><span data-stu-id="318ed-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="318ed-106">Tomcat 提供用來執行 Java 程式碼的純 Java HTTP 網頁伺服器環境。</span><span class="sxs-lookup"><span data-stu-id="318ed-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="318ed-107">在最簡單的組態中，Tomcat 會在單一作業系統處理序中執行。</span><span class="sxs-lookup"><span data-stu-id="318ed-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="318ed-108">此程序會執行 Java 虛擬機器 (JVM)。</span><span class="sxs-lookup"><span data-stu-id="318ed-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="318ed-109">從瀏覽器到 Tomcat 的每個 HTTP 要求都會以 Tomcat 程序中個別的執行緒形式予以處理。</span><span class="sxs-lookup"><span data-stu-id="318ed-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="318ed-110">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="318ed-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="318ed-111">本文說明如何使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="318ed-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="318ed-112">我們建議讓大部分的新部署使用 Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="318ed-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="318ed-113">若要透過 Resource Manager 範本使用 Open JDK 與 Tomcat 部署 Ubuntu VM 的詳細資訊，請參閱[本文](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/)。</span><span class="sxs-lookup"><span data-stu-id="318ed-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="318ed-114">在本文中，您將在 Linux 映像上安裝 Tomcat7 並且部署於 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="318ed-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="318ed-115">您將了解：</span><span class="sxs-lookup"><span data-stu-id="318ed-115">You will learn:</span></span>  

* <span data-ttu-id="318ed-116">如何在 Azure 中建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="318ed-117">如何準備 Tomcat7 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="318ed-118">如何安裝 Tomcat7。</span><span class="sxs-lookup"><span data-stu-id="318ed-118">How to install Tomcat7.</span></span>

<span data-ttu-id="318ed-119">假設您已經有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="318ed-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="318ed-120">如果沒有，您可以在 [Azure 網站](https://azure.microsoft.com/)上註冊免費試用版。</span><span class="sxs-lookup"><span data-stu-id="318ed-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="318ed-121">如果您擁有 MSDN 訂用帳戶，請參閱 [Microsoft Azure 特價：MSDN、MPN 及 BizSpark 優惠](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39)。</span><span class="sxs-lookup"><span data-stu-id="318ed-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="318ed-122">若要深入了解 Azure，請參閱 [什麼是 Azure？](https://azure.microsoft.com/overview/what-is-azure/)。</span><span class="sxs-lookup"><span data-stu-id="318ed-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="318ed-123">本文假設您有 Tomcat 和 Linux 的基本操作知識。</span><span class="sxs-lookup"><span data-stu-id="318ed-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="318ed-124">第 1 階段：建立映像。</span><span class="sxs-lookup"><span data-stu-id="318ed-124">Phase 1: Create an image</span></span>
<span data-ttu-id="318ed-125">在這個階段，您將在 Azure 中使用 Linux 映像建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="318ed-126">步驟 1：產生 SSH 驗證金鑰</span><span class="sxs-lookup"><span data-stu-id="318ed-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="318ed-127">SSH 對系統管理員而言是很重要的工具。</span><span class="sxs-lookup"><span data-stu-id="318ed-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="318ed-128">不過，不建議根據人為決定的密碼來設定存取安全性。</span><span class="sxs-lookup"><span data-stu-id="318ed-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="318ed-129">惡意使用者可以依據使用者名稱和弱式密碼侵入系統。</span><span class="sxs-lookup"><span data-stu-id="318ed-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="318ed-130">好消息是，有辦法保持遠端存取開啟，而且不需要擔心密碼。</span><span class="sxs-lookup"><span data-stu-id="318ed-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="318ed-131">此方法是由使用非對稱密碼編譯的驗證所組成。</span><span class="sxs-lookup"><span data-stu-id="318ed-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="318ed-132">使用者的私密金鑰就是一種授與驗證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="318ed-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="318ed-133">您甚至可以鎖定使用者的帳戶，而不允許密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="318ed-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="318ed-134">這個方法的另一個優點是，您不需要不同的密碼來登入不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="318ed-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="318ed-135">您可以使用所有伺服器上的個人私密金鑰進行驗證，因此不需要記住多組密碼。</span><span class="sxs-lookup"><span data-stu-id="318ed-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="318ed-136">依照下列步驟來產生 SSH 驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="318ed-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="318ed-137">從下列位置下載並安裝 PuTTYgen：[http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="318ed-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="318ed-138">執行 Puttygen.exe。</span><span class="sxs-lookup"><span data-stu-id="318ed-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="318ed-139">按一下 [產生]  來產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="318ed-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="318ed-140">在這個程序中，您可以在視窗中的空白區域移動滑鼠來提高隨機性。</span><span class="sxs-lookup"><span data-stu-id="318ed-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="318ed-141">![PuTTY 金鑰產生器螢幕擷取畫面，其中顯示 [產生新金鑰] 按鈕][1]</span><span class="sxs-lookup"><span data-stu-id="318ed-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="318ed-142">在產生程序之後，Puttygen.exe 會顯示新的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="318ed-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![PuTTY 金鑰產生器螢幕擷取畫面，其中顯示新的公開金鑰和 [儲存私密金鑰] 按鈕][2]
5. <span data-ttu-id="318ed-144">選取並複製公開金鑰，並將它儲存在名為 publicKey.pem 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="318ed-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="318ed-145">不要按 [儲存公開金鑰] ，因為儲存的公開金鑰檔案格式與我們想要的公開金鑰不同。</span><span class="sxs-lookup"><span data-stu-id="318ed-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="318ed-146">按一下 [儲存私密金鑰]，並將它儲存在名為 privateKey.ppk 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="318ed-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="318ed-147">步驟 2：在 Azure 入口網站中建立映像</span><span class="sxs-lookup"><span data-stu-id="318ed-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="318ed-148">在[入口網站](https://portal.azure.com/)中，按一下工作列中的 [新增] 來建立映像。</span><span class="sxs-lookup"><span data-stu-id="318ed-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="318ed-149">然後根據您的需求選擇 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="318ed-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="318ed-150">下列範例使用 Ubuntu 14.04 映像。</span><span class="sxs-lookup"><span data-stu-id="318ed-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="318ed-151">![顯示 [新增] 按鈕的入口網站螢幕擷取畫面][3]</span><span class="sxs-lookup"><span data-stu-id="318ed-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="318ed-152">對於 [主機名稱]，指定您和網際網路用戶端將用來存取此虛擬機器的 URL 名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="318ed-153">定義 DNS 名稱的最後一個部分，例如 tomcatdemo。</span><span class="sxs-lookup"><span data-stu-id="318ed-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="318ed-154">Azure 會接著產生如 tomcatdemo.cloudapp.net 的 URL。</span><span class="sxs-lookup"><span data-stu-id="318ed-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="318ed-155">對於 [SSH 驗證金鑰]，從 publicKey.pem 檔案複製金鑰值，其中包含 PuTTYgen 所產生的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="318ed-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="318ed-156">![入口網站中的 [SSH 驗證金鑰] 方塊][4]</span><span class="sxs-lookup"><span data-stu-id="318ed-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="318ed-157">視需要設定其他設定，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="318ed-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="318ed-158">第 2 階段：準備用於 Tomcat7 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="318ed-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="318ed-159">在這個階段，您將設定 Tomcat 流量的端點，然後連線到新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="318ed-160">步驟 1：開啟允許 Web 存取的 HTTP 連接埠</span><span class="sxs-lookup"><span data-stu-id="318ed-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="318ed-161">Azure 中的端點包含 TCP 或 UDP 通訊協定，以及公用和私人連接埠。</span><span class="sxs-lookup"><span data-stu-id="318ed-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="318ed-162">私人連接埠是服務在虛擬機器上接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="318ed-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="318ed-163">公用連接埠是 Azure 雲端服務接聽外部內送、網際網路流量的連接埠。</span><span class="sxs-lookup"><span data-stu-id="318ed-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="318ed-164">TCP 連接埠 8080 是 Tomcat 用於接聽的預設連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="318ed-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="318ed-165">如果使用 Azure 端點開啟這個連接埠，您和其他網際網路用戶端即可存取 Tomcat 頁面。</span><span class="sxs-lookup"><span data-stu-id="318ed-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="318ed-166">在入口網站中，按一下 [瀏覽]  > [虛擬機器]，然後按一下您建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="318ed-167">![虛擬機器目錄的螢幕擷取畫面][5]</span><span class="sxs-lookup"><span data-stu-id="318ed-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="318ed-168">若要將端點新增至虛擬機器，請按一下 [端點]  方塊。</span><span class="sxs-lookup"><span data-stu-id="318ed-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="318ed-169">![顯示 [端點] 方塊的螢幕擷取畫面][6]</span><span class="sxs-lookup"><span data-stu-id="318ed-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="318ed-170">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="318ed-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="318ed-171">對於端點，在 [端點] 中輸入端點的名稱，然後在 [公用連接埠] 中輸入 80。</span><span class="sxs-lookup"><span data-stu-id="318ed-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="318ed-172">如果設定為 80，您就不需要在用來存取 Tomcat 的 URL 中包含連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="318ed-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="318ed-173">例如，http://tomcatdemo.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="318ed-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="318ed-174">如果您將它設定為另一個值 (例如 81)，您就必須將此連接埠號碼新增 URL 才能存取 Tomcat。</span><span class="sxs-lookup"><span data-stu-id="318ed-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="318ed-175">例如，http://tomcatdemo.cloudapp.net:81/。</span><span class="sxs-lookup"><span data-stu-id="318ed-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="318ed-176">在 [私人連接埠] 中輸入 8080。</span><span class="sxs-lookup"><span data-stu-id="318ed-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="318ed-177">Tomcat 預設會接聽 TCP 連接埠 8080。</span><span class="sxs-lookup"><span data-stu-id="318ed-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="318ed-178">如果您變更 Tomcat 的預設接聽連接埠，則必須更新 [私人連接埠]，使其與 Tomcat 接聽連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="318ed-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="318ed-179">![UI 的螢幕擷取畫面，其中顯示 [新增] 命令、[公用連接埠] 和 [私人連接埠]][7]</span><span class="sxs-lookup"><span data-stu-id="318ed-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="318ed-180">按一下 [確定]  ，將端點加入您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="318ed-181">步驟 2：連線到您建立的映像</span><span class="sxs-lookup"><span data-stu-id="318ed-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="318ed-182">您可以選擇任何 SSH 工具來連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="318ed-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="318ed-183">在此範例中，我們使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="318ed-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="318ed-184">從入口網站取得您虛擬機器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="318ed-185">按一下 [瀏覽] > [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="318ed-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="318ed-186">選取虛擬機器的名稱，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="318ed-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="318ed-187">在 [屬性] 圖格中，查看 [網域名稱] 方塊以取得 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="318ed-188">從 [SSH] 方塊取得 SSH 連線的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="318ed-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="318ed-189">![顯示 SSH 連線連接埠號碼的螢幕擷取畫面][8]</span><span class="sxs-lookup"><span data-stu-id="318ed-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="318ed-190">下載 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="318ed-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="318ed-191">下載之後，按一下可執行檔 Putty.exe。</span><span class="sxs-lookup"><span data-stu-id="318ed-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="318ed-192">在 PuTTY 組態中，使用從虛擬機器屬性取得的主機名稱和連接埠號碼設定基本選項。</span><span class="sxs-lookup"><span data-stu-id="318ed-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![顯示 PuTTY 組態主機名稱和連接埠選項的螢幕擷取畫面][9]

5. <span data-ttu-id="318ed-194">在左窗格中，按一下 [連線]  > [SSH]  > [驗證]，然後按一下 [瀏覽] 來指定 privateKey.ppk 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="318ed-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="318ed-195">PrivateKey.ppk 檔案包含 PuTTYgen 稍早在本文的＜第 1 階段：建立映像＞一節中產生的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="318ed-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="318ed-196">![顯示連線目錄階層和 [瀏覽] 按鈕的螢幕擷取畫面][10]</span><span class="sxs-lookup"><span data-stu-id="318ed-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="318ed-197">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="318ed-197">Click **Open**.</span></span> <span data-ttu-id="318ed-198">您可能會收到警告訊息方塊。</span><span class="sxs-lookup"><span data-stu-id="318ed-198">You might be alerted by a message box.</span></span> <span data-ttu-id="318ed-199">如果您已正確設定 DNS 名稱和連接埠號碼，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="318ed-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="318ed-200">![顯示通知的螢幕擷取畫面][11]</span><span class="sxs-lookup"><span data-stu-id="318ed-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="318ed-201">系統會提示您輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-201">You are prompted to enter your username.</span></span>  
![螢幕擷取畫面，其中顯示輸入使用者名稱的位置][12]

8. <span data-ttu-id="318ed-203">輸入您稍早在本文的＜第 1 階段：建立映像＞一節中用來建立虛擬機器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="318ed-204">您會看到類似下列的畫面：</span><span class="sxs-lookup"><span data-stu-id="318ed-204">You will see something like the following:</span></span>  
![顯示驗證確認的螢幕擷取畫面][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="318ed-206">第 3 階段：安裝軟體</span><span class="sxs-lookup"><span data-stu-id="318ed-206">Phase 3: Install software</span></span>
<span data-ttu-id="318ed-207">在這個階段，您會安裝 Java 執行階段環境、Tomcat7 和其他 Tomcat7 元件。</span><span class="sxs-lookup"><span data-stu-id="318ed-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="318ed-208">Java 執行階段環境</span><span class="sxs-lookup"><span data-stu-id="318ed-208">Java runtime environment</span></span>
<span data-ttu-id="318ed-209">Tomcat 是以 Java 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="318ed-209">Tomcat is written in Java.</span></span> <span data-ttu-id="318ed-210">Java 開發套件 (JDK) 有兩種類型 (OpenJDK 和 Oracle JDK)。</span><span class="sxs-lookup"><span data-stu-id="318ed-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="318ed-211">您可以選擇所需的其中一個。</span><span class="sxs-lookup"><span data-stu-id="318ed-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="318ed-212">這兩個 JDK 對於 Java API 中的類別有幾乎相同的程式碼，但是對於虛擬機器的程式碼則有所不同。</span><span class="sxs-lookup"><span data-stu-id="318ed-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="318ed-213">OpenJDK 傾向使用開放程式庫，而 Oracle JDK 傾向於使用非開放程式庫。</span><span class="sxs-lookup"><span data-stu-id="318ed-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="318ed-214">Oracle JDK 有較多的類別和一些已修復的錯誤，而 Oracle JDK 則比 OpenJDK 穩定。</span><span class="sxs-lookup"><span data-stu-id="318ed-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="318ed-215">安裝 OpenJDK</span><span class="sxs-lookup"><span data-stu-id="318ed-215">Install OpenJDK</span></span>  

<span data-ttu-id="318ed-216">使用下列命令來下載 OpenJDK。</span><span class="sxs-lookup"><span data-stu-id="318ed-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="318ed-217">若要建立包含 JDK 檔案的目錄：</span><span class="sxs-lookup"><span data-stu-id="318ed-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="318ed-218">若要將 JDK 檔案擷取到 /usr/lib/jvm/ 目錄：</span><span class="sxs-lookup"><span data-stu-id="318ed-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="318ed-219">安裝 Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="318ed-219">Install Oracle JDK</span></span>


<span data-ttu-id="318ed-220">使用下列命令從 Oracle 網站下載 Oracle JDK。</span><span class="sxs-lookup"><span data-stu-id="318ed-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="318ed-221">若要建立包含 JDK 檔案的目錄：</span><span class="sxs-lookup"><span data-stu-id="318ed-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="318ed-222">若要將 JDK 檔案擷取到 /usr/lib/jvm/ 目錄：</span><span class="sxs-lookup"><span data-stu-id="318ed-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="318ed-223">若要將 Oracle JDK 設定為預設 Java 虛擬機器︰</span><span class="sxs-lookup"><span data-stu-id="318ed-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="318ed-224">確認 Java 安裝成功</span><span class="sxs-lookup"><span data-stu-id="318ed-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="318ed-225">您可以使用如下所示的命令，測試是否已正確安裝 Java 執行階段環境：</span><span class="sxs-lookup"><span data-stu-id="318ed-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="318ed-226">如果您已安裝 OpenJDK，應該會看見如下的訊息：![OpenJDK 安裝成功訊息][14]</span><span class="sxs-lookup"><span data-stu-id="318ed-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="318ed-227">如果您已安裝 Oracle JDK，應該會看見如下的訊息：![Oracle JDK 安裝成功訊息][15]</span><span class="sxs-lookup"><span data-stu-id="318ed-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="318ed-228">安裝 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="318ed-228">Install Tomcat7</span></span>
<span data-ttu-id="318ed-229">使用下列命令來安裝 Tomcat7。</span><span class="sxs-lookup"><span data-stu-id="318ed-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="318ed-230">如果您不使用 Tomcat7，請適度修改此命令。</span><span class="sxs-lookup"><span data-stu-id="318ed-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="318ed-231">確認 Tomcat7 安裝成功</span><span class="sxs-lookup"><span data-stu-id="318ed-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="318ed-232">若要檢查是否已成功安裝 Tomcat7，請瀏覽至 Tomcat 伺服器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="318ed-233">在本文中，範例 URL 是 http://tomcatexample.cloudapp.net/。</span><span class="sxs-lookup"><span data-stu-id="318ed-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="318ed-234">如果您看到類似下列的訊息，則表示 Tomcat7 安裝正確。</span><span class="sxs-lookup"><span data-stu-id="318ed-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="318ed-235">![Tomcat7 安裝成功訊息][16]</span><span class="sxs-lookup"><span data-stu-id="318ed-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="318ed-236">安裝其他 Tomcat7 元件</span><span class="sxs-lookup"><span data-stu-id="318ed-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="318ed-237">您也可以安裝其他選用 Tomcat 元件。</span><span class="sxs-lookup"><span data-stu-id="318ed-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="318ed-238">使用 **sudo apt-cache search tomcat7** 命令來查看所有可用的元件。</span><span class="sxs-lookup"><span data-stu-id="318ed-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="318ed-239">使用下列命令來安裝一些實用的元件。</span><span class="sxs-lookup"><span data-stu-id="318ed-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="318ed-240">第 4 階段：設定 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="318ed-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="318ed-241">在這個階段，您可以管理 Tomcat。</span><span class="sxs-lookup"><span data-stu-id="318ed-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="318ed-242">啟動和停止 Tomcat7</span><span class="sxs-lookup"><span data-stu-id="318ed-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="318ed-243">Tomcat7 伺服器會在您進行安裝時自動啟動。</span><span class="sxs-lookup"><span data-stu-id="318ed-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="318ed-244">您也可以使用下列命令啟動它：</span><span class="sxs-lookup"><span data-stu-id="318ed-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="318ed-245">若要停止 Tomcat7：</span><span class="sxs-lookup"><span data-stu-id="318ed-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="318ed-246">若要檢視 Tomcat7 的狀態：</span><span class="sxs-lookup"><span data-stu-id="318ed-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="318ed-247">若要重新啟動 Tomcat 服務：</span><span class="sxs-lookup"><span data-stu-id="318ed-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="318ed-248">Tomcat7 系統管理</span><span class="sxs-lookup"><span data-stu-id="318ed-248">Tomcat7 administration</span></span>
<span data-ttu-id="318ed-249">您可以編輯 Tomcat 使用者組態檔，以設定您的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="318ed-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="318ed-250">使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="318ed-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="318ed-251">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="318ed-251">Here is an example:</span></span>  
![顯示 sudo vi 命令輸出的螢幕擷取畫面][17]  

> [!NOTE]
> <span data-ttu-id="318ed-253">建立系統管理員使用者名稱的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="318ed-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="318ed-254">編輯此檔案之後，您應該使用下列命令重新啟動 Tomcat7 服務，以確保變更生效：</span><span class="sxs-lookup"><span data-stu-id="318ed-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="318ed-255">開啟瀏覽器，並輸入 **http://<your tomcat server DNS name>/manager/html** 做為 URL。</span><span class="sxs-lookup"><span data-stu-id="318ed-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="318ed-256">對於本文中的範例，URL 是 http://tomcatexample.cloudapp.net/manager/html。</span><span class="sxs-lookup"><span data-stu-id="318ed-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="318ed-257">連接之後，您應該會看到類似下面的內容：</span><span class="sxs-lookup"><span data-stu-id="318ed-257">After connecting, you should see something similar to the following:</span></span>  
![Tomcat Web 應用程式管理員的螢幕擷取畫面][18]

## <a name="common-issues"></a><span data-ttu-id="318ed-259">常見問題</span><span class="sxs-lookup"><span data-stu-id="318ed-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="318ed-260">無法從網際網路存取使用 Tomcat 和 Moodle 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="318ed-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="318ed-261">徵狀</span><span class="sxs-lookup"><span data-stu-id="318ed-261">Symptom</span></span>  
  <span data-ttu-id="318ed-262">Tomcat 正在執行中，但無法使用瀏覽器來查看 Tomcat 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="318ed-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="318ed-263">可能的根本原因</span><span class="sxs-lookup"><span data-stu-id="318ed-263">Possible root cause</span></span>   

  * <span data-ttu-id="318ed-264">Tomcat 接聽連接埠與虛擬機器上用於 Tomcat 流量的端點私人連接埠不同。</span><span class="sxs-lookup"><span data-stu-id="318ed-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="318ed-265">檢查您的公用連接埠和私人連接埠端點設定，並確定私人連接埠與 Tomcat 接聽連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="318ed-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="318ed-266">請參閱本文＜第 1 階段：建立映像＞一節，以取得為虛擬機器設定端點的指示。</span><span class="sxs-lookup"><span data-stu-id="318ed-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="318ed-267">若要決定 Tomcat 接聽連接埠，請開啟 /etc/httpd/conf/httpd.conf (Red Hat 版本) 或 /etc/tomcat7/server.xml (Debian 版本)。</span><span class="sxs-lookup"><span data-stu-id="318ed-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="318ed-268">Tomcat 接聽連接埠預設為 8080。</span><span class="sxs-lookup"><span data-stu-id="318ed-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="318ed-269">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="318ed-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="318ed-270">如果您使用 Debian 或 Ubuntu 之類的虛擬機器，而且您要變更 Tomcat 接聽的預設連接埠 (例如 8081)，您也應該對於作業系統開啟該連接埠。</span><span class="sxs-lookup"><span data-stu-id="318ed-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="318ed-271">首先，開啟設定檔：</span><span class="sxs-lookup"><span data-stu-id="318ed-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="318ed-272">然後移除最後一行的註解，並將「否」變更為「是」。</span><span class="sxs-lookup"><span data-stu-id="318ed-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="318ed-273">防火牆已停用 Tomcat 的接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="318ed-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="318ed-274">您只可以從本機主機看見 Tomcat 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="318ed-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="318ed-275">此問題很可能是防火牆封鎖了 Tomcat 所接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="318ed-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="318ed-276">您可以使用 w3m 工具瀏覽網頁。</span><span class="sxs-lookup"><span data-stu-id="318ed-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="318ed-277">下列命令會安裝 w3m，並瀏覽至 Tomcat 預設頁面：</span><span class="sxs-lookup"><span data-stu-id="318ed-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="318ed-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="318ed-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="318ed-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="318ed-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="318ed-280">方案</span><span class="sxs-lookup"><span data-stu-id="318ed-280">Solution</span></span>

  * <span data-ttu-id="318ed-281">如果 Tomcat 接聽連接埠與虛擬機器上用於流量的端點私人連接埠不同，您需要將私人連接埠變更為與 tomcat 接聽連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="318ed-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="318ed-282">如果問題是由防火牆/iptables 造成，請在 /etc/sysconfig/iptables 中新增下列幾行。</span><span class="sxs-lookup"><span data-stu-id="318ed-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="318ed-283">https 流量才需要第二行：</span><span class="sxs-lookup"><span data-stu-id="318ed-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="318ed-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="318ed-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="318ed-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="318ed-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="318ed-286">確定上述幾行位於會全域限制存取的任何程式行上方，例如下列這一行：-A INPUT -j REJECT --reject-with icmp-host-prohibited</span><span class="sxs-lookup"><span data-stu-id="318ed-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="318ed-287">若要重新載入 iptables，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="318ed-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="318ed-288">這在 CentOS 6.3 上已經過測試。</span><span class="sxs-lookup"><span data-stu-id="318ed-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="318ed-289">將專案檔案上傳到 /var/lib/tomcat7/webapps/ 時權限遭拒</span><span class="sxs-lookup"><span data-stu-id="318ed-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="318ed-290">徵狀</span><span class="sxs-lookup"><span data-stu-id="318ed-290">Symptom</span></span>
  <span data-ttu-id="318ed-291">當您使用 SFTP 用戶端 (例如 FileZilla) 連線到虛擬機器，並瀏覽到 /var/lib/tomcat7/webapps/ 以發佈網站時，您收到類似下列的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="318ed-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="318ed-292">可能的根本原因</span><span class="sxs-lookup"><span data-stu-id="318ed-292">Possible root cause</span></span>
  <span data-ttu-id="318ed-293">您沒有存取 /var/lib/tomcat7/webapps 資料夾的權限。</span><span class="sxs-lookup"><span data-stu-id="318ed-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="318ed-294">方案</span><span class="sxs-lookup"><span data-stu-id="318ed-294">Solution</span></span>  
  <span data-ttu-id="318ed-295">您需要從 root 帳戶取得權限。</span><span class="sxs-lookup"><span data-stu-id="318ed-295">You need to get permission from the root account.</span></span> <span data-ttu-id="318ed-296">您可以將該資料夾的擁有權從 root 變更為佈建機器時所用的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="318ed-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="318ed-297">下列是一個 azureuser 帳戶名稱的範例：</span><span class="sxs-lookup"><span data-stu-id="318ed-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="318ed-298">使用-R 選項對目錄內的所有檔案也一併套用權限。</span><span class="sxs-lookup"><span data-stu-id="318ed-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="318ed-299">此命令也適用於目錄。</span><span class="sxs-lookup"><span data-stu-id="318ed-299">This command also works for directories.</span></span> <span data-ttu-id="318ed-300">-R 選項會變更目錄內所有檔案和目錄的權限。</span><span class="sxs-lookup"><span data-stu-id="318ed-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="318ed-301">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="318ed-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="318ed-302">此命令會變更目錄內所有檔案和目錄的擁有權 (使用者和群組兩者)。</span><span class="sxs-lookup"><span data-stu-id="318ed-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="318ed-303">下列命令只會變更資料夾目錄的權限。</span><span class="sxs-lookup"><span data-stu-id="318ed-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="318ed-304">但不會變更目錄內的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="318ed-304">The files and folders inside the directory are not changed.</span></span>  

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
