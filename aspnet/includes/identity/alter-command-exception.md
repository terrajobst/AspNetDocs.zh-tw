> 如果應用程式使用 SQLite 作為其身分識別資料存放區，則不支援某些命令。 由於資料庫引擎的限制，`Alter` 命令會擲回下列例外狀況：
>
> 「NotSupportedException： SQLite 不支援這種遷移作業」。 
>
> 解決方法是在資料庫上執行 Code First 的遷移，以變更資料表。
