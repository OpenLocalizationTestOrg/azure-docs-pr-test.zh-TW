<!--author=alkohli last changed: 01/13/17-->

<span data-ttu-id="6099e-101">如果磁碟區容器有相關聯的磁碟區，請先將那些磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="6099e-101">If the volume container has associated volumes, take those volumes offline first.</span></span> <span data-ttu-id="6099e-102">請遵循 [使磁碟區離線](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="6099e-102">Follow the steps in [Take a volume offline](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="6099e-103">磁碟機離線後，才可以刪除它們。</span><span class="sxs-lookup"><span data-stu-id="6099e-103">After the volumes are offline, you can delete them.</span></span> <span data-ttu-id="6099e-104">當磁碟區容器沒有相關聯的磁碟區時，請將磁碟區容器刪除。</span><span class="sxs-lookup"><span data-stu-id="6099e-104">When the volume container has no associated volumes, delete the volume container.</span></span> <span data-ttu-id="6099e-105">執行下列程序可將磁碟區容器刪除。</span><span class="sxs-lookup"><span data-stu-id="6099e-105">Perform the following procedure to delete a volume container.</span></span>

#### <a name="to-delete-a-volume-container"></a><span data-ttu-id="6099e-106">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="6099e-106">To delete a volume container</span></span>
1. <span data-ttu-id="6099e-107">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="6099e-107">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="6099e-108">選取並按一下裝置，然後移至 [設定] > [管理] > [磁碟區容器]。</span><span class="sxs-lookup"><span data-stu-id="6099e-108">Select and click the device and then go to **Settings > Manage > Volume containers**.</span></span>

    ![磁碟區容器刀鋒視窗](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

2. <span data-ttu-id="6099e-110">從表格式的磁碟區容器清單中，選取您想要刪除的磁碟區容器，以滑鼠右鍵按一下 [...]，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="6099e-110">From the tabular list of volume containers, select the volume container you want to delete, right click **...** and then select **Delete**.</span></span>

    ![將磁碟區容器刪除](./media/storsimple-8000-delete-volume-container/deletevolumecontainer1.png)

3. <span data-ttu-id="6099e-112">磁碟區容器沒有相關聯的磁碟區時，才能刪除它。</span><span class="sxs-lookup"><span data-stu-id="6099e-112">If a volume container has no associated volumes, then it can be deleted.</span></span> <span data-ttu-id="6099e-113">當系統提示您進行確認時，請檢閱並選取指出刪除磁碟區容器影響的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6099e-113">When prompted for confirmation, review and select the checkbox stating the impact of deleting the volume container.</span></span> <span data-ttu-id="6099e-114">按一下 [刪除] 即可將磁碟區容器刪除。</span><span class="sxs-lookup"><span data-stu-id="6099e-114">Click **Delete** to then delete the volume container.</span></span>

    ![確認刪除](./media/storsimple-8000-delete-volume-container/deletevolumecontainer2.png)

<span data-ttu-id="6099e-116">磁碟區容器清單會加以更新，來反映已刪除的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="6099e-116">The list of volume containers is updated to reflect the deleted volume container.</span></span>

![](./media/storsimple-8000-delete-volume-container/deletevolumecontainer5.png)


