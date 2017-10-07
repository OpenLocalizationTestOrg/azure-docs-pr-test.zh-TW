---
title: "為 IPython Notebook 伺服器的虛擬機器 aaaSet |Microsoft 文件"
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
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="0915b-103">將 Azure 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用</span><span class="sxs-lookup"><span data-stu-id="0915b-103">Set up an Azure virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="0915b-104">本主題說明如何 tooprovision 及設定 Azure 虛擬機器執行進階分析，可用來當做資料科學環境的一部分。</span><span class="sxs-lookup"><span data-stu-id="0915b-104">This topic shows how tooprovision and configure an Azure virtual machine for advanced analytics that can be used as part of a data science environment.</span></span> <span data-ttu-id="0915b-105">hello Windows 虛擬機器設定有支援 IPython 筆記型電腦、 Azure 儲存體總管、 AzCopy，以及可用於進階的分析專案的其他公用程式之類的工具。</span><span class="sxs-lookup"><span data-stu-id="0915b-105">hello Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, AzCopy, as well as other utilities that are useful for advanced analytics projects.</span></span> <span data-ttu-id="0915b-106">Azure 儲存體總管和 AzCopy，例如，提供方便的方式 tooupload 資料 tooAzure blob 儲存體從您的本機電腦或 toodownload 它 tooyour 從 blob 儲存體的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="0915b-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways tooupload data tooAzure blob storage from your local machine or toodownload it tooyour local machine from blob storage.</span></span>

