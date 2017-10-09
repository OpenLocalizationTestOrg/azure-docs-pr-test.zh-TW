---
title: "aaaCreate 和上傳 FreeBSD VM 映像 |Microsoft 文件"
description: "了解 toocreate 並上傳虛擬硬碟 (VHD)，其中包含 hello FreeBSD 作業系統 toocreate Azure 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>建立及上傳 VHD FreeBSD tooAzure
本文章將示範如何 toocreate 和上傳虛擬硬碟 (VHD)，其中包含 hello FreeBSD 作業系統。 將它上傳之後，您可以為您自己的映像 toocreate Azure 中的虛擬機器 (VM) 使用它。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需上傳 VHD 使用 hello 資源管理員模型資訊，請參閱[這裡](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="prerequisites"></a>必要條件
本文假設您有下列項目 hello:

* **Azure 訂用帳戶**-- 如果您沒有，只需要幾分鐘的時間就可以建立帳戶。 如果您有 MSDN 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。 否則，了解如何太[建立免費的試用帳戶](https://azure.microsoft.com/pricing/free-trial/)。  
* **Azure PowerShell 工具**-hello Azure PowerShell 模組必須安裝並設定 toouse 您 Azure 訂用帳戶。 toodownload hello 模組，請參閱[Azure 下載](https://azure.microsoft.com/downloads/)。 教學課程，描述如何 tooinstall 及設定這裡會提供 hello 模組。 使用 hello [Azure 下載](https://azure.microsoft.com/downloads/)cmdlet tooupload hello VHD。
* **安裝中的.vhd 檔案的 FreeBSD 作業系統**-支援的 FreeBSD 作業系統必須安裝 tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案。 例如，您可以使用的虛擬化解決方案，例如 HYPER-V toocreate hello.vhd 檔案，並安裝 hello 作業系統。 如需有關如何 tooinstall 並使用 HYPER-V，請參閱指示[安裝 HYPER-V 並建立虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。

> [!NOTE]
> 在 Azure 中不支援 hello 較新的 VHDX 格式。 您可以使用 HYPER-V 管理員轉換 hello 磁碟 tooVHD 格式或 hello cmdlet[轉換-vhd](https://technet.microsoft.com/library/hh848454.aspx)。 此外，還有[MSDN 上的方式相關教學課程 toouse hyper-v FreeBSD](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx)。
>
>

這項工作包含五個步驟的 hello:

## <a name="step-1-prepare-hello-image-for-upload"></a>步驟 1： 準備上傳 hello 映像
Hello 虛擬機器上安裝 hello FreeBSD 作業系統，完成下列程序的 hello:

1. 啟用 DHCP。

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. 啟用 SSH。

    請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。 根據預設，它從 FreeBSD 光碟安裝之後就會啟用。 
3. 設定序列主控台。

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. 安裝 sudo。

    hello 根帳戶已停用在 Azure 中。 這表示您需要以提高權限的無特殊權限的使用者 toorun 命令 tooutilize sudo。

        # pkg install sudo
   
5. Azure 代理程式的必要條件。

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. 安裝 Azure 代理程式。

    hello hello Azure 代理程式的最新版本能找到上[github](https://github.com/Azure/WALinuxAgent/releases)。 hello 版本 2.0.10 + 正式支援 FreeBSD 10 10.1，與 hello 2.1.4 + （包括 2.2.x） 正式支援 FreeBSD 10.2 和更新版本的版本。

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    針對 2.0 版，以下使用 2.0.16 做為範例：

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    針對 2.1 版，以下使用 2.1.4 做為範例：

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > 安裝 Azure 代理程式之後，它是個不錯的主意 tooverify 它正在執行：
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. 取消佈建 hello 系統。

    取消佈建 hello 系統 tooclean，並讓它適用於重新佈建。 hello 下列命令也會刪除 hello 最後一個佈建的使用者帳戶和相關聯的 hello 資料：

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    現在您可以關閉您的 VM。

## <a name="step-2-create-a-storage-account-in-azure"></a>步驟 2：在 Azure 中建立儲存體帳戶
您需要 Azure tooupload.vhd 檔案的儲存體帳戶，所以您可能會使用的 toocreate 虛擬機器。 您可以使用 hello Azure 傳統入口網站 toocreate 儲存體帳戶。

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 在 hello 命令列中，選取 **新增**。
3. 選取 [資料服務] > [儲存體]  > [快速建立]。

    ![快速建立儲存體帳戶](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. 填滿 hello 的欄位，如下所示：

   * 在 hello **URL**欄位中，輸入子網域名稱 toouse hello 儲存體帳戶 URL。 hello 項目可以包含 3-24 數字和小寫字母。 這個名稱會變成 hello hello URL 使用的 tooaddress Azure Blob 儲存體、 Azure 佇列儲存體或 Azure 資料表儲存體資源 hello 訂用帳戶內的主機名稱。
   * 在 hello**位置/同質群組**下拉式選單中，選擇 hello**位置或同質群組**hello 儲存體帳戶。 同質群組可讓您將雲端服務和儲存體放在 hello 相同的資料中心。
   * 在 hello**複寫**欄位中，決定是否 toouse**異地備援**hello 儲存體帳戶的複寫。 依預設會開啟異地複寫。 此選項會將複寫資料 tooa 次要位置，在沒有成本 tooyou，使您的儲存體容錯移轉 toothat 位置，如果主要的失敗，就會發生在 hello 主要位置。 hello 次要位置會自動指派，而且無法變更。 如果您需要更充分掌控您的雲端儲存體 toolegal 需求或組織的原則到期的 hello 位置時，您可以關閉地理複寫。 不過，請注意，如果您稍後啟用異地複寫，您將會產生單次資料傳輸費用 tooreplicate 您現有的資料 toohello 次要位置。 不含異地複寫的儲存服務會有相對的折扣。 如需深入了解如何管理儲存體帳戶的異地複寫，請參閱：[Azure 儲存體複寫](../../../storage/common/storage-redundancy.md)。

     ![輸入儲存體帳戶詳細資料](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. 選取 [建立儲存體帳戶] 。 hello 帳戶現在會出現在**儲存體**。

    ![已成功建立儲存體帳戶](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. 接下來，為您上傳的 .vhd 檔案建立容器。 選取 hello 儲存體帳戶名稱，然後再選取**容器**。

    ![儲存體帳戶詳細資訊](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. 選取 [建立容器] 。

    ![儲存體帳戶詳細資訊](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. 在 hello**名稱**欄位中，輸入您的容器的名稱。 然後，在 hello**存取**下拉式功能表上，選取您想要的存取原則的型別。

    ![容器名稱](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > 根據預設，hello 容器是私人的而且只能存取 hello 帳戶擁有者。 tooallow 公用讀取權限 toohello blob，在 [hello] 容器中，但 toohello 容器屬性和中繼資料，使用 hello**公用 Blob**選項。 tooallow 完整公開讀取權限 hello 容器和 blob，請使用 hello**公用容器**選項。
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>步驟 3： 準備 hello 連接 tooAzure
您可以上傳.vhd 檔案之前，您會需要您的電腦與您 Azure 訂用帳戶之間 tooestablish 安全連線。 您可以使用 hello Azure Active Directory (Azure AD) 方法或 hello 憑證方法 toodo 它。

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>使用 Azure AD hello 方法 tooupload.vhd 檔案
1. 開啟 hello Azure PowerShell 主控台。
2. 輸入下列命令的 hello:  
    `Add-AzureAccount`

    這個命令會開啟登入視窗，您可在此以您的工作或學校帳戶登入。

    ![PowerShell Window](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure 驗證，並將儲存 hello 認證資訊。 然後它會關閉 hello 視窗。

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>使用 hello 憑證方法 tooupload.vhd 檔案
1. 開啟 hello Azure PowerShell 主控台。
2. 輸入：`Get-AzurePublishSettingsFile`。
3. 在瀏覽器視窗開啟，並提示您 toodownload hello.publishsettings 檔案。 此檔案包含您 Azure 訂用帳戶的資訊和憑證。

    ![瀏覽器下載頁面](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. 儲存 hello.publishsettings 檔案。
5. 類型： `Import-AzurePublishSettingsFile <PathToFile>`，其中`<PathToFile>`hello 完整路徑 toohello.publishsettings 檔案。

   如需詳細資訊，請參閱 [開始使用 Azure Cmdlet](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)。

   如需有關安裝和設定 PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="step-4-upload-hello-vhd-file"></a>步驟 4: Hello.vhd 檔案上傳
當您上傳 hello.vhd 檔案時，您可以將它放 Blob 儲存的地方。 以下是您上傳 hello 檔案時要使用的一些術語：

* **BlobStorageURL**是 hello hello 您在步驟 2 中建立的儲存體帳戶的 URL。
* **YourImagesFolder**是 hello Blob 儲存容器所在 toostore 您的映像。
* **VHDName** hello 標籤出現在 hello Azure 傳統入口網站 tooidentify hello 虛擬硬碟中。
* **PathToVHDFile**是 hello 完整路徑和 hello.vhd 檔案的名稱。

從 hello Azure PowerShell 視窗 hello 先前步驟中，輸入：

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>步驟 5： 建立 VM 與 hello 上傳的.vhd 檔案
Hello.vhd 檔案上傳之後，您可以將它當做自訂映像，都與您訂用帳戶相關聯的自訂映像建立虛擬機器的映像 toohello 清單。

1. 從 hello Azure PowerShell 視窗 hello 先前步驟中，輸入：

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > 使用 Linux hello OS 類型。 hello 新版 Azure PowerShell 接受只有"Linux"或"Windows"做為參數。
   >
   >
2. 當您選擇 hello，完成 hello 上述步驟後，會列出 hello 新映像**映像**hello Azure 傳統入口網站上的索引標籤。  

    ![Choose an image](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. 從 hello 組件庫中建立虛擬機器。 這個新映像現在會出現在 [我的映像] 下。
4. 選取 hello 新映像。 接下來，瀏覽 hello 提示 tooset 註冊主機名稱、 密碼、 SSH 金鑰和等等。

    ![自訂映像](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Hello 佈建完成之後，您會看到 FreeBSD VM 在 Azure 中執行。

    ![Azure 中的 FreeBSD 映像](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
