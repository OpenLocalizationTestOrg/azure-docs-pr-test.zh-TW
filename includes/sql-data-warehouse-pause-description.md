
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, the following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="46130-101">為了節省成本，您可以隨選暫停和繼續計算資源。</span><span class="sxs-lookup"><span data-stu-id="46130-101">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="46130-102">例如，如果您在夜間和週末不會使用資料庫，可以在這段時間暫停，並且在白天時繼續。</span><span class="sxs-lookup"><span data-stu-id="46130-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="46130-103">資料庫暫停時，不會向您收取 DWU 的費用。</span><span class="sxs-lookup"><span data-stu-id="46130-103">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="46130-104">當您暫停資料庫時︰</span><span class="sxs-lookup"><span data-stu-id="46130-104">When you pause a database:</span></span>

* <span data-ttu-id="46130-105">計算和記憶體資源會傳回資料中心內的可用資源集區</span><span class="sxs-lookup"><span data-stu-id="46130-105">Compute and memory resources are returned to the pool of available resources in the data center</span></span>
* <span data-ttu-id="46130-106">暫停期間 DWU 的成本是零。</span><span class="sxs-lookup"><span data-stu-id="46130-106">DWU costs are zero for the duration of the pause.</span></span>
* <span data-ttu-id="46130-107">不會影響資料儲存體，您的資料保持不變。</span><span class="sxs-lookup"><span data-stu-id="46130-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="46130-108">SQL 資料倉儲會取消所有執行中或已排入佇列的作業。</span><span class="sxs-lookup"><span data-stu-id="46130-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

