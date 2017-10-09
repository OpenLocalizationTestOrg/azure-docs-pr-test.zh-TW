---
title: "資料磁碟 tooa Linux VM aaaAttach |Microsoft 文件"
description: "如何 tooattach 新的或現有的資料磁碟 tooa Linux VM 在 Azure 入口網站中，使用 hello hello Resource Manager 部署模型。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Tooattach 資料磁碟 tooa Linux VM hello Azure 入口網站中的方式
本文章將示範如何 tooattach 新的和現有磁碟 tooa Linux 虛擬機器透過 hello Azure 入口網站。 您也可以[附加 hello Azure 入口網站中的資料磁碟 tooa Windows VM](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 您可以選擇 toouse 任一 Azure 受管理磁碟或受管理的磁碟。 受管理的磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。 非受控磁碟需要儲存體帳戶且[套用一些配額和限制](../../azure-subscription-service-limits.md#storage-limits)。 如需 Azure 受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。

附加磁碟 tooyour VM 之前，請先檢閱下列提示：

* hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* toouse 高階儲存體，您需要將 DS 系列或 GS 系列虛擬機器。 您可以使用進階或標準磁碟搭配這些虛擬機器。 僅特定地區可用進階儲存體。 如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 磁碟附加的 toovirtual 機器是實際的.vhd 檔案儲存在 Azure 中。 如需詳細資訊，請參閱 [有關虛擬機器的磁碟和 VHD](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。


## <a name="find-hello-virtual-machine"></a>尋找 hello 虛擬機器
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **虛擬機器**。
3. 從 [hello] 清單中選取 hello 虛擬機器。
4. toohello 虛擬機器刀鋒視窗中，在**Essentials**，按一下 **磁碟**。
   
    ![開啟磁碟設定](./media/attach-disk-portal/find-disk-settings.png)

接著，依照指示來附加[受控磁碟](#use-azure-managed-disks)或[非受控磁碟](#use-unmanaged-disks)。

## <a name="use-azure-managed-disks"></a>使用 Azure 受控磁碟

### <a name="attach-a-new-disk"></a>附加新的磁碟

1. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
2. 按一下 hello 下拉式選單，如**名稱**選取**建立磁碟**:

    ![建立 Azure 受控磁碟](./media/attach-disk-portal/create-new-md.png)

3. 輸入受控磁碟的名稱。 檢閱 hello 預設設定，如有必要，更新，然後按一下**建立**。
   
   ![檢閱磁碟設定](./media/attach-disk-portal/create-new-md-settings.png)

4. 按一下**儲存**toocreate hello 管理磁碟和更新的 hello VM 組態：

   ![儲存新的 Azure 受控磁碟](./media/attach-disk-portal/confirm-create-new-md.png)

5. Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。 由於受管理的磁碟是最上層資源，hello 磁碟隨即顯示 hello 資源群組的 hello 根目錄：

   ![資源群組中的 Azure 受控磁碟](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>連接現有磁碟
1. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
2. 按一下 hello 下拉式選單，如**名稱**tooview 的現有清單管理磁碟存取 tooyour Azure 訂用帳戶。 選取受管理的 hello 磁碟 tooattach:

   ![附加現有的 Azure 受控磁碟](./media/attach-disk-portal/select-existing-md.png)

3. 按一下**儲存**tooattach hello 現有受管理磁碟和更新的 hello VM 組態：
   
   ![儲存 Azure 受控磁碟更新](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Azure 將 hello 磁碟 toohello 虛擬機器之後，它會列在下方的 hello 虛擬機器的磁碟設定**資料磁碟**。

## <a name="use-unmanaged-disks"></a>使用非受控磁碟

### <a name="attach-a-new-disk"></a>附加新的磁碟

1. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
2. 檢閱 hello 預設設定，如有必要，更新，然後按一下**確定**。
   
   ![檢閱磁碟設定](./media/attach-disk-portal/attach-new.png)
3. Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。

### <a name="attach-an-existing-disk"></a>連接現有磁碟
1. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
2. 在 [連結現有磁碟] 底下，按一下 [VHD 檔案]。
   
   ![連接現有磁碟](./media/attach-disk-portal/attach-existing.png)
3. 在下**儲存體帳戶**，選取 hello 帳戶和容器，其中含有 hello.vhd 檔案。
   
   ![尋找 VHD 位置](./media/attach-disk-portal/find-storage-container.png)
4. 選取 hello.vhd 檔案。
5. 在下**將現有磁碟**，您只選取的 hello 檔案列在**VHD 檔案**。 按一下 [確定] 。
6. Azure 將 hello 磁碟 toohello 虛擬機器之後，它會列在下方的 hello 虛擬機器的磁碟設定**資料磁碟**。


## <a name="next-steps"></a>後續步驟
加入 hello 磁碟之後，您需要 tooprepare 它供使用。 如需詳細資訊，請參閱這篇[做法：在 Linux 中初始化新的資料磁碟](add-disk.md)。
