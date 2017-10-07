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
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>將 Azure 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用
本主題說明如何 tooprovision 及設定 Azure 虛擬機器執行進階分析，可用來當做資料科學環境的一部分。 hello Windows 虛擬機器設定有支援 IPython 筆記型電腦、 Azure 儲存體總管、 AzCopy，以及可用於進階的分析專案的其他公用程式之類的工具。 Azure 儲存體總管和 AzCopy，例如，提供方便的方式 tooupload 資料 tooAzure blob 儲存體從您的本機電腦或 toodownload 它 tooyour 從 blob 儲存體的本機電腦。

## <a name="create-vm"></a>步驟 1：建立一般用途的 Azure 虛擬機器
如果您已經有 Azure 虛擬機器，而且只想 tooset IPython 筆記型電腦的伺服器上，則可以略過此步驟，並繼續太[步驟 2： 加入 IPython Notebook tooan 現有虛擬機器的端點](#add-endpoint)。

開始之前的 Azure 上建立虛擬機器的 hello 程序，您需要其專案所需的 tooprocess hello 資料的 hello 機器 toodetermine hello 大小。 比起較大型的機器，較小型的機器配備較少的記憶體和較少的 CPU 核心數目，但價格也較便宜。 如需電腦類型和價格的清單，請參閱 hello<a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">虛擬機器定價</a>頁面

1. 登入太<a href="https://manage.windowsazure.com" target="_blank">Azure 傳統入口網站</a>，然後按一下**新增**hello 左下角中。 隨即會快顯一個視窗。 選取 [計算] -> [虛擬機器] -> [從組件庫]。
   
    ![建立工作區][24]
2. 選擇其中一個 hello 下列影像：
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials 體驗 (Windows Server 2012 R2)
     
     然後，按一下 hello 指向 hello 較低權限 toogo hello 下一個組態頁面的右邊的箭號。
     
     ![建立工作區][25]
3. 輸入的名稱要 toocreate，選取 hello hello 機器大小為 hello 虛擬機器 (預設： A3) 根據 hello 資料 hello 機器 hello 大小會持續 tooprocess，而且您想 hello 機器 toobe （記憶體大小和 hello 數目計算核心） 的功能強大輸入 hello 機器使用者名稱和密碼。 然後，按一下 hello 箭號向右 toogo toohello 下一個組態頁面。
   
    ![建立工作區][26]
4. 選取 hello**區域/同質群組/虛擬網路**包含 hello**儲存體帳戶**toouse 此虛擬機器，計劃，然後選取該儲存體帳戶。 將端點加入在 hello hello 底部**端點**欄位輸入 hello hello 端點 ("IPython"這裡) 名稱。 您可以選擇任何字串 hello 做**名稱**hello 結束點，以及介於 0 到 65536 之間的任何整數**可用**為 hello**公用連接埠**。 hello**私用連接埠**具有 toobe **9999**。 您應該**避免**使用已經指派給網際網路服務的公用連接埠。 <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">適用於網際網路服務的連接埠</a>會提供已指派且應避免的連接埠清單。
   
    ![建立工作區][27]
5. 按一下 hello 核取記號 toostart hello 虛擬機器佈建程序。
   
    ![建立工作區][28]

可能需要 15-25 分鐘 toocomplete hello 虛擬機器佈建程序。 建立 hello 虛擬機器之後，此機器 hello 狀態應該顯示為**執行**。

![建立工作區][29]

## <a name="add-endpoint"></a>步驟 2： 新增 IPython Notebook tooan 現有虛擬機器的端點
如果您在步驟 1 中的 hello 指示建立 hello 虛擬機器，然後 IPython 筆記型電腦的 hello 端點已經加入，並略過此步驟。

如果 hello 虛擬機器已存在，而且您需要您將在下面步驟 3 中安裝的 IPython 筆記型電腦 tooadd 端點，第一個登入 tooAzure 傳統入口網站，選取 hello 虛擬機器，並加入 IPython Notebook 伺服器 hello 端點。 hello 圖包含 hello 入口網站的螢幕擷取畫面之後加入的 IPython 筆記型電腦的 hello 端點 tooa Windows 虛擬機器。

![建立工作區][17]

## <a name="run-commands"></a>步驟 3：安裝 IPython Notebook 和其他支援工具
Hello 虛擬機器建立之後，使用遠端桌面通訊協定 (RDP) toolog toohello Windows 虛擬機器上。 如需指示，請參閱[如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 開啟 hello**命令提示字元**(**不 hello Powershell 命令視窗**) 做為**管理員**和 hello 執行下列命令。

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Hello 安裝完成時，在 hello IPython Notebook 伺服器會自動啟動的 hello *c:\\使用者\\\<使用者名\>\\文件\\IPython筆記本*目錄。

出現提示時，輸入 hello IPython 筆記型電腦的密碼和 hello hello 機器系統管理員密碼。 如此 hello IPython 筆記型電腦 toorun hello 電腦上以服務。

## <a name="access"></a>步驟 4：從網頁瀏覽器存取 IPython Notebook
tooaccess hello IPython Notebook 伺服器，開啟 web 瀏覽器，然後輸入*https://&#60;virtual 電腦的 DNS 名稱 >: & #60; 公用連接埠號碼 >* hello [URL] 文字方塊中。 在這裡，hello *& #60; 公用連接埠號碼 >*應該是您指定當 hello IPython 筆記型電腦加入端點的 hello 連接埠號碼。

hello *& #60; 虛擬機器 DNS 名稱 >*位於 hello Azure 傳統入口網站。 登入 toohello 傳統入口網站之後，按一下 [**虛擬機器**，選取您建立、，然後選取 hello 機器**儀表板**，hello DNS 名稱將會顯示，如下所示：

![建立工作區][19]

您將會遇到警告，告知*沒有此網站的安全性憑證有問題*(Internet Explorer) 或*您的連接不是私用*(Chrome) 中 hello 下列所示數字。 按一下**繼續 toothis 網站 （不建議）** (Internet Explorer) 或**進階**然後**太繼續 & #60;*DNS 名稱*> （不安全） * * toocontinue (Chrome)。 然後輸入您指定的早期 tooaccess hello IPython Notebook hello 密碼。

**Internet Explorer：**
![建立工作區][20]

**Chrome：**
![建立工作區][21]

登入 toohello IPython 筆記型電腦，目錄之後*DataScienceSamples* hello 瀏覽器上會顯示。 此目錄包含由 Microsoft toohelp 使用者進行資料科學工作所共用的範例 IPython Notebook。 這些範例 IPython Notebook 從簽出[ **GitHub 儲存機制**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello hello IPython 筆記型電腦伺服器安裝程序期間的虛擬機器。 Microsoft 會經常維護並更新此儲存機制。 使用者可能瀏覽 hello GitHub 儲存機制 tooget hello 最近更新的範例 IPython Notebook。
![建立工作區][18]

## <a name="upload"></a>步驟 5： 上傳現有的 IPython 筆記型電腦從本機電腦 toohello IPython Notebook 伺服器
IPython Notebook 使用者 tooupload 現有的 IPython 筆記型電腦在其本機電腦 toohello hello 虛擬機器上的 IPython Notebook 伺服器上提供一個簡單的方法。 登入 toohello IPython 筆記型電腦網頁瀏覽器中之後，按到 hello**目錄**IPython 筆記型電腦將會上傳到該 hello。 然後，從在 hello hello 本機電腦中選取 [IPython 筆記型電腦.ipynb 檔案 tooupload**檔案總管**，並將拖放 toohello IPython 筆記型電腦目錄 hello web 瀏覽器上。 按一下 hello**上傳**按鈕，tooupload hello.ipynb 檔案 toohello IPython Notebook 伺服器。 其他使用者接著就可以從 Web 瀏覽器開始使用它。

![建立工作區][22]

![建立工作區][23]

## <a name="shutdown"></a>關閉並取消配置未使用的虛擬機器
Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。 tooensure，不會計費不使用虛擬機器時，它具有 toobe 中的 hello**已停止 （取消配置）**在不使用時的狀態。

> [!NOTE]
> 如果您關閉 hello 虛擬機器從 hello VM （使用 Windows 電源選項），內部 hello VM 已停止，但會維持配置。 不會繼續計費，toobe tooensure 一律停駐虛擬機器從 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。 您也可以藉由呼叫停止 VM，透過 Powershell hello **ShutdownRoleOperation**太與 「 PostShutdownAction"等於"StoppedDeallocated"。
> 
> 

tooshut 向下，及取消配置 hello 虛擬機器：

1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用您的帳戶。  
2. 選取**虛擬機器**從 hello 左側的導覽列。
3. 在 hello 清單中的虛擬機器，按一下您的虛擬機器，然後移 toohello hello 名稱**儀表板**頁面。
4. 在 [hello hello 頁面底部，按一下**關機**。

![VM 關閉][15]

hello 虛擬機器將會取消配置，但是不會刪除。 您可以隨時從 hello Azure 傳統入口網站，以重新啟動您的虛擬機器。

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>Azure VM 已準備好 toouse： 後續步驟？
您的虛擬機器就準備好在您的資料科學練習 toouse。 也可以使用 IPython Notebook 伺服器 hello 瀏覽和處理的資料，以及其他工作搭配使用 Azure 機器學習和 hello 資料科學的小組流程 hello 虛擬機器。

後續步驟的 hello hello 中對應資料科學的小組流程中的 hello[學習路徑](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)，而且可能包括將資料移入 HDInsight，程序、 範例它那里與 Azure 機器學習 hello 資料的準備步驟了解。

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
