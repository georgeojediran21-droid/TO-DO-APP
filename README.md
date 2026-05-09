<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Modern To-Do App</title>

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family: Arial, sans-serif;
    }

    body{
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      background:linear-gradient(135deg,#0f172a,#1e293b,#334155);
      padding:15px;
    }

    .todo-container{
      width:100%;
      max-width:450px;
      background:rgba(255,255,255,0.08);
      backdrop-filter:blur(10px);
      border:1px solid rgba(255,255,255,0.1);
      border-radius:20px;
      padding:25px;
      color:white;
      box-shadow:0 10px 30px rgba(0,0,0,0.3);
    }

    .todo-container h1{
      text-align:center;
      margin-bottom:20px;
      font-size:2rem;
    }

    .input-box{
      display:flex;
      gap:10px;
      margin-bottom:20px;
    }

    .input-box input{
      flex:1;
      padding:14px;
      border:none;
      border-radius:12px;
      outline:none;
      font-size:1rem;
      background:#e2e8f0;
      color:#111;
      min-width:0;
    }

    .input-box button{
      padding:14px 18px;
      border:none;
      border-radius:12px;
      cursor:pointer;
      background:#38bdf8;
      color:white;
      font-weight:bold;
      transition:0.3s;
      white-space:nowrap;
    }

    .input-box button:hover{
      background:#0ea5e9;
      transform:scale(1.05);
    }

    ul{
      list-style:none;
    }

    li{
      background:rgba(255,255,255,0.1);
      padding:14px;
      border-radius:12px;
      margin-bottom:12px;
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:10px;
      flex-wrap:wrap;
      animation:fadeIn 0.3s ease;
    }

    li span{
      flex:1;
      word-break:break-word;
    }

    li.completed span{
      text-decoration:line-through;
      opacity:0.6;
    }

    .task-buttons{
      display:flex;
      gap:8px;
    }

    .complete-btn,
    .delete-btn{
      border:none;
      padding:8px 12px;
      border-radius:8px;
      cursor:pointer;
      color:white;
      transition:0.3s;
      font-size:0.9rem;
    }

    .complete-btn{ background:#22c55e; }
    .complete-btn:hover{ background:#16a34a; }

    .delete-btn{ background:#ef4444; }
    .delete-btn:hover{ background:#dc2626; }

    .empty-message{
      text-align:center;
      opacity:0.7;
      margin-top:10px;
    }

    @keyframes fadeIn{
      from{opacity:0; transform:translateY(10px);}
      to{opacity:1; transform:translateY(0);}
    }

    /* ======================
       MOBILE RESPONSIVENESS
    ======================= */
    @media (max-width: 600px){

      .todo-container{
        padding:18px;
        border-radius:16px;
      }

      .todo-container h1{
        font-size:1.5rem;
      }

      .input-box{
        flex-direction:column;
      }

      .input-box input{
        width:100%;
      }

      .input-box button{
        width:100%;
      }

      li{
        flex-direction:column;
        align-items:flex-start;
      }

      .task-buttons{
        width:100%;
        justify-content:flex-end;
      }

      .complete-btn,
      .delete-btn{
        flex:1;
        text-align:center;
      }
    }
  </style>
</head>

<body>

  <div class="todo-container">
    <h1>To-Do App</h1>

    <div class="input-box">
      <input type="text" id="taskInput" placeholder="Enter a task..." />
      <button onclick="addTask()">Add</button>
    </div>

    <ul id="taskList"></ul>

    <p class="empty-message" id="emptyMessage">No tasks yet...</p>
  </div>

  <script>
    const taskInput = document.getElementById("taskInput");
    const taskList = document.getElementById("taskList");
    const emptyMessage = document.getElementById("emptyMessage");

    function addTask() {
      const taskText = taskInput.value.trim();

      if(taskText === ""){
        alert("Please enter a task");
        return;
      }

      const li = document.createElement("li");

      li.innerHTML = `
        <span>${taskText}</span>
        <div class="task-buttons">
          <button class="complete-btn">Done</button>
          <button class="delete-btn">Delete</button>
        </div>
      `;

      li.querySelector(".complete-btn").addEventListener("click", () => {
        li.classList.toggle("completed");
      });

      li.querySelector(".delete-btn").addEventListener("click", () => {
        li.remove();
        checkEmptyState();
      });

      taskList.appendChild(li);
      taskInput.value = "";

      checkEmptyState();
    }

    function checkEmptyState() {
      emptyMessage.style.display =
        taskList.children.length === 0 ? "block" : "none";
    }

    taskInput.addEventListener("keypress", (e) => {
      if(e.key === "Enter") addTask();
    });

    checkEmptyState();
  </script>

</body>
</html># TO-DO-APP
TO DO
