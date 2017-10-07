---
title: "aaaCreating hello Azure Marketplace 的虛擬機器映像 |Microsoft 文件"
description: "取得如何 toocreate 虛擬機器的映像 hello Azure Marketplace 供其他人 toopurchase 的詳細的指示。"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>指南 toocreate hello Azure Marketplace 的虛擬機器映像
這篇文章，**步驟 2**，會引導您完成準備 hello 虛擬硬碟 (Vhd) 會將部署 toohello Azure Marketplace。 您的 Vhd 是您 SKU 的 hello foundation。 您是否提供 Linux 或 Windows 為基礎的 SKU 有所不同 hello 程序。 本文將探討這兩種狀況。 這個程序可與[帳戶建立和註冊][link-acct-creation]同步執行。

## <a name="1-define-offers-and-skus"></a>1.定義供應項目和 SKU
在本節中，您將學會 toodefine hello 優惠和其相關聯的 Sku。

提供項目是其 Sku 的 「 父 」 tooall。 您可以擁有多個供應項目。 如何決定 toostructure 您提供項目是最多 tooyou。 當 toostaging 推入的供應項目時，它是推入及所有其 Sku。 請仔細評估 SKU 的識別項，因為它們會顯示在 hello URL:

* Azure.com：http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}
* Azure Preview 入口網站︰https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}  

SKU 不 hello 商業 VM 映像名稱。 VM 映像包含一個作業系統磁碟以及零或多個資料磁碟。 它是基本上 hello 完成存放裝置設定檔的虛擬機器。 每個磁碟都需要一個 VHD。 即使是空白的資料磁碟需要建立 VHD toobe。

不論您使用的作業系統，加入只 hello 最小數目的資料磁碟所需的 hello SKU。 客戶無法移除磁碟映像一起部署的 hello 次，但可以隨時加入磁碟期間或部署後可視需要。

> [!IMPORTANT]
> **請勿變更新映像版本中的磁碟計數。** 如果您必須重新設定 hello 映像中的資料磁碟，定義新的 SKU。 發行新的映像版本，以不同的磁碟計數將會有中斷 hello 中的新映像版本的自動調整大小、 自動部署的解決方案，透過 ARM 範本和其他案例的情況下為基礎的新部署的 hello 可能性。
>
>

### <a name="11-add-an-offer"></a>1.1 加入供應項目
1. 登入 toohello[發佈入口網站][ link-pubportal]使用賣方帳戶。
2. 選取 hello**虛擬機器**hello 發佈入口網站 索引標籤。 在 hello 提示項目欄位中，輸入您提供的名稱。 hello 供應項目名稱通常是 hello 產品或服務計劃 toosell hello Azure Marketplace 中的 hello 名稱。
3. 選取 [ **建立**]。

### <a name="12-define-a-sku"></a>1.2 定義 SKU
加入提供項目之後，您會需要 toodefine，並識別您的 Sku。 您可以有多個供應項目，每個供應項目在其下可以有多個 SKU。 當 toostaging 推入的供應項目時，它是推入及所有其 Sku。

1. **加入 SKU。** hello SKU 需要 hello URL 中使用的識別項。 hello 識別碼中必須是唯一您的發行設定檔，但沒有與其他 「 發行者 」 的識別項衝突的風險。

   > [!NOTE]
   > 會顯示 hello Marketplace 中的 hello 優惠 URL 中的 hello 優惠和 SKU 識別碼。
   >
   >
