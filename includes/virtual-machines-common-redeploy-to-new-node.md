## <a name="use-the-azure-portal"></a><span data-ttu-id="b7e64-101">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b7e64-101">Use the Azure portal</span></span>
1. <span data-ttu-id="b7e64-102">選取您想要重新部署的 VM，然後選取下 [設定] 刀鋒視窗中的 [重新部署] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7e64-102">Select the VM you wish to redeploy, then select the *Redeploy* button in the *Settings* blade.</span></span> <span data-ttu-id="b7e64-103">您可能需要向下捲動以查看 [支援與疑難排解]  區段，其中包含 [重新部署] 按鈕，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="b7e64-103">You may need to scroll down to see the **Support and Troubleshooting** section that contains the 'Redeploy' button as in the following example:</span></span>
   
    ![Azure VM 刀鋒視窗](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. <span data-ttu-id="b7e64-105">若要確認此作業，請選取 [重新部署] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="b7e64-105">To confirm the operation, select the *Redeploy* button:</span></span>
   
    ![重新部署 VM 刀鋒視窗](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. <span data-ttu-id="b7e64-107">當 VM 準備重新部署時，VM 的 [狀態] 會變更為 [正在更新]，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="b7e64-107">The **Status** of the VM changes to *Updating* as the VM prepares to redeploy, as shown in the following example:</span></span>
   
    ![VM 正在更新](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. <span data-ttu-id="b7e64-109">當 VM 在新的 Azure 主機上開機時，[狀態] 會接著變更為 [正在啟動]，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="b7e64-109">The **Status** then changes to *Starting* as the VM boots up on a new Azure host, as shown in the following example:</span></span>
   
    ![VM 正在啟動](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. <span data-ttu-id="b7e64-111">在 VM 完成開機程序之後，[狀態] 則會回復為 [正在執行]，表示已順利重新部署 VM︰</span><span class="sxs-lookup"><span data-stu-id="b7e64-111">After the VM finishes the boot process, the **Status** then returns to *Running*, indicating the VM has been successfully redeployed:</span></span>
   
    ![VM 正在執行](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)

