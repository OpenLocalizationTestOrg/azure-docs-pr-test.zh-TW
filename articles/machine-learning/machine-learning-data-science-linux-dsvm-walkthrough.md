---
title: "hello Linux Data Science 虛擬機器上的 aaaData 科學 |Microsoft 文件"
description: "影響 tooperform 幾個常見的資料科學工作以 hello Linux 資料科學 VM。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="9e572-103">在 hello Linux Data Science 虛擬機器上的資料科學</span><span class="sxs-lookup"><span data-stu-id="9e572-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="9e572-104">本逐步解說會示範如何 tooperform 幾個常見的資料科學工作以 hello Linux 資料科學 VM。</span><span class="sxs-lookup"><span data-stu-id="9e572-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="9e572-105">hello Linux 資料科學虛擬機器 (DSVM) 是預先安裝工具常用於資料分析和機器學習的集合，在 Azure 上的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="9e572-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="9e572-106">hello 索引鍵的軟體元件會分在 hello [Linux Data Science 虛擬機器的佈建 hello](machine-learning-data-science-linux-dsvm-intro.md)主題。</span><span class="sxs-lookup"><span data-stu-id="9e572-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="9e572-107">hello VM 映像可讓您輕鬆 tooget 開始執行以分鐘為單位的資料科學，而不需要 tooinstall 並個別設定每個 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="9e572-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="9e572-108">您可以輕鬆地向上延展 hello VM，如有需要和它在不使用時停止。</span><span class="sxs-lookup"><span data-stu-id="9e572-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="9e572-109">因此，這項資源既有彈性，又符合成本效益。</span><span class="sxs-lookup"><span data-stu-id="9e572-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="9e572-110">hello 本逐步解說中所示範的資料科學工作步驟 hello 述 hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)。</span><span class="sxs-lookup"><span data-stu-id="9e572-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="9e572-111">這個程序提供系統化的方法 toodata 科學中，可讓資料科學家 tooeffectively 共同作業在 hello 生命週期的建置智慧型應用程式的小組。</span><span class="sxs-lookup"><span data-stu-id="9e572-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="9e572-112">hello 資料科學程序也提供可供遵循個人資料科學反覆的架構。</span><span class="sxs-lookup"><span data-stu-id="9e572-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="9e572-113">我們分析 hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase)本逐步解說中的資料集。</span><span class="sxs-lookup"><span data-stu-id="9e572-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="9e572-114">這是一組電子郵件標示為垃圾郵件或 ham （亦即它們不垃圾郵件），而且也包含 hello 內容 hello 電子郵件的一些統計資料。</span><span class="sxs-lookup"><span data-stu-id="9e572-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="9e572-115">包含的 hello 統計資料中會討論 hello 接下來但有一個區段。</span><span class="sxs-lookup"><span data-stu-id="9e572-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e572-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e572-116">Prerequisites</span></span>
<span data-ttu-id="9e572-117">您可以使用 Linux Data Science 虛擬機器之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9e572-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="9e572-118">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="9e572-118">An **Azure subscription**.</span></span> <span data-ttu-id="9e572-119">如果您還沒有訂用帳戶，請參閱 [立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="9e572-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9e572-120">[**Linux 資料科學 VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm)。</span><span class="sxs-lookup"><span data-stu-id="9e572-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="9e572-121">如需此 VM 佈建資訊，請參閱[Linux Data Science 虛擬機器的佈建 hello](machine-learning-data-science-linux-dsvm-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="9e572-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="9e572-122">[X2Go](http://wiki.x2go.org/doku.php) 已安裝在電腦上並已開啟 XFCE 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9e572-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="9e572-123">如需安裝和設定 **X2Go 用戶端**的相關資訊，請參閱[安裝和設定 X2Go 用戶端](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client)。</span><span class="sxs-lookup"><span data-stu-id="9e572-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="9e572-124">**AzureML 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="9e572-124">An **AzureML account**.</span></span> <span data-ttu-id="9e572-125">如果您還沒有一個申請新一 hello [AzureML 首頁](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9e572-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="9e572-126">沒有可用的使用量層 toohelp 您立即開始。</span><span class="sxs-lookup"><span data-stu-id="9e572-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="9e572-127">下載 hello spambase 資料集</span><span class="sxs-lookup"><span data-stu-id="9e572-127">Download hello spambase dataset</span></span>
<span data-ttu-id="9e572-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase)資料集是一組較小包含只 4601 範例的資料。</span><span class="sxs-lookup"><span data-stu-id="9e572-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="9e572-129">這是 hello 的方便大小 toouse 示範的某些 hello 的主要功能，因為它資料科學 VM 保留 hello 資源需求適度時。</span><span class="sxs-lookup"><span data-stu-id="9e572-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="9e572-130">本逐步解說建立在 D2 v2 大小的 Linux 資料科學虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="9e572-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="9e572-131">此大小 DSVM 是能夠處理這個逐步解說中的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="9e572-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="9e572-132">如果您需要更多儲存空間，您可以建立額外的磁碟，並將它們附加 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="9e572-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="9e572-133">這些磁碟使用永續性的 Azure 儲存體，因此其資料時，會保留甚至 hello 伺服器重新佈建到期 tooresizing 或已關閉。</span><span class="sxs-lookup"><span data-stu-id="9e572-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="9e572-134">tooadd 磁碟並將它附加 tooyour VM，請依照中的 hello 指示[新增磁碟 tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9e572-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e572-135">這些步驟使用 hello 的 hello DSVM 上已安裝的 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="9e572-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="9e572-136">因此可以完全從 hello VM 本身完成這些程序。</span><span class="sxs-lookup"><span data-stu-id="9e572-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="9e572-137">另一個選項 tooincrease 儲存體是 toouse [Azure 檔案](../storage/files/storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="9e572-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="9e572-138">toodownload hello 資料中，開啟終端機視窗，然後執行此命令：</span><span class="sxs-lookup"><span data-stu-id="9e572-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="9e572-139">hello 下載的檔案沒有標頭資料列，因此讓我們來建立另一個檔案沒有標頭。</span><span class="sxs-lookup"><span data-stu-id="9e572-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="9e572-140">Hello 適當的標頭以執行此命令 toocreate 檔案：</span><span class="sxs-lookup"><span data-stu-id="9e572-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="9e572-141">再進行串連 hello 以及 hello 命令的兩個檔案：</span><span class="sxs-lookup"><span data-stu-id="9e572-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="9e572-142">hello 資料集上每個電子郵件，有幾種類型的統計資料：</span><span class="sxs-lookup"><span data-stu-id="9e572-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="9e572-143">資料行要***word\_頻率\_WORD***表示比對的文字在 hello 電子郵件中的 hello 百分比*WORD*。</span><span class="sxs-lookup"><span data-stu-id="9e572-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="9e572-144">例如，如果*word\_頻率\_進行*是 1，則在 hello 電子郵件中的所有文字的 1%已*進行*。</span><span class="sxs-lookup"><span data-stu-id="9e572-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="9e572-145">資料行要***char\_頻率\_CHAR***指出 hello 電子郵件中的所有字元所 hello 百分比*CHAR*。</span><span class="sxs-lookup"><span data-stu-id="9e572-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="9e572-146">***資本\_執行\_長度\_最長***hello 大寫的字母順序的最長的長度。</span><span class="sxs-lookup"><span data-stu-id="9e572-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="9e572-147">***資本\_執行\_長度\_平均***是 hello 大寫的字母的所有序列的平均時間長度。</span><span class="sxs-lookup"><span data-stu-id="9e572-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="9e572-148">***資本\_執行\_長度\_總***是大寫的字母的所有序列 hello 總長度。</span><span class="sxs-lookup"><span data-stu-id="9e572-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="9e572-149">***垃圾郵件***表示 hello 電子郵件是否被視為垃圾郵件 (1 = 垃圾郵件，0 = 不垃圾郵件)。</span><span class="sxs-lookup"><span data-stu-id="9e572-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="9e572-150">瀏覽 Microsoft R open hello 資料集</span><span class="sxs-lookup"><span data-stu-id="9e572-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="9e572-151">讓我們來檢查 hello 資料並執行以 r hello 資料科學 VM 隨附一些基本的機器學習[Microsoft R Open](https://mran.revolutionanalytics.com/open/)預先安裝。</span><span class="sxs-lookup"><span data-stu-id="9e572-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="9e572-152">hello 多執行緒的數學程式庫在這個版本的 R 提供較佳的效能比單一執行緒的各種版本。</span><span class="sxs-lookup"><span data-stu-id="9e572-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="9e572-153">Microsoft R Open 也提供重現使用 hello CRAN 封裝儲存機制的快照集。</span><span class="sxs-lookup"><span data-stu-id="9e572-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="9e572-154">tooget 副本 hello 程式碼範例使用在這個逐步解說中，複製 hello **Azure-Machine-學習的資料-科學**使用 git，也就預先安裝 hello VM 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9e572-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="9e572-155">從 hello git 命令列執行：</span><span class="sxs-lookup"><span data-stu-id="9e572-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="9e572-156">開啟 終端機視窗，並與 hello R 互動式主控台啟動新的 R 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9e572-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="9e572-157">您也可以使用 RStudio hello 下列程序。</span><span class="sxs-lookup"><span data-stu-id="9e572-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="9e572-158">tooinstall RStudio、 執行此命令在終端機：`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="9e572-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="9e572-159">tooimport hello 資料和設定 hello 環境中，執行：</span><span class="sxs-lookup"><span data-stu-id="9e572-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="9e572-160">toosee 每個資料行的相關摘要統計資料：</span><span class="sxs-lookup"><span data-stu-id="9e572-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="9e572-161">針對不同的 hello 資料檢視：</span><span class="sxs-lookup"><span data-stu-id="9e572-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="9e572-162">這會顯示 hello 每個變數的型別，並先 hello hello 資料集中的幾個值。</span><span class="sxs-lookup"><span data-stu-id="9e572-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="9e572-163">hello*垃圾郵件*讀取資料行做為整數，但實際上類別變數 （或係數）。</span><span class="sxs-lookup"><span data-stu-id="9e572-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="9e572-164">tooset 其型別：</span><span class="sxs-lookup"><span data-stu-id="9e572-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="9e572-165">toodo 一些探勘分析，使用 hello [ggplot2](http://ggplot2.org/)封裝，hello VM 上已安裝的的熱門圖形文件庫。</span><span class="sxs-lookup"><span data-stu-id="9e572-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="9e572-166">請注意，從 hello 摘要資料顯示更早版本，我們 hello 頻率 hello 驚嘆號字元有摘要統計資料。</span><span class="sxs-lookup"><span data-stu-id="9e572-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="9e572-167">讓我們以下列命令的 hello 繪製這些的頻率：</span><span class="sxs-lookup"><span data-stu-id="9e572-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="9e572-168">因為 hello 零列會扭曲 hello 繪圖，讓我們來刪除它：</span><span class="sxs-lookup"><span data-stu-id="9e572-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="9e572-169">在 1 上面有看起來很有意思的不尋常密度。</span><span class="sxs-lookup"><span data-stu-id="9e572-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="9e572-170">讓我們只看該資料︰</span><span class="sxs-lookup"><span data-stu-id="9e572-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="9e572-171">然後按照垃圾郵件和非垃圾郵件進行分割：</span><span class="sxs-lookup"><span data-stu-id="9e572-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="9e572-172">這些範例應可讓您的 hello toomake 類似繪圖其他資料行 tooexplore hello 它們所包含的資料。</span><span class="sxs-lookup"><span data-stu-id="9e572-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="9e572-173">訓練和測試 ML 模型</span><span class="sxs-lookup"><span data-stu-id="9e572-173">Train and test an ML model</span></span>
<span data-ttu-id="9e572-174">現在讓我們來定型數個機器學習模型 hello 集中 tooclassify hello 電子郵件做為包含跨越或 ham。</span><span class="sxs-lookup"><span data-stu-id="9e572-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="9e572-175">在本節中，我們會訓練決策樹模型和隨機樹系模型，然後測試其預測的精確度。</span><span class="sxs-lookup"><span data-stu-id="9e572-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="9e572-176">hello 資料科學 VM 上已安裝在 hello 下列程式碼中使用的 hello rpart （遞迴資料分割和迴歸樹） 封裝。</span><span class="sxs-lookup"><span data-stu-id="9e572-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="9e572-177">首先，我們將 hello 資料集分割成定型和測試集：</span><span class="sxs-lookup"><span data-stu-id="9e572-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="9e572-178">然後再建立決策樹 tooclassify hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9e572-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="9e572-179">以下是 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="9e572-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="9e572-181">toodetermine 以及它對 hello 訓練設定，請使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e572-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="9e572-182">它對 hello 測試集的 toodetermine 程度：</span><span class="sxs-lookup"><span data-stu-id="9e572-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="9e572-183">讓我們同時嘗試隨機樹系模型。</span><span class="sxs-lookup"><span data-stu-id="9e572-183">Let's also try a random forest model.</span></span> <span data-ttu-id="9e572-184">隨機樹系訓練的決策樹，並輸出是從所有 hello 個別的決策樹的 hello 分類 hello 模式的類別。</span><span class="sxs-lookup"><span data-stu-id="9e572-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="9e572-185">它們提供的功能更強大的機器學習方法，如它們更正 hello 普遍的傾向的決策樹模型 toooverfit 定型資料集。</span><span class="sxs-lookup"><span data-stu-id="9e572-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="9e572-186">部署模型 tooAzure ML</span><span class="sxs-lookup"><span data-stu-id="9e572-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="9e572-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) 是一種雲端服務，可讓您輕鬆 toobuild 及部署模型的預測分析。</span><span class="sxs-lookup"><span data-stu-id="9e572-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="9e572-188">AzureML hello nice 功能之一是其任何 R 函式做為 web 服務的能力 toopublish。</span><span class="sxs-lookup"><span data-stu-id="9e572-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="9e572-189">hello AzureML R 封裝會在建立部署簡單 toodo 直接從我們的 R 工作階段 hello DSVM。</span><span class="sxs-lookup"><span data-stu-id="9e572-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="9e572-190">toodeploy hello 決策樹狀結構的程式碼 hello 前一節，您需要 toosign tooAzure Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="9e572-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="9e572-191">您需要工作區識別碼和授權權杖 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="9e572-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="9e572-192">toofind 這些值和它們的初始化 hello AzureML 變數：</span><span class="sxs-lookup"><span data-stu-id="9e572-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="9e572-193">選取**設定**hello 左側功能表上。</span><span class="sxs-lookup"><span data-stu-id="9e572-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="9e572-194">記下您的**工作區識別碼**。</span><span class="sxs-lookup"><span data-stu-id="9e572-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="9e572-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="9e572-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="9e572-196">選取**授權權杖**從 hello 負擔功能表和附註您**主要授權權杖**。![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="9e572-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="9e572-197">負載 hello **AzureML**封裝，然後在 hello DSVM 上的 R 工作階段中將以您的語彙基元和工作區識別碼 hello 變數的值：</span><span class="sxs-lookup"><span data-stu-id="9e572-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="9e572-198">讓我們來簡化此示範更容易 tooimplement hello 模型 toomake。</span><span class="sxs-lookup"><span data-stu-id="9e572-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="9e572-199">挑選 hello hello 決策樹狀結構最接近 toohello 根目錄中的三個變數，並建置使用只是那些三個變數的新樹狀結構：</span><span class="sxs-lookup"><span data-stu-id="9e572-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="9e572-200">我們需要使用 hello 功能做為輸入的預測函式，並傳回 hello 預測的值：</span><span class="sxs-lookup"><span data-stu-id="9e572-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="9e572-201">發行使用 hello hello predictSpam 函式 tooAzureML **publishWebService**函式：</span><span class="sxs-lookup"><span data-stu-id="9e572-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="9e572-202">此函數會採用 hello **predictSpam**函式中，會建立名為 web 服務**spamWebService**與定義輸入和輸出，並傳回 hello 新端點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9e572-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="9e572-203">檢視詳細資料的 hello 發佈 web 服務，包括其應用程式開發介面端點和存取金鑰與 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="9e572-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="9e572-204">tootry 它在 hello hello 測試集中的前 10 個資料列：</span><span class="sxs-lookup"><span data-stu-id="9e572-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="9e572-205">使用其他可用工具</span><span class="sxs-lookup"><span data-stu-id="9e572-205">Use other tools available</span></span>
<span data-ttu-id="9e572-206">hello 其餘各節說明如何 toouse 部分 hello 工具安裝在 hello Linux 資料科學 VM。以下是工具所討論的 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="9e572-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="9e572-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="9e572-207">XGBoost</span></span>
* <span data-ttu-id="9e572-208">Python</span><span class="sxs-lookup"><span data-stu-id="9e572-208">Python</span></span>
* <span data-ttu-id="9e572-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="9e572-209">Jupyterhub</span></span>
* <span data-ttu-id="9e572-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="9e572-210">Rattle</span></span>
* <span data-ttu-id="9e572-211">PostgreSQL 和 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="9e572-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="9e572-212">SQL Server 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9e572-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="9e572-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="9e572-213">XGBoost</span></span>
<span data-ttu-id="9e572-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) 工具可提供快速且正確的推進式決策樹實作。</span><span class="sxs-lookup"><span data-stu-id="9e572-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="9e572-215">XGBoost 也可以從 Python 或命令列進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="9e572-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="9e572-216">Python</span><span class="sxs-lookup"><span data-stu-id="9e572-216">Python</span></span>
<span data-ttu-id="9e572-217">程式開發中使用 Python，hello Anaconda Python 分佈 2.7 和 3.5 已安裝在 hello DSVM。</span><span class="sxs-lookup"><span data-stu-id="9e572-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="9e572-218">hello Anaconda 發佈包含[Condas](http://conda.pydata.org/docs/index.html)，也可以使用的 toocreate 有不同的版本及/或在其中安裝封裝的 python 是自訂的環境。</span><span class="sxs-lookup"><span data-stu-id="9e572-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="9e572-219">讓我們在某些 hello spambase 資料集的讀取和分類 hello 電子郵件中，搭配支援向量機器 scikit-了解：</span><span class="sxs-lookup"><span data-stu-id="9e572-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="9e572-220">toomake 預測：</span><span class="sxs-lookup"><span data-stu-id="9e572-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="9e572-221">tooshow 如何 toopublish AzureML 端點，讓我們來建立簡單的模型 hello 三個變數為我們所做的我們先前發行 hello R 模型。</span><span class="sxs-lookup"><span data-stu-id="9e572-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="9e572-222">toopublish hello 模型 tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="9e572-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="9e572-223">此操作只適用於 Python 2.7，3.5 版則尚未支援。</span><span class="sxs-lookup"><span data-stu-id="9e572-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="9e572-224">請使用 **/anaconda/bin/python2.7**來執行。</span><span class="sxs-lookup"><span data-stu-id="9e572-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="9e572-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="9e572-225">Jupyterhub</span></span>
<span data-ttu-id="9e572-226">在 hello hello Anaconda 發佈 DSVM 隨附 Jupyter 筆記本、 跨平台環境 tooshare Python、 R 或 Julia 的程式碼和分析。</span><span class="sxs-lookup"><span data-stu-id="9e572-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="9e572-227">hello Jupyter 筆記本是透過 JupyterHub 存取。</span><span class="sxs-lookup"><span data-stu-id="9e572-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="9e572-228">您可以在 ***https://\<VM DNS 名稱或 IP 位址\>:8000/*** 使用本機 Linux 使用者名稱和密碼來登入。</span><span class="sxs-lookup"><span data-stu-id="9e572-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="9e572-229">JupyterHub 的所有組態檔可在 **eg /etc/ jupyterhub**目錄中找到。</span><span class="sxs-lookup"><span data-stu-id="9e572-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="9e572-230">Hello VM 上已安裝數個範例筆記本：</span><span class="sxs-lookup"><span data-stu-id="9e572-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="9e572-231">請參閱 hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb)範例 Python 筆記本。</span><span class="sxs-lookup"><span data-stu-id="9e572-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="9e572-232">如需 [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) 的 Notebook 範例，請參閱 **IntroTutorialinR** 。</span><span class="sxs-lookup"><span data-stu-id="9e572-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="9e572-233">請參閱 hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb)如需其他範例**Python**筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="9e572-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="9e572-234">hello Julia 語言也會提供 hello hello Linux 資料科學 VM 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="9e572-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="9e572-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="9e572-235">Rattle</span></span>
<span data-ttu-id="9e572-236">[祕](https://cran.r-project.org/web/packages/rattle/index.html)(輕鬆 hello R 分析工具 tooLearn) 是用於資料採礦圖形的 R 工具。</span><span class="sxs-lookup"><span data-stu-id="9e572-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="9e572-237">它有直覺式的介面，可讓您輕鬆 tooload、 探索和轉換資料和建立及評估模型。</span><span class="sxs-lookup"><span data-stu-id="9e572-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="9e572-238">hello 文章[祕： R 的資料採礦 GUI](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf)提供逐步解說，示範它的功能。</span><span class="sxs-lookup"><span data-stu-id="9e572-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="9e572-239">安裝並啟動祕以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="9e572-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="9e572-240">Hello DSVM 上不需要安裝。</span><span class="sxs-lookup"><span data-stu-id="9e572-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="9e572-241">但祕可能會提示您 tooinstall 其他封裝在載入時。</span><span class="sxs-lookup"><span data-stu-id="9e572-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="9e572-242">Rattle 使用索引標籤式介面。</span><span class="sxs-lookup"><span data-stu-id="9e572-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="9e572-243">大部分的 hello 索引標籤對應中 hello toosteps[資料科學程序](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)： 如載入資料，或瀏覽它。</span><span class="sxs-lookup"><span data-stu-id="9e572-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="9e572-244">從透過 hello 索引標籤的左 tooright 傳送 hello 資料科學程序。</span><span class="sxs-lookup"><span data-stu-id="9e572-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="9e572-245">但 hello 最後一個索引標籤包含執行祕 hello R 命令的記錄。</span><span class="sxs-lookup"><span data-stu-id="9e572-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="9e572-246">tooload 及設定 hello 資料集：</span><span class="sxs-lookup"><span data-stu-id="9e572-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="9e572-247">tooload hello 檔案、 選取 hello**資料**索引標籤，然後</span><span class="sxs-lookup"><span data-stu-id="9e572-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="9e572-248">選擇 hello 選取器接下來太**Filename**選擇**spambaseHeaders.data**。</span><span class="sxs-lookup"><span data-stu-id="9e572-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="9e572-249">tooload hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e572-249">tooload hello file.</span></span> <span data-ttu-id="9e572-250">選取**Execute** hello 頂端列的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e572-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="9e572-251">您應該會看到每個資料行，包括其識別的資料類型，其是否為輸入，為目標，或其他類型的變數及 hello 唯一值數目的摘要。</span><span class="sxs-lookup"><span data-stu-id="9e572-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="9e572-252">祕正確地識別 hello**垃圾郵件**hello 目標資料行。</span><span class="sxs-lookup"><span data-stu-id="9e572-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="9e572-253">選取 hello 垃圾郵件 欄中，然後設定 hello**目標資料型別**太**Categoric**。</span><span class="sxs-lookup"><span data-stu-id="9e572-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="9e572-254">tooexplore hello 資料：</span><span class="sxs-lookup"><span data-stu-id="9e572-254">tooexplore hello data:</span></span>

* <span data-ttu-id="9e572-255">選取 hello**瀏覽** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9e572-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="9e572-256">按一下**摘要**，然後**Execute**，toosee 某些 hello 變數型別資訊和一些摘要統計資料。</span><span class="sxs-lookup"><span data-stu-id="9e572-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="9e572-257">tooview 其他類型的每個變數的相關統計資料選取其他選項，例如**描述**或**基本概念**。</span><span class="sxs-lookup"><span data-stu-id="9e572-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="9e572-258">hello**瀏覽** 索引標籤也可讓您有許多繪製的 toogenerate。</span><span class="sxs-lookup"><span data-stu-id="9e572-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="9e572-259">tooplot 長條圖的 hello 資料：</span><span class="sxs-lookup"><span data-stu-id="9e572-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="9e572-260">選取 [分佈] 。</span><span class="sxs-lookup"><span data-stu-id="9e572-260">Select **Distributions**.</span></span>
* <span data-ttu-id="9e572-261">為 **word_freq_remove** 和 **word_freq_you** 勾選 [長條圖]。</span><span class="sxs-lookup"><span data-stu-id="9e572-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="9e572-262">選取 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="9e572-262">Select **Execute**.</span></span> <span data-ttu-id="9e572-263">您應該會看到這兩個密度繪製在單一圖表視窗中，會清除這個 hello 文字的 「 您 」 更經常出現在電子郵件比 「 移除 」。</span><span class="sxs-lookup"><span data-stu-id="9e572-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="9e572-264">hello 相互關聯的繪圖也是有趣的。</span><span class="sxs-lookup"><span data-stu-id="9e572-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="9e572-265">其中一個 toocreate:</span><span class="sxs-lookup"><span data-stu-id="9e572-265">toocreate one:</span></span>

* <span data-ttu-id="9e572-266">選擇**相互關聯**為 hello**類型**，然後</span><span class="sxs-lookup"><span data-stu-id="9e572-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="9e572-267">選取 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="9e572-267">Select **Execute**.</span></span>
* <span data-ttu-id="9e572-268">Rattle 會警告您，它建議的上限為 40 個變數。</span><span class="sxs-lookup"><span data-stu-id="9e572-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="9e572-269">選取**是**tooview hello 繪圖。</span><span class="sxs-lookup"><span data-stu-id="9e572-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="9e572-270">有一些有趣的相互關聯的: 「 技術 」 強大關聯太"HP 」 和 「 實驗室 」，例如。</span><span class="sxs-lookup"><span data-stu-id="9e572-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="9e572-271">此外，強烈相互關聯太"650"，因為 hello 區域的程式碼的 hello 資料集的捐血人 650。</span><span class="sxs-lookup"><span data-stu-id="9e572-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="9e572-272">hello 瀏覽視窗中可用 hello hello 字與字之間的關聯性的數字值。</span><span class="sxs-lookup"><span data-stu-id="9e572-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="9e572-273">很有趣 toonote，例如，「 技術 」 與 「 貴用戶 」 負面相互關聯和"money"。</span><span class="sxs-lookup"><span data-stu-id="9e572-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="9e572-274">祕可以轉換 hello 資料集 toohandle 一些常見的問題。</span><span class="sxs-lookup"><span data-stu-id="9e572-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="9e572-275">比方說，它可讓您 toorescale 功能、 推算遺漏值、 處理極端值，並移除變數或資料遺失的觀察值。</span><span class="sxs-lookup"><span data-stu-id="9e572-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="9e572-276">Rattle 也可以識別觀察值和 (或) 變數之間的關聯規則。</span><span class="sxs-lookup"><span data-stu-id="9e572-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="9e572-277">這些索引標籤不在此入門逐步解說的討論範圍內。</span><span class="sxs-lookup"><span data-stu-id="9e572-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="9e572-278">Rattle 也可以執行叢集分析。</span><span class="sxs-lookup"><span data-stu-id="9e572-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="9e572-279">讓我們來排除某些功能 toomake hello 輸出更容易 tooread。</span><span class="sxs-lookup"><span data-stu-id="9e572-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="9e572-280">在 hello**資料**索引標籤上，選擇**忽略**下一步 tooeach 的 hello 變數，但這十個項目：</span><span class="sxs-lookup"><span data-stu-id="9e572-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="9e572-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="9e572-281">word_freq_hp</span></span>
* <span data-ttu-id="9e572-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="9e572-282">word_freq_technology</span></span>
* <span data-ttu-id="9e572-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="9e572-283">word_freq_george</span></span>
* <span data-ttu-id="9e572-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="9e572-284">word_freq_remove</span></span>
* <span data-ttu-id="9e572-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="9e572-285">word_freq_your</span></span>
* <span data-ttu-id="9e572-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="9e572-286">word_freq_dollar</span></span>
* <span data-ttu-id="9e572-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="9e572-287">word_freq_money</span></span>
* <span data-ttu-id="9e572-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="9e572-288">capital_run_length_longest</span></span>
* <span data-ttu-id="9e572-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="9e572-289">word_freq_business</span></span>
* <span data-ttu-id="9e572-290">spam</span><span class="sxs-lookup"><span data-stu-id="9e572-290">spam</span></span>

<span data-ttu-id="9e572-291">然後返回 toohello**叢集**索引標籤上，選擇**KMeans**，並設定 hello*群集數目*too4。</span><span class="sxs-lookup"><span data-stu-id="9e572-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="9e572-292">然後**執行**。</span><span class="sxs-lookup"><span data-stu-id="9e572-292">Then **Execute**.</span></span> <span data-ttu-id="9e572-293">hello 結果會顯示 hello [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="9e572-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="9e572-294">有一個叢集具有高頻率的「george」和「hp」，因此可能是合法的商業電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9e572-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="9e572-295">toobuild 簡單的決策樹的機器學習模型：</span><span class="sxs-lookup"><span data-stu-id="9e572-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="9e572-296">選取 hello**模型**索引標籤上，</span><span class="sxs-lookup"><span data-stu-id="9e572-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="9e572-297">選擇**樹狀**為 hello**類型**。</span><span class="sxs-lookup"><span data-stu-id="9e572-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="9e572-298">選取**Execute** toodisplay hello 樹狀目錄中的 hello 文字格式輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="9e572-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="9e572-299">選取 hello**繪製**按鈕 tooview 圖形化版本。</span><span class="sxs-lookup"><span data-stu-id="9e572-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="9e572-300">這看起來非常類似 toohello 樹狀目錄中我們取得之前使用*rpart*。</span><span class="sxs-lookup"><span data-stu-id="9e572-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="9e572-301">Hello nice 祕功能之一是其能力 toorun 數個機器學習方法，並快速地對其進行評估。</span><span class="sxs-lookup"><span data-stu-id="9e572-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="9e572-302">以下是 hello 程序：</span><span class="sxs-lookup"><span data-stu-id="9e572-302">Here is hello procedure:</span></span>

* <span data-ttu-id="9e572-303">選擇**所有**hello**類型**。</span><span class="sxs-lookup"><span data-stu-id="9e572-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="9e572-304">選取 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="9e572-304">Select **Execute**.</span></span>
* <span data-ttu-id="9e572-305">完成之後，您可以按一下任何單一**類型**、 like **SVM**，並檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="9e572-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="9e572-306">您也可以比較 hello 模型上設定使用 hello hello 驗證 hello 效能**評估** 索引標籤。例如，hello**錯誤矩陣**選取範圍會顯示 hello 混淆矩陣、 整體的錯誤和每個模型的平均的類別錯誤 hello 驗證組。</span><span class="sxs-lookup"><span data-stu-id="9e572-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="9e572-307">您也可以繪製 ROC 曲線、執行敏感度分析和進行其他類型的模型評估。</span><span class="sxs-lookup"><span data-stu-id="9e572-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="9e572-308">一旦您完成建立模型時，選取 hello**記錄**tooview hello R 程式碼在您的工作階段期間執行的祕索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="9e572-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="9e572-309">您可以選取 hello**匯出**按鈕 toosave 它。</span><span class="sxs-lookup"><span data-stu-id="9e572-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="9e572-310">最新版 Rattle 中有一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="9e572-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="9e572-311">toomodify hello 指令碼，或使用 toorepeat 您步驟之後，您必須插入 # 字元前面的 * 匯出此記錄檔 … * hello 文字 hello 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="9e572-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="9e572-312">PostgreSQL 和 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="9e572-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="9e572-313">hello DSVM 隨附 PostgreSQL 安裝。</span><span class="sxs-lookup"><span data-stu-id="9e572-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="9e572-314">PostgreSQL 是複雜的開放原始碼關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="9e572-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="9e572-315">此區段會顯示如何 tooload 我們 PostgreSQL 到垃圾資料集，然後進行查詢。</span><span class="sxs-lookup"><span data-stu-id="9e572-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="9e572-316">您可以載入 hello 資料之前，您必須從 hello localhost tooallow 密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="9e572-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="9e572-317">在命令提示字元中︰</span><span class="sxs-lookup"><span data-stu-id="9e572-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="9e572-318">Hello 底部 hello 設定檔會詳細說明 hello 允許連線的幾行：</span><span class="sxs-lookup"><span data-stu-id="9e572-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="9e572-319">變更而不是 ident，hello [IPv4 本機連線] 列 toouse md5，因此我們可以使用登入使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="9e572-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="9e572-320">然後重新啟動 hello postgres 服務：</span><span class="sxs-lookup"><span data-stu-id="9e572-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="9e572-321">PostgreSQL，作為 hello postgres 內建使用者，執行下列命令提示字元中的 hello interactive 終端機 toolaunch psql:</span><span class="sxs-lookup"><span data-stu-id="9e572-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="9e572-322">建立新的使用者帳戶，請使用如 hello 您目前的登入，Linux 帳戶 hello 相同的使用者名稱和指定的密碼：</span><span class="sxs-lookup"><span data-stu-id="9e572-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="9e572-323">然後您的使用者身分登入 toopsql:</span><span class="sxs-lookup"><span data-stu-id="9e572-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="9e572-324">和 hello 資料匯入至新的資料庫：</span><span class="sxs-lookup"><span data-stu-id="9e572-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="9e572-325">現在，讓我們來瀏覽 hello 資料並執行一些查詢使用**松鼠 SQL**，可讓您與 JDBC 驅動程式透過資料庫互動的圖形工具。</span><span class="sxs-lookup"><span data-stu-id="9e572-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="9e572-326">tooget 啟動中，從 hello 應用程式 功能表啟動松鼠 SQL。</span><span class="sxs-lookup"><span data-stu-id="9e572-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="9e572-327">tooset 向上 hello 驅動程式：</span><span class="sxs-lookup"><span data-stu-id="9e572-327">tooset up hello driver:</span></span>

* <span data-ttu-id="9e572-328">依序選取 [Windows] 和 [檢視驅動程式]。</span><span class="sxs-lookup"><span data-stu-id="9e572-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="9e572-329">以滑鼠右鍵按一下 [PostgreSQL]，然後選取 [修改驅動程式]。</span><span class="sxs-lookup"><span data-stu-id="9e572-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="9e572-330">依序選取 [額外類別路徑] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9e572-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="9e572-331">輸入***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** hello**檔案名稱**和</span><span class="sxs-lookup"><span data-stu-id="9e572-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="9e572-332">選取 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="9e572-332">Select **Open**.</span></span>
* <span data-ttu-id="9e572-333">選擇 [列出驅動程式]，接著在 [類別名稱] 中選取 [org.postgresql.Driver]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9e572-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="9e572-334">tooset hello 連接 toohello 本機伺服器上：</span><span class="sxs-lookup"><span data-stu-id="9e572-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="9e572-335">依序選取 [Windows] 和 [檢視別名]。</span><span class="sxs-lookup"><span data-stu-id="9e572-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="9e572-336">選擇 hello  **+** 按鈕 toomake 新的別名。</span><span class="sxs-lookup"><span data-stu-id="9e572-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="9e572-337">命名*垃圾郵件資料庫*，選擇**PostgreSQL**在 hello**驅動程式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="9e572-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="9e572-338">設定 hello URL 太*jdbc:postgresql://localhost/spam*。</span><span class="sxs-lookup"><span data-stu-id="9e572-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="9e572-339">輸入您的*使用者名稱*和*密碼*。</span><span class="sxs-lookup"><span data-stu-id="9e572-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="9e572-340">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9e572-340">Click **OK**.</span></span>
* <span data-ttu-id="9e572-341">tooopen hello**連接**視窗中，按兩下 hello***垃圾郵件資料庫***別名。</span><span class="sxs-lookup"><span data-stu-id="9e572-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="9e572-342">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="9e572-342">Select **Connect**.</span></span>

<span data-ttu-id="9e572-343">toorun 某些查詢：</span><span class="sxs-lookup"><span data-stu-id="9e572-343">toorun some queries:</span></span>

* <span data-ttu-id="9e572-344">選取 hello **SQL**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9e572-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="9e572-345">輸入一個簡單的查詢，例如`SELECT * from data;`hello 查詢在 hello hello SQL 索引標籤頂端 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="9e572-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="9e572-346">按**Ctrl-enter** toorun 它。</span><span class="sxs-lookup"><span data-stu-id="9e572-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="9e572-347">根據預設松鼠 SQL 傳回 hello 前 100 個資料列從您的查詢。</span><span class="sxs-lookup"><span data-stu-id="9e572-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="9e572-348">有許多您可以執行 tooexplore 這項資料的多個查詢。</span><span class="sxs-lookup"><span data-stu-id="9e572-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="9e572-349">例如，如何執行 hello hello word 的頻率*進行*垃圾郵件和火腿之間有差異？</span><span class="sxs-lookup"><span data-stu-id="9e572-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="9e572-350">什麼是經常包含的 hello 特性的電子郵件或者*3d*嗎？</span><span class="sxs-lookup"><span data-stu-id="9e572-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="9e572-351">大部分的電子郵件，具有高次數*3d*會很明顯在極垃圾郵件，因此可能很實用的功能，來建立預測模型 tooclassify hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9e572-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="9e572-352">如果您想 tooperform 機器學習 PostgreSQL 資料庫中所儲存的資料，請考慮使用[MADlib](http://madlib.incubator.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="9e572-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="9e572-353">SQL Server 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9e572-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="9e572-354">Azure SQL 資料倉儲是一種雲端架構、相應放大的資料庫，可處理大量的關聯式與非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="9e572-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="9e572-355">如需詳細資訊，請參閱 [什麼是 Azure SQL 資料倉儲？](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="9e572-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="9e572-356">tooconnect toohello 資料倉儲，並建立 hello 資料表，請從命令提示字元的 hello 執行的下列命令：</span><span class="sxs-lookup"><span data-stu-id="9e572-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="9e572-357">然後在 hello sqlcmd 提示字元：</span><span class="sxs-lookup"><span data-stu-id="9e572-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="9e572-358">使用 bcp 複製資料︰</span><span class="sxs-lookup"><span data-stu-id="9e572-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="9e572-359">hello hello 下載的檔案中的行尾結束符號視窗樣式，但 bcp 需要 UNIX 樣式，因此我們需要 tootell bcp，使用 hello-r 旗標。</span><span class="sxs-lookup"><span data-stu-id="9e572-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="9e572-360">並使用 sqlcmd 進行查詢︰</span><span class="sxs-lookup"><span data-stu-id="9e572-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="9e572-361">您也可以使用 Squirrel SQL 進行查詢。</span><span class="sxs-lookup"><span data-stu-id="9e572-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="9e572-362">遵循 PostgreSQL，使用 hello Microsoft MSSQL Server JDBC 驅動程式，可以在中找到類似的步驟***/usr/share/java/jdbcdrivers/sqljdbc42.jar***。</span><span class="sxs-lookup"><span data-stu-id="9e572-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e572-363">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e572-363">Next steps</span></span>
<span data-ttu-id="9e572-364">如需這些主題會逐步引導您完成組成 hello 資料科學程序，在 Azure 中的 hello 工作的概觀，請參閱[資料科學的小組流程](http://aka.ms/datascienceprocess)。</span><span class="sxs-lookup"><span data-stu-id="9e572-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="9e572-365">如需其他端對端逐步解說示範如何針對特定案例的 hello 小組資料科學程序中的 hello 步驟的說明，請參閱[小組資料科學程序的逐步解說](data-science-process-walkthroughs.md)。</span><span class="sxs-lookup"><span data-stu-id="9e572-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="9e572-366">hello 逐步解說也說明如何 toocombine 雲端和內部部署工具和服務至工作流程或管線 toocreate 智慧型應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e572-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
