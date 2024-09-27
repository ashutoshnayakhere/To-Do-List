# To-Do-List
![image](https://github.com/user-attachments/assets/97acc7c6-124b-4a6b-a410-35bd2bb1775d)

### To-Do List Documentation

This HTML document creates a functional To-Do list web application where users can add tasks, check/uncheck completed tasks, and delete tasks. The tasks are saved in the browser’s `localStorage`, so they persist even after the page is refreshed.

---

### HTML Structure

1. **Basic HTML Setup**:
    - The document uses standard HTML5 structure, with a `<head>` for metadata and styling and a `<body>` for the content.
    - The `meta` tags ensure proper character encoding and responsive behavior across devices.

2. **Body Section**:
    - The body contains a container for the To-Do list (`.todo-app`), an input field, and an "Add Task" button wrapped inside a `div` with class `.row`.
    - An empty `<ul>` element (`id="list-container"`) is used to display the list of tasks.

---

### CSS (Style)

1. **General Styling**:
    - **`* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Poppins', sans-serif; }`**: This resets the default styles for all elements and applies the `Poppins` font.
    - The `.container` takes up the entire viewport height (`100vh`), and the To-Do list box is centered on the screen using `flexbox`.

2. **To-Do App Container (`.todo-app`)**:
    - The To-Do list box is styled with a white background, rounded corners (`border-radius: 50px`), and a shadow effect (`box-shadow`), making it stand out.
    - The padding around the content provides space for elements inside the box.

3. **Task Input Section (`.row`)**:
    - The task input field is styled with a background color, no borders, and padding for comfortable typing. The placeholder text is styled in a dark purple color.
    - The "Add Task" button has a background gradient, white text, rounded corners, and no borders, giving it a sleek and modern look.

4. **Task List (`ul li`)**:
    - Each task is presented as an `li` element without bullet points (`list-style: none`). Tasks are spaced vertically and have padding for readability.
    - A span element (`<span>`) is appended to each task to act as a delete button (a cross symbol `"\u00d7"`).
    - When a task is checked (i.e., clicked), it gets a new background color, white text, and rounded corners to indicate completion. The cross symbol also changes color on hover.

---

### JavaScript (Script)

1. **Variable Declarations**:
    - `listContainer`: References the `<ul>` where tasks will be added.
    - `inputBox`: References the input field where users type their tasks.

2. **Adding a Task**:
    ```javascript
    function addTask(){
        if(inputBox.value == ''){
            alert('Please Enter the Text');
        } else {
            const task = document.createElement('li');
            task.textContent = inputBox.value;
            listContainer.appendChild(task);
            
            let span = document.createElement('span');
            span.textContent = "\u00d7";
            task.appendChild(span);
            span.style.right = '0px';
        }
        inputBox.value = '';
        saveData();
    }
    ```
    - When the "Add Task" button is clicked, the `addTask()` function is executed.
    - If the input field is empty, an alert is shown.
    - If there is input, a new `<li>` element (task) is created, and its text content is set to the input field's value.
    - A `<span>` element (representing a delete button) is appended to each task.
    - After a task is added, the input field is cleared, and `saveData()` is called to store the current task list.

3. **Task Interaction (Check and Delete)**:
    ```javascript
    listContainer.addEventListener('click', (e) => {
        if(e.target.tagName === 'LI'){
            e.target.classList.toggle("checked");
            saveData();
        } else if(e.target.tagName === 'SPAN'){
            e.target.parentElement.remove();
            saveData();
        }
    });
    ```
    - The `listContainer` listens for clicks on its child elements.
    - If a task (`<li>`) is clicked, its `classList` is toggled with the class `checked`, which styles it as a completed task.
    - If the delete button (`<span>`) is clicked, the parent task (`<li>`) is removed.
    - After each interaction, `saveData()` is called to update the saved task list.

4. **Saving and Retrieving Tasks (`localStorage`)**:
    ```javascript
    function saveData(){
        localStorage.setItem("data", listContainer.innerHTML);
    }

    function showTask(){
        listContainer.innerHTML = localStorage.getItem("data");
    }

    showTask();
    ```
    - The `saveData()` function stores the current state of the task list in the browser’s `localStorage`.
    - The `showTask()` function retrieves and displays the stored tasks when the page is loaded or refreshed.
    - The `showTask()` function is called immediately when the page loads, ensuring that previously added tasks are displayed from the start.

---

### Summary of Interaction

1. Users can add a task by typing into the input field and clicking the "Add Task" button.
2. Tasks are displayed in a list and can be marked as complete by clicking on them (which toggles a background color and font style).
3. Each task has a delete button (a cross) to remove it from the list.
4. Tasks are saved in the browser's `localStorage` so that they persist across page reloads.

This application provides a simple but effective way to manage a To-Do list, with an intuitive interface and persistent storage functionality using `localStorage`.
