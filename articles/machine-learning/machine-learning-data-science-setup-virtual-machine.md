---
title: "將虛擬機器設定為 IPython Notebook 伺服器 | Microsoft Docs"
description: "設定 Azure 虛擬機器，以在資料科學環境中搭配 IPython 伺服器進行進階分析。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 66fd9e5573390ac6faeb82ad5b0f7ddb18d50a77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="4b5c8-103">將 Azure 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用</span><span class="sxs-lookup"><span data-stu-id="4b5c8-103">Set up an Azure virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="4b5c8-104">本主題示範如何針對可用來做為資料科學環境一部分的進階分析，佈建及設定 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-104">This topic shows how to provision and configure an Azure virtual machine for advanced analytics that can be used as part of a data science environment.</span></span> <span data-ttu-id="4b5c8-105">Windows 虛擬機器是使用支援工具 (例如 IPython Notebook、Azure 儲存體總管、AzCopy)，以及其他對於進階分析專案非常實用的公用程式來設定。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, AzCopy, as well as other utilities that are useful for advanced analytics projects.</span></span> <span data-ttu-id="4b5c8-106">例如，Azure 儲存體總管和 AzCopy 會提供便利的方法，將資料從本機電腦上傳至 Azure Blob 儲存體，或者從 Blob 儲存體將資料下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure blob storage from your local machine or to download it to your local machine from blob storage.</span></span>

