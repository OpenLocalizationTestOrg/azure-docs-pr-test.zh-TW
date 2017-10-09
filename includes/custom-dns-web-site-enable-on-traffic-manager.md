<span data-ttu-id="a9ba9-101">傳播 hello 記錄您的網域名稱之後，您應該要能夠 toouse 您可以將自訂網域名稱的瀏覽器 tooverify 是使用的 tooaccess 在 Azure App Service web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-101">After hello records for your domain name have propagated, you should be able toouse your browser tooverify that your custom domain name can be used tooaccess your web app in Azure App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ba9-102">可能需要一些時間，您的 CNAME toopropagate 透過 hello DNS 系統。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-102">It can take some time for your CNAME toopropagate through hello DNS system.</span></span> <span data-ttu-id="a9ba9-103">您可以使用服務，例如<a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> hello CNAME 的 tooverify 為止。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-103">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify that hello CNAME is available.</span></span>
> 
> 

<span data-ttu-id="a9ba9-104">如果您在 Traffic Manager 端點並不加入您的 web 應用程式，您必須進行才能執行名稱解析，為 hello 自訂網域名稱的路由 tooTraffic 管理員。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-104">If you have not already added your web app as a Traffic Manager endpoint, you must do this before name resolution will work, as hello custom domain name routes tooTraffic Manager.</span></span> <span data-ttu-id="a9ba9-105">然後，traffic Manager 路由傳送 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-105">Traffic Manager then routes tooyour web app.</span></span> <span data-ttu-id="a9ba9-106">使用中的 hello 資訊[新增或刪除端點](../articles/traffic-manager/traffic-manager-endpoints.md)tooadd web 應用程式為您的 Traffic Manager 設定檔中的端點。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-106">Use hello information in [Add or Delete Endpoints](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd your web app as an endpoint in your Traffic Manager profile.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ba9-107">如果在新增端點時未列出您的 Web 應用程式，請確認模式是設為 [ **標準** ] App Service 計劃模式。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-107">If your web app is not listed when adding an endpoint, verify that it is configured for **Standard** App Service plan mode.</span></span> <span data-ttu-id="a9ba9-108">您必須使用**標準**順序 toowork 使用 Traffic Manager 中的 web 應用程式的模式。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-108">You must use **Standard** mode for your web app in order toowork with Traffic Manager.</span></span>
> 
> 

1. <span data-ttu-id="a9ba9-109">在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-109">In your browser, open hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9ba9-110">在 hello **Web 應用程式**索引標籤上，按一下您 web 應用程式，選取 hello 名稱**設定**，然後選取**自訂網域**</span><span class="sxs-lookup"><span data-stu-id="a9ba9-110">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="a9ba9-111">在 hello**自訂網域**刀鋒視窗中，按一下 **新增主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-111">In hello **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="a9ba9-112">使用 hello **Hostname**文字方塊 tooenter hello Traffic Manager 網域名稱 tooassociate 與此 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-112">Use hello **Hostname** text boxes tooenter hello Traffic Manager domain name tooassociate with this web app.</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. <span data-ttu-id="a9ba9-113">按一下**驗證**toosave hello 網域名稱設定。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-113">Click **Validate** toosave hello domain name configuration.</span></span>
6. <span data-ttu-id="a9ba9-114">按一下 [驗證] 後，Azure 便會開始進行網域驗證工作流程。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-114">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="a9ba9-115">這會檢查網域擁有權，以及主機名稱可用性和報告成功或規定 guidence 上 toofix hello 錯誤的方式與詳細的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-115">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how toofix hello error.</span></span>    
7. <span data-ttu-id="a9ba9-116">成功驗證後**新增 hostname**按鈕會變成作用中，您也可以 toohello 指派主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-116">Upon successful validation **Add hostname** button will become active and you will be able toohello assign hostname.</span></span> <span data-ttu-id="a9ba9-117">現在您可以瀏覽 tooyour 瀏覽器中的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-117">Now navigate tooyour custom domain name in a browser.</span></span> <span data-ttu-id="a9ba9-118">您現在應會看到您應用程式正在使用您的自訂網域名稱執行。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-118">You should now see your app running using your custom domain name.</span></span> 
   
   <span data-ttu-id="a9ba9-119">一旦組態完成之後，hello 自訂網域名稱將會列在 hello**網域名稱**web 應用程式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-119">Once configuration has completed, hello custom domain name will be listed in hello **domain names** section of your web app.</span></span>

<span data-ttu-id="a9ba9-120">此時，您也應該能夠 tooenter hello Traffic Manager 網域名稱在瀏覽器並查看它成功採用您 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9ba9-120">At this point, you should be able tooenter hello Traffic Manager domain name name in your browser and see that it successfully takes you tooyour web app.</span></span>