2. **為 SKU 加入摘要描述。** 摘要描述都是可見的 toocustomers，因此您應該讓它們可輕鬆地讀取。 這項資訊不需要 toobe 鎖定直到 hello 「 推入 tooStaging 」 階段。 之前，您是免費 tooedit 它。
3. 如果您使用 Windows 架構的 Sku，請遵循 hello 建議的連結 tooacquire hello 核准的 Windows Server 版本。

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2.建立與 Azure 相容的 VHD (以 Linux 為基礎)
本節著重於建立以 Linux 為基礎的 VM 映像的 hello Azure Marketplace 的最佳作法。 逐步解說中，請參閱下列文件的 toohello:[建立及上傳的虛擬硬碟包含 hello Linux 作業系統](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3.建立與 Azure 相容的 VHD (以 Windows 為基礎)
本節著重於 hello 步驟 toocreate 根據 Windows Server hello Azure Marketplace 的 SKU。

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 請確定您使用 hello 更正基底 Vhd
hello 作業系統 VHD 為 VM 映像必須使用 Azure 核准基底映像包含 Windows Server 或 SQL Server 為基礎。

toobegin，從下列映像，位於 hello hello 建立 VM [Microsoft Azure 入口網站][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2]、[2012 Datacenter][link-datactr-2012]、[2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent]、[Standard][link-sql-2014-std]、[Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent]、[Standard][link-sql-2012-std]、[Web][link-sql-2012-web])

也可以在 hello SKU 頁面下方的 hello 發佈入口網站中找到這些連結。

> [!TIP]
> 如果您使用 hello 目前的 Azure 入口網站或 PowerShell，會核准已於 2014 年 9 月 8 日發行及更新版本的 Windows Server 映像。
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 建立您的 Windows 型 VM
從 hello Microsoft Azure 入口網站，您可以建立您只需要幾個簡單步驟中的核准基底映像為基礎的 VM。 hello 下面是 hello 程序的概觀：

1. 從 hello 基底映像 頁面上，選取**建立虛擬機器**toobe 導向 toohello 新[Microsoft Azure 入口網站][link-azure-portal]。

    ![繪圖][img-acom-1]
2. 登入 toohello 入口網站以 hello Microsoft 帳戶和 hello 想 toouse 的 Azure 訂用帳戶的密碼。
3. 使用您已選取 hello 基底映像，請遵循 hello 提示 toocreate VM。 您的主機名稱 （hello 電腦名稱）、 （系統管理員身分註冊），使用者名稱和密碼需要 tooprovide hello VM。

    ![繪圖][img-portal-vm-create]
4. 選取 hello VM toodeploy hello 大小：

    a.    如果您計劃 toodevelop hello VHD 在內部，hello 大小並不重要。 請考慮使用 hello 其中較小的 Vm。

    b.    如果您計劃 Azure 中的 toodevelop hello 映像，請考慮使用其中一種 hello 建議 hello 選映像的 VM 大小。

    c.    如需定價資訊，請參閱 toohello**建議定價層**hello 入口網站上顯示的選取器。 它會提供 hello hello 發行者所提供的三種建議的大小。 （在此情況下，hello 發行者是 Microsoft）。

    ![繪圖][img-portal-vm-size]
5. 設定屬性：

    a.    針對快速部署，您可以保留 hello hello 屬性底下的預設值**選擇性組態**和**資源群組**。

    b.    在下**儲存體帳戶**，您可以選擇性地選取 VHD 儲存在作業系統的 hello hello 儲存體帳戶。

    c.    在下**資源群組**，您可以選擇性地選取 hello 中哪些 tooplace hello VM 的邏輯群組。
6. 選取 hello**位置**部署：

    a.    如果您計劃 toodevelop hello VHD 在內部部署，因為您稍後將上傳 hello 映像 tooAzure，並不重要 hello 位置。

    b.    如果您計劃 Azure 中的 toodevelop hello 映像，請考慮使用其中一種從 hello 開頭的 hello 美國為基礎的 Microsoft Azure 區域。 這可加速 hello VHD 複製程序，Microsoft 會代替您執行，當您送出您的映像的憑證。

    ![繪圖][img-portal-vm-location]
7. 按一下 [建立] 。 hello VM 啟動 toodeploy。 分鐘內，您可以成功部署，而且您 sku 就可以開始 toocreate hello 映像。

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 開發您的 VHD hello 雲端中
我們強烈建議您在使用遠端桌面通訊協定 (RDP) 來開發您 hello 雲端中的 VHD。 您可以連接 tooRDP 與佈建期間指定 hello 使用者名稱和密碼。

