<!-----
layout: lab
exclude: true
----->

<img src="assets/cs171-logo.png" width="200">

&nbsp;

# Week 4 - Lab

## Introduction

Our labs are designed as interactive, self-guided workbooks. You’ll read and work through practical example problems at your own pace, continuing any unfinished parts at home during the week. Although labs are **not submitted for a grade**, we **strongly recommend completing all lab exercises**. Skipping labs will make homework assignments and the final project much more challenging.

We embrace the concept of learning by doing. To truly master new programming and development skills, you have to spend the time to figure things out and to try different approaches and examples.
However, you are not alone in this! CS1710 staff is available for any questions that pop up along the way. We encourage you to pester them with questions, but at the same time, make sure that you come to the lab prepared and ready to code!

### ChatGPT et al.

We encourage you to use AI for exploring questions and deepening your understanding of specific topics. However, we strongly recommend completing these lab exercises primarily through **manual work**. Building a solid foundation through hands-on practice is essential. This foundational understanding will enable you to use AI tools more effectively in the future.

### Prerequisites

- You have installed a code editor such as *Visual Studio Code* ([https://code.visualstudio.com/](https://code.visualstudio.com/)) with the Live Server extension for local development. (You are free to use your own IDE, but we will only officially support VS Code.)
- We encourage you to use [Google Chrome](https://www.google.com/chrome/) or [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/) as your primary web browser during all labs and homeworks.


## Learning Objectives

After completing this lab you will be able to:

- Set up, structure, and modify modern HTML5 documents with semantic elements
- Apply modern CSS rules including Flexbox
- Execute JavaScript functions using modern ES6+ syntax, utilize array methods, and interact with the console for debugging
- Integrate HTML, CSS, and JavaScript to create your first interactive website using client-side scripting
- Utilize modern web development tools effectively, including VS Code, Chrome/Firefox developer tools, and the browser-integrated console

## Agenda

In today's session ([download template](week_04_lab_template.zip)), we will be working with a dataset that provides global attractions data to build a themed website.

![Lab Preview](assets/week-04_lab_preview.png?raw=true "Lab Preview")

- **Activity 1: Modern HTML5 & CSS Foundations**
	- Learn modern HTML5 semantic elements and CSS Flexbox to create layouts for our attractions website.

- **Activity 2: Modern JavaScript Fundamentals**
	- Learn how to use modern JavaScript (ES6+) to manipulate data and explore it in the console.

- **Activity 3: Synthesizing and Applying Skills**
	- Apply the HTML5, CSS, and modern JavaScript skills acquired in the previous activities to create a dynamic, interactive website that effectively presents global attractions data.

-----

## Activity 1: Background, Concepts & Resources

### Modern HTML5
HTML5 introduced semantic elements that provide better structure and meaning to web content. Modern HTML development emphasizes accessibility, semantic markup, and clean structure.

- **HTML5 Semantic Structure**: Modern HTML documents should use semantic elements that describe the meaning of content, not just its appearance.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Global Attractions Dashboard</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <h1>Global Attractions</h1>
        <nav>
            <!-- Navigation elements -->
        </nav>
    </header>
    <main>
        <section class="dashboard">
            <!-- Main content -->
        </section>
    </main>
    <footer>
        <!-- Footer content -->
    </footer>
</body>
</html>
```

- **Semantic Elements**: HTML5 provides meaningful elements that improve accessibility and SEO:
  - `<header>`: Introductory content or navigational aids
  - `<nav>`: Navigation links
  - `<main>`: Main content of the document
  - `<section>`: Thematic grouping of content
  - `<article>`: Self-contained composition
  - `<aside>`: Content tangentially related to main content
  - `<footer>`: Footer information

- **Attributes for Modern Web**:
  - **ID Attribute**: Unique identifier for an element, used for targeting with JavaScript and CSS
  - **Class Attribute**: Used to define styles for multiple elements or for targeting groups with JavaScript
  - **Data Attributes**: Custom attributes for storing data (`data-*`)
  - **Accessibility**: Modern HTML includes ARIA attributes for screen readers, though we'll focus on semantic elements for this lab

```html
<section class="attractions-dashboard" id="dashboard" data-category="all">
    <div class="control-panel">
        <select id="category-select">
            <option value="all">All Attractions</option>
            <option value="theme">Theme Parks</option>
        </select>
    </div>
</section>
```

### CSS

CSS (Cascading Style Sheets) is used to create visually engaging web pages by styling the HTML structure. CSS can be embedded directly into HTML files in various ways, ensuring flexibility and control over the appearance of web content.


#### Including CSS in HTML

CSS can be included in your HTML in three ways:

**1. External Stylesheet (Recommended)**
```html
<head>
    <link rel="stylesheet" href="css/style.css">
</head>
```

**2. Internal CSS**
```html
<head>
    <style>
        body { margin: 0; padding: 0; }
    </style>
</head>
```

**3. Inline CSS**
```html
<div style="color: blue; font-size: 16px;">Content</div>
```

#### Basic CSS Setup

```css
/* Modern CSS Reset */
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    line-height: 1.6;
    color: #1e293b;
    background-color: #f8fafc;
}
```

**CSS Selectors**:
- **ID Selectors**: Target a unique element identified by an attribute id. Ideal for styling that should only apply to a single element.

```css
/* Styling an element with a specific ID */
#my-div {
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    padding: 20px;
}
```
- **Class Selectors**: Target all elements that share a common class attribute. Useful for applying uniform styles to groups of elements.
```css
/* Styling all elements with a specific class */
.my-custom-div-class {
    color: navy;
    font-size: 18px;
    margin: 10px;
}
```

The **CSS box model** is the foundation of web page layout. Every element on a web page is represented as a rectangular box, made up of four areas: **content**, **padding**, **border**, and **margin**.

- **Content:** The actual text or image.
- **Padding:** Space between the content and the border.
- **Border:** The edge surrounding the padding.
- **Margin:** The outermost layer, creating space between the element and others on the page.

**Margins** are especially useful for spacing elements apart and controlling layout. By adjusting the margin property in CSS, you can increase or decrease the space outside of an element’s border, helping you design clean and organized web pages.

### Introduction to CSS Flexbox

Flexbox (Flexible Box Layout) is the modern CSS standard for creating layouts. It makes it easy to align items, distribute space, and create responsive designs without complex calculations or external frameworks.

**Key Concept**: Flexbox works with a **container** (parent) and **items** (children). The container controls how items are arranged.

#### Simple Flexbox Example

Let's start with a basic horizontal layout:

```html
<div class="simple-flex">
    <div class="item">Item 1</div>
    <div class="item">Item 2</div>
    <div class="item">Item 3</div>
</div>
```

```css
.simple-flex {
    display: flex; /* This makes it a flex container */
}

.item {
    padding: 1rem;
    background-color: lightblue;
    margin: 0.5rem;
}
```

This creates three items in a horizontal row. Now let's add some control:

#### Flexbox Properties Explained

```css
.flex-container {
    display: flex;
    
    /* Direction: row (horizontal) or column (vertical) */
    flex-direction: row;
    
    /* Horizontal alignment (main axis) */
    justify-content: space-between; /* or center, flex-start, flex-end */
    
    /* Vertical alignment (cross axis) */
    align-items: center; /* or flex-start, flex-end, stretch */
    
    /* Space between items */
    gap: 1rem;
}

.flex-item {
    /* How much an item should grow */
    flex: 1; /* All items grow equally */
    /* flex: 0 0 300px; - Don't grow/shrink, stay 300px wide */
}
```

#### Visual Example

Change `flex-direction` and `justify-content`/`align-items` to quickly switch between horizontal and vertical layouts and experiment with how items align.

```
flex-direction: row + justify-content: space-between
┌─────────────────────────────────────────┐
│ [Item 1]      [Item 2]      [Item 3]   │
└─────────────────────────────────────────┘

flex-direction: column + align-items: center  
┌─────────────────────────────────────────┐
│              [Item 1]                   │
│              [Item 2]                   │
│              [Item 3]                   │
└─────────────────────────────────────────┘
```


**Tip:**  

For more details, check out the [CSS Flexbox Guide on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox).

---


### Project Folder Structure

A well-organized folder structure is essential for efficient web project management and scalability. Below is the recommended setup for your CS1710 projects.
- **Root Directory**: Contains the `index.html` file, which is the main entry point of the website.
- **CSS Folder**: Stores all CSS files.
- **JS Folder**: Contains various JavaScript files, each serving different parts of the project.
- **Assets Folder**: Used to store all the images used in the project.



```plaintext
week-04/lab/
│
├── index.html                  # Main HTML file
│
├── css/                        # Folder for CSS files
│   ├── style.css              # Main stylesheet with modern CSS
│   └── components.css         # Component-specific styles (optional)
│
├── js/              	# Folder for JavaScript files
│   ├── activity_2.js      	# JavaScript for Activity 2
│   ├── activity_3.js      	# JavaScript for Activity 3
│   ├── barchart.js        	# JavaScript for bar chart functionality
│   └── global-attractions.js 	# JavaScript for global attractions functionality
│
├── assets/                    # Static assets
│   ├── images/               # Image files
│   └── icons/                # Icon files
│
└── README.md                 # Project documentation
```

-----

## Activity 1: Tasks

1. **Download the Lab Template:**  
   Download this week's [lab template](week_04_lab_template.zip) to your working directory.

2. **Review `index.html`:**  
   Open the `index.html` file from the template directory. Take a few minutes to read through and understand its basic structure and provided elements.

3. **Set Up Page Layout:**  
   - Structure your page layout using Flexbox and semantic HTML tags.
   - Create a single, centered main column occupying half of the screen, with empty space (columns) on either side to fill the remaining width. You can use relative widths (e.g. 50%) to achieve this.
   - Use appropriate semantic tags such as `<main>` and `<section>` for markup clarity.

4. **Add Headings:**  
   - Inside the central/main column:
     - Include a `<header>` section as the first row.
     - Place an `<h2>` element with the title `Theme Parks, Water Parks and Museums`.
     - Directly underneath, add an `<h1>` element with the heading `Global Attractions Attendance`.

5. **Insert a Category Dropdown:**  
   - Directly below the headings, add a dropdown menu for selecting the attraction category.
   - Use the following HTML snippet:

      ```html
      <div class="controls">
          <label for="attraction-category">Choose Category:</label>
          <select id="attraction-category">
              <option value="all">All Attractions</option>
              <option value="Water Park">Water Park</option>
              <option value="Museum">Museum</option>
              <option value="Theme Park">Theme Park</option>
          </select>
      </div>
      ```

6. **Designate a Chart Display Area:**  
   - Below the dropdown, set up a distinct row for your chart display.
   - Add a container with a visible background color to separate it visually:

      ```html
      <div class="chart-container">
          <div id="chart-area"></div>
      </div>
      ```

7. **Style Using `style.css`:**  
   - Open and edit `css/style.css` to enhance your layout.
   - Apply styles, such as:
     - Use Flexbox to implement your column layout.
     - Style rows and the chart area with appropriate `background` colors and spacing.
     - For headings, specify `font-family`, `font-weight`, and `font-size` for hierarchy and readability.
     - Consider using padding, margin, and height values to visually organize your content.

**Tips:**  
- Use semantic HTML tags for accessibility and structure.
- Take time to experiment with Flexbox properties (e.g., `justify-content`, `align-items`, `flex-basis`).
- Make sure your page layout looks clean, organized, and visually separated into logical rows/sections.

---


## Activity 2: Background, Concepts & Resources

### Modern JavaScript (ES6+)

Modern JavaScript development uses ES6+ features that provide cleaner, more readable code. We'll focus on current best practices and syntax.

#### Including JavaScript in HTML

JavaScript can be included in your HTML in three ways:

**1. External Script (Recommended)**
```html
<head>
    <script src="js/main.js"></script>
</head>
<!-- OR before closing body tag -->
<body>
    <!-- HTML content -->
    <script src="js/main.js"></script>
</body>
```

**2. Internal JavaScript**
```html
<head>
    <script>
        console.log('Hello, world!');
    </script>
</head>
```

**3. Inline JavaScript**
```html
<button onclick="alert('Button clicked!')">Click me</button>
```




### JavaScript Basics

Understanding the basics of JavaScript is crucial for any web developer. This section covers the core components such as variables, data types, functions, and control structures.


#### Variables
In modern JavaScript, `let` and `const` are preferred for declaring variables due to their block scope limitations, which enhance code readability and reduce errors:

- `let`: Allows you to declare variables that can be changed later. It is block-scoped, meaning it exists only within the nearest set of curly braces (`{}`).
- `const`: Used to declare variables meant to remain constant. A `const` variable cannot be reassigned, and like `let`, it is block-scoped.

```javascript
let message = "Hello, world!";
const pi = 3.14;
```

#### Data Types

JavaScript is a loosely typed language, meaning you don't have to declare the type of variable ahead of time. The language automatically determines the data types during execution. Here are some common types:

```javascript
// String
let name = "Alice";

// Number
let age = 30;

// Boolean
let isStudent = true;

// Array
let fruits = ["Apple", "Banana", "Cherry"];

// Object / Dictionary
let person = {
    firstName: "John",
    lastName: "Doe",
    age: 50
};
```

#### Functions 

Functions are blocks of code that perform specific tasks and are executed when called. They help keep code modular and reusable.

```javascript
function greet(name) {
    return "Hello, " + name + "!";
}

console.log(greet("Alice"));

// Arrow functions for concise syntax
const greetUser = (name) => {
    return `Hello, ${name}!`;
};

// Shorter arrow function for simple operations
const square = (x) => x * x;

// Template literals for string interpolation
const createMessage = (name, age) => `${name} is ${age} years old.`;
```




#### Destructuring and Spread Operator

Concise ways to extract and copy data:

```javascript
// Object destructuring
const person = { name: 'Alice', age: 25, city: 'Boston' };
const { name, age } = person;

// Array destructuring
const [first, second, ...rest] = [1, 2, 3, 4, 5];

// Spread operator for copying arrays (avoiding mutation)
const originalArray = [1, 2, 3];
const newArray = [...originalArray, 4, 5];
```

#### Control Structures

Control structures manage the flow of your program’s execution based on conditions. The most common type is the if-else statement.

```javascript
if (age > 18) {
    console.log("You are an adult.");
} else {
    console.log("You are a minor.");
}
```

### Array Methods

JavaScript provides powerful methods for working with arrays:

```javascript
const attractions = [
  { name: "Magic Kingdom", visitors: 20859000, category: "Theme Park" },
  { name: "Tokyo Disneyland", visitors: 17214000, category: "Theme Park" },
  // ...more items
];
```

- **forEach:** Run a function on each item.
  ```javascript
  attractions.forEach(({ name, visitors }) => {
    console.log(`${name}: ${visitors.toLocaleString()} visitors`);
  });
  ```

- **map:** Create a new array by transforming each item.
  ```javascript
  const attractionNames = attractions.map(attraction => attraction.name);
  ```

- **filter:** Create a new array with items that match a condition.
  ```javascript
  const popularThemeParks = attractions.filter(
    attraction => attraction.category === "Theme Park" && attraction.visitors > 15000000
  );
  ```

- **sort:** Sort items based on a compare function.
  ```javascript
  // Sort by visitors descending
  const sortedByVisitors = [...attractions].sort((a, b) => b.visitors - a.visitors);

  // Sort by name ascending
  const sortedByName = [...attractions].sort((a, b) => a.name.localeCompare(b.name));
  ```

- **Chaining methods:**
  ```javascript
  const topAttractionNames = attractions
    .filter(a => a.visitors > 12000000)
    .sort((a, b) => b.visitors - a.visitors)
    .map(a => a.name);
  ```

---

**Tip:**  
Refer to the [MDN JavaScript documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript) for more details and practice examples.

---

### Debugging with Developer Tools


Debugging is a critical skill in web development, allowing developers to understand and fix issues that arise in their code. The JavaScript console, along with browser developer tools, provides a powerful environment for diagnosing and resolving problems, bridging the gap between the visible elements (HTML) and the invisible logic (JavaScript). 

#### The Role of the Console in Debugging
The console is more than just a place to log messages. It's a comprehensive tool that allows developers to interact with the JavaScript running on the page, inspect variables, and execute code in real-time.

- **Logging and Inspecting**: Use `console.log()` to print out values, helping to track down where things might be going wrong in your code. The console also allows you to inspect objects and arrays in detail, showing their properties and methods available.

```javascript
// Different log levels
console.log('General information');
console.info('Informational message');
console.warn('Warning message');
console.error('Error message');

// Grouped logging
console.group('Attraction Processing');
console.log('Processing attractions...');
console.log('Found 60 attractions');
console.groupEnd();

// Table view for arrays of objects
console.table(attractions);

// Performance timing
console.time('Data Processing');
// ... your code here
console.timeEnd('Data Processing');
```
- Error Reporting: JavaScript errors are automatically logged in the console, providing a stack trace that helps in locating the source of the error quickly.

#### Developer Tools for a Deeper Insight
Browser developer tools offer several functionalities that complement the console by providing a visual interface to the underpinnings of a web page:

- **Elements Panel**: Directly inspect and manipulate the HTML and CSS of a page. This is particularly useful for understanding how JavaScript changes affect the DOM and visual layout.
- **Sources Panel**: View and edit JavaScript files directly, set breakpoints, and step through the code to observe its execution in real-time.
- **Network Panel**: Monitor network requests made by your page, inspect the data being sent and received, and understand the performance implications of your scripts.
- **Performance Panel**: Analyze the runtime performance of your page, identify slow-running scripts, and optimize accordingly.

#### Best Practices for Effective Debugging
- **Consistent Logging**: Establish a habit of logging important checkpoints within your code, which can help in quickly identifying where things go wrong.
- **Use Breakpoints**: Instead of using console.log() excessively, set breakpoints where you suspect issues to step through the code and inspect variables at specific points in execution.



-----

## Activity 2: Tasks

1. **Setup Environment:**
   - Create a new file named `activity_2.js` in your `js` folder.
   - Ensure it's included in your `index.html` after `global-attractions.js`.

2. **Initial Data Exploration:**
   - Review `global-attractions.js` to understand the data structure.
   - Add a `console.log` statement in `activity_2.js` to log all the attractions:
   - Use the browser’s console and developer tools to explore the logged attractions. Familiarize yourself with the data types and structure.

3. **Implement `forEach` to Display Names:**
	- Write a `forEach` loop in `activity_2.js` that logs the name of each attraction with more than 10 million visitors.

4. **Filtering Data:**
	- Use the `filter` method to create a new array, `filteredData`, that includes only those attractions with visitors greater than 10 million:

5. **Sorting the Filtered Data (Introducing a Common Issue):**
	- Attempt to sort `filteredData` based on the number of visitors in descending order.
    - Compare if there is a difference between the filtered and the sorted log output.
	- Notice how even `filteredData` is now permanently sorted. Reflect on why this might not always be desirable.

6. **Using `map` to Prevent Unintended Side Effects:**
	- Introduce a `map` operation between the filtering and sorting to create a shallow copy of the array and then sort the copy:
	- **Explanation on Shallow vs. Deep Copying**:
		- A **shallow copy** (as done above) copies the immediate values of the array, but if those values are objects (as in our case), the copied values still reference the same objects. This is sufficient for our sorting scenario because we are not modifying the objects themselves.
		- A **deep copy** would be necessary if we needed to duplicate every level of object nested within the array, ensuring completely independent arrays and objects.


-----

## Activity 3: Background, Concepts & Resources

### Template

The following files and folders have been provided:
- **css**: You have already worked with this in Activity 1 when you styled your `index.html`.
- **js**:
	- `global-attractions.js`: Contains the global attractions dataset.
	- `barchart.js`: Contains the function `renderBarChart()` that you will call after filtering the data.
	- `activity_3.js`: Includes the empty function `updateBarChart()`, that you will have to populate. The function should 
  be triggered through an event listener, filter the attractions data, and, lastly, call `renderBarChart()`.
- **index.html**: Serves as the canvas for your visualization and initially included some boilerplate HTML. In Activity 1, you've added the main layout.

### Data
The dataset provided includes details on 60 global attractions. Each entry in the JSON array, stored in the `attractionData` global variable, includes:
- **Location**: Name, city, and country of the attraction.
- **Category**: Type of attraction (theme park, water park, or museum).
- **Visitors**: Annual visitor count for 2013.
- **Entry**: Indicates whether entry is paid or free.



### DOM

The **DOM (Document Object Model)** is a programming interface for web documents. When a web page loads, the browser turns the HTML into a structured, tree-like representation called the DOM. Each part of the HTML (such as elements, attributes, and text) becomes a **node** in this tree.

With JavaScript, you can use the DOM to:
- Access and read elements on the web page,
- Change content and styles dynamically,
- Add, remove, or modify HTML elements,
- Handle user interactions (like clicks or form submissions).

In essence, the DOM connects your JavaScript code to the visible web page, making interactive, dynamic websites possible.


### Event Handling


Event listeners are crucial for making web pages interactive. They allow you to define how your page should respond to user actions, such as clicks, changes, or mouse movements. You can attach event listeners directly in your HTML (inline) or through your JavaScript code, and each method has its uses depending on the scenario.

#### Inline Event Listeners

Inline event listeners are added directly within your HTML elements. This method can be straightforward for simple interactions and helps visually connect the HTML structure with its interactive behaviors.

```html
<select id="communicationMethod" onchange="updatePreference()">
	<option value="email">Email</option>
	<option value="phone">Phone</option>
	<option value="text">Text Message</option>
</select>
```
In this example, this.value within the inline onchange attribute refers to the value of the currently selected option, which is passed directly to the updatePreference() function.

#### JavaScript Event Listeners

Alternatively, you can attach event listeners using JavaScript. This approach is generally preferred for more complex applications because it keeps your JavaScript separate from your HTML, aligning with modern web development practices that favor separation of concerns.

```javascript
document.getElementById('communicationMethod').addEventListener('change', (event) => {
	updatePreference();
});
```

### DOM Manipulation

Get one specific element via its unique identifier or use a more flexible query approach:

```javascript
// Element selection
const chartArea = document.getElementById('chart-area');
const categorySelect = document.querySelector('#attraction-category');

// Update content based on css class
const updateChartTitle = (category) => {
    const titleElement = document.querySelector('.chart-title');
    titleElement.textContent = category === 'all' 
        ? 'All Attractions' 
        : `${category} Attractions`;
};

// Create elements programmatically
const createAttractionCard = (attraction) => {
    const card = document.createElement('div');
    card.className = 'attraction-card';
    card.innerHTML = `
        <h3>${attraction.name}</h3>
        <p>Visitors: ${attraction.visitors.toLocaleString()}</p>
        <span class="category">${attraction.category}</span>
    `;
    return card;
};
```

### Retrieving

When dealing with `<select>` elements, it's essential to know how to retrieve the selected value effectively. Here are two common methods:

1. **Using `this.value` as an Argument**
   
	When an event handler is called, this refers to the element that received the event, unless the function uses an arrow function, in which case this does not bind to the event target. You can pass this.value directly to a function when setting up inline event handlers.

	```html
	<select id="communicationMethod" onchange="updatePreference(this.value)">
	    <option value="email">Email</option>
	    <option value="phone">Phone</option>
	    <option value="text">Text Message</option>
	</select>
	```

	```javascript
	function updatePreference(selectedValue) {
    console.log("Selected communication method:", selectedValue);
	}
	```

2. **Retrieving the Value with getElementById**
   For a more explicit retrieval, especially useful in JavaScript files where you might want to keep HTML clean of JavaScript logic, you can use getElementById to access the select element and then get its value.

   ```html
   <select id="communicationMethod" onchange="updatePreference()">
       <option value="email">Email</option>
       <option value="phone">Phone</option>
       <option value="text">Text Message</option>
   </select>
   ```
   
	```javascript
	function updatePreference() {
    let selectBox = document.getElementById('communicationMethod');    
    let selectedValue = selectBox.value;
    console.log("Selected communication method:", selectedValue);
	}
	```


-----

## Activity 3: Tasks

1. **Familiarize Yourself with `activity_3.js`**:
	- Begin by reviewing the `activity_3.js` file to understand the structure and existing code. Pay close attention to any `TO DO` comments that outline incomplete sections needing your input.

2. **Render Initial BarChart**:
	- Modify the `updateChart` function in `activity_3.js` to automatically display the top 5 attractions based on visitor count when the page first loads. This involves sorting the data and selecting the top items before passing them to the `renderBarChart` function.

3. **Add Event Listener to Dropdown**:
	- Add an `onchange` event listener to the dropdown menu in your `index.html`. This listener should call the `updateChart` function whenever the user selects a new category.

4. **Enhance the `updateChart` Function**:
	- Update the `updateChart` function to dynamically read the selected category from the dropdown menu.
	- Implement logic within `updateChart` to filter the attractions array based on the selected category.
	- After filtering, ensure that the function continues to sort and limit the array to the top 5 attractions, then calls `renderBarChart` with this filtered data.

5. **Debug and Test**:
   - Ensure that the `updateChart` function is properly connected to the dropdown's event listener, allowing the chart to update dynamically with each change in selection.
   - Test the updated functionality by selecting different categories from the dropdown to ensure the chart updates accordingly.
   - Debug any issues that arise, such as the chart not updating correctly or displaying incorrect data.

