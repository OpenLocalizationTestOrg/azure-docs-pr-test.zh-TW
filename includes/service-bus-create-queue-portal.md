<span data-ttu-id="63670-101">請確定您已建立服務匯流排命名空間，如[這裡][namespace-how-to]所示。</span><span class="sxs-lookup"><span data-stu-id="63670-101">Please ensure that you have already created a Service Bus namespace, as shown [here][namespace-how-to].</span></span>

1. <span data-ttu-id="63670-102">登入 [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="63670-102">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="63670-103">在入口網站的左方瀏覽窗格中，按一下 [服務匯流排] \(如果您未看見 [服務匯流排]，請按一下 [更多服務])。</span><span class="sxs-lookup"><span data-stu-id="63670-103">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="63670-104">按一下要在其中建立佇列的命名空間。</span><span class="sxs-lookup"><span data-stu-id="63670-104">Click the namespace in which you would like to create the queue.</span></span> <span data-ttu-id="63670-105">在本例中是 **nstest1**。</span><span class="sxs-lookup"><span data-stu-id="63670-105">In this case, it is **nstest1**.</span></span>
   
    ![建立佇列][createqueue1]
4. <span data-ttu-id="63670-107">在 [服務匯流排命名空間] 刀鋒視窗中，選取 [佇列]，然後按一下 [新增佇列]。</span><span class="sxs-lookup"><span data-stu-id="63670-107">In the **Service Bus namespace** blade, select **Queues**, then click **Add queue**.</span></span>
   
    ![選取佇列][createqueue2]
5. <span data-ttu-id="63670-109">輸入 [佇列名稱]  並且讓其他值保留其預設值。</span><span class="sxs-lookup"><span data-stu-id="63670-109">Enter the **Queue Name** and leave the other values with their defaults.</span></span>
   
    ![選取新增][createqueue3]
6. <span data-ttu-id="63670-111">按一下刀鋒視窗底部的 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="63670-111">At the bottom of the blade, click **Create**.</span></span>

[createqueue1]: ./media/service-bus-create-queue-portal/create-queue1.png
[createqueue2]: ./media/service-bus-create-queue-portal/create-queue2.png
[createqueue3]: ./media/service-bus-create-queue-portal/create-queue3.png

[namespace-how-to]: ../articles/service-bus-messaging/service-bus-create-namespace-portal.md
[azure-portal]: https://portal.azure.com
