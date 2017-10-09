<span data-ttu-id="f4d6d-101">如果以下條件成立 ，Azure 將會確定您的應用程式使用 Python：</span><span class="sxs-lookup"><span data-stu-id="f4d6d-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="f4d6d-102">requirements.txt hello 根資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="f4d6d-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="f4d6d-103">hello 根資料夾中的任何.py 檔案或指定 python 的 runtime.txt</span><span class="sxs-lookup"><span data-stu-id="f4d6d-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="f4d6d-104">Hello 案例時，它會使用執行 hello 的檔案，以及其他的 Python 作業，例如標準同步處理的 Python 特定部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="f4d6d-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="f4d6d-105">自動管理虛擬環境</span><span class="sxs-lookup"><span data-stu-id="f4d6d-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="f4d6d-106">使用 PIP 安裝列在 requirements.txt 中的封裝</span><span class="sxs-lookup"><span data-stu-id="f4d6d-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="f4d6d-107">建立根據 hello hello 適當 web.config 選取 Python 版本。</span><span class="sxs-lookup"><span data-stu-id="f4d6d-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="f4d6d-108">收集適用於 Django 應用程式的靜態檔案</span><span class="sxs-lookup"><span data-stu-id="f4d6d-108">Collect static files for Django applications</span></span>

<span data-ttu-id="f4d6d-109">您可以控制 hello 預設的部署步驟的某些層面，而不需要 toocustomize hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4d6d-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="f4d6d-110">如果您想 tooskip Python 特定部署的所有步驟，您可以建立此空白檔案：</span><span class="sxs-lookup"><span data-stu-id="f4d6d-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="f4d6d-111">如需更多控制部署的詳細資訊，您都可以建立下列檔案的 hello 來覆寫 hello 預設部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="f4d6d-111">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="f4d6d-112">您可以使用 hello [Azure 命令列介面][ Azure command-line interface] toocreate hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="f4d6d-112">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="f4d6d-113">從您的專案資料夾中使用此命令：</span><span class="sxs-lookup"><span data-stu-id="f4d6d-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="f4d6d-114">當這些檔案不存在時，Azure 會建立一個暫存的部署指令碼，並執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4d6d-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="f4d6d-115">您使用上述的 hello 命令建立的相同 toohello 它。</span><span class="sxs-lookup"><span data-stu-id="f4d6d-115">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
