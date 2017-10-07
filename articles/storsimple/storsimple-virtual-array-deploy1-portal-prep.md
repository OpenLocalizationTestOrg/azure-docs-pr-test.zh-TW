---
title: "StorSimple Virtual Array 的 aaaPortal 準備 |Microsoft 文件"
description: "第一個教學課程 toodeploy StorSimple 虛擬陣列包括準備 hello Azure 入口網站"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>部署 StorSimple 虛擬陣列-準備 hello Azure 入口網站

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>概觀

這是 hello 第一篇文章 hello 數列中的 部署教學課程所需 toocompletely 部署您的虛擬陣列做為檔案伺服器或 iSCSI 伺服器使用 hello 資源管理員的模型。 本文描述 hello 所需的準備 toocreate，並設定您 StorSimple 裝置管理員服務之前 tooprovisioning 虛擬陣列。 本文也會連結出 tooa 部署組態檢查清單及設定必要條件。

您需要系統管理員權限 toocomplete hello 安裝和設定程序。 我們建議您先檢閱 hello 部署組態檢查清單。 hello 入口網站的準備工作會小於 10 分鐘。

這篇文章中發行的 hello 資訊適用於 StorSimple hello Azure 入口網站中的虛擬陣列和 Microsoft Azure 政府雲端 toohello 部署。

### <a name="get-started"></a>開始使用
hello 部署工作流程包含準備 hello 入口網站中，佈建您的虛擬化環境中的虛擬陣列和 hello 安裝完成。 tooget 入門 hello StorSimple Virtual Array 部署為檔案伺服器或 iSCSI 伺服器，您需要下列資料表的資源 toorefer toohello。

#### <a name="deployment-articles"></a>部署相關文章

toodeploy StorSimple 虛擬陣列，請參閱下列文章中 hello 規定順序 toohello。