> [!IMPORTANT]
> 如果您開發 VHD 內部部署 (不建議)，請參閱 [建立虛擬機器映像內部部署](marketplace-publishing-vm-image-creation-on-premise.md)。 下載您的 VHD 不需要，如果您正在開發 hello 雲端中。
>
>

**透過使用 hello 的 RDP 連線[Microsoft Azure 入口網站][link-azure-portal]**

1. 選取 [瀏覽] > [VM]。
2. hello 虛擬機器刀鋒視窗隨即開啟。 請確定該 hello 想與 tooconnect 的 VM 正在執行，然後再從已部署的 Vm hello 清單中選取。
3. 描述 hello 刀鋒視窗中開啟選取的 VM。 在 hello 頂端，按一下**連接**。
4. 您會提示的 tooenter hello 使用者名稱和您在佈建期間指定的密碼。

**使用 PowerShell，透過 RDP 連接**

toodownload 遠端桌面檔案 tooa 本機電腦，使用 hello [Get-azureremotedesktopfile cmdlet][link-technet-2]。 在順序 toouse 這個指令程式，您需要 tooknow hello hello 服務名稱和 hello VM 的名稱。 如果您從 hello 建立 hello VM [Microsoft Azure 入口網站][link-azure-portal]，您可以找到此資訊在 VM 屬性：

1. 在 hello Microsoft Azure 入口網站中，選取 **瀏覽** > **Vm**。
2. hello 虛擬機器刀鋒視窗隨即開啟。 選取 hello 您部署的 VM。
3. 描述 hello 刀鋒視窗中開啟選取的 VM。
4. 按一下 [內容] 。
5. hello hello 網域名稱的第一個部分是 hello 服務名稱。 hello 主機名稱是 hello VM 名稱。

    ![繪圖][img-portal-vm-rdp]
6. 如下所示為 hello cmdlet toodownload hello RDP 檔案建立 hello VM toohello 系統管理員的本機桌面。

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

