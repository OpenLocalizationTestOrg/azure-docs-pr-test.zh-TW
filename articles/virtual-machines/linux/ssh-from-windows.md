---
title: "適用於 Linux Vm aaaUse SSH 金鑰與 Windows |Microsoft 文件"
description: "了解如何 toogenerate 及使用 SSH 金鑰的 Windows 電腦 tooconnect tooa Linux 虛擬機器上 Azure。"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>TooUse SSH 與 Windows Azure 上的索引鍵
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

當您連接 tooLinux Azure 虛擬機器 (Vm) 中時，您應該使用[公開金鑰密碼編譯](https://wikipedia.org/wiki/Public-key_cryptography)tooprovide 更安全的方式 toolog tooyour Linux VM 中。 此程序牽涉到自行使用 hello 安全殼層 (SSH) 命令 tooauthenticate，而不使用者名稱和密碼的公用和私用金鑰交換。 密碼是很容易遭受 toobrute 強制的攻擊，尤其是在網際網路對向 Vm，例如網頁伺服器上。 本文提供的 SSH 金鑰和 toogenerate hello 適當的 Windows 電腦上的索引鍵的方式的概觀。

## <a name="overview-of-ssh-and-keys"></a>SSH 和金鑰的概觀
您可以安全地登入 tooyour Linux VM 使用公開和私密金鑰：

* hello**公開金鑰**置於 Linux VM 或您想 toouse 公開金鑰加密中使用的任何其他服務。
* hello**私密金鑰**時，您有 tooyour Linux VM 登入時，tooverify 您的身分識別。 保護此私密金鑰。 不要共用它。

這些公用和私密金鑰可以使用於多個 VM 和服務。 您不需要針對每個 VM 或服務想 tooaccess 的金鑰組。 如需更詳細的概觀，請參閱[公開金鑰加密](https://wikipedia.org/wiki/Public-key_cryptography)。

SSH 是允許透過不安全的連線進行安全登入的加密連線通訊協定。 它是在 Azure 中裝載的 Linux Vm 的 hello 預設連線通訊協定。 雖然本身 SSH 提供加密的連接，但是使用 SSH 連線的密碼會保留 hello VM 很容易遭受 toobrute 強制攻擊或破解的密碼。 使用 SSH 的 VM 是使用這些公用和私用金鑰，也稱為 SSH 金鑰連接 tooa 更為安全且慣用方法。

如果您不想 toouse SSH 金鑰，您仍然可以記錄 tooyour Linux Vm 使用的密碼。 如果您的 VM 不公開的 toohello 網際網路，請使用密碼可能不足。 不過，您仍然需要為每個 Linux VM toomanage 您的密碼，並維護狀況良好的密碼原則和作法，例如最小密碼長度和定期更新它們。 hello 使用 SSH 金鑰可降低管理跨多個 Vm 的個別認證 hello 複雜性。

## <a name="windows-packages-and-ssh-clients"></a>Windows 套件和 SSH 用戶端
連接 tooand 管理 Linux Vm 在 Azure 中使用**SSH 用戶端**。 Windows 電腦通常不會安裝 SSH 用戶端。 Windows 10 年度更新 hello 加入撞 for Windows，並 hello 最新的 Windows 10 建立者更新提供其他的更新。 這個適用於 Linux 的 Windows 子系統，可讓您 toorun 及存取公用程式，例如 Bash 殼層中的原生的 SSH 用戶端。 您可以依照任何 hello Linux 文件，例如[如何 toogenerate SSH 金鑰組適用於 Linux](mac-create-ssh-keys.md)。 Bash for Windows 仍處於開發階段，而且被視為測試版。 如需 Bash for Windows 的詳細資訊，請參閱 [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about)。

如果您想 toouse 東西撞適用於 Windows 以外，一般 Windows SSH 用戶端可以安裝包含下列封裝的 hello:

* [Git For Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>金鑰檔需要 toocreate 嗎？
Azure 需要至少 2048 位元的 **ssh-rsa** 格式公開和私密金鑰。 如果您管理 Azure 資源使用 hello 傳統部署模型，您也需要 toogenerate PEM (`.pem`檔案)。

以下是 hello 部署案例，以及您使用在每個檔案的 hello 類型：

1. **ssh rsa**金鑰所需的任何部署使用 hello [Azure 入口網站](https://portal.azure.com)，並使用 hello 的資源管理員部署[Azure CLI](../../cli-install-nodejs.md)。
   * 通常大部分的人都需要這些金鑰。
2. A`.pem`檔案是使用 hello 傳統部署的必要的 toocreate Vm。 在傳統部署支援這些索引鍵時使用 hello [Azure 入口網站](https://portal.azure.com)或[Azure CLI](../../cli-install-nodejs.md)。
   * 您只需要 toocreate 這些額外的金鑰和憑證如果您要管理使用 hello 傳統部署模型所建立的資源。

## <a name="install-git-for-windows"></a>安裝 Git for Windows
hello 上一節中列出數個封裝，包括 hello`openssl`適用於 Windows 的工具。 此工具是需要的 toocreate 公用和私用金鑰。 hello 如何遵循範例詳細資料 tooinstall 並用**Git for Windows**，但是您可以選擇任何您偏好的套件。 **Git for Windows**可讓您存取 toosome 其他開放原始碼軟體 ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) 工具和公用程式，當您使用 Linux Vm 可能會很有用。

1. 下載並安裝**Git for Windows**從下列位置的 hello: [https://git-for-windows.github.io/](https://git-for-windows.github.io/)。
2. 接受 hello hello 期間的預設選項安裝程序，除非您特別需要 toochange 它們。
3. 執行**Git Bash**從 hello**開始功能表** > **Git** > **Git Bash**。 hello 主控台看起來類似下列範例的 toohello:

    ![Git for Windows Bash Shell](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>建立私密金鑰
1. 在您**Git Bash**  視窗中，使用`openssl.exe`toocreate 私用金鑰。 hello 下列範例會建立名為`myPrivateKey`和名為憑證`myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    hello 輸出看起來類似下列範例的 toohello:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   如果 Bash 報告錯誤，嘗試以提高的權限開啟新的 **Git Bash** 視窗。 然後，重新執行 hello`openssl`命令。

2. 回應 hello 提示國家/地區名稱、 位置、 組織名稱等等。
3. 您的私密金鑰和憑證已建立在您目前的工作目錄中。 基於安全性考量，您應該在您的私密金鑰設定 hello 權，讓您只可以存取它：

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. hello[下一節](#create-a-private-key-for-putty)使用 Ssh-keygen tooboth 詳細資料檢視和使用 hello 公開金鑰，並建立適合使用 PuTTY tooSSH tooLinux Vm 的私密金鑰。 hello 下列命令會產生名為的公開金鑰檔案`myPublicKey.key`，您可以立即使用：

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. 如果您也需要 toomanage 傳統資源，將轉換 hello`myCert.pem`太`myCert.cer`(DER 編碼 X509 憑證)。 執行此選擇性步驟中，只有當您需要 toospecifically 管理較舊的傳統資源。

    轉換使用下列命令的 hello hello 憑證：

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>建立 PuTTY 的私密金鑰
PuTTY 是適用於 Windows 的常見 SSH 用戶端。 您是免費 toouse 任何您想要的 SSH 用戶端。 toouse PuTTY，您需要 toocreate 其他類型的索引鍵-PuTTY 私用金鑰 (PPK)。 如果您不想 toouse PuTTY，略過本節。

hello 下列範例會建立專為 PuTTY toouse 這個額外私密金鑰：

1. 使用**Git Bash** tooconvert 私人金鑰到 RSA 私密金鑰 Ssh-keygen 可以了解。 hello 下列範例會建立名為`myPrivateKey_rsa`從名為 hello 現有索引鍵`myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    基於安全性考量，您應該在您的私密金鑰設定 hello 權，讓您只可以存取它：

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. 下載並執行從下列位置的 hello Ssh-keygen: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. 按一下 [hello] 功能表：**檔案** > **負載私密金鑰**
4. 找出您的私密金鑰 (`myPrivateKey_rsa` hello 前一個範例中)。 當您啟動 hello 預設目錄**Git Bash**是`C:\Users\%username%`。 變更 hello 檔案篩選器 tooshow**所有檔案 (\*。\*)**:

    ![載入 Ssh-keygen hello 現有的私密金鑰](./media/ssh-from-windows/load-private-key.png)
5. 按一下 [開啟] 。 提示表示該 hello 金鑰已成功匯入：

    ![已成功匯入金鑰 tooPuTTYgen](./media/ssh-from-windows/successfully-imported-key.png)
6. 按一下**確定**tooclose hello 提示字元。
7. hello 公開金鑰會顯示在 hello hello 頂端**Ssh-keygen**視窗。 您複製並貼入此公開金鑰 hello Azure 入口網站或 Azure Resource Manager 範本當您建立 Linux VM。 您也可以按一下**儲存公開金鑰**toosave 複製 tooyour 電腦：

    ![儲存 PuTTY 公用金鑰檔案](./media/ssh-from-windows/save-public-key.png)

    hello 下列範例顯示如何您會複製並貼到 hello Azure 入口網站的這個公開金鑰，當您建立 Linux VM。 hello 公開金鑰然後通常儲存在`~/.ssh/authorized_keys`新 VM 上。

    ![Hello Azure 入口網站中建立 VM 時使用的公開金鑰](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. 回到 **PuTTYgen**，按一下 [儲存私密金鑰]：

    ![儲存 PuTTY 私密金鑰檔案](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > 出現提示要求您是否想 toocontinue，而不需輸入金鑰複雜密碼。 複雜密碼就像是密碼附加的 tooyour 私用金鑰。 即使其他人為 tooobtain 私密金鑰，它們仍不會使用只 hello 金鑰無法 tooauthenticate。 它們也需要 hello 複雜密碼。 如果沒有複雜密碼，如果有人取得您的私密金鑰，他們可以登入 tooany VM 或服務使用該索引鍵。 我們建議您建立複雜密碼。 不過，如果您忘記 hello 複雜密碼，沒有任何方式 toorecover 它。
   >
   >

    如果您想 tooenter 複雜密碼，按一下**否**hello 主要 Ssh-keygen 視窗中輸入的複雜密碼，然後按**儲存私密金鑰**一次。 否則，請按一下**是**toocontinue 而不需提供 hello 選用的複雜密碼。
9. 輸入名稱和位置 toosave PPK 檔案。

## <a name="use-putty-toossh-tooa-linux-machine"></a>使用 Putty tooSSH tooa Linux 機器
同樣地，PuTTY 是適用於 Windows 的常見 SSH 用戶端。 您是免費 toouse 任何您想要的 SSH 用戶端。 hello 如何遵循步驟詳細 toouse 您與使用 SSH Azure VM 的私用金鑰 tooauthenticate。 hello 步驟的很類似其他 SSH 金鑰的用戶端方面需要 tooload 您私用金鑰 tooauthenticate hello SSH 連線。

1. 下載並執行的 putty 從下列位置的 hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. 填滿 hello 主機名稱或 IP 位址，您的 VM 從 hello Azure 入口網站：

    ![開啟新的 PuTTY 連線](./media/ssh-from-windows/putty-new-connection.png)
3. 選取 [開啟] 之前，按一下 [連線] > [SSH] > [Auth] 索引標籤。瀏覽 tooand 選取您的私密金鑰：

    ![選取您的 PuTTY 私密金鑰進行驗證](./media/ssh-from-windows/putty-auth-dialog.png)
4. 按一下**開啟**tooconnect tooyour 虛擬機器

## <a name="next-steps"></a>後續步驟
您也可以產生 hello 公用和私用金鑰[使用 OS X 和 Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

如需撞 for Windows 和 Windows 電腦上擁有 OSS 工具方便的 hello 優點的詳細資訊，請參閱[撞在 Windows 上的 Ubuntu 上](https://msdn.microsoft.com/commandline/wsl/about)。

如果您有使用 SSH tooconnect tooyour Linux Vm 時發生問題，請參閱[疑難排解 SSH 連線 tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
