1. <span data-ttu-id="65ca4-101">建立並執行 Azure 虛擬機器後，請按一下 Azure 入口網站中的 [虛擬機器] 圖示，以檢視您的 VM。</span><span class="sxs-lookup"><span data-stu-id="65ca4-101">After the Azure virtual machine is created and running, click the Virtual Machines icon in the Azure portal to view your VMs.</span></span>

1. <span data-ttu-id="65ca4-102">按一下新 VM 的省略符號 (**...**)。</span><span class="sxs-lookup"><span data-stu-id="65ca4-102">Click the ellipsis, **...**, for your new VM.</span></span>

1. <span data-ttu-id="65ca4-103">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="65ca4-103">Click **Connect**.</span></span>

   ![在入口網站中連線到 VM](./media/virtual-machines-sql-server-remote-desktop-connect/azure-virtual-machine-connect.png)

1. <span data-ttu-id="65ca4-105">開啟您的瀏覽器為 VM 下載的 **RDP** 檔案。</span><span class="sxs-lookup"><span data-stu-id="65ca4-105">Open the **RDP** file that your browser downloads for the VM.</span></span>

1. <span data-ttu-id="65ca4-106">[遠端桌面連線] 會通知您無法識別這個遠端連線的發行者。</span><span class="sxs-lookup"><span data-stu-id="65ca4-106">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="65ca4-107">按一下 [連接]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="65ca4-107">Click **Connect** to continue.</span></span>

1. <span data-ttu-id="65ca4-108">在 [Windows 安全性] 對話方塊中，按一下 [使用不同帳戶]。</span><span class="sxs-lookup"><span data-stu-id="65ca4-108">In the **Windows Security** dialog, click **Use a different account**.</span></span> <span data-ttu-id="65ca4-109">您可能必須按一下 [更多選擇] 才能看到它。</span><span class="sxs-lookup"><span data-stu-id="65ca4-109">You might have to click **More choices** to see this.</span></span> <span data-ttu-id="65ca4-110">指定您建立 VM 時所設定的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="65ca4-110">Specify the user name and password that you configured when you created the VM.</span></span> <span data-ttu-id="65ca4-111">您必須在使用者名稱之前新增反斜線。</span><span class="sxs-lookup"><span data-stu-id="65ca4-111">You must add a backslash before the user name.</span></span>

   ![遠端桌面驗證](./media/virtual-machines-sql-server-remote-desktop-connect/remote-desktop-connect.png)

1. <span data-ttu-id="65ca4-113">按一下 [確定] 進行連線。</span><span class="sxs-lookup"><span data-stu-id="65ca4-113">Click **OK** to connect.</span></span>