---
title: "當您刪除 Azure 儲存體帳戶、 容器或 Vhd aaaTroubleshoot 錯誤 |Microsoft 文件"
description: "針對刪除 Azure 儲存體帳戶、容器或 VHD 時所發生的錯誤進行疑難排解"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 33261562a2dd2614b35bc1118924513f8c624d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>針對刪除 Azure 儲存體帳戶、容器或 VHD 時所發生的錯誤進行疑難排解

您可能會在 hello 中收到錯誤時的 Azure 儲存體帳戶、 容器或虛擬硬碟 (VHD)，請嘗試 toodelete [Azure 入口網站](https://portal.azure.com)。 本文章提供在 Azure Resource Manager 部署指南 toohelp 解析 hello 問題疑難排解。

如果這份文件並不能解決您的 Azure 問題，請瀏覽 hello Azure 論壇上[MSDN 和堆疊溢位](https://azure.microsoft.com/support/forums/)。 您可以在這些論壇張貼問題或too@AzureSupportTwitter 上。 此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。

## <a name="symptoms"></a>徵兆
### <a name="scenario-1"></a>案例 1
當您嘗試 toodelete 資源管理員部署的儲存體帳戶中的 VHD 時，您會收到下列錯誤訊息的 hello:

**無法 toodelete blob 'vhds/BlobName.vhd'。錯誤： 目前沒有租用 hello blob 上和 hello 要求中指定任何租用識別碼。**

因為虛擬機器 (VM) 具有 hello 嘗試 toodelete VHD 上的租用，可能會發生此問題。

### <a name="scenario-2"></a>案例 2
當您嘗試 toodelete 資源管理員部署的儲存體帳戶中的容器時，您會收到下列錯誤訊息的 hello:

**無法 toodelete 儲存體容器 'vhd'。錯誤： 目前沒有租用 hello 容器和 hello 要求中指定任何租用識別碼。**

因為 hello 容器具有 hello 租用處於已鎖定的 VHD，可能會發生此問題。

### <a name="scenario-3"></a>案例 3
當您嘗試 toodelete 資源管理員部署的儲存體帳戶時，您會收到下列錯誤訊息的 hello:

**無法 toodelete 儲存體帳戶 'StorageAccountName'。錯誤： 無法刪除 hello 儲存體帳戶，因為 tooits 成品正在使用中。**

因為 hello 儲存體帳戶包含在 hello 租用狀態的 VHD，可能會發生此問題。

## <a name="solution"></a>方案 
tooresolve 這些問題，您必須識別 hello hello 錯誤造成的 VHD 和 hello 相關聯的 VM。 然後，卸離 hello VHD 從 hello VM （適用於資料磁碟），或刪除 hello 使用 hello VHD （適用於作業系統磁碟） 的 VM。 這會移除 hello 租用 hello VHD，並允許 toobe 刪除。 

toodo，使用其中一個 hello 下列方法：

### <a name="method-1---use-azure-storage-explorer"></a>方法 1 - 使用 Azure 儲存體總管

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>步驟 1 識別 hello 導致無法刪除 hello 儲存體帳戶的 VHD

1. 當您刪除 hello 儲存體帳戶時，您會收到 hello 如下的訊息對話方塊： 

    ![當刪除 hello 儲存體帳戶時，訊息](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. 檢查 hello**磁碟 URL** tooidentify hello 儲存體帳戶和 hello VHD，讓您刪除 hello 儲存體帳戶。 在下列範例的 hello，hello 之前字串 」。 account>.blob.core.windows.net"hello 儲存體帳戶名稱，而 「 SCCM2012-2015年-08-28.vhd"hello VHD 名稱。  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>使用 Azure 儲存體總管的步驟 2 Delete hello VHD

1. 下載並安裝 hello 最新版本[Azure 儲存體總管](http://storageexplorer.com/)。 此工具是 microsoft Windows、 macOS 和 Linux 的 Azure 儲存體資料 tooeasily 工作可讓您的獨立應用程式。
2. 開啟 [Azure 儲存體總管]，選取 ![帳戶圖示](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) hello 左在列上，選取您的 Azure 環境，然後再登入。

3. 選取所有的訂閱或 hello 訂用帳戶包含您想 toodelete hello 儲存體帳戶。

    ![新增訂用帳戶](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. 移 toohello 儲存體帳戶，我們取自 hello 磁碟 URL 之前，請選取 hello **Blob 容器** > **vhd**並刪除 hello 儲存體帳戶上搜尋 hello 會讓您的 VHD。
5. 如果找到 hello VHD，請檢查 hello **VM 名稱**資料行 toofind hello 正在使用此 VHD 的 VM。

    ![檢查 VM](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. 使用 Azure 入口網站移除 hello VHD hello 租用。 如需詳細資訊，請參閱[移除 hello 租用 hello VHD 從](#remove-the-lease-from-the-vhd)。 

7. 移 toohello Azure 儲存體總管 hello VHD 上按一下滑鼠右鍵，然後選取 [刪除]。

8. 刪除 hello 儲存體帳戶。

### <a name="method-2---use-azure-portal"></a>方法 2 - 使用 Azure 入口網站 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>步驟 1： 識別 hello 導致無法刪除 hello 儲存體帳戶的 VHD

1. 當您刪除 hello 儲存體帳戶時，您會收到 hello 如下的訊息對話方塊： 

    ![當刪除 hello 儲存體帳戶時，訊息](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. 檢查 hello**磁碟 URL** tooidentify hello 儲存體帳戶和 hello VHD，讓您刪除 hello 儲存體帳戶。 在下列範例的 hello，hello 之前字串 」。 account>.blob.core.windows.net"hello 儲存體帳戶名稱，而 「 SCCM2012-2015年-08-28.vhd"hello VHD 名稱。  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
3. 在 hello 中樞功能表中，選取 **所有資源**。 移 toohello 儲存體帳戶，然後再選取**Blob** > **vhd**。

    ![Hello 入口網站中，反白顯示 hello"vhds"容器與 hello 儲存體帳戶的螢幕擷取畫面](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. 找出 hello 我們稍早取得從 hello 磁碟 URL 的 VHD。 然後，判斷哪些 VM 正在使用 hello VHD。 通常，您可以判斷其 VM 保留 hello VHD 藉由檢查 hello VHD 的名稱：

資源管理員開發模型中的 VM

   * 作業系統磁碟一般會遵循此命名慣例︰VMName-YYYY-MM-DD-HHMMSS.vhd
   * 資料磁碟一般會遵循此命名慣例︰VMName-YYYY-MM-DD-HHMMSS.vhd

傳統開發模型中的 VM

   * 作業系統磁碟一般會遵循此命名慣例︰CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * 資料磁碟一般會遵循此命名慣例︰CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>步驟 2: Hello 租用移除 hello VHD

[移除 hello VHD 中的 hello 租用](#remove-the-lease-from-the-vhd)，然後再刪除 hello 儲存體帳戶。

## <a name="what-is-a-lease"></a>租用是什麼？
使用期是可以使用的 toocontrol 存取 tooa blob (例如 VHD) 的鎖定。 當 blob 租用時，只有 hello 租用的 hello 擁有者可以存取 hello blob。 使用期是很重要的 hello 下列原因：

* 它可防止資料損毀，如果多個擁有者嘗試 toowrite toohello hello blob hello 相同部分相同的時間。
* 它會防止 hello blob 遭到刪除的項目正在使用它 (例如 VM)。
* 它可以防止 hello 儲存體帳戶刪除如果項目正在使用它 (例如 VM)。

### <a name="remove-hello-lease-from-hello-vhd"></a>Hello 租用移除 hello VHD
如果作業系統磁碟 hello VHD，您必須刪除 hello VM tooremove hello 租用：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello**中樞**功能表上，選取**虛擬機器**。
3. 選取 hello 保存租用 hello VHD 的 VM。
4. 請確定不會主動使用 hello 虛擬機器，並確認您不再需要 hello 虛擬機器。
5. 頂端的 hello hello **VM 詳細資料**刀鋒視窗中，選取**刪除**，然後按一下**是**tooconfirm。
6. 應刪除 hello VM，但可以保留 hello VHD。 不過，hello VHD 應該不會再有租用。 可能需要幾分鐘，讓 hello 租用 toobe 釋出。 hello 租用的 tooverify 已發行，請跳過**所有資源** > **儲存體帳戶名稱** > **Blob**  >  **vhd**。 在 hello **Blob 屬性**窗格中，hello**租用狀態**值應該是**已解除鎖定**。

如果 hello VHD 資料磁碟，卸離 hello VHD 從 hello VM tooremove hello 租用：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello**中樞**功能表上，選取**虛擬機器**。
3. 選取 hello 保存租用 hello VHD 的 VM。
4. 選取**磁碟**上 hello **VM 詳細資料**刀鋒視窗。
5. 選取對 hello VHD 保持租用的 hello 資料磁碟。 您可以判斷哪些 VHD 附加在 hello 磁碟，藉由檢查 hello hello VHD URL。
6. 判斷確實不主動使用 hello 資料磁碟。
7. 按一下**卸離**上 hello**磁碟詳細資料**刀鋒視窗。
8. hello 磁碟現在會中斷 hello VM，並 hello VHD 應該不再需要在其上的租用。 可能需要幾分鐘，讓 hello 租用 toobe 釋出。 已釋放 hello 租用的 tooverify、 跳過**所有資源** > **儲存體帳戶名稱** > **Blob**  >  **vhd**。 在 hello **Blob 屬性**窗格中，hello**租用狀態**值應該是**已解除鎖定**。

## <a name="next-steps"></a>後續步驟
* [刪除儲存體帳戶](storage-create-storage-account.md#delete-a-storage-account)
* [如何 toobreak hello 鎖定租用的 blob 儲存體在 Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
