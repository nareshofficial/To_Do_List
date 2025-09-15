# Ex03 To-Do List using JavaScript
## Date:15-9-2025

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>To-Do App</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>
    <div class="app-container">
        <h1>To-Do List</h1>
        <div class="input-section">
            <input type="text" id="taskInput" placeholder="Add a new task..." />
            <button id="addTaskBtn">Add</button>
        </div>
        <ul id="taskList"></ul>
    </div>

    <script src="app.js"></script>
</body>
</html>
```
style.css
```
body {
    background-color: #fffbea;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: #5a4d00;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.app-container {
    background: #ffffff;
    box-shadow: 0 4px 10px rgba(255, 206, 52, 0.3);
    border-radius: 12px;
    padding: 20px 30px;
    margin-top: 40px;
    width: 100%;
    max-width: 400px;
    text-align: center;
}

h1 {
    font-weight: 700;
    font-size: 2rem;
    margin-bottom: 20px;
    color: #ff3b8d;
    text-shadow: 1px 1px 2px #bf0092;
}

.input-section {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

#taskInput {
    flex: 1;
    padding: 10px 15px;
    border: 2px solid #ff3bb1;
    border-radius: 8px;
    font-size: 1rem;
    outline: none;
    transition: border-color 0.3s;
}

#taskInput:focus {
    border-color: #fb2d78;
}

#addTaskBtn {
    background-color: #ff3ba3;
    border: none;
    padding: 10px 18px;
    border-radius: 8px;
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    color: #5a4d00;
    box-shadow: 0 3px 6px rgba(255, 206, 52, 0.4);
    transition: background-color 0.3s;
}

#addTaskBtn:hover {
    background-color: #fb2dac;
}

#taskList {
    list-style: none;
    padding: 0;
}

#taskList li {
    background: #fffdee;
    padding: 12px 15px;
    margin-bottom: 10px;
    border-radius: 8px;
    box-shadow: 0 1px 3px rgba(255, 206, 52, 0.2);
    font-size: 1.1rem;
    color: #5a4d00;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

#taskList li span.completed {
    text-decoration: line-through;
    opacity: 0.6;
}

.delete-btn {
    background: transparent;
    border: none;
    color: #b71c1c;
    cursor: pointer;
    font-size: 1.2rem;
    font-weight: bold;
    margin-left: 10px;
    transition: color 0.2s;
}

.delete-btn:hover {
    color: #7a0a0a;
}

.complete-btn {
    background-color: #ff3bbe;
    border: none;
    padding: 6px 10px;
    margin-left: 10px;
    border-radius: 6px;
    color: #5a003f;
    cursor: pointer;
    font-size: 0.85rem;
    font-weight: 600;
    box-shadow: 0 2px 4px rgba(255, 52, 197, 0.4);
    transition: background-color 0.3s;
}

.complete-btn:hover {
    background-color: #fb2db6;
}

#progressBarBackground {
    width: 100%;
    height: 20px;
    background-color: #ffa1d6;
    border-radius: 15px;
    margin-bottom: 15px;
    box-shadow: inset 0 2px 5px rgba(255, 52, 187, 0.6);
}

#progressBarFill {
    height: 100%;
    width: 0%;
    background-color: #ff3bd5;
    border-radius: 15px;
    transition: width 0.4s ease;
}

#progressText {
    text-align: center;
    font-weight: 700;
    color: #5a4d00;
    margin: 0 0 10px 0;
}
```
app.js
```
const taskInput = document.getElementById('taskInput');
const addTaskBtn = document.getElementById('addTaskBtn');
const taskList = document.getElementById('taskList');

const appContainer = document.querySelector('.app-container');
const progressBarContainer = document.createElement('div');
progressBarContainer.id = 'progressBarContainer';
progressBarContainer.innerHTML = `
  <div id="progressBarBackground">
    <div id="progressBarFill"></div>
  </div>
  <p id="progressText">0% completed</p>
`;
appContainer.insertBefore(progressBarContainer, taskList);

const progressBarFill = document.getElementById('progressBarFill');
const progressText = document.getElementById('progressText');

addTaskBtn.addEventListener('click', () => {
    const taskText = taskInput.value.trim();

    if (taskText === '') {
        alert('Please enter a task!');
        return;
    }

    addTask(taskText);
    taskInput.value = '';
    updateProgress();
});

taskInput.addEventListener('keydown', e => {
    if (e.key === 'Enter') {
        addTaskBtn.click();
    }
});

function addTask(text) {
    const li = document.createElement('li');

    const taskSpan = document.createElement('span');
    taskSpan.textContent = text;

    const completeBtn = document.createElement('button');
    completeBtn.textContent = 'Mark as Completed';
    completeBtn.className = 'complete-btn';
    completeBtn.addEventListener('click', () => {
        taskSpan.classList.toggle('completed');
        completeBtn.textContent = taskSpan.classList.contains('completed') ?
            'Mark as Incomplete' : 'Mark as Completed';
        updateProgress();
    });

    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = '×';
    deleteBtn.className = 'delete-btn';
    deleteBtn.addEventListener('click', () => {
        li.remove();
        updateProgress();
    });

    li.appendChild(taskSpan);
    li.appendChild(completeBtn);
    li.appendChild(deleteBtn);
    taskList.appendChild(li);
}

function updateProgress() {
    const allTasks = taskList.querySelectorAll('li span');
    if (allTasks.length === 0) {
        progressBarFill.style.width = '0%';
        progressText.textContent = '0% completed';
        return;
    }
    const completedTasks = taskList.querySelectorAll('li span.completed');
    const percentage = Math.round((completedTasks.length / allTasks.length) * 100);
    progressBarFill.style.width = percentage + '%';
    progressText.textContent = percentage + '% completed';
}
```

## OUTPUT
<img width="1795" height="830" alt="image" src="https://github.com/user-attachments/assets/a8c368bc-493e-45f1-9daf-818d252609d4" />

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
