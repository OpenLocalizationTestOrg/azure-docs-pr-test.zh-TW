<span data-ttu-id="9148f-101">傳播 hello 記錄您的網域名稱之後，您必須使其與您 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9148f-101">After hello records for your domain name have propagated, you must associate them with your Web App.</span></span> <span data-ttu-id="9148f-102">使用下列步驟 tooenable hello 網域名稱使用網頁瀏覽器的 hello。</span><span class="sxs-lookup"><span data-stu-id="9148f-102">Use hello following steps tooenable hello domain names using your web browser.</span></span>

> [!NOTE]
> <span data-ttu-id="9148f-103">它可能需要一些時間透過 DNS 系統 hello hello 上一個步驟 toopropagate 中建立 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="9148f-103">It can take some time for TXT records created in hello previous steps toopropagate through hello DNS system.</span></span> <span data-ttu-id="9148f-104">Hello TXT 記錄已傳播之前，您無法加入 hello tooyour web 應用程式的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="9148f-104">You cannot add hello domain name of tooyour web app until hello TXT record has propagated.</span></span> <span data-ttu-id="9148f-105">如果您使用 A 記錄，您無法加入 hello 記錄的網域名稱 tooyour web 應用程式，直到傳播到 hello 先前步驟中建立的 hello TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="9148f-105">If you are using an A record, you cannot add hello A record domain name tooyour web app until hello TXT record created in hello previous step has propagated.</span></span>
> 
> <span data-ttu-id="9148f-106">您可以使用服務，例如<a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> hello TXT 記錄的 tooverify 為止。</span><span class="sxs-lookup"><span data-stu-id="9148f-106">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify that hello TXT record is available.</span></span>
> 
> 

1. <span data-ttu-id="9148f-107">在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9148f-107">In your browser, open hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9148f-108">在 hello **Web 應用程式**索引標籤上，按一下您的 web 應用程式，hello 名稱，然後選取**自訂網域**</span><span class="sxs-lookup"><span data-stu-id="9148f-108">In hello **Web Apps** tab, click hello name of your web app, and then select **Custom domains**</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="9148f-109">在 hello**自訂網域**刀鋒視窗中，按一下 **新增主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="9148f-109">In hello **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="9148f-110">使用 hello **Hostname**文字方塊 tooenter hello 網域名稱 tooassociate 與此 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9148f-110">Use hello **Hostname** text boxes tooenter hello domain names tooassociate with this web app.</span></span>
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. <span data-ttu-id="9148f-111">按一下 [驗證] 。</span><span class="sxs-lookup"><span data-stu-id="9148f-111">Click **Validate**.</span></span>
6. <span data-ttu-id="9148f-112">按一下 [驗證] 後，Azure 便會開始進行網域驗證工作流程。</span><span class="sxs-lookup"><span data-stu-id="9148f-112">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="9148f-113">這會檢查網域擁有權，以及主機名稱可用性和報告成功或規定 guidence 上 toofix hello 錯誤的方式與詳細的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9148f-113">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how toofix hello error.</span></span>    

<span data-ttu-id="9148f-114">此時，您應該瀏覽器中是無法 tooenter hello 自訂網域名稱，並查看它成功採用您 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9148f-114">At this point, you should be able tooenter hello custom domain name in your browser and see that it successfully takes you tooyour web app.</span></span>

