## 🗂 任務管理系統 UML 類別圖（中文）

```mermaid
classDiagram
    %% === 使用者 ===
    class 使用者 {
        +整數 使用者ID
        +字串 使用者名稱
        +字串 電子郵件
        +字串 密碼
        +註冊()
        +登入()
        +更新資料()
    }

    %% === 任務 ===
    class 任務 {
        +整數 任務ID
        +字串 標題
        +字串 描述
        +日期 截止日期
        +字串 狀態
        +建立任務()
        +編輯任務()
        +刪除任務()
        +標記完成()
    }

    %% === 留言 ===
    class 留言 {
        +整數 留言ID
        +字串 內容
        +日期時間 建立時間
        +新增留言()
        +刪除留言()
    }

    %% === 分類 ===
    class 分類 {
        +整數 分類ID
        +字串 名稱
        +新增分類()
        +刪除分類()
    }

    %% === 標籤 ===
    class 標籤 {
        +整數 標籤ID
        +字串 名稱
        +新增標籤()
        +移除標籤()
    }

    %% === 關係 ===
    使用者 "1" --> "0..*" 任務 : 建立
    任務 "1" --> "0..*" 留言 : 包含
    分類 "1" --> "0..*" 任務 : 分組
    任務 "*" --> "*" 標籤 : 標記

## 🗂 任務管理系統 UML 類別圖

```mermaid
classDiagram
    %% === 使用者 ===
    class User {
        +int userID
        +string username
        +string email
        +string password
        +register()
        +login()
        +updateProfile()
    }

    %% === 任務 ===
    class Task {
        +int taskID
        +string title
        +string description
        +date dueDate
        +string status
        +createTask()
        +editTask()
        +deleteTask()
        +markAsComplete()
    }

    %% === 留言 ===
    class Comment {
        +int commentID
        +string content
        +datetime createdAt
        +addComment()
        +deleteComment()
    }

    %% === 分類 ===
    class Category {
        +int categoryID
        +string name
        +addCategory()
        +deleteCategory()
    }

    %% === 標籤 ===
    class Tag {
        +int tagID
        +string name
        +addTag()
        +removeTag()
    }

    %% === 關係 ===
    User "1" --> "0..*" Task : creates
    Task "1" --> "0..*" Comment : has
    Category "1" --> "0..*" Task : groups
    Task "*" --> "*" Tag : labeled with


