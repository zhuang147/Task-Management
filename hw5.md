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

