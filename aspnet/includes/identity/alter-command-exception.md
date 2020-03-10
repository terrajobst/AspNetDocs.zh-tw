> <span data-ttu-id="f5b34-101">如果應用程式使用 SQLite 作為其身分識別資料存放區，則不支援某些命令。</span><span class="sxs-lookup"><span data-stu-id="f5b34-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="f5b34-102">由於資料庫引擎的限制，`Alter` 命令會擲回下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="f5b34-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="f5b34-103">「NotSupportedException： SQLite 不支援這種遷移作業」。</span><span class="sxs-lookup"><span data-stu-id="f5b34-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="f5b34-104">解決方法是在資料庫上執行 Code First 的遷移，以變更資料表。</span><span class="sxs-lookup"><span data-stu-id="f5b34-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
