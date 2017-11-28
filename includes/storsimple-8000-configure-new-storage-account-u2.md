<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a><span data-ttu-id="0f7c0-101">若要在與 StorSimple 裝置管理員服務相同的 Azure 訂用帳戶中新增儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="0f7c0-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span></span>

1. <span data-ttu-id="0f7c0-102">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="0f7c0-103">在 [設定] 區段中，按一下 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-103">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![儲存體帳戶認證](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. <span data-ttu-id="0f7c0-105">在 [儲存體帳戶認證] 刀鋒視窗上，按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-105">On the **Storage account credentials** blade, click **+ Add**.</span></span>

    ![新增儲存體帳戶認證](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. <span data-ttu-id="0f7c0-107">在 [新增儲存體帳戶認證] 刀鋒視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="0f7c0-107">In the **Add a storage account credential** blade, do the following steps:</span></span>

    1. <span data-ttu-id="0f7c0-108">當您在與服務相同的 Azure 訂用帳戶中新增儲存體帳戶認證時，請確認已選取 [目前]。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span></span>

    2. <span data-ttu-id="0f7c0-109">從 [儲存體帳戶] 下拉式清單中，選取現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-109">From the **storage account** dropdown list, select an existing storage account.</span></span>

    3. <span data-ttu-id="0f7c0-110">根據選取的儲存體帳戶，會顯示 [位置] (呈現灰色且無法在此變更)。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span></span>

    4. <span data-ttu-id="0f7c0-111">選取 [啟用 SSL 模式]  來建立裝置與雲端之間網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="0f7c0-112">只有當您在私人雲端內操作時，才將 [啟用 SSL] 停用。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-112">Disable **Enable SSL** only if you are operating within a private cloud.</span></span>

        ![新增 [儲存體帳戶認證] 刀鋒視窗](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. <span data-ttu-id="0f7c0-114">按一下 [新增] 可啟動儲存體帳戶認證的作業建立。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-114">Click **Add** to start the job creation for the storage account credential.</span></span> <span data-ttu-id="0f7c0-115">成功建立儲存體帳戶認證之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-115">You will be notified after the storage account credential is successfully created.</span></span>

        ![儲存體帳戶認證的成功通知](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

<span data-ttu-id="0f7c0-117">新建立的儲存體帳戶認證將會顯示在 [儲存體帳戶認證] 清單中。</span><span class="sxs-lookup"><span data-stu-id="0f7c0-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span></span>

![儲存體帳戶認證的清單](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

