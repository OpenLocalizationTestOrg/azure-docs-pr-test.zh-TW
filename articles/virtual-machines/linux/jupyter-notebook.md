---
title: "aaaCreate Jupyter/IPython 筆記型電腦 |Microsoft 文件"
description: "了解如何在 Linux 虛擬機器上的 toodeploy hello Jupyter/IPython 筆記型電腦建立 hello 資源管理員在 Azure 中的部署模型。"
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>在 Azure 上建立 Azure VM、安裝 Jupyter 並執行 Jupyter Notebook
hello [Jupyter 專案](http://jupyter.org)，先前稱為 hello [IPython 專案](http://ipython.org)，提供的工具集合，使用功能強大結合使用 hello 建立程式碼執行的互動式殼層科學運算即時運算文件。 這些 Notebook 文件可以包含任何文字、數學公式、輸入程式碼、結果、圖形、視訊，以及新型 Web 瀏覽器能夠顯示的其他任何類型的媒體。 您是絕對新 tooPython，且要 toolearn 有趣、 互動式環境或某些嚴重平行/技術運算、 hello Jupyter 筆記本是很好的選擇中。

![螢幕擷取畫面](./media/jupyter-notebook/ipy-notebook-spectral.png)使用 SciPy 和 Matplotlib 封裝 tooanalyze hello 結構的聲音錄製內容。

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter 的兩個方法：Azure Notebook 或自訂部署
Azure 提供的服務，您也可以使用[快速開始使用 Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)。  藉由使用 hello Azure 筆記本服務，您可以輕鬆地取得存取 tooJupyter 可存取 web 介面的所有 hello 電源的 Python 和許多的程式庫可調整計算資源。  因為 hello 安裝由 hello 服務，使用者可以存取這些資源，而 hello 需要在管理和設定由 hello 使用者。

如果 hello 筆記本服務不適用於您案例請繼續 tooread 本文這將會顯示如何 toodeploy hello Jupyter 筆記本，Microsoft Azure 上使用 Linux 虛擬機器 (Vm)。

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>在 Azure 上建立並設定 VM
hello 第一個步驟是 toocreate 在 Azure 上執行的虛擬機器 (VM)。
此 VM 是 hello 雲端中的完整作業系統，並將用來執行 hello Jupyter 筆記本。 Azure 能夠執行 Linux 和 Windows 虛擬機器，並且討論 hello Jupyter 這兩種類型的虛擬機器上安裝。

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>建立 Linux VM 並開啟適用於 Jupyter 的連接埠
請遵循所提供的 hello 指示[這裡][ portal-vm-linux] toocreate 虛擬機器的 hello *Ubuntu*發佈。 本教學課程使用 Ubuntu Server 14.04 LTS。 我們假設 hello 使用者名*azureuser*。

Hello 虛擬機器部署之後，我們必須 tooopen 向上 hello 網路安全性群組安全性規則。  從 hello Azure 入口網站，移過**網路安全性群組**和開啟 hello hello 安全性群組對應 tooyour VM 索引標籤。 您需要 tooadd 輸入安全性規則以 hello 下列設定： **TCP** hello 通訊協定，  **\***  hello 來源 （公用） 連接埠和**9999**的hello （私人） 目的地連接埠。

![螢幕擷取畫面](./media/jupyter-notebook/azure-add-endpoint.png)

在您網路的安全性群組，而按一下**網路介面**和附註 hello**公用 IP 位址**因為 hello 下一個步驟中將需要的 tooconnect tooyour VM。

## <a name="install-required-software-on-hello-vm"></a>在 hello VM 上安裝必要的軟體
toorun hello Jupyter 筆記本我們 VM 上，我們必須先安裝 Jupyter 和其相依性。 連接使用 ssh tooyour linux vm，然後建立時所選擇的 hello 使用者名稱/密碼組 hello vm。 在本教學課程中，我們將使用 PuTTY 並從 Windows 連接。

### <a name="installing-jupyter-on-ubuntu"></a>在 Ubuntu 上安裝 Jupyter
安裝 Anaconda 的常見資料科學 python 分佈中，使用其中一種從提供的 hello 連結[Continuum Analytics](https://www.continuum.io/downloads)。  Hello 撰寫此文件，hello 下列連結是 hello 最向上 toodate 版本。

#### <a name="anaconda-installs-for-linux"></a>適用於 Linux 的 Anaconda 安裝
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 位元</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 位元</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 位元</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 位元</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>在 Ubuntu 上安裝 Anaconda3 2.3.0 64 位元
例如，這是您可以在 Ubuntu 上安裝 Anaconda 的方式

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![螢幕擷取畫面](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>設定 Jupyter 並使用 SSL
在安裝之後我們需要 tootake 時刻 toosetup hello 設定檔 Jupyter。 如果您遇到的問題與設定 Jupyter 可能很有幫助 toolook 在 hello [Jupyter 筆記本 Server 文件](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html)。

下一步我們`cd`toohello 設定檔目錄 toocreate 我們的 SSL 憑證，然後編輯 hello 設定檔組態檔。

在 Linux 上使用下列命令的 hello。

    cd ~/.jupyter

使用下列命令 toocreate hello SSL 憑證 （Linux 和 Windows） 的 hello。

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

請注意，由於連接 toohello 筆記本時，我們會建立自我簽署的 SSL 憑證，您的瀏覽器會提供您的安全性警告。  用於長期實際執行環境，您會想 toouse 正確簽署的憑證與您的組織相關聯。  由於憑證管理超出範圍 hello 這個示範中，我們將著重 tooa 自我簽署的憑證現在。

此外 toousing 憑證，您必須也提供密碼 tooprotect 筆記本免於未經授權使用。  基於安全性理由 Jupyter 加密的密碼，其組態檔中，因此您需要 tooencrypt 密碼會先使用。  IPython 提供公用程式 toodo，;在命令提示字元執行下列命令的 hello。

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

這會提示您輸入密碼和確認訊息，並將然後列印 hello 密碼。 請注意此步驟之後的 hello。

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

接下來，我們將在其中編輯 hello 設定檔的組態檔，也就是`jupyter_notebook_config.py`您是在 hello 目錄中的檔案。  請注意，這個檔案可能不存在-在 hello 情形下直接建立。  此檔案有許多欄位，預設為注釋排除所有欄位。您可以使用您慣用的任何文字編輯器開啟這個檔案，您應該確定至少有 hello 下列內容。 **會在與 hello 先前步驟中的 hello sha1 hello 組態中的確定 tooreplace hello c.NotebookApp.password**。

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>執行 hello Jupyter 筆記本
此時我們已經準備好 toostart hello Jupyter 筆記本。 toodo，瀏覽您想 toostore 筆記本，並以下列命令的 hello 啟動 hello Jupyter 筆記本伺服器 toohello 目錄。

    /anaconda3/bin/jupyter-notebook

您現在應該會無法 tooaccess Jupyter 筆記本 hello 位址`https://[PUBLIC-IP-ADDRESS]:9999`。

當您第一次存取筆記本時，hello 登入頁面會要求您輸入密碼。 一旦您登入，您會看到 hello"Jupyter 筆記本儀表板 」，這是所有筆記本作業下時中心。  從此頁面中，您可以建立新 Notebook 和開啟現有 Notebook。

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>使用 hello Jupyter 筆記本
如果您按一下 hello**新增** 按鈕，您會看到下列開啟頁面上的 hello。

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-untitled-notebook.png)

hello 區域標記為`In []:`提示是 hello 輸入的區域中，您可以在這裡輸入有效的 Python 程式碼，且當您叫用時，它會執行`Shift-Enter`或按一下 hello 「 播放 」 圖示 （hello 指向右方的三角形 hello 工具列中）。

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>強大的典範：具有多樣化媒體的即時運算文件
hello 筆記本本身應該覺得很自然 tooanyone Python 和文書處理器，已使用的使用者，因為它是在某些方面兩者的混合： 您可以執行 Python 程式碼區塊，但您也可以讓便箋及其他文字，藉由變更從 「 程式碼 」 儲存格樣式 hello 太"Markdown 」 使用工具列中的 hello 下拉式選單。

Jupyter 不只是文字處理器，因為它能夠混合運算和多樣化媒體 (文字、圖形、視訊及新型網頁瀏覽器可以顯示的任何內容)。 您可以混合文字、程式碼、影片及更多項目！

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-editing-experience.png)

可以使用相同簡化為複雜的網路分析，在其中一種環境中的 hello 執行簡單的計算與 Python 的許多絕佳的程式庫用於科學運算，hello 下列螢幕擷取畫面中的 hello 電源。

此範例與即時計算混合的 hello 新式 web hello 電源提供許多的可能性，和最適合 hello 雲端;hello 筆記本可以用於：

* 探勘測試計算手寫板 toorecord 為處理問題。
* 與同事 '即時' 的計算表單中或硬拷貝格式 （HTML、 PDF） 會產生 tooshare。
* toodistribute 存在即時教學資料牽涉到計算，因此學生可以立即試驗 hello 真正的程式碼，進行修改並以互動方式重新執行。
* tooprovide"可執行檔白皮書"，都可以立即重新產生，而沒有 hello 結果的參考資料進行驗證，並由其他擴充。
* 做為計算的共同作業平台： 多個使用者可以登入 toothe 相同的筆記本伺服器 tooshare 即時計算的工作階段。

如果您 IPython 原始程式碼 toohello[儲存機制][repository]，您會發現使用筆記本的範例，其中您可以下載並在您自己的 Azure Jupyter VM 然後試驗整個目錄。  只要下載 hello`.ipynb`檔案 hello 從站台和將它們上傳到 Azure VM 筆記本的 hello 儀表板 （或直接在 hello VM 下載它們）。

## <a name="conclusion"></a>結論
hello Jupyter 筆記本提供功能強大的介面存取以互動方式在 Azure 上的 hello Python 生態系統的 hello 電源。  它涵蓋的用途範圍相當廣泛，包括簡單的探究和學習 Python、資料分析和視覺化、模擬和平行運算。 hello 產生筆記本文件包含 hello 計算會執行，而且可以與其他 Jupyter 使用者共用的完整記錄。  hello Jupyter 筆記本可以當做本機應用程式，但是它非常適合在 Azure 上的雲端部署

Jupyter hello 核心功能也會提供在 Visual Studio 中透過[Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS)。 PTVS 是 Microsoft 提供的免費開放原始碼外掛程式，可以將 Visual Studio 轉變為進階 Python 開發環境，其中包括具有 IntelliSense、偵錯、剖析和平行運算整合功能的進階編輯器。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