## <span data-ttu-id="4b5c8-107"><a name="create-vm"></a>步驟 1：建立一般用途的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4b5c8-107"><a name="create-vm"></a>Step 1: Create a general-purpose Azure virtual machine</span></span>
<span data-ttu-id="4b5c8-108">如果您已經具有 Azure 虛擬機器，而且只想在其上設定 IPython Notebook 伺服器，就可以略過這個步驟，繼續執行 [步驟 2：將 IPython Notebook 的端點加入現有的虛擬機器](#add-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-108">If you already have an Azure virtual machine and just want to set up an IPython Notebook server on it, you can skip this step and proceed to [Step 2: Add an endpoint for IPython Notebooks to an existing virtual machine](#add-endpoint).</span></span>

<span data-ttu-id="4b5c8-109">在 Azure 上建立虛擬機器的程序開始之前，您必須決定處理適用於其專案之資料所需的機器大小。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-109">Before starting the process of creating a virtual machine on Azure, you need to determine the size of the machine that is needed to process the data for their project.</span></span> <span data-ttu-id="4b5c8-110">比起較大型的機器，較小型的機器配備較少的記憶體和較少的 CPU 核心數目，但價格也較便宜。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-110">Smaller machines have less memory and fewer CPU cores than larger machines, but they are also less expensive.</span></span> <span data-ttu-id="4b5c8-111">如需機器類型和價格清單，請參閱<a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">虛擬機器定價</a>頁面</span><span class="sxs-lookup"><span data-stu-id="4b5c8-111">For a list of machine types and prices, see the <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">Virtual Machines Pricing </a> page</span></span>

1. <span data-ttu-id="4b5c8-112">登入 <a href="https://manage.windowsazure.com" target="_blank">Azure 傳統入口網站</a>，然後按一下左上角的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-112">Log in to <a href="https://manage.windowsazure.com" target="_blank">Azure classic portal</a>, and click **New** in the bottom left corner.</span></span> <span data-ttu-id="4b5c8-113">隨即會快顯一個視窗。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-113">A window will pop up.</span></span> <span data-ttu-id="4b5c8-114">選取 [計算] -> [虛擬機器] -> [從組件庫]。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-114">Select **COMPUTE** -> **VIRTUAL MACHINE** -> **FROM GALLERY**.</span></span>
   
    ![建立工作區][24]
2. <span data-ttu-id="4b5c8-116">選擇下列其中一個映像：</span><span class="sxs-lookup"><span data-stu-id="4b5c8-116">Choose one of the following images:</span></span>
   
   * <span data-ttu-id="4b5c8-117">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="4b5c8-117">Windows Server 2012 R2 Datacenter</span></span>
   * <span data-ttu-id="4b5c8-118">Windows Server Essentials 體驗 (Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="4b5c8-118">Windows Server Essentials Experience (Windows Server 2012 R2)</span></span>
     
     <span data-ttu-id="4b5c8-119">然後按一下右下方指向右側的箭號，前往下一個設定頁面。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-119">Then, click the arrow pointing right at the lower right to go the next configuration page.</span></span>
     
     ![建立工作區][25]
3. <span data-ttu-id="4b5c8-121">輸入您想要建立的虛擬機器名稱、根據機器即將處理的資料大小和您想要的機器功能有多強大 (記憶體大小和運算核心數目) 來選取機器的大小 (預設值：A3)、輸入機器的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-121">Enter a name for the virtual machine you want to create, select the size of the machine (Default: A3) based on the size of the data the machine is going to process and how powerful you want the machine to be (memory size and the number of compute cores), enter a user name and password for the machine.</span></span> <span data-ttu-id="4b5c8-122">接著，按一下指向右側的箭號，前往下一個設定頁面。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-122">Then, click the arrow pointing right to go to the next configuration page.</span></span>
   
    ![建立工作區][26]
4. <span data-ttu-id="4b5c8-124">選取 [區域/同質群組/虛擬網路]，其中包含您規劃要用於這部虛擬機器的 [儲存體帳戶]，然後選取該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-124">Select the **REGION/AFFINITY GROUP/VIRTUAL NETWORK** that contains the **STORAGE ACCOUNT** that you are planning to use for this virtual machine, and then select that storage account.</span></span> <span data-ttu-id="4b5c8-125">輸入端點的名稱 (此處為 "IPython")，藉此在 [端點] 欄位底部新增端點。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-125">Add an endpoint at the bottom in the **ENDPOINTS**  field by entering the name of the endpoint ("IPython" here).</span></span> <span data-ttu-id="4b5c8-126">您可以選擇任何字串做為端點的 [名稱]，以及任何介於 0 和 65536 之間的整數**用作** [公用連接埠]。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-126">You can choose any string as the **NAME** of the end point, and any integer between 0 and 65536 that is **available** as the **PUBLIC PORT**.</span></span> <span data-ttu-id="4b5c8-127">[私人連接埠] 必須為 **9999**。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-127">The **PRIVATE PORT** has to be **9999**.</span></span> <span data-ttu-id="4b5c8-128">您應該**避免**使用已經指派給網際網路服務的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-128">You should **avoid** using public ports that have already been assigned for internet services.</span></span> <span data-ttu-id="4b5c8-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">適用於網際網路服務的連接埠</a>會提供已指派且應避免的連接埠清單。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Ports for Internet Services</a> provides a list of ports that have been assigned and should be avoided.</span></span>
   
    ![建立工作區][27]
5. <span data-ttu-id="4b5c8-131">按一下勾號以啟動虛擬機器佈建程序。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-131">Click the check mark to start the virtual machine provisioning process.</span></span>
   
    ![建立工作區][28]

<span data-ttu-id="4b5c8-133">它可能需要 15-25 分鐘，才能完成虛擬機器佈建程序。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-133">It may take 15-25 minutes to complete the virtual machine provisioning process.</span></span> <span data-ttu-id="4b5c8-134">建立虛擬機器之後，這部機器的狀態應顯示為 [執行中] 。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-134">After the virtual machine has been created, the status of this machine should show as **Running**.</span></span>

![建立工作區][29]

## <span data-ttu-id="4b5c8-136"><a name="add-endpoint"></a>步驟 2：將 IPython Notebook 的端點新增到現有的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4b5c8-136"><a name="add-endpoint"></a>Step 2: Add an endpoint for IPython Notebooks to an existing virtual machine</span></span>
<span data-ttu-id="4b5c8-137">如果您已遵循步驟 1 中的指示建立虛擬機器，則已經新增適用於 IPython Notebook 的端點，可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-137">If you created the virtual machine by following the instructions in Step 1, then the endpoint for IPython Notebook has already been added and this step can be skipped.</span></span>

<span data-ttu-id="4b5c8-138">如果虛擬機器已經存在，而且您需要新增將在以下步驟 3 中安裝的 IPython Notebook 端點，請先登入 Azure 傳統入口網站、選取虛擬機器，然後新增 IPython Notebook 伺服器的端點。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-138">If the virtual machine already exists, and you need to add an endpoint for IPython Notebook that you will install in Step 3 below, first login to Azure classic portal, select the virtual machine, and add the endpoint for IPython Notebook server.</span></span> <span data-ttu-id="4b5c8-139">下圖包含在將 IPython Notebook 的端點新增到 Windows 虛擬機器之後入口網站的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-139">The following figure contains a screen shot of the portal after the endpoint for IPython Notebook has been added to a Windows virtual machine.</span></span>

![建立工作區][17]

## <span data-ttu-id="4b5c8-141"><a name="run-commands"></a>步驟 3：安裝 IPython Notebook 和其他支援工具</span><span class="sxs-lookup"><span data-stu-id="4b5c8-141"><a name="run-commands"></a>Step 3: Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="4b5c8-142">建立虛擬機器之後，請使用遠端桌面通訊協定 (RDP) 登入 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-142">After the virtual machine is created, use Remote Desktop Protocol (RDP) to log on to the Windows virtual machine.</span></span> <span data-ttu-id="4b5c8-143">如需指示，請參閱[如何登入執行 Windows Server 的虛擬機器](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-143">For instructions, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="4b5c8-144">以**系統管理員**身分開啟 **命令提示字元** (**不是 Powershell 命令視窗**)，並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-144">Open the **Command Prompt** (**Not the Powershell command window**) as an **Administrator** and run the following command.</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="4b5c8-145">完成安裝時，會在 *C:\\Users\\\<使用者名稱\>\\Documents\\IPython Notebooks* 目錄中自動啟動 IPython Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-145">When the installation completes, the IPython Notebook server is launched automatically in the *C:\\Users\\\<user name\>\\Documents\\IPython Notebooks* directory.</span></span>

<span data-ttu-id="4b5c8-146">出現提示時，請輸入 IPython Notebook 的密碼，以及機器系統管理員的密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-146">When prompted, enter a password for the IPython Notebook and the password of the machine administrator.</span></span> <span data-ttu-id="4b5c8-147">這讓 IPython Notebook 能夠做為機器上的服務來執行 。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-147">This enables the IPython Notebook to run as a service on the machine.</span></span>

## <span data-ttu-id="4b5c8-148"><a name="access"></a>步驟 4：從網頁瀏覽器存取 IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="4b5c8-148"><a name="access"></a>Step 4: Access IPython Notebooks from a web browser</span></span>
<span data-ttu-id="4b5c8-149">若要存取 IPython Notebook 伺服器，請開啟網頁瀏覽器，然後在 [URL] 文字方塊中輸入 *https://&#60;虛擬機器 DNS 名稱>:&#60;公用連接埠號碼>*。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-149">To access the IPython Notebook server, open a web browser, and input *https://&#60;virtual machine DNS name>:&#60;public port number>* in the URL text box.</span></span> <span data-ttu-id="4b5c8-150">其中 *&#60;公用連接埠號碼>* 應該是您在新增 IPython Notebook 端點時所指定的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-150">Here, the *&#60;public port number>* should  be the port number you specified when the IPython Notebook endpoint was added.</span></span>

<span data-ttu-id="4b5c8-151">在 Azure 傳統入口網站中可找到 *&#60;虛擬機器 DNS 名稱>*。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-151">The *&#60;virtual machine DNS name>* can be found at the Azure classic portal.</span></span> <span data-ttu-id="4b5c8-152">登入傳統入口網站之後，按一下 [虛擬機器]，並選取您建立的機器，然後選取 [儀表板]，DNS 名稱隨即顯示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b5c8-152">After logging in to the classic portal, click **VIRTUAL MACHINES**, select the machine you created, and then select **DASHBOARD**, the DNS name will be shown as follows:</span></span>

![建立工作區][19]

<span data-ttu-id="4b5c8-154">您將會看見一則警告，指出「此網站的安全性憑證有問題」(Internet Explorer) 或「您的連接不是私人連接」(Chrome)，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-154">You will encounter a warning stating that *There is a problem with this website's security certificate* (Internet Explorer) or *Your connection is not private* (Chrome), as shown in the following figures.</span></span> <span data-ttu-id="4b5c8-155">按一下 **繼續瀏覽此網站 (不建議)** (Internet Explorer)，或者依序按一下 **進階** 和 **前往 &#60;*DNS 名稱*> (不安全)** (Chrome)，以便繼續進行。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-155">Click **Continue to this website (not recommended)** (Internet Explorer) or **Advanced** and then **Proceed to &#60;*DNS Name*> (unsafe)** (Chrome) to continue.</span></span> <span data-ttu-id="4b5c8-156">接著，輸入您先前指定的密碼來存取 IPython Notebook。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-156">Then input the password you specified earlier to access the IPython Notebooks.</span></span>

<span data-ttu-id="4b5c8-157">**Internet Explorer：**
![建立工作區][20]</span><span class="sxs-lookup"><span data-stu-id="4b5c8-157">**Internet Explorer:**
![Create workspace][20]</span></span>

<span data-ttu-id="4b5c8-158">**Chrome：**
![建立工作區][21]</span><span class="sxs-lookup"><span data-stu-id="4b5c8-158">**Chrome:**
![Create workspace][21]</span></span>

<span data-ttu-id="4b5c8-159">登入 IPython Notebook 之後， *DataScienceSamples* 目錄將顯示在瀏覽器上。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-159">After you log on to the IPython Notebook, a directory *DataScienceSamples* will show on the browser.</span></span> <span data-ttu-id="4b5c8-160">此目錄包含由 Microsoft 共用的 IPython Notebook 範例，可協助使用者進行資料科學工作。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-160">This directory contains sample IPython Notebooks that are shared by Microsoft to help users conduct data science tasks.</span></span> <span data-ttu-id="4b5c8-161">這些 IPython Notebook 範例是在 IPython Notebook 伺服器設定程序期間，從 [**GitHub 存放庫**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)簽出至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-161">These sample IPython Notebooks are checked out from [**GitHub repository**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) to the virtual machines during the IPython Notebook server setup process.</span></span> <span data-ttu-id="4b5c8-162">Microsoft 會經常維護並更新此儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-162">Microsoft maintains and updates this repository frequently.</span></span> <span data-ttu-id="4b5c8-163">使用者可以瀏覽 GitHub 存放庫，以取得最近更新的 IPython Notebook 範例。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-163">Users may visit the GitHub repository to get the most recently updated sample IPython Notebooks.</span></span>
<span data-ttu-id="4b5c8-164">![建立工作區][18]</span><span class="sxs-lookup"><span data-stu-id="4b5c8-164">![Create workspace][18]</span></span>

## <span data-ttu-id="4b5c8-165"><a name="upload"></a>步驟 5：從本機電腦將現有的 IPython Notebook 上傳至 IPython Notebook 伺服器</span><span class="sxs-lookup"><span data-stu-id="4b5c8-165"><a name="upload"></a>Step 5: Upload an existing IPython Notebook from a local machine to the IPython Notebook server</span></span>
<span data-ttu-id="4b5c8-166">IPython Notebook 提供一種簡單的方式，讓使用者可將其本機電腦上現有的 IPython Notebook 上傳至虛擬機器上的 IPython Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-166">IPython Notebooks provide an easy way for users to upload an existing IPython Notebook on their local machines to the IPython Notebook server on the virtual machines.</span></span> <span data-ttu-id="4b5c8-167">當您在網頁瀏覽器上登入 IPython Notebook 之後，可按一下以進入將上傳 IPython Notebook 的 **目錄** 。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-167">After you log on to the IPython Notebook in a web browser, click into the **directory** that the IPython Notebook will be uploaded to.</span></span> <span data-ttu-id="4b5c8-168">然後，在 [ **檔案總管**] 中選取要從本機電腦上傳的 IPython Notebook .ipynb 檔案，並將其拖放到網頁瀏覽器上的 IPython Notebook 目錄。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-168">Then, select an IPython Notebook .ipynb file to upload from the local machine in the **File Explorer**, and drag and drop it to the IPython Notebook directory on the web browser.</span></span> <span data-ttu-id="4b5c8-169">按一下 [ **上傳** ] 按鈕，將 .ipynb 檔案上傳到 IPython Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-169">Click the **Upload** button, to upload the .ipynb file to the IPython Notebook server.</span></span> <span data-ttu-id="4b5c8-170">其他使用者接著就可以從 Web 瀏覽器開始使用它。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-170">Other users can then start using it in from their web browsers.</span></span>

![建立工作區][22]

![建立工作區][23]

## <span data-ttu-id="4b5c8-173"><a name="shutdown"></a>關閉並取消配置未使用的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4b5c8-173"><a name="shutdown"></a>Shut down and de-allocate virtual machine when not in use</span></span>
<span data-ttu-id="4b5c8-174">Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-174">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="4b5c8-175">若要確保未使用虛擬機器時不會被計費，當它閒置時，其狀態必須是 [ **已停止 (已取消配置)** ]。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-175">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state when not in use.</span></span>

> [!NOTE]
> <span data-ttu-id="4b5c8-176">如果您從 VM 內部關閉虛擬機器 (使用 Windows 電源選項)，雖然 VM 已停止，但仍然處於已配置狀態。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-176">If you shut down the virtual machine from inside the VM (using Windows power options), the VM is stopped but remains allocated.</span></span> <span data-ttu-id="4b5c8-177">若要確保系統不會繼續計費，請一律從 [Azure 傳統入口網站](http://manage.windowsazure.com/)停止虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-177">To ensure you do not continue to be billed, always stop virtual machines from the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="4b5c8-178">您也可以藉由呼叫 **ShutdownRoleOperation** 搭配相當於 "StoppedDeallocated" 的 "PostShutdownAction"，透過 Powershell 來停止 VM。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-178">You can also stop the VM through Powershell by calling **ShutdownRoleOperation** with "PostShutdownAction" equal to "StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="4b5c8-179">關閉及解除配置虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="4b5c8-179">To shut down and deallocate the virtual machine:</span></span>

1. <span data-ttu-id="4b5c8-180">使用您的帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-180">Log in to the [Azure classic portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="4b5c8-181">從左側導覽列選取 [ **虛擬機器** ]。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-181">Select **VIRTUAL MACHINES** from the left navigation bar.</span></span>
3. <span data-ttu-id="4b5c8-182">在虛擬機器清單中，按一下虛擬機器的名稱，然後移至 [ **儀表板** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-182">In the list of virtual machines, click on the name of your virtual machine then go to the **DASHBOARD** page.</span></span>
4. <span data-ttu-id="4b5c8-183">按一下頁面底部的 [ **關閉**]。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-183">At the bottom of the page, click **SHUTDOWN**.</span></span>

![VM 關閉][15]

<span data-ttu-id="4b5c8-185">虛擬機器將會取消配置，但不是刪除。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-185">The virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="4b5c8-186">您隨時都可從 Azure 傳統入口網站重新啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-186">You may restart your virtual machine at any time from the Azure classic portal.</span></span>

## <a name="your-azure-vm-is-ready-to-use-whats-next"></a><span data-ttu-id="4b5c8-187">您的 Azure VM 已準備好可供使用：下一步是什麼？</span><span class="sxs-lookup"><span data-stu-id="4b5c8-187">Your Azure VM is ready to use: what's next?</span></span>
<span data-ttu-id="4b5c8-188">您的虛擬機器已經準備好在資料科學練習中使用。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-188">Your virtual machine is now ready to use in your data science exercises.</span></span> <span data-ttu-id="4b5c8-189">虛擬機器也已經準備好用來做為 IPython Notebook 伺服器，以進行資料探索和處理，以及其他可與 Azure 機器學習服務和 Team Data Science Process 一起使用的工作。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-189">The virtual machine is also ready for use as an IPython Notebook server for the exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and the Team Data Science Process.</span></span>

<span data-ttu-id="4b5c8-190">[學習路徑](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 中說明了 Team Data Science Process 的後續步驟，其中可能包含將資料移至 HDInsight 並在其中處理資料與取樣，做為透過 Azure Machine Learning 從資料學習的準備。</span><span class="sxs-lookup"><span data-stu-id="4b5c8-190">The next steps in the Team Data Science Process are mapped in the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
