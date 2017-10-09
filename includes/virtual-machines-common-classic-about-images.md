

映像可用 Azure tooprovide 中新的虛擬機器的作業系統。 一個映像可能有一或多個資料磁碟。 映像可來自多個來源：

* Azure 提供的映像中 hello [Marketplace](https://azure.microsoft.com/gallery/virtual-machines/)。 有新版的 Windows Server 和 hello Linux 作業系統的散發。 有些映像也包含應用程式，例如 SQL Server。 MSDN Benefit 和 MSDN Pay-as-You-Go 訂閱者有存取 tooadditional 映像。
* hello 開放原始碼社群提供的映像透過[VM Depot](http://vmdepot.msopentech.com/List/Index)。
* 您也可以擷取現有的 Azure 虛擬機器作為映像或上傳映像，並在 Azure 中儲存和使用自己的映像。

## <a name="about-vm-images-and-os-images"></a>關於 VM 映像和 OS 映像
在 Azure 中可用的映像有兩種類型：*VM 映像*和 *OS 映像*。 VM 映像包含作業系統和建立 hello 映像時，所有磁碟都附加 tooa 虛擬機器。 VM 映像為 hello 映像的較新的類型。 導入 VM 映像前，Azure 中的映像可能只會有一般化的作業系統，而沒有其他磁碟。 包含僅一般化的作業系統的 VM 映像基本上 hello 與 hello 的映像，hello OS 映像的原始類型相同。

您可以根據 Azure 上的虛擬機器，或您複製及上傳並正在其他地方執行的虛擬機器，來建立自己的映像。 如果您想 toouse 映像 toocreate 多部虛擬機器，您需要 tooprepare 它用來將它一般化映像做。 toocreate Windows Server 映像，執行的 hello Sysprep 命令上 hello 伺服器 toogeneralize 它之前 hello.vhd 檔案上傳。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://go.microsoft.com/fwlink/p/?LinkId=392030)和[伺服器角色的 Sysprep 支援](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。 執行 Sysprep 之前先備份 hello VM。 視散發套件而異，建立 Linux 映像。 一般而言，您需要 toorun 一組特定的 toohello 發佈及執行 hello Azure Linux 代理程式的命令。
