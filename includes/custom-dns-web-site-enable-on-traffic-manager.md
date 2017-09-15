<span data-ttu-id="c49af-101">傳播網域名稱的記錄後，您應該要能夠使用瀏覽器來確認您自訂的網域名稱可用來存取 Azure App Service 中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c49af-101">After the records for your domain name have propagated, you should be able to use your browser to verify that your custom domain name can be used to access your web app in Azure App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="c49af-102">需要一些時間，CNAME 才能傳播至整個 DNS 系統。</span><span class="sxs-lookup"><span data-stu-id="c49af-102">It can take some time for your CNAME to propagate through the DNS system.</span></span> <span data-ttu-id="c49af-103">您可以使用 <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> 之類的服務來驗證 CNAME 已生效。</span><span class="sxs-lookup"><span data-stu-id="c49af-103">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the CNAME is available.</span></span>
> 
> 

<span data-ttu-id="c49af-104">若尚未新增 Web 應用程式作為流量管理員端點，則必須先執行此作業，名稱解析才能正常運作，因為自訂網域名稱會路由至流量管理員。</span><span class="sxs-lookup"><span data-stu-id="c49af-104">If you have not already added your web app as a Traffic Manager endpoint, you must do this before name resolution will work, as the custom domain name routes to Traffic Manager.</span></span> <span data-ttu-id="c49af-105">接著會將流量管理員路由至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c49af-105">Traffic Manager then routes to your web app.</span></span> <span data-ttu-id="c49af-106">使用 [新增或刪除端點](../articles/traffic-manager/traffic-manager-endpoints.md) 中的資訊，將 Web 應用程式新增為流量管理員設定檔中的端點。</span><span class="sxs-lookup"><span data-stu-id="c49af-106">Use the information in [Add or Delete Endpoints](../articles/traffic-manager/traffic-manager-endpoints.md) to add your web app as an endpoint in your Traffic Manager profile.</span></span>

> [!NOTE]
> <span data-ttu-id="c49af-107">如果在新增端點時未列出您的 Web 應用程式，請確認模式是設為 [ **標準** ] App Service 計劃模式。</span><span class="sxs-lookup"><span data-stu-id="c49af-107">If your web app is not listed when adding an endpoint, verify that it is configured for **Standard** App Service plan mode.</span></span> <span data-ttu-id="c49af-108">您必須讓 Web 應用程式使用 [ **標準** ] 模式，才能與流量管理員搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c49af-108">You must use **Standard** mode for your web app in order to work with Traffic Manager.</span></span>
> 
> 

1. <span data-ttu-id="c49af-109">在瀏覽器中，開啟 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c49af-109">In your browser, open the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c49af-110">在 [Web Apps] 索引標籤中，按一下您 Web 應用程式的名稱，並選取 [設定]，然後選取 [自訂網域]</span><span class="sxs-lookup"><span data-stu-id="c49af-110">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="c49af-111">在 [自訂網域] 刀鋒視窗中，按一下 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="c49af-111">In the **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="c49af-112">使用 [主機名稱]  文字方塊輸入與此 Web 應用程式相關聯的流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="c49af-112">Use the **Hostname** text boxes to enter the Traffic Manager domain name to associate with this web app.</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. <span data-ttu-id="c49af-113">按一下 [驗證]  以儲存網域名稱設定。</span><span class="sxs-lookup"><span data-stu-id="c49af-113">Click **Validate** to save the domain name configuration.</span></span>
6. <span data-ttu-id="c49af-114">按一下 [驗證] 後，Azure 便會開始進行網域驗證工作流程。</span><span class="sxs-lookup"><span data-stu-id="c49af-114">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="c49af-115">此流程將會檢查網域擁有權及主機名稱可用性，並回報成功與否。在發生錯誤的情況下，將會提供錯誤詳細資料，以及錯誤修復方式的規範指引。</span><span class="sxs-lookup"><span data-stu-id="c49af-115">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how to fix the error.</span></span>    
7. <span data-ttu-id="c49af-116">成功驗證後，[新增主機名稱]  按鈕將會變成作用中，使您可以指派主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c49af-116">Upon successful validation **Add hostname** button will become active and you will be able to the assign hostname.</span></span> <span data-ttu-id="c49af-117">現在請在瀏覽器中瀏覽到您的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="c49af-117">Now navigate to your custom domain name in a browser.</span></span> <span data-ttu-id="c49af-118">您現在應會看到您應用程式正在使用您的自訂網域名稱執行。</span><span class="sxs-lookup"><span data-stu-id="c49af-118">You should now see your app running using your custom domain name.</span></span> 
   
   <span data-ttu-id="c49af-119">完成設定後，自訂網域名稱將列在 Web 應用程式的 [ **網域名稱** ] 區段中。</span><span class="sxs-lookup"><span data-stu-id="c49af-119">Once configuration has completed, the custom domain name will be listed in the **domain names** section of your web app.</span></span>

<span data-ttu-id="c49af-120">此時，您應該能夠在瀏覽器中輸入流量管理員網域名稱，並且能成功移至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c49af-120">At this point, you should be able to enter the Traffic Manager domain name name in your browser and see that it successfully takes you to your web app.</span></span>

