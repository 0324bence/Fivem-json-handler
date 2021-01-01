# Json handler for FiveM

Json handler is a resource which is capable of **writing** and **getting** data from json files.

## Usage
---
There are 2 methods for calling the functions in this resource from anywhere.

1.   **Using events.** There are 3 server events declared in the resourece which are:
        - **json:getFile** Expects 1 variable. The `filename` (without extension) and it returns a `cb` value.  
            *Examples:*
            ```lua
                TriggerEvent("json:getFile", "users", function(cb)
                    print(cb[steamid].name)
                end)
            ```
            This example returns the name according to the steamid from the users table. `steamid` is a variable.

        - **json:getItem** Expects 2 variables. The `filename` (without extension), the `name of the item` you want and it returns a `cb` value.  
            *Examples:*
            ```lua
                TriggerEvent("json:getItem", "users", steamid, function(cb)
                    print(cb.name)
                end)
            ```
            This example print out the same as the last one, but it only returns the item that is called `steamid`. `steamid` is a variable

        - **json:addItem** Expects 3 variables. The `filename` (without extension), the `name of the item` you want to create and a `lua table` with the data of your item, and their value.  
            *Examples:*
            ```lua
                TriggerEvent("json:addItem", "users", steamid, { name = "example", example = 5 })
            ```
            This example creates an item in `users.json` called *steamid* with the givem parameters. `steamid` is a variable

        - **json:deleteItem** Expects 2 variables. The `filename` (without extension) and the `name of the item` you want to delete.  
            *Examples:*
            ```lua
                TriggerEvent("json:deleteItem", "users", steamid)
            ```
            This example deletes the `steamid` item from `users.json`.

        - **json:replaceItem** Expects 3 variables. The `filename` (without extension), the `name of the item` you want to replace and a `lua table` with the data of your item, and their value.  
            *Examples:*
            ```lua
                TriggerEvent("json:replaceItem", "users", steamid, { name = "example", example = 6 })
            ```
            This example replaces an item in `users.json` called `steamid` with the givem parameters. `steamid` is a variable

        - **json:replaceData** Expects 3 variables. The `filename` (without extension), the `name of the item` you want to replace in and a `lua table` with another lua table inside it. The second table has 2 variables. name and content. You will understand it form the example.  
            *Examples:*
            ```lua
                TriggerEvent("json:replaceData", "users", steamid, { { name = "name", content = "bence" }, { name = "money", content= 10 } })
            ```
            This example replaces the `name` and the `money` in `users.json` 
        `steamid` is a variable
        
        - **json:deleteData** Expects 3 variables. The `filename` (without extension), the `name of the item` you want to do the delete in and the name of the data you want to delete.  
            *Examples:*
            ```lua
                TriggerEvent("json:deleteData", "users", steamid, "money")
            ```
            This example deletes the data named `money` from the `steamid` item in `users.json`  
            in the `steamid` item with the corresponding content.  
2. **Using exports.** There is an option to import a class using exports.
    The class work like this:
    ```lua
        local file =  exports.json_handler:InitiateFile(filename)
    ```
    Then if you copied in this line, you can access 7 functions. These are:
    - **file.GetFile()**
    - **file.GetItem(itemname)**
    - **file.AddItem(itemname, content)** 
    - **file.DeleteItem(itemname)**
    - **file.ReplaceItem(itemname, itemcontent)**
    - **file.ReplaceData(itemname, table)**
    - **file.DeleteData(itemname, dataname)**

    *Note that you can use whatever variable name you want*   
    *Note that these functions do the same, as the events mentioned above. If you do not understand what they do, have a look at the corresponding event.*   
    I suggest using exports if you executing the request on the server side, becouse they are more resource friendly.

*Note that files need to be created by the developer, who plans to use this, and it can contain anything that json can. I used users in the examples, but you might not have that file.*

---
copyright © 0324bence 