| **#** | **在此步驟中** | **執行此動作...** | **並使用這些文件。** |
| --- | --- | --- | --- |
| 1. |**設定 hello Azure 入口網站** |建立並設定您 StorSimple 裝置管理員服務之前 tooprovisioning StorSimple Virtual Array。 |[準備 hello 入口網站](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**佈建 hello 虛擬陣列** |HYPER-V，佈建，並連接 tooa StorSimple Virtual Array 在 Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 上執行 HYPER-V 的主機系統上。 <br></br> <br></br> 適用於 VMware，佈建，並連接 tooa StorSimple Virtual Array 和更新版本上執行 VMware ESXi 5.5 主機系統。<br></br> |[在 Hyper-V 中佈建虛擬陣列](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [在 VMware 中佈建虛擬陣列](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**設定 hello 虛擬陣列** |檔案伺服器，執行初始設定，註冊您的 StorSimple 檔案伺服器，並完成 hello 裝置設定。 接下來，您可以佈建 SMB 共用。 <br></br> <br></br> 為您的 iSCSI 伺服器執行初始設定，註冊您的 StorSimple iSCSI 伺服器，並完成 hello 裝置設定。 接下來，您可以佈建 iSCSI 磁碟區。 |[將虛擬陣列設定為檔案伺服器](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[將虛擬陣列設定為 iSCSI 伺服器](storsimple-virtual-array-deploy3-iscsi-setup.md) |

您現在可以開始 tooset 向上 hello Azure 入口網站。

## <a name="configuration-checklist"></a>設定檢查清單

hello 組態檢查清單描述在您的 StorSimple Virtual Array 設定 hello 軟體之前，需要 toocollect hello 資訊。 正在準備時間有助於此資訊的部署環境中的 hello StorSimple 裝置的簡化 hello 程序。 根據您的 StorSimple Virtual Array 是否為檔案伺服器或 iSCSI 伺服器部署，需要一個 hello 下列檢查清單。

* 下載 hello [StorSimple 虛擬陣列檔案伺服器設定檢查清單](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf)。
* 下載 hello [StorSimple Virtual Array iSCSI 伺服器組態檢查清單](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf)。

## <a name="prerequisites"></a>必要條件

您在這裡找到您的 StorSimple 裝置管理員服務、 StorSimple Virtual Array 和 hello 資料中心網路的 hello 組態必要條件。

### <a name="for-hello-storsimple-device-manager-service"></a>Hello StorSimple 裝置管理員服務

在您開始前，請確定：

* 您擁有的 Microsoft 帳戶具有存取認證。
* 您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。
* 您的 Microsoft Azure 訂用帳戶應該已啟用來使用 StorSimple 裝置管理員服務。

### <a name="for-hello-storsimple-virtual-array"></a>Hello StorSimple Virtual Array

在您部署虛擬陣列之前，請確定：

* 您可以存取 tooa 主機系統執行 HYPER-V 的 Windows Server 2008 R2 或更新版本，或是 VMware (ESXi 5.5 或更新版本) 可以使用的 tooa 佈建裝置。
* hello 主機系統是無法 toodedicate hello 下列資源 tooprovision 虛擬陣列：
  
  * 至少 4 顆核心。
  * 至少 8 GB 的 RAM。 如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援 2 百萬個檔案。 您需要 16 GB RAM toosupport 2-4 百萬個檔案。
  * 一個網路介面。
  * 供系統資料使用的 500 GB 虛擬磁碟。

### <a name="for-hello-datacenter-network"></a>Hello 資料中心網路

在您開始前，請確定：

* 資料中心中的 hello 網路設定根據您的 StorSimple 裝置 hello 網路需求。 如需詳細資訊，請參閱 hello [StorSimple 虛擬陣列系統需求](storsimple-ova-system-requirements.md)。
* StorSimple Virtual Array 隨時都有專用的 5 Mbps 網際網路頻寬 (或更多) 可用。 此頻寬不應與任何其他應用程式共用。

## <a name="step-by-step-preparation"></a>逐步的準備程序

使用您的入口網站 hello 遵循逐步指示 tooprepare hello StorSimple 裝置管理員服務。

## <a name="step-1-create-a-new-service"></a>步驟 1：建立新的服務

Hello StorSimple 裝置管理員服務的單一執行個體可以管理多個 StorSimple 虛擬陣列。 執行下列步驟 toocreate hello StorSimple 裝置管理員服務的執行個體的 hello。 如果您有現有的 StorSimple 裝置管理員服務 toomanage 您的虛擬陣列，略過此步驟中，然後太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> 如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。
> 
> * 如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#optional-step-configure-a-new-storage-account-for-the-service)如需詳細指示。
> * 如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>步驟 2： 取得 hello 服務註冊金鑰

Hello StorSimple 裝置管理員服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。 這個金鑰是使用的 tooregister，而且與 hello 服務連接您的 StorSimple 裝置。

執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)。

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> hello 服務註冊金鑰是使用的 tooregister 所有 hello 必須與您的 StorSimple 裝置管理員服務 tooregister StorSimple 裝置管理員裝置。
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>步驟 3： 下載 hello 虛擬陣列映像

您已擁有 hello 服務註冊金鑰之後，您必須 toodownload hello 適當的虛擬陣列映像 tooprovision 虛擬陣列主機系統上。 hello 虛擬陣列影像都是特定的作業系統，而且可以從 hello Azure 入口網站中的 hello 快速入門頁面下載。

> [!IMPORTANT]
> hello StorSimple Virtual Array 上所執行的 hello 軟體只能搭配 hello StorSimple 裝置管理員服務。
> 
> 

執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)。

#### <a name="tooget-hello-virtual-array-image"></a>tooget hello 虛擬陣列映像

1. 登入 hello [Azure 入口網站](https://portal.azure.com/)。 
2. 在 hello Azure 入口網站，按一下 **瀏覽 > StorSimple 裝置管理員**。
3. 選取現有的 StorSimple 裝置管理員服務。 在 hello **StorSimple 裝置管理員**刀鋒視窗中，按一下 **快速入門**。 
4. 按一下 hello 連結對應 toohello 映像您想要從 Microsoft 下載中心 hello toodownload。 hello 映像檔案是大約 4.8 GB。
   
   * VHDX (適用於 Windows Server 2012 及更新版本上的 Hyper-V)
   * VHD (適用於 Windows Server 2008 R2 及更新版本上的 Hyper-V)
   * VMDK (適用於 VMWare ESXi 5.5 及更新版本)
5. 下載並解壓縮 hello 檔案 tooa 本機磁碟機，記下 hello 解壓縮的檔案所在的位置。

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>選擇性步驟： 設定新的儲存體帳戶 hello 服務

此步驟為選擇性，而且您並未啟用 hello 自動建立儲存體帳戶與您的服務時，才應執行。

如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[如何 toocreate 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)如需逐步指示。

執行下列步驟在 hello hello [Azure 入口網站](https://ms.portal.azure.com/)hello StorSimple 裝置管理員服務頁面 tooadd 現有的 Microsoft Azure 儲存體帳戶上。

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務

1. 瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。 這會開啟 hello**概觀**刀鋒視窗。
2. 選取**儲存體帳戶認證**內 hello**組態**> 一節。
3. 按一下 [新增] 。
4. 在 hello**加入儲存體帳戶**刀鋒視窗中，請勿遵循 hello:
   
    1. 在 [訂用帳戶] 中，選取 [目前]。
   
    2. 提供 hello Azure 儲存體帳戶名稱。
   
    3. 選取**啟用**toocreate StorSimple 裝置與 hello 雲端之間的網路通訊的安全通道。 只有當您在私人雲端內操作時，才選取 [停用]。
   
    4. 按一下 [新增] 。 已成功建立 hello 儲存體帳戶之後，您會收到通知。<br></br>
   
     ![新增現有儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>後續步驟

hello 下一個步驟是 tooprovision 是您的 StorSimple Virtual Array 的虛擬機器。 根據您主機的作業系統，請參閱 hello 詳細中的指示：

* [在 Hyper-V 中佈建 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [在 VMware 中佈建 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-vmware.md)