## <span data-ttu-id="0915b-107"><a name="create-vm"></a>步驟 1：建立一般用途的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0915b-107"><a name="create-vm"></a>Step 1: Create a general-purpose Azure virtual machine</span></span>
<span data-ttu-id="0915b-108">如果您已經有 Azure 虛擬機器，而且只想 tooset IPython 筆記型電腦的伺服器上，則可以略過此步驟，並繼續太[步驟 2： 加入 IPython Notebook tooan 現有虛擬機器的端點](#add-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="0915b-108">If you already have an Azure virtual machine and just want tooset up an IPython Notebook server on it, you can skip this step and proceed too[Step 2: Add an endpoint for IPython Notebooks tooan existing virtual machine](#add-endpoint).</span></span>

<span data-ttu-id="0915b-109">開始之前的 Azure 上建立虛擬機器的 hello 程序，您需要其專案所需的 tooprocess hello 資料的 hello 機器 toodetermine hello 大小。</span><span class="sxs-lookup"><span data-stu-id="0915b-109">Before starting hello process of creating a virtual machine on Azure, you need toodetermine hello size of hello machine that is needed tooprocess hello data for their project.</span></span> <span data-ttu-id="0915b-110">比起較大型的機器，較小型的機器配備較少的記憶體和較少的 CPU 核心數目，但價格也較便宜。</span><span class="sxs-lookup"><span data-stu-id="0915b-110">Smaller machines have less memory and fewer CPU cores than larger machines, but they are also less expensive.</span></span> <span data-ttu-id="0915b-111">如需電腦類型和價格的清單，請參閱 hello<a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">虛擬機器定價</a>頁面</span><span class="sxs-lookup"><span data-stu-id="0915b-111">For a list of machine types and prices, see hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">Virtual Machines Pricing </a> page</span></span>

1. <span data-ttu-id="0915b-112">登入太<a href="https://manage.windowsazure.com" target="_blank">Azure 傳統入口網站</a>，然後按一下**新增**hello 左下角中。</span><span class="sxs-lookup"><span data-stu-id="0915b-112">Log in too<a href="https://manage.windowsazure.com" target="_blank">Azure classic portal</a>, and click **New** in hello bottom left corner.</span></span> <span data-ttu-id="0915b-113">隨即會快顯一個視窗。</span><span class="sxs-lookup"><span data-stu-id="0915b-113">A window will pop up.</span></span> <span data-ttu-id="0915b-114">選取 [計算] -> [虛擬機器] -> [從組件庫]。</span><span class="sxs-lookup"><span data-stu-id="0915b-114">Select **COMPUTE** -> **VIRTUAL MACHINE** -> **FROM GALLERY**.</span></span>
   
    ![建立工作區][24]
2. <span data-ttu-id="0915b-116">選擇其中一個 hello 下列影像：</span><span class="sxs-lookup"><span data-stu-id="0915b-116">Choose one of hello following images:</span></span>
   
   * <span data-ttu-id="0915b-117">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="0915b-117">Windows Server 2012 R2 Datacenter</span></span>
   * <span data-ttu-id="0915b-118">Windows Server Essentials 體驗 (Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="0915b-118">Windows Server Essentials Experience (Windows Server 2012 R2)</span></span>
     
     <span data-ttu-id="0915b-119">然後，按一下 hello 指向 hello 較低權限 toogo hello 下一個組態頁面的右邊的箭號。</span><span class="sxs-lookup"><span data-stu-id="0915b-119">Then, click hello arrow pointing right at hello lower right toogo hello next configuration page.</span></span>
     
     ![建立工作區][25]
3. <span data-ttu-id="0915b-121">輸入的名稱要 toocreate，選取 hello hello 機器大小為 hello 虛擬機器 (預設： A3) 根據 hello 資料 hello 機器 hello 大小會持續 tooprocess，而且您想 hello 機器 toobe （記憶體大小和 hello 數目計算核心） 的功能強大輸入 hello 機器使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0915b-121">Enter a name for hello virtual machine you want toocreate, select hello size of hello machine (Default: A3) based on hello size of hello data hello machine is going tooprocess and how powerful you want hello machine toobe (memory size and hello number of compute cores), enter a user name and password for hello machine.</span></span> <span data-ttu-id="0915b-122">然後，按一下 hello 箭號向右 toogo toohello 下一個組態頁面。</span><span class="sxs-lookup"><span data-stu-id="0915b-122">Then, click hello arrow pointing right toogo toohello next configuration page.</span></span>
   
    ![建立工作區][26]
4. <span data-ttu-id="0915b-124">選取 hello**區域/同質群組/虛擬網路**包含 hello**儲存體帳戶**toouse 此虛擬機器，計劃，然後選取該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0915b-124">Select hello **REGION/AFFINITY GROUP/VIRTUAL NETWORK** that contains hello **STORAGE ACCOUNT** that you are planning toouse for this virtual machine, and then select that storage account.</span></span> <span data-ttu-id="0915b-125">將端點加入在 hello hello 底部**端點**欄位輸入 hello hello 端點 ("IPython"這裡) 名稱。</span><span class="sxs-lookup"><span data-stu-id="0915b-125">Add an endpoint at hello bottom in hello **ENDPOINTS**  field by entering hello name of hello endpoint ("IPython" here).</span></span> <span data-ttu-id="0915b-126">您可以選擇任何字串 hello 做**名稱**hello 結束點，以及介於 0 到 65536 之間的任何整數**可用**為 hello**公用連接埠**。</span><span class="sxs-lookup"><span data-stu-id="0915b-126">You can choose any string as hello **NAME** of hello end point, and any integer between 0 and 65536 that is **available** as hello **PUBLIC PORT**.</span></span> <span data-ttu-id="0915b-127">hello**私用連接埠**具有 toobe **9999**。</span><span class="sxs-lookup"><span data-stu-id="0915b-127">hello **PRIVATE PORT** has toobe **9999**.</span></span> <span data-ttu-id="0915b-128">您應該**避免**使用已經指派給網際網路服務的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="0915b-128">You should **avoid** using public ports that have already been assigned for internet services.</span></span> <span data-ttu-id="0915b-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">適用於網際網路服務的連接埠</a>會提供已指派且應避免的連接埠清單。</span><span class="sxs-lookup"><span data-stu-id="0915b-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Ports for Internet Services</a> provides a list of ports that have been assigned and should be avoided.</span></span>
   
    ![建立工作區][27]
5. <span data-ttu-id="0915b-131">按一下 hello 核取記號 toostart hello 虛擬機器佈建程序。</span><span class="sxs-lookup"><span data-stu-id="0915b-131">Click hello check mark toostart hello virtual machine provisioning process.</span></span>
   
    ![建立工作區][28]

<span data-ttu-id="0915b-133">可能需要 15-25 分鐘 toocomplete hello 虛擬機器佈建程序。</span><span class="sxs-lookup"><span data-stu-id="0915b-133">It may take 15-25 minutes toocomplete hello virtual machine provisioning process.</span></span> <span data-ttu-id="0915b-134">建立 hello 虛擬機器之後，此機器 hello 狀態應該顯示為**執行**。</span><span class="sxs-lookup"><span data-stu-id="0915b-134">After hello virtual machine has been created, hello status of this machine should show as **Running**.</span></span>

![建立工作區][29]

## <span data-ttu-id="0915b-136"><a name="add-endpoint"></a>步驟 2： 新增 IPython Notebook tooan 現有虛擬機器的端點</span><span class="sxs-lookup"><span data-stu-id="0915b-136"><a name="add-endpoint"></a>Step 2: Add an endpoint for IPython Notebooks tooan existing virtual machine</span></span>
<span data-ttu-id="0915b-137">如果您在步驟 1 中的 hello 指示建立 hello 虛擬機器，然後 IPython 筆記型電腦的 hello 端點已經加入，並略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="0915b-137">If you created hello virtual machine by following hello instructions in Step 1, then hello endpoint for IPython Notebook has already been added and this step can be skipped.</span></span>

<span data-ttu-id="0915b-138">如果 hello 虛擬機器已存在，而且您需要您將在下面步驟 3 中安裝的 IPython 筆記型電腦 tooadd 端點，第一個登入 tooAzure 傳統入口網站，選取 hello 虛擬機器，並加入 IPython Notebook 伺服器 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="0915b-138">If hello virtual machine already exists, and you need tooadd an endpoint for IPython Notebook that you will install in Step 3 below, first login tooAzure classic portal, select hello virtual machine, and add hello endpoint for IPython Notebook server.</span></span> <span data-ttu-id="0915b-139">hello 圖包含 hello 入口網站的螢幕擷取畫面之後加入的 IPython 筆記型電腦的 hello 端點 tooa Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0915b-139">hello following figure contains a screen shot of hello portal after hello endpoint for IPython Notebook has been added tooa Windows virtual machine.</span></span>

![建立工作區][17]

## <span data-ttu-id="0915b-141"><a name="run-commands"></a>步驟 3：安裝 IPython Notebook 和其他支援工具</span><span class="sxs-lookup"><span data-stu-id="0915b-141"><a name="run-commands"></a>Step 3: Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="0915b-142">Hello 虛擬機器建立之後，使用遠端桌面通訊協定 (RDP) toolog toohello Windows 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="0915b-142">After hello virtual machine is created, use Remote Desktop Protocol (RDP) toolog on toohello Windows virtual machine.</span></span> <span data-ttu-id="0915b-143">如需指示，請參閱[如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0915b-143">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="0915b-144">開啟 hello**命令提示字元**(**不 hello Powershell 命令視窗**) 做為**管理員**和 hello 執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="0915b-144">Open hello **Command Prompt** (**Not hello Powershell command window**) as an **Administrator** and run hello following command.</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="0915b-145">Hello 安裝完成時，在 hello IPython Notebook 伺服器會自動啟動的 hello *c:\\使用者\\\<使用者名\>\\文件\\IPython筆記本*目錄。</span><span class="sxs-lookup"><span data-stu-id="0915b-145">When hello installation completes, hello IPython Notebook server is launched automatically in hello *C:\\Users\\\<user name\>\\Documents\\IPython Notebooks* directory.</span></span>

<span data-ttu-id="0915b-146">出現提示時，輸入 hello IPython 筆記型電腦的密碼和 hello hello 機器系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="0915b-146">When prompted, enter a password for hello IPython Notebook and hello password of hello machine administrator.</span></span> <span data-ttu-id="0915b-147">如此 hello IPython 筆記型電腦 toorun hello 電腦上以服務。</span><span class="sxs-lookup"><span data-stu-id="0915b-147">This enables hello IPython Notebook toorun as a service on hello machine.</span></span>

## <span data-ttu-id="0915b-148"><a name="access"></a>步驟 4：從網頁瀏覽器存取 IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="0915b-148"><a name="access"></a>Step 4: Access IPython Notebooks from a web browser</span></span>
<span data-ttu-id="0915b-149">tooaccess hello IPython Notebook 伺服器，開啟 web 瀏覽器，然後輸入*https://&#60;virtual 電腦的 DNS 名稱 >: & #60; 公用連接埠號碼 >* hello [URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="0915b-149">tooaccess hello IPython Notebook server, open a web browser, and input *https://&#60;virtual machine DNS name>:&#60;public port number>* in hello URL text box.</span></span> <span data-ttu-id="0915b-150">在這裡，hello *& #60; 公用連接埠號碼 >*應該是您指定當 hello IPython 筆記型電腦加入端點的 hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="0915b-150">Here, hello *&#60;public port number>* should  be hello port number you specified when hello IPython Notebook endpoint was added.</span></span>

<span data-ttu-id="0915b-151">hello *& #60; 虛擬機器 DNS 名稱 >*位於 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="0915b-151">hello *&#60;virtual machine DNS name>* can be found at hello Azure classic portal.</span></span> <span data-ttu-id="0915b-152">登入 toohello 傳統入口網站之後，按一下 [**虛擬機器**，選取您建立、，然後選取 hello 機器**儀表板**，hello DNS 名稱將會顯示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0915b-152">After logging in toohello classic portal, click **VIRTUAL MACHINES**, select hello machine you created, and then select **DASHBOARD**, hello DNS name will be shown as follows:</span></span>

![建立工作區][19]

<span data-ttu-id="0915b-154">您將會遇到警告，告知*沒有此網站的安全性憑證有問題*(Internet Explorer) 或*您的連接不是私用*(Chrome) 中 hello 下列所示數字。</span><span class="sxs-lookup"><span data-stu-id="0915b-154">You will encounter a warning stating that *There is a problem with this website's security certificate* (Internet Explorer) or *Your connection is not private* (Chrome), as shown in hello following figures.</span></span> <span data-ttu-id="0915b-155">按一下**繼續 toothis 網站 （不建議）** (Internet Explorer) 或**進階**然後**太繼續 & #60;*DNS 名稱*> （不安全） * * toocontinue (Chrome)。</span><span class="sxs-lookup"><span data-stu-id="0915b-155">Click **Continue toothis website (not recommended)** (Internet Explorer) or **Advanced** and then **Proceed too&#60;*DNS Name*> (unsafe)** (Chrome) toocontinue.</span></span> <span data-ttu-id="0915b-156">然後輸入您指定的早期 tooaccess hello IPython Notebook hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0915b-156">Then input hello password you specified earlier tooaccess hello IPython Notebooks.</span></span>

<span data-ttu-id="0915b-157">**Internet Explorer：**
![建立工作區][20]</span><span class="sxs-lookup"><span data-stu-id="0915b-157">**Internet Explorer:**
![Create workspace][20]</span></span>

<span data-ttu-id="0915b-158">**Chrome：**
![建立工作區][21]</span><span class="sxs-lookup"><span data-stu-id="0915b-158">**Chrome:**
![Create workspace][21]</span></span>

<span data-ttu-id="0915b-159">登入 toohello IPython 筆記型電腦，目錄之後*DataScienceSamples* hello 瀏覽器上會顯示。</span><span class="sxs-lookup"><span data-stu-id="0915b-159">After you log on toohello IPython Notebook, a directory *DataScienceSamples* will show on hello browser.</span></span> <span data-ttu-id="0915b-160">此目錄包含由 Microsoft toohelp 使用者進行資料科學工作所共用的範例 IPython Notebook。</span><span class="sxs-lookup"><span data-stu-id="0915b-160">This directory contains sample IPython Notebooks that are shared by Microsoft toohelp users conduct data science tasks.</span></span> <span data-ttu-id="0915b-161">這些範例 IPython Notebook 從簽出[ **GitHub 儲存機制**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello hello IPython 筆記型電腦伺服器安裝程序期間的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0915b-161">These sample IPython Notebooks are checked out from [**GitHub repository**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello virtual machines during hello IPython Notebook server setup process.</span></span> <span data-ttu-id="0915b-162">Microsoft 會經常維護並更新此儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0915b-162">Microsoft maintains and updates this repository frequently.</span></span> <span data-ttu-id="0915b-163">使用者可能瀏覽 hello GitHub 儲存機制 tooget hello 最近更新的範例 IPython Notebook。</span><span class="sxs-lookup"><span data-stu-id="0915b-163">Users may visit hello GitHub repository tooget hello most recently updated sample IPython Notebooks.</span></span>
<span data-ttu-id="0915b-164">![建立工作區][18]</span><span class="sxs-lookup"><span data-stu-id="0915b-164">![Create workspace][18]</span></span>

## <span data-ttu-id="0915b-165"><a name="upload"></a>步驟 5： 上傳現有的 IPython 筆記型電腦從本機電腦 toohello IPython Notebook 伺服器</span><span class="sxs-lookup"><span data-stu-id="0915b-165"><a name="upload"></a>Step 5: Upload an existing IPython Notebook from a local machine toohello IPython Notebook server</span></span>
<span data-ttu-id="0915b-166">IPython Notebook 使用者 tooupload 現有的 IPython 筆記型電腦在其本機電腦 toohello hello 虛擬機器上的 IPython Notebook 伺服器上提供一個簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="0915b-166">IPython Notebooks provide an easy way for users tooupload an existing IPython Notebook on their local machines toohello IPython Notebook server on hello virtual machines.</span></span> <span data-ttu-id="0915b-167">登入 toohello IPython 筆記型電腦網頁瀏覽器中之後，按到 hello**目錄**IPython 筆記型電腦將會上傳到該 hello。</span><span class="sxs-lookup"><span data-stu-id="0915b-167">After you log on toohello IPython Notebook in a web browser, click into hello **directory** that hello IPython Notebook will be uploaded to.</span></span> <span data-ttu-id="0915b-168">然後，從在 hello hello 本機電腦中選取 [IPython 筆記型電腦.ipynb 檔案 tooupload**檔案總管**，並將拖放 toohello IPython 筆記型電腦目錄 hello web 瀏覽器上。</span><span class="sxs-lookup"><span data-stu-id="0915b-168">Then, select an IPython Notebook .ipynb file tooupload from hello local machine in hello **File Explorer**, and drag and drop it toohello IPython Notebook directory on hello web browser.</span></span> <span data-ttu-id="0915b-169">按一下 hello**上傳**按鈕，tooupload hello.ipynb 檔案 toohello IPython Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0915b-169">Click hello **Upload** button, tooupload hello .ipynb file toohello IPython Notebook server.</span></span> <span data-ttu-id="0915b-170">其他使用者接著就可以從 Web 瀏覽器開始使用它。</span><span class="sxs-lookup"><span data-stu-id="0915b-170">Other users can then start using it in from their web browsers.</span></span>

![建立工作區][22]

![建立工作區][23]

## <span data-ttu-id="0915b-173"><a name="shutdown"></a>關閉並取消配置未使用的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0915b-173"><a name="shutdown"></a>Shut down and de-allocate virtual machine when not in use</span></span>
<span data-ttu-id="0915b-174">Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。</span><span class="sxs-lookup"><span data-stu-id="0915b-174">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="0915b-175">tooensure，不會計費不使用虛擬機器時，它具有 toobe 中的 hello**已停止 （取消配置）**在不使用時的狀態。</span><span class="sxs-lookup"><span data-stu-id="0915b-175">tooensure that you are not being billed when not using your virtual machine, it has toobe in hello **Stopped (Deallocated)** state when not in use.</span></span>

> [!NOTE]
> <span data-ttu-id="0915b-176">如果您關閉 hello 虛擬機器從 hello VM （使用 Windows 電源選項），內部 hello VM 已停止，但會維持配置。</span><span class="sxs-lookup"><span data-stu-id="0915b-176">If you shut down hello virtual machine from inside hello VM (using Windows power options), hello VM is stopped but remains allocated.</span></span> <span data-ttu-id="0915b-177">不會繼續計費，toobe tooensure 一律停駐虛擬機器從 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0915b-177">tooensure you do not continue toobe billed, always stop virtual machines from hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="0915b-178">您也可以藉由呼叫停止 VM，透過 Powershell hello **ShutdownRoleOperation**太與 「 PostShutdownAction"等於"StoppedDeallocated"。</span><span class="sxs-lookup"><span data-stu-id="0915b-178">You can also stop hello VM through Powershell by calling **ShutdownRoleOperation** with "PostShutdownAction" equal too"StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="0915b-179">tooshut 向下，及取消配置 hello 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="0915b-179">tooshut down and deallocate hello virtual machine:</span></span>

1. <span data-ttu-id="0915b-180">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0915b-180">Log in toohello [Azure classic portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="0915b-181">選取**虛擬機器**從 hello 左側的導覽列。</span><span class="sxs-lookup"><span data-stu-id="0915b-181">Select **VIRTUAL MACHINES** from hello left navigation bar.</span></span>
3. <span data-ttu-id="0915b-182">在 hello 清單中的虛擬機器，按一下您的虛擬機器，然後移 toohello hello 名稱**儀表板**頁面。</span><span class="sxs-lookup"><span data-stu-id="0915b-182">In hello list of virtual machines, click on hello name of your virtual machine then go toohello **DASHBOARD** page.</span></span>
4. <span data-ttu-id="0915b-183">在 [hello hello 頁面底部，按一下**關機**。</span><span class="sxs-lookup"><span data-stu-id="0915b-183">At hello bottom of hello page, click **SHUTDOWN**.</span></span>

![VM 關閉][15]

<span data-ttu-id="0915b-185">hello 虛擬機器將會取消配置，但是不會刪除。</span><span class="sxs-lookup"><span data-stu-id="0915b-185">hello virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="0915b-186">您可以隨時從 hello Azure 傳統入口網站，以重新啟動您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0915b-186">You may restart your virtual machine at any time from hello Azure classic portal.</span></span>

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a><span data-ttu-id="0915b-187">Azure VM 已準備好 toouse： 後續步驟？</span><span class="sxs-lookup"><span data-stu-id="0915b-187">Your Azure VM is ready toouse: what's next?</span></span>
<span data-ttu-id="0915b-188">您的虛擬機器就準備好在您的資料科學練習 toouse。</span><span class="sxs-lookup"><span data-stu-id="0915b-188">Your virtual machine is now ready toouse in your data science exercises.</span></span> <span data-ttu-id="0915b-189">也可以使用 IPython Notebook 伺服器 hello 瀏覽和處理的資料，以及其他工作搭配使用 Azure 機器學習和 hello 資料科學的小組流程 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0915b-189">hello virtual machine is also ready for use as an IPython Notebook server for hello exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and hello Team Data Science Process.</span></span>

<span data-ttu-id="0915b-190">後續步驟的 hello hello 中對應資料科學的小組流程中的 hello[學習路徑](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)，而且可能包括將資料移入 HDInsight，程序、 範例它那里與 Azure 機器學習 hello 資料的準備步驟了解。</span><span class="sxs-lookup"><span data-stu-id="0915b-190">hello next steps in hello Team Data Science Process are mapped in hello [Learning Path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

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