RDP 的詳細資訊可以在 hello 文章中找到 MSDN 上[透過 RDP 或 SSH 連接 tooan Azure VM](http://msdn.microsoft.com/library/azure/dn535788.aspx)。

**設定 VM 並建立您的 SKU**

下載 VHD hello 作業系統之後, 使用 HyperV 並設定建立您的 SKU VM toobegin。 詳細的步驟，請參閱下列 TechNet 連結 hello:[安裝 HyperV 和設定 VM](http://technet.microsoft.com/library/hh846766.aspx)。

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 選擇 hello 正確的 VHD 大小
hello Windows 作業系統 VHD VM 映像中應該建立為 128 GB 的固定格式 VHD。  

如果 hello 實體大小小於 128 GB，hello VHD 應該為疏鬆。 hello 基底 Windows 和 SQL Server 提供的映像已經符合這些需求，因此不會變更的 hello VHD 取得 hello 格式或 hello 大小。  

資料磁碟的大小可高達 1 TB。 決定時 hello 磁碟大小，請記住，客戶無法調整大小 Vhd 映像內部署的 hello 次。 資料磁碟 VHD 應建立為固定格式 VHD。 也可以是疏鬆 VHD。 資料磁碟可以空白或包含資料。

### <a name="35-install-hello-latest-windows-patches"></a>3.5 安裝 hello 最新 Windows 修補程式
hello 基底映像包含最新修補程式 hello 向上 tootheir 發行日期。 之前發行 hello 作業系統已建立的 VHD，請確定已經執行的 Windows Update 以及所有 hello 最新重大，和已安裝重要的安全性更新。

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 必要時執行其他設定並排程工作
如果需要進行其他設定，請考慮使用排定的工作後，在執行啟動 toomake 在任何最後的變更 toohello VM 已部署：

* 它是最佳的作法 toohave hello 工作本身成功執行後刪除。
* 沒有設定應依賴 C 或 D 磁碟機以外的磁碟機，因為它們永遠會保證 tooexist hello 只有兩個磁碟機。 磁碟機 C 是 hello 作業系統磁碟，以及磁碟機 D 是 hello 暫存本機磁碟。

### <a name="37-generalize-hello-image"></a>3.7 hello 映像一般化
Hello Azure Marketplace 中的所有映像必須是可重複使用，以一般方式。 換句話說，必須先一般化 hello 作業系統 VHD:

* 適用於 Windows、 hello 映像應該是 「 已執行 sysprep，"，而且沒有組態應該不支援 hello **sysprep**命令。
* 您可以執行下列命令從 hello 目錄 windir%\System32\Sysprep hello。

        sysprep.exe /generalize /oobe /shutdown

  Toosysprep hello 作業系統如何在下列 MSDN 文章 hello 的步驟中提供的指引：[建立並上傳 Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="4-deploy-a-vm-from-your-vhds"></a>4.從您的 VHD 部署 VM
您已上傳您的 Vhd （hello 一般化作業系統 VHD 和零個或多個資料磁碟 Vhd） 之後 tooan Azure 儲存體帳戶，您可以註冊他們的使用者 VM 映像。 您可以接著測試該映像。 注意，因為您的作業系統 VHD 經過一般化後，您無法直接部署 hello VM 提供 hello VHD URL。

toolearn 更多關於 VM 映像，檢閱 hello 下列部落格文章：

* [VM 映像](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [VM 映像 PowerShell 如何](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [關於 Azure 中的 VM 映像](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Hello 必要工具、 PowerShell 和 Azure CLI 設定
* [如何 toosetup PowerShell](/powershell/azure/overview)
* [如何 toosetup Azure CLI](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 建立使用者 VM 映像
#### <a name="capture-vm"></a>擷取 VM
請閱讀下面提供的指引擷取 hello VM 使用 API/PowerShell Azure CLI 的 hello 連結。

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>一般化映像
請閱讀下面提供的指引擷取 hello VM 使用 API/PowerShell Azure CLI 的 hello 連結。

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 從使用者 VM 映像部署 VM
toodeploy 將 VM 從使用者 VM 映像，您可以使用目前的 hello [Azure 入口網站](https://manage.windowsazure.com)或 PowerShell。

**從 hello 目前的 Azure 入口網站部署 VM**

1. 跳過**新增** > **計算** > **虛擬機器** > **從組件庫**。

    ![繪圖][img-manage-vm-new]
2. 跳過**我的映像**，，然後選取會 hello VM 映像從哪些 toodeploy VM:

   1. 請特別注意 toowhich 映像選取，因為 hello**我的映像**檢視會列出作業系統映像和 VM 映像。
   2. 查看 hello 磁碟數目，有助於判斷您部署的映像類型，因為 hello 多數的 VM 映像具有多個磁碟。 但是，所以仍有可能 toohave 只有一個單一的作業系統磁碟，就必須使用的 VM 映像**的磁碟數目**設定 too1。

      ![繪圖][img-manage-vm-select]
3. 遵循 hello VM 建立精靈，並指定 hello VM 名稱、 VM 大小、 位置、 使用者名稱和密碼。

**從 PowerShell 部署 VM**

toodeploy hello 從大型 VM 一般化剛才建立的 VM 映像，您可以使用下列 cmdlet 的 hello。

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> 如需其他協助，請參閱 [針對 VHD 建立常見問題進行疑難排解]。
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5.取得 VM 映像的認證
hello VM 映像的準備 hello Azure Marketplace 中的下一個步驟是的 toohave 其認證。

此程序包括執行特殊的憑證 」 工具上, 傳 hello 驗證結果 toohello Azure Vhd 所在的容器、 加入提供項目、 定義您 SKU 和送出您的 VM 映像的憑證。

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 下載並執行的 Azure 認證的 hello 憑證測試工具
hello 憑證工具在執行中的 VM，佈建使用者的 VM 映像上執行，hello VM 映像的 tooensure 與 Microsoft Azure 相容。 它會確認 hello 指引和需求的相關準備您的 VHD 符合。 hello 工具 hello 輸出是相容性報告，應在 hello 發佈入口網站時提出要求的憑證上傳。

hello 憑證 」 工具可以搭配 Windows 和 Linux Vm。 它會連接透過 PowerShell tooWindows 為基礎的 Vm，並連接透過 SSH.Net tooLinux Vm:

1. 首先，下載 hello 憑證 」 工具在 hello [Microsoft 下載網站][link-msft-download]。
2. 開啟 hello 憑證 」 工具，然後再按一下 [hello**啟動新的測試**] 按鈕。
3. 從 hello**測試資訊**畫面上，輸入 hello 測試回合的名稱。
4. 選擇您的 VM 位於 Linux 或 Windows。 根據選擇的方法，請選取 hello 後續的選項。

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**連接 hello 憑證工具 tooa Linux VM 映像**
1. 選取 hello SSH 驗證模式： 密碼或金鑰檔案。
2. 如果使用密碼型驗證，請輸入 hello 網域名稱系統 (DNS) 名稱、 使用者名稱和密碼。
3. 如果使用金鑰檔的驗證，請輸入 hello DNS 名稱、 使用者名稱和私用金鑰的位置。

   ![Linux VM 映像的密碼驗證][img-cert-vm-pswd-lnx]

   ![Linux VM 映像的金鑰檔案驗證][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**連接 hello 憑證工具 tooa windows VM 映像**
1. 輸入完整的 hello VM DNS 名稱 (例如，MyVMName.Cloudapp.net)。
2. 輸入 hello 使用者名稱和密碼。

   ![Windows VM 映像的密碼驗證][img-cert-vm-pswd-win]

您已選取正確的 hello 選項為 Linux 或 windows VM 映像之後，請選取**測試連接**tooensure SSH.Net 或 PowerShell 具有有效的連接，基於測試目的。 建立連接之後，請選取**下一步**toostart hello 測試。

Hello 測試完成時，您會收到 hello 結果 （成功/失敗/警告） 的每個測試項目。

![Linux VM 映像的測試案例][img-cert-vm-test-lnx]

![Windows VM 映像的測試案例][img-cert-vm-test-win]

如果任何 hello 測試失敗，未經過認證您的映像。 如果發生這種情況，請檢閱 hello 需求，並進行任何必要的變更。

Hello 自動化測試之後，系統會詢問 tooprovide 其他輸入您的 VM 映像，透過問卷螢幕上。  完成 hello 問題，然後選取 **下一步**。

![認證工具問卷][img-cert-vm-questionnaire]

![認證工具問卷][img-cert-vm-questionnaire-2]

Hello 問卷完成之後，您可以提供其他資訊，例如 hello Linux VM 映像的 SSH 存取資訊以及說明任何失敗的評估。 您可以下載 hello 測試結果中和記錄檔 hello 執行測試案例加入 tooyour 答案 toohello 問卷。 將 hello 結果儲存在 hello 相同的容器，為您的 Vhd。

![儲存認證測試結果][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 會取得您的 VM 映像中的 hello 共用的存取簽章 URI
在發行程序 hello，您可以指定 hello 統一資源識別元 (Uri) 會導致 tooeach 的 hello 您已建立您的 sku 的 Vhd。 Microsoft hello 憑證程序期間需要存取 toothese Vhd。 因此，您必須針對每個 VHD toocreate 共用的存取簽章 URI。 這是應該進入的 URI hello**映像**hello 發佈入口網站中的索引標籤。

hello 共用的存取簽章建立 URI 應該遵守 toohello 下列需求：

* 為 VHD 產生共用存取簽章 URI 時，必須有足夠的列出和讀取權限。 不提供寫入或刪除存取權。
* 建立 hello 共用的存取簽章 URI 時 hello 持續時間的存取應該至少三 （3） 中的週。
* UTC 時間，hello 目前日期之前的選取 hello 天 toosafeguard。 例如，如果 hello 目前日期為 2014 年 10 月 6 日，選取時間 2014 年 10 月 5 日。

可以是 SAS URL 中產生多個方式 tooshare VHD Azure marketplace。
下列是 hello 3 建議使用的工具：

1.  Azure 儲存體總管
2.  Microsoft 儲存體總管
3.  Azure CLI

**Azure 儲存體總管 (建議 Windows 使用者採用)**

下面是使用 Azure 儲存體總管來產生 SAS URL 的 hello 步驟

1. 從 CodePlex 下載 [Azure 儲存體總管 6 預覽 3](https://azurestorageexplorer.codeplex.com/)。 跳過[Azure 儲存體總管 6 預覽](https://azurestorageexplorer.codeplex.com/)按一下**「 下載 」**。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. 下載 [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668)，解壓縮之後安裝。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. 安裝之後，開啟 hello 應用程式。
4. 按一下 [加入帳戶] 。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. 指定 hello 儲存體帳戶名稱、 儲存體帳戶金鑰，以及儲存體端點網域。 這是您 Azure 訂用帳戶中的 hello 儲存體帳戶，您已保留您的 VHD 在 Azure 入口網站上。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. 一旦連線 Azure 儲存體總管 tooyour 特定儲存體帳戶，就會開始的顯示所有 hello 包含 hello 儲存體帳戶內。 選取您複製 hello 作業系統磁碟的 VHD 檔案 （也資料磁碟如果它們適用於您的案例） 的 hello 容器。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. 選取後 hello blob 容器，Azure 儲存體總管啟動 hello 容器內的顯示 hello 檔案。 選取需要 toobe 送出的 hello 映像檔案 (.vhd)。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  選取之後 hello.vhd 檔案 hello 容器中，按一下 hello**安全性** 索引標籤。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  在 hello **Blob 容器安全性**對話方塊中，保留 hello 的預設值在 hello**存取層級**索引標籤，然後再按一下**共用存取簽章** 索引標籤。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. 請遵循下列 toogenerate hello.vhd 映像的共用的存取簽章 URI 的 hello 步驟：

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **從允許的存取：** toosafeguard UTC 時間，hello 目前日期前的選取 hello 一天。 例如，如果 hello 目前日期為 2014 年 10 月 6 日，選取時間 2014 年 10 月 5 日。

    b. **若要允許存取：**選取 hello 之後至少 3 週的日期**從允許存取**日期。

    c. **允許的動作：**選取 hello**清單**和**讀取**權限。

    d. 如果您已正確，選取.vhd 檔案，則您的檔案會出現在**Blob 名稱 tooaccess**與擴充功能的.vhd。

    e. 按一下 [產生簽章]。

    f. 在**產生共用存取簽章 URI 這個容器的**，hello 遵循以反白顯示上方的核取：

       - 請確定您的映像檔案名稱和**".vhd"** hello URI 中。
       - 結尾 hello hello 簽章，請確定**"= rl"**隨即出現。 這表明已成功提供 [讀取] 和 [列出] 存取權。
       - Hello 簽章的中間，請確定**"sr-iov = c 」**隨即出現。 這示範您具有容器層級存取

11. hello 的 tooensure 產生共用存取簽章 URI 如何運作，請按一下**瀏覽器中的測試**。 它應該開始 hello 下載程序。

12. 將複製 hello 共用的存取簽章 URI。 這是將 URI toopaste hello 到 hello 發佈入口網站。

13. 針對每個 VHD hello SKU 中重複步驟 6-10。

**Microsoft Azure 儲存體總管 (Windows/MAC/Linux)**

下面是使用 Microsoft Azure 儲存體總管來產生 SAS URL 的 hello 步驟

1.  從 [http://storageexplorer.com/](http://storageexplorer.com/) 網站下載 Microsoft Azure 儲存體總管。 跳過[Microsoft Azure 儲存體總管](http://storageexplorer.com/releasenotes.html)按一下**"下載 for Windows"**。

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  安裝之後，開啟 hello 應用程式。

3.  按一下 [加入帳戶] 。

4.  登入 tooyour 帳戶來設定 Microsoft Azure 儲存體總管 tooyour 訂用帳戶

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  移 toostorage 帳戶，然後選取 hello 容器

6.  選取 [取得共用存取簽章...] 使用滑鼠右鍵按一下的 hello**容器**

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  根據下列指示，更新 [開始時間]、[到期時間] 和 [權限]

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **開始時間：** toosafeguard UTC 時間，hello 目前日期前的選取 hello 一天。 例如，如果 hello 目前日期為 2014 年 10 月 6 日，選取時間 2014 年 10 月 5 日。

    b.  **到期時間：**選取 hello 之後至少 3 週的日期**開始時間**日期。

    c.  **權限：**選取 hello**清單**和**讀取**權限

8.  複製容器共用存取簽章 URI

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    產生的 SAS URL 是用於容器層級，現在我們需要在它 tooadd VHD 名稱。

    容器層級 SAS URL 的格式︰`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    SAS URL 中，如下所示的 hello 容器名稱後面插入 VHD 的名稱`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    範例：

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd 為 hello VHD 名稱，然後將 VHD SAS URL`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - 請確定您的映像檔案名稱和**".vhd"** hello URI 中。
    - Hello 簽章的中間，請確定**"sp = rl"**隨即出現。 這表明已成功提供 [讀取] 和 [列出] 存取權。
    - Hello 簽章的中間，請確定**"sr-iov = c 」**隨即出現。 這示範您具有容器層級存取

9.  tooensure 的 hello 產生共用的存取簽章 URI 是有效的在瀏覽器測試它。 它應該啟動 hello 下載程序

10. 將複製 hello 共用的存取簽章 URI。 這是將 URI toopaste hello 到 hello 發佈入口網站。

11. 針對每個 VHD hello SKU 中重複這些步驟。

**Azure CLI (建議用於非 Windows 和持續整合)**

下面是使用 Azure CLI 來產生 SAS URL 的 hello 步驟

1.  從[這裡](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/)下載 Microsoft Azure CLI。 您也可以找到適用於 **[Windows](http://aka.ms/webpi-azure-cli)** 和 **[MAC OS](http://aka.ms/mac-azure-cli)** 的不同連結。

2.  下載之後，請安裝

3.  使用下列程式碼建立 PowerShell 檔案，並將它儲存在本機

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    更新下列 hello 中上方的參數

    a. **`<StorageAccountName>`**：提供您的儲存體帳戶名稱

    b.這是另一個 C# 主控台應用程式。 **`<Storage Account Key>`**：提供您的儲存體帳戶金鑰

    c. **`<Permission Start Date>`**: toosafeguard UTC 時間，hello 目前日期前的選取 hello 一天。 比方說，如果 hello 目前日期為 2016 年 10 月 26 日，則值應該是 2016 年 10 月 25

    d. **`<Permission End Date>`**： 選取的日期，之後 hello 至少 3 週**開始日期**。 所以值應該為 **11/02/2016**。

    以下是 hello 範例程式碼之後更新適當的參數

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  使用「以系統管理員身分執行」模式下開啟 Powershell 編輯器，並在步驟 #3 中開啟檔案。

5.  執行的 hello 指令碼，它會提供您 hello 容器層級存取 SAS URL

    下列將會是 hello SAS 簽章和複製 hello 反白顯示組件，[記事本] 中的 hello 輸出

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  現在，您會看到容器層級 SAS URL，您需要在它 tooadd VHD 名稱。

    容器等級 SAS URL #

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  SAS URL 中的 hello 容器名稱後面插入 VHD 的名稱，如下所示`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    範例：

    TestRGVM201631920152.vhd 為 hello VHD 名稱，然後將 VHD SAS URL

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - 請確定您的映像檔案名稱和".vhd"位於 hello URI。
    -   Hello 簽章的中間，請確定 「 sp = rl 」 隨即出現。 這表明已成功提供 [讀取] 和 [列出] 存取權。
    -   Hello 簽章的中間，請確定 「 sr-iov = c"會出現。 這示範您具有容器層級存取

8.  tooensure 的 hello 產生共用的存取簽章 URI 是有效的在瀏覽器測試它。 它應該啟動 hello 下載程序

9.  將複製 hello 共用的存取簽章 URI。 這是將 URI toopaste hello 到 hello 發佈入口網站。

10. 針對每個 VHD hello SKU 中重複這些步驟。


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 提供 hello VM 映像的相關資訊，並要求 hello 發佈入口網站中的憑證
您已建立您的優惠和 SKU 之後，您應該輸入 hello 與該 SKU 相關聯的映像詳細資料：

1. 移 toohello[發佈入口網站][link-pubportal]，然後使用賣方帳戶登入。
2. 選取 hello **VM 映像** 索引標籤。
3. 列在 hello hello 頁面頂端的 hello 識別碼實際上是 hello 供應項目識別碼和 hello SKU 識別碼。
4. 填寫 [hello] 下的 hello 屬性**Sku** > 一節。
5. 在下**作業系統系列**，按一下 hello 與 hello 作業系統 VHD 相關聯的作業系統類型。
6. 在 hello**作業系統**方塊中，描述 hello 作業系統。 請考慮使用作業系統系列、類型、版本和更新等格式。 其中一個範例為 "Windows Server Datacenter 2014 R2"。
7. 選取 toosix 建議虛擬機器大小。 這些是決定 toopurchase 並部署您的映像時，取得顯示的 toohello 客戶 hello Azure 入口網站中的 hello 定價層刀鋒視窗中的建議。 **這些只是建議。hello 客戶都可以 tooselect 映像中指定任何可容納 hello 磁碟的 VM 大小。**
8. 輸入 hello 的版本。 hello 版本 欄位會封裝的語意版本 tooidentify hello 產品和它的更新：
   * 版本應為 hello 表單 X.Y.Z，X、 Y 和 Z 都是整數。
   * 不同 SKU 中的映像可以有不同的主要和次要版本。
   * SKU 中的版本只應該增加 hello 修補程式的版本 (從 X.Y.Z Z) 的累加變更。
9. 在 hello **OS VHD URL**方塊中，輸入 hello 共用的存取簽章建立 hello 作業系統 VHD URI。
10. 如果有與此 SKU 相關聯的資料磁碟，請選取 hello 邏輯單元編號 (LUN) toowhich 您想要部署時裝載此資料磁碟 toobe。
11. 在 hello **LUN X VHD URL**方塊中，輸入 hello 共用的存取簽章建立 hello 第一個資料 VHD URI。

    ![繪圖](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>常見的 SAS URL 問題和修正

|問題|失敗訊息|修正|文件連結|
|---|---|---|---|
|複製映像失敗 - 在 SAS url 中找不到 "?"|失敗︰複製映像。 您不能 toodownload blob 使用提供的 SAS Uri。|建議您更新 hello SAS Url 使用工具|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|映像複製失敗 - SAS url 中未設定 “st” 和 “se” 參數|失敗︰複製映像。 您不能 toodownload blob 使用提供的 SAS Uri。|更新 hello SAS Url 與它的開始和結束日期|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|複製映像失敗 - SAS url 中沒有 “sp=rl”|失敗︰複製映像。 您不能 toodownload blob 使用所提供的 SAS Uri|更新 hello SAS Url 設定為 「 讀取 」 和 「 清單的權限|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|複製映像失敗 - SAS url 中的 vhd 名稱含有空格|失敗︰複製映像。 您不能 toodownload blob 使用提供的 SAS Uri。|更新不含空格的 hello SAS Url|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|複製映像失敗 – SAS Url 授權錯誤的|失敗︰複製映像。 您不能 toodownload blob 到期 tooauthorization 錯誤|重新產生 hello SAS Url|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>後續步驟
您完成 hello SKU 詳細資料之後，您可以移動轉寄 toohello [Azure Marketplace 行銷內容指南][link-pushstaging]。 您可以在該步驟 hello 發行程序中，提供 hello 太行銷內容、 價格和其他資訊的必要之前**步驟 3： 在預備環境中測試您的 VM 提供**、 部署之前測試各種案例，使用案例hello 公用可視性的優惠 toohello Azure Marketplace 並購買。  

## <a name="see-also"></a>另請參閱
* [快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
