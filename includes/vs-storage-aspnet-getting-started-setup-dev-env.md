## <a name="set-up-hello-development-environment"></a><span data-ttu-id="82163-101">設定 hello 開發環境</span><span class="sxs-lookup"><span data-stu-id="82163-101">Set up hello development environment</span></span>

<span data-ttu-id="82163-102">本節將引導您設定您的開發環境，包括建立 ASP.NET MVC 應用程式中，加入已連接服務連接，加入控制器，並指定 hello 所需的命名空間指示詞。</span><span class="sxs-lookup"><span data-stu-id="82163-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="82163-103">建立 ASP.NET MVC 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="82163-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="82163-104">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="82163-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="82163-105">選取**檔案]-> [新增專案]-> [**從 hello 主功能表</span><span class="sxs-lookup"><span data-stu-id="82163-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="82163-106">在 hello**新專案** 對話方塊中，指定下列圖中反白顯示 hello hello 選項：</span><span class="sxs-lookup"><span data-stu-id="82163-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![建立 ASP.NET 專案](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="82163-108">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="82163-108">Select **OK**.</span></span>

1. <span data-ttu-id="82163-109">在 hello**新增 ASP.NET 專案** 對話方塊中，指定下列圖中反白顯示 hello hello 選項：</span><span class="sxs-lookup"><span data-stu-id="82163-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![指定 MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="82163-111">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="82163-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="82163-112">使用已連接服務 tooconnect tooan Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="82163-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="82163-113">在 [hello**方案總管] 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**加入已連接服務]-> [**。</span><span class="sxs-lookup"><span data-stu-id="82163-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="82163-114">在 hello**加入已連接服務**對話方塊中，選取**Azure 儲存體**，然後選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="82163-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![已連接的服務對話方塊](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="82163-116">在 hello **Azure 儲存體**對話方塊中，選取 hello 所需的 Azure 儲存體帳戶與您想 toowork，並選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="82163-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
