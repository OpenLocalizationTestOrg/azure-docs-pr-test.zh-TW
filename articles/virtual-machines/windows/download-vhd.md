---
title: "從 Azure Windows VHD aaaDownload |Microsoft 文件"
description: "下載 Windows VHD 使用 hello Azure 入口網站。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>從 Azure 下載 Windows VHD

在本文中，您將學習如何 toodownload [Windows 虛擬硬碟 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)檔案從 Azure 中，使用 hello Azure 入口網站。 

Azure 的使用中的虛擬機器 (Vm)[磁碟](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)位置 toostore 作業系統、 應用程式，以及資料。 所有 Azure VM 都至少有兩個磁碟：一個 Windows 作業系統磁碟和一個暫存磁碟。 從映像，一開始建立 hello 作業系統磁碟和 hello 作業系統磁碟和 hello 映像會儲存在 Azure 儲存體帳戶的 Vhd。 虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。

## <a name="stop-hello-vm"></a>停止 hello VM

如果它已附加，無法從 Azure 下載 VHD tooa 執行 VM。 您需要 toostop hello VM toodownload VHD。 如果您想 toouse VHD 當做[映像](tutorial-custom-images.md)toocreate 您使用其他的 Vm 與新的磁碟， [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello hello 檔案中包含的作業系統，然後再停止 hello VM。 toouse hello VHD 現有的 VM 或資料磁碟的新執行個體的磁碟，您只需要 toostop 和解除配置 hello VM。

toouse hello 做為映像 toocreate 其他 Vm 的 VHD，請完成下列步驟：

1.  如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2.  [連接 toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 
3.  在 hello VM，系統管理員身分開啟 hello 命令提示字元視窗。
4.  變更 hello 目錄太*%windir%\system32\sysprep*執行 sysprep.exe。
5.  在 hello 系統準備工具 對話方塊中，選取 **進入系統的全新體驗 (OOBE)**，並確定**一般化**已選取。
6.  在 關機選項 中選取 關機，然後按一下確定。 

toouse hello 做為現有的 VM 或資料磁碟的新執行個體磁碟的 VHD 會完成下列步驟：

1.  Hello 中樞 hello Azure 入口網站中，按一下功能表上**虛擬機器**。
2.  Hello 清單中選取 hello VM。
3.  Hello VM hello] 刀鋒視窗，按一下 [**停止**。

    ![停止 VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>產生 SAS URL

toodownload hello VHD 檔案，您需要 toogenerate[共用的存取簽章 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL。 當產生 hello URL 時，到期時間會指派 toohello URL。

1.  在 hello VM 的 hello 刀鋒視窗的 [hello] 功能表上按一下**磁碟**。
2.  選取 VM，hello hello 作業系統磁碟，然後按一下**匯出**。
3.  設定 hello URL hello 到期時間太*36000*。
4.  按一下 [產生 URL]。

    ![產生 URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> hello 到期時間會增加從 hello 預設 tooprovide 足夠 toodownload hello Windows 伺服器作業系統的大型 VHD 檔案的時間。 您可以預期包含 hello Windows Server 作業系統 tootake 取決於您的連線數個小時 toodownload 的 VHD 檔案。 如果您正在下載資料磁碟的 VHD，hello 預設時間已足夠。 
> 
> 

## <a name="download-vhd"></a>下載 VHD

1.  下所產生的 hello URL，按一下 下載 hello VHD 檔案。

    ![下載 VHD](./media/download-vhd/export-download.png)

2.  您可能需要 tooclick**儲存**hello 瀏覽器 toostart hello 下載中。 hello hello VHD 檔案的預設名稱是*abcd*。

    ![Hello 瀏覽器中，按一下 [儲存]](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>後續步驟

- 了解如何太[上傳 VHD 檔案 tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 
- [從儲存體帳戶中的非受控磁碟建立受控磁碟](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
- [使用 PowerShell 管理 Azure 磁碟](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

