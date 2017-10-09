### <a name="prerequisites"></a><span data-ttu-id="299f8-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="299f8-101">Prerequisites</span></span>
* <span data-ttu-id="299f8-102">Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="299f8-102">A Twilio account</span></span>
* <span data-ttu-id="299f8-103">已驗證的 Twilio 電話號碼，以便接收簡訊</span><span class="sxs-lookup"><span data-stu-id="299f8-103">A verified Twilio phone number that can receive SMS</span></span>
* <span data-ttu-id="299f8-104">已驗證的 Twilio 電話號碼，以便傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="299f8-104">A verified Twilio phone number that can send SMS</span></span>

> [!NOTE]
> <span data-ttu-id="299f8-105">如果您使用的 Twilio 試用版帳戶，您可以只傳送 SMS 太**驗證**電話號碼。</span><span class="sxs-lookup"><span data-stu-id="299f8-105">If you are using a Twilio trial account, you can only send SMS too**verified** phone numbers.</span></span>  
> 
> 

<span data-ttu-id="299f8-106">您可以在邏輯應用程式中使用 Twilio 帳戶之前，您必須授權 hello 邏輯應用程式 tooconnect tooyour Twilio 帳戶。</span><span class="sxs-lookup"><span data-stu-id="299f8-106">Before you can use your Twilio account in a Logic app, you must authorize hello Logic app tooconnect tooyour Twilio account.</span></span> <span data-ttu-id="299f8-107">幸運的是，您可以輕鬆地在 hello Azure 入口網站上的應用程式邏輯中。</span><span class="sxs-lookup"><span data-stu-id="299f8-107">Fortunately, you can do this easily from within your Logic app on hello Azure Portal.</span></span> 

<span data-ttu-id="299f8-108">以下是您的邏輯應用程式 tooconnect tooyour Twilio 帳戶 hello 步驟 tooauthorize:</span><span class="sxs-lookup"><span data-stu-id="299f8-108">Here are hello steps tooauthorize your Logic app tooconnect tooyour Twilio account:</span></span>

1. <span data-ttu-id="299f8-109">toocreate 連接 tooTwilio，在 hello 邏輯應用程式設計師中，選取**顯示 Microsoft managed Api** hello 在下拉式清單，然後輸入*Twilio* hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="299f8-109">toocreate a connection tooTwilio, in hello Logic app designer, select **Show Microsoft managed APIs** in hello drop down list then enter *Twilio* in hello search box.</span></span> <span data-ttu-id="299f8-110">選取 hello 觸發程序或您一定會喜歡 toouse 的動作：</span><span class="sxs-lookup"><span data-stu-id="299f8-110">Select hello trigger or action you'll like toouse:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. <span data-ttu-id="299f8-111">如果您尚未建立任何連線 tooTwilio 之前，您會取得提示的 tooprovide Twilio 認證。</span><span class="sxs-lookup"><span data-stu-id="299f8-111">If you haven't created any connections tooTwilio before, you'll get prompted tooprovide your Twilio credentials.</span></span> <span data-ttu-id="299f8-112">這些認證會使用的 tooauthorize，您的邏輯應用程式 tooconnect 並存取您的 Twilio 帳戶資料：</span><span class="sxs-lookup"><span data-stu-id="299f8-112">These credentials will be used tooauthorize your Logic app tooconnect to, and access your Twilio account's data:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. <span data-ttu-id="299f8-113">您將需要 hello **Twilio 帳戶識別碼**和**Twilio 存取權杖**hello 儀表板中 Twilio 因此登入 tooyour Twilio 帳戶現在 toograb 這兩個資訊片段：</span><span class="sxs-lookup"><span data-stu-id="299f8-113">You'll need hello **Twilio account id** and **Twilio access token**  from hello dashboard in Twilio, so log in tooyour Twilio account now toograb these two pieces of information:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. <span data-ttu-id="299f8-114">Twilio 和邏輯的應用程式使用不同的名稱 tooidentify 這兩個資訊片段。</span><span class="sxs-lookup"><span data-stu-id="299f8-114">Twilio and Logic apps use different names tooidentify these two pieces of infomation.</span></span> <span data-ttu-id="299f8-115">以下是如何您必須將其對應 toohello 邏輯應用程式 對話方塊：![](./media/connectors-create-api-twilio/twilio-3.png)</span><span class="sxs-lookup"><span data-stu-id="299f8-115">Here is how you must map them toohello Logic apps dialog: ![](./media/connectors-create-api-twilio/twilio-3.png)</span></span>  
5. <span data-ttu-id="299f8-116">選取 hello**建立連線**按鈕：</span><span class="sxs-lookup"><span data-stu-id="299f8-116">Select hello **Create connection** button:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. <span data-ttu-id="299f8-117">請注意，已經建立 hello 連接，而且現在可用以 hello 其他 tooproceed 邏輯應用程式中的步驟：</span><span class="sxs-lookup"><span data-stu-id="299f8-117">Notice hello connection has been created and you are now free tooproceed with hello other steps in your Logic app:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

