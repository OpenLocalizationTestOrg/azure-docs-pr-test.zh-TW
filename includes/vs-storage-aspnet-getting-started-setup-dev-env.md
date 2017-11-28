## <a name="set-up-the-development-environment"></a><span data-ttu-id="fe4af-101">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="fe4af-101">Set up the development environment</span></span>

<span data-ttu-id="fe4af-102">本節將引導您設定開發環境，包括建立 ASP.NET MVC 應用程式、新增已連接的服務連線、新增控制器，以及指定必要的命名空間指示詞。</span><span class="sxs-lookup"><span data-stu-id="fe4af-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying the required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="fe4af-103">建立 ASP.NET MVC 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="fe4af-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="fe4af-104">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="fe4af-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="fe4af-105">從主功能表選取 [檔案] -> [新增] -> [專案]</span><span class="sxs-lookup"><span data-stu-id="fe4af-105">Select **File->New->Project** from the main menu</span></span>

1. <span data-ttu-id="fe4af-106">在 [新增專案] 對話方塊上，指定下圖中醒目提示的選項︰</span><span class="sxs-lookup"><span data-stu-id="fe4af-106">On the **New Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![建立 ASP.NET 專案](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="fe4af-108">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fe4af-108">Select **OK**.</span></span>

1. <span data-ttu-id="fe4af-109">在 [新增 ASP.NET 專案] 對話方塊上，指定下圖中醒目提示的選項︰</span><span class="sxs-lookup"><span data-stu-id="fe4af-109">On the **New ASP.NET Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![指定 MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="fe4af-111">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fe4af-111">Select **OK**.</span></span>

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a><span data-ttu-id="fe4af-112">使用已連接的服務連接到 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fe4af-112">Use Connected Services to connect to an Azure storage account</span></span>

1. <span data-ttu-id="fe4af-113">在 [方案總管] 中，用滑鼠右鍵按一下專案，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="fe4af-113">In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="fe4af-114">在 [新增已連接的服務] 對話方塊上，選取 [Azure 儲存體]，然後選取 [設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe4af-114">On the **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![已連接的服務對話方塊](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="fe4af-116">在 [Azure 儲存體] 對話方塊上，選取您想要使用的所需 Azure 儲存體帳戶，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fe4af-116">On the **Azure Storage** dialog, select the desired Azure storage account with which you want to work, and select **Add**.</span></span>
