---
title: "備份 Azure Linux VM | Microsoft Docs"
description: "使用 Azure 備份來備份並保護 Linux VM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>備份 Azure 中的 Linux 虛擬機器

您可以定期建立備份以保護您的資料。 Azure 備份會建立復原點，並儲存在異地備援復原保存庫。 當您從復原點還原時，您可以還原 hello 整個 VM 或特定的檔案。 本文說明如何 toorestore 單一檔案 tooa Linux VM 執行 nginx。 如果您還沒有 VM toouse，您可以建立一個使用 hello [Linux 快速入門](quick-create-cli.md)。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 VM 的備份
> * 排定每日備份
> * 從備份還原檔案



## <a name="backup-overview"></a>備份概觀

當 hello Azure 備份服務啟動備份時，它就會觸發 hello 備用分機號碼 tootake 時間點快照集。 hello Azure 備份服務會使用 hello _VMSnapshotLinux_ Linux 中的擴充功能。 hello 延伸模組會安裝在第一個 VM 備份 hello hello VM 正在執行。 如果 hello 未執行 VM，hello Backup service 的快照 hello 基礎儲存體 （因為 VM 已停止的 hello 時，會不發生任何應用程式寫入）。

根據預設，Azure Backup 所需的檔案系統的一致備份 Linux VM，但它可以設定的 tootake[使用前指令碼和後置指令碼架構的應用程式一致備份](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)。 一旦 hello Azure 備份服務會擷取 hello 快照，hello 資料就是傳送的 toohello 保存庫。 toomaximize 效率 hello 服務識別，以及傳輸只 hello 的 hello 上一次備份之後變更資料的區塊。

Hello 資料傳輸完成時，會移除 hello 快照集，並建立復原點。


## <a name="create-a-backup"></a>建立備份
建立簡單排定每日備份 tooa 復原服務保存庫。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在左側 hello hello 功能表中選取**虛擬機器**。 
3. 從 hello 清單中，選取 VM tooback。
4. 在 hello VM 刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。 hello**啟用備份**刀鋒視窗隨即開啟。
5. 在**復原服務保存庫**，按一下 **建立新**並提供 hello hello 新的保存庫名稱。 新的保存庫中建立 hello 相同資源群組及做為 hello 虛擬機器的位置。
6. 按一下 [備份原則]。 此範例中，保留 hello 預設然後按一下**確定**。
7. 在 hello**啟用備份**刀鋒視窗中，按一下 **啟用備份**。 這會建立根據 hello 預設排程每日備份。
10. toocreate 初始的復原點，在 hello**備份**刀鋒視窗中按一下**備份現在**。
11. 在 hello**立即備份**刀鋒視窗中，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。
12. 在 hello**備份**刀鋒視窗中的 VM，您會看到 hello 都已完成的復原點數目。

    ![復原點](./media/tutorial-backup-vms/backup-complete.png)

hello 第一次備份大約需要 20 分鐘。 在您的備份完成之後，請繼續 toohello 本教學課程的下一個部分。

## <a name="restore-a-file"></a>還原檔案

如果您不小心刪除或變更 tooa 檔案，您可以使用檔案復原 toorecover hello 檔案從您的備份保存庫。 檔案復原使用 hello VM 執行的指令碼為本機磁碟機 toomount hello 復原點。 這些磁碟機仍會掛接為 12 小時，讓您可以從 hello 復原點複製檔案並將它們還原 toohello VM。  

在此範例中，我們會示範如何 toorecover hello 預設 nginx 網頁 /var/www/html/index.nginx-debian.html。 在此範例中我們 VM 的 hello 公用 IP 位址是*13.69.75.209*。 您可以找到 hello vm 使用的 IP 位址：

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. 在您的本機電腦上開啟瀏覽器並輸入中的 VM toosee hello 預設 nginx 網頁 hello 公用 IP 位址。

    ![預設的 nginx 網頁](./media/tutorial-backup-vms/nginx-working.png)

1. 透過 SSH 連線到您的 VM。

    ```bash
    ssh 13.69.75.209
    ```
2. 刪除 /var/www/html/index.nginx-debian.html。

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. 在您的本機電腦上重新整理 hello 瀏覽器所按下 CTRL + F5 toosee 預設 nginx 網頁就會消失。

    ![預設的 nginx 網頁](./media/tutorial-backup-vms/nginx-broken.png)
    
1. 在您的本機電腦上登入 toohello [Azure 入口網站](https://portal.azure.com/)。
6. 在左側 hello hello 功能表中選取**虛擬機器**。 
7. 從 hello 清單中，選取 hello VM。
8. 在 hello VM 刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。 hello**備份**刀鋒視窗隨即開啟。 
9. 在 hello 在 hello hello 刀鋒視窗頂端的功能表中選取**檔案復原**。 hello**檔案復原**刀鋒視窗隨即開啟。
10. 在**步驟 1： 選取的復原點**，從 hello 下拉式清單中選取的復原點。
11. 在**步驟 2： 下載指令碼 toobrowse 並復原檔案**，按一下 hello**下載可執行檔** 按鈕。 儲存 hello 下載的檔案 tooyour 本機電腦。
7. 按一下**下載指令碼**toodownload hello 指令碼檔案儲存在本機。
8. 開啟 Bash 提示字元並輸入 hello 遵循、 取代*Linux_myVM_05-05-2017.sh* hello 包含正確的路徑和檔名，您所下載的 hello 指令碼*azureuser*與 hello hello VM 的使用者名稱和*13.69.75.209* vm hello 公用 IP 位址。
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. 在您的本機電腦上開啟 SSH 連線 toohello VM。

    ```bash
    ssh 13.69.75.209
    ```
    
10. 您在 VM 上，將執行權限 toohello 指令檔。

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. 在您的 VM 執行 hello 指令碼 toomount hello 復原點為檔案系統。

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. hello hello 指令碼可提供從輸出 hello hello 掛接點路徑。 hello 輸出看起來類似 toothis:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. 您在 VM 上，複製 hello nginx 預設 web 網頁 hello 掛接點後 toowhere 從已刪除 hello 檔案。

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. 在您的本機電腦上開啟 hello 瀏覽器索引標籤，您連接 toohello hello VM 顯示 hello nginx 預設頁面的 IP 位址。 按 CTRL + F5 toorefresh hello 瀏覽器頁面。 您現在應該會看到該 hello 預設頁面又重新運作。

    ![預設的 nginx 網頁](./media/tutorial-backup-vms/nginx-working.png)

18. 在本機電腦，請返回 toohello 瀏覽器索引標籤的 hello Azure 入口網站，並在**步驟 3： 在復原之後卸載 hello 磁碟**按一下 hello**取消掛接磁碟**按鈕。 如果您忘記 toodo 此步驟中，hello 連接 toohello 掛接點在 12 小時後已自動關閉。 這些 12 小時之後，您需要 toodownload 新的指令碼 toocreate 新的掛接點。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 建立 VM 的備份
> * 排定每日備份
> * 從備份還原檔案

前進 toohello 下一個教學課程的 toolearn 有關監視虛擬機器。

> [!div class="nextstepaction"]
> [監視虛擬機器](tutorial-monitoring.md)

