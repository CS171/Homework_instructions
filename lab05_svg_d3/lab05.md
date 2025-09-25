<!-----
layout: lab
exclude: true
----->

<img src="assets/cs171-logo.png" width="200">

&nbsp;

# Week 05 - Lab


## Learning Objectives

- Master basic SVG elements and coordinate systems for web-based graphics
- Apply advanced JavaScript concepts: *method chaining*, *anonymous functions*, and *asynchronous execution*
- Integrate D3.js into web projects effectively
- Understand the fundamental structure of D3 visualizations
- Load and process external data using D3's data loading methods
- Bind data to visual elements and create data-driven graphics

## Prerequisites

- You have downloaded the template for this week's lab. This [link](week-05_lab_template.zip) should get you there quickly.
- Understanding of basic HTML, CSS, and JavaScript concepts from previous weeks

---

## Part 1: Introduction to SVG (Scalable Vector Graphics)

### What is SVG?

SVG (Scalable Vector Graphics) is a powerful markup language for creating two-dimensional graphics directly in web browsers. Unlike raster images (JPG, PNG), SVG graphics are vector-based, meaning they maintain crisp quality at any scale.

### Key SVG Characteristics

- **Markup-based**: Defined using XML-like syntax similar to HTML
- **Scalable**: No quality loss when resized (perfect for responsive visualizations)
- **DOM-integrated**: Can be included directly in HTML or dynamically created with JavaScript
- **Styleable**: Supports CSS styling and JavaScript manipulation
- **Interactive**: Supports event handling for user interactions

### SVG Coordinate System

Understanding SVG's coordinate system is crucial for positioning elements correctly:

- **Origin (0,0)**: Located at the top-left corner
- **X-axis**: Increases from left to right
- **Y-axis**: Increases from top to bottom (opposite of mathematical convention)
- **Units**: Default unit is pixels, but other units (em, %, etc.) are supported

```html
<svg width="300" height="200">
    <!-- Origin (0,0) is at top-left corner -->
    <!-- Point (300,200) is at bottom-right corner -->
</svg>
```

### Essential SVG Elements

#### Container Element
Every SVG graphic starts with a container that defines the drawing area:

```html
<svg width="500" height="300">
    <!-- All SVG elements go here -->
</svg>
```

#### Basic Shape Elements

**Rectangle** - Defined by position and dimensions:
```html
<rect x="10" y="20" width="100" height="50" fill="blue" stroke="black" stroke-width="2"/>
```

**Circle** - Defined by center point and radius:
```html
<circle cx="50" cy="50" r="25" fill="red" opacity="0.7"/>
```

**Ellipse** - Defined by center point and separate x/y radii:
```html
<ellipse cx="100" cy="75" rx="40" ry="20" fill="green"/>
```

**Line** - Defined by start and end points:
```html
<line x1="0" y1="0" x2="100" y2="100" stroke="purple" stroke-width="3"/>
```

**Text** - For adding labels and annotations:
```html
<text x="50" y="30" font-family="Arial" font-size="16" fill="black">Hello SVG!</text>
```

### SVG Styling and Attributes

SVG elements can be styled using:

1. **Inline attributes**:
   ```html
   <circle cx="50" cy="50" r="20" fill="blue" stroke="red" stroke-width="2"/>
   ```

2. **CSS classes**:
   ```html
   <circle cx="50" cy="50" r="20" class="primary-circle"/>
   ```
   
   ```css
   .primary-circle {
       fill: blue;
       stroke: red;
       stroke-width: 2;
   }
   ```

### Complete SVG Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>SVG Basics</title>
    <style>
        .highlight-text { fill: orange; font-weight: bold; }
    </style>
</head>
<body>
    <svg width="400" height="100" style="border: 1px solid #ccc;">
        <!-- Background rectangle -->
        <rect x="0" y="0" width="400" height="100" fill="#f0f0f0"/>
        
        <!-- Colored rectangles -->
        <rect x="10" y="10" width="60" height="40" fill="blue"/>
        <rect x="80" y="10" width="60" height="40" fill="green"/>
        
        <!-- Circles with different properties -->
        <circle cx="200" cy="30" r="20" fill="red" opacity="0.8"/>
        <circle cx="250" cy="30" r="15" fill="purple" stroke="black" stroke-width="2"/>
        
        <!-- Lines creating a simple shape -->
        <line x1="300" y1="10" x2="350" y2="50" stroke="gray" stroke-width="3"/>
        <line x1="350" y1="10" x2="300" y2="50" stroke="gray" stroke-width="3"/>
        
        <!-- Text labels -->
        <text x="35" y="70" font-size="12" text-anchor="middle">Blue</text>
        <text x="110" y="70" font-size="12" text-anchor="middle">Green</text>
        <text x="200" y="70" class="highlight-text" font-size="14" text-anchor="middle">Circle</text>
    </svg>
</body>
</html>
```

*Result:*


![SVG Examples](assets/cs171-svg-example.png?raw=true "SVG Examples")


Be sure to also check out Josh W. Comeau's [A Friendly Introduction to SVG](https://www.joshwcomeau.com/svg/friendly-introduction-to-svg/) which offers a more extensive and comprehensive overview of SVG.


---



## Part 2: Introduction to D3.js

### What is D3?

> **D3.js (Data-Driven Documents)** is a JavaScript library for manipulating documents based on data using web standards.

D3 enables you to bind arbitrary data to the Document Object Model (DOM) and apply data-driven transformations. Unlike other visualization libraries that provide pre-built chart types, D3 gives you the building blocks to create custom, interactive visualizations.

### Core D3 Capabilities

**Scott Murray's summary of D3's key features:**

- **Loading**: Import data from various sources (CSV, JSON, APIs) into browser memory
- **Binding**: Associate data with DOM elements, creating new elements as needed
- **Transforming**: Modify element properties based on bound data values
- **Transitioning**: Animate elements smoothly in response to data changes or user interaction

### D3 Version Notes

**This course uses D3 version 7**, which includes several improvements over earlier versions:

- **Modern JavaScript**: Full ES6+ support with arrow functions and promises
- **Simplified data loading**: Promise-based approach replaces older callback patterns
- **Enhanced performance**: Optimized for modern browsers

When referencing online examples, be aware that many use older D3 versions. The most common difference you'll encounter is in data loading syntax.

### Setting Up D3

#### Project Structure
Organize your D3 projects with this recommended structure:

```
project/
├── index.html
├── data/
│   ├── dataset.csv
│   └── ...
├── css/
│   └── style.css
└── js/
    ├── main.js
    └── visualization.js
```

#### Including D3
Add D3 to your project via CDN:

```html
<script src="https://d3js.org/d3.v7.min.js"></script>
```

### Fundamental D3 Concepts

#### Method Chaining

Method chaining is a fundamental programming pattern in JavaScript, particularly prevalent in D3.js, that enables writing more concise and readable code when performing multiple operations on the same object.
Method chaining connects multiple function calls using the dot operator (.), where each method returns an object that the next method can operate on. This creates a fluent, pipeline-like syntax that reads naturally from left to right.


```javascript
// Method chaining example
d3.select("body")
  .append("svg")
  .attr("width", 400)
  .attr("height", 300)
  .append("circle")
  .attr("cx", 200)
  .attr("cy", 150)
  .attr("r", 50)
  .style("fill", "steelblue");
```

**Benefits of method chaining:**
- More concise code
- Clear sequence of operations
- Functional programming style

**Alternative without chaining:**
```javascript
let body = d3.select("body");
let svg = body.append("svg");
svg.attr("width", 400);
svg.attr("height", 300);
let circle = svg.append("circle");
circle.attr("cx", 200);
circle.attr("cy", 150);
circle.attr("r", 50);
circle.style("fill", "steelblue");
```



#### Selections

D3 selections are the foundation of the library - they represent elements you want to manipulate.
The D3 *select()* method uses CSS selectors as an input to grab page elements (think of it as the d3 equivalent of ```document.getElementById()``` or ```document.querySelector()```). It will return a reference to the first element in the DOM that matches the selector.
Once an element is selected - and handed off to the next method in the chain - you can apply *operators*. These D3 operators allow you to get and set ***properties***, ***styles*** and ***content*** (and will again return the current selection).

**`d3.select(selector)`** - Selects the first matching element:
```javascript
d3.select("body")        // Select body element
d3.select("#myDiv")      // Select element with id="myDiv"
d3.select(".chart")      // Select first element with class="chart"
```

**`d3.selectAll(selector)`** - Selects all matching elements:
```javascript
d3.selectAll("p")        // Select all paragraphs
d3.selectAll(".item")    // Select all elements with class="item"
```

#### Basic DOM Manipulation

After selecting elements, D3 provides powerful operators to modify the DOM dynamically. Understanding these fundamental operations is essential for creating data-driven visualizations.

##### Core DOM Operations

**Adding Elements with `append()`**
The `append()` operator creates a new element as the last child of the current selection. The newly created element automatically becomes the active selection for subsequent operations:

```javascript
d3.select("body")
  .append("h1")                    // Creates <h1></h1> inside body
  .text("My Title");               // Adds text to the h1
```

**Setting Content**
- `text()` - Sets plain text content (safe, escapes HTML)
- `html()` - Sets HTML content (allows HTML tags)

```javascript
d3.select("h1")
  .text("My Visualization");       // <h1>My Visualization</h1>

d3.select("div")
  .html("<em>Italic text</em>");   // <div><em>Italic text</em></div>
```

**Managing Attributes with `attr()`**
Use `attr()` to set HTML attributes:

```javascript
d3.select("svg")
  .attr("width", 500)              // Set width attribute
  .attr("height", 300)             // Set height attribute
  .attr("class", "main-chart");    // Set CSS class
```

**Applying Styles with `style()`**
The `style()` method directly applies CSS properties:

```javascript
d3.select("h1")
  .style("color", "darkblue")      // Text color
  .style("text-align", "center");  // Center alignment
```


##### Method Chaining Best Practices

**Use readable formatting** - Put each method on its own indented line:
```javascript
// Good: Easy to read and modify
d3.select("body")
  .append("svg")
  .attr("width", 400)
  .attr("height", 300)
  .style("border", "1px solid #ccc");
```

**Store selections when reusing** - Save references for complex manipulations:
```javascript
const svg = d3.select("body")
  .append("svg")
  .attr("width", 500)
  .attr("height", 400);

// Add multiple elements to the same SVG
svg.append("rect");
svg.append("circle");
```

This foundation of DOM manipulation serves as the building blocks for all D3 visualizations, allowing you to create and style elements programmatically.



## Activity I

1. **Download the Template for this week.**

2. **Navigate to 'activity_1' and set up a new (D3) project inside the folder.**

   *At this point it might also be a good idea to create a boilerplate template project (i.e., directory structure) that you can copy every time you create a new project. The template project should include the directory structure for your project and all the files and boilerplate you usually need (e.g., D3 libraries).

3. **Add an SVG drawing area (canvas) to the HTML document manually**

   *CSS: width: 400px; height: 200px; background: black*

4. Add a rectangle in the center of your SVG canvas.
   *CSS: width: 200px; height: 100px; background: beige*

5. Add a circle in the center of your rectangle.
   *CSS: radius: 20px; background: blue*

6. **Create and embed a .js file and use D3 to add a ```div```-container with the text "Blue Circle on Beige Canvas in Dark Room" to the DOM dynamically**

   *do this task in a separate JS file (e.g. main.js) that you embed in your HTML document*



![D3 - Bind Data 1](assets/cs171-activity-1.png?raw=true "D3 - Bind Data 1")

-----



### Binding Data to DOM Elements

> "Data visualization is a process of *mapping* data to visuals." - Scott Murray

The power of D3 lies in its ability to bind data to DOM elements, creating visualizations where each visual element represents a piece of data. Let's explore this fundamental concept.

#### The Data Binding Pattern

Here's how we create one paragraph element for each item in an array:

```javascript
const states = ["Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont"];

d3.select("body")
    .selectAll("p")
    .data(states)
    .enter()
    .append("p")
    .text("State name here");
```

Let's break down this pattern step by step:

**Step 1: Select the container**
```javascript
.select("body")  // Choose where to add elements
```

**Step 2: Select elements that don't exist yet**
```javascript
.selectAll("p")  // Select all paragraphs (even though none exist)
```
This might seem strange - we're selecting elements that don't exist! This creates an empty selection that D3 can work with.

**Step 3: Bind data to the selection**
```javascript
.data(states)  // Attach our array to the selection
```
The `data()` method creates a relationship between our data array and the DOM elements we want to create.

#### Understanding Enter, Update, and Exit

When you call `.data()`, D3 creates three virtual selections:

- **Enter**: Placeholders for data items that need new DOM elements
- **Update**: Existing DOM elements that have data bound to them  
- **Exit**: Existing DOM elements that no longer have data (for removal)

For now, we'll focus on the **Enter** selection, which handles creating new elements.

**Step 4: Access the enter selection**
```javascript
.enter()  // Get placeholders for missing elements
```

**Step 5: Create actual DOM elements**
```javascript
.append("p")  // Turn placeholders into real <p> elements
```

**Step 6: Set content**
```javascript
.text("State name here")  // Add text to each paragraph
```

#### Making Properties Data-Driven

Currently, all paragraphs show the same text. To make each element reflect its data, we use **anonymous functions**:

```javascript
d3.select("body")
    .selectAll("p")
    .data(states)
    .enter()
    .append("p")
    .text(d => d);  // 'd' represents each data item
```

![D3 - Bind Data 2](assets/cs171-d3-bind-data-2.png?raw=true "D3 - Bind Data 2")

#### Anonymous Functions in D3

D3 passes two parameters to your anonymous functions:
- **`d`** - the current data element
- **`i`** - the index (position) of the current element

```javascript
.text((d, i) => `${i + 1}. ${d}`)  // "1. Connecticut", "2. Maine", etc.
```

For more complex logic, use full function syntax:

```javascript
.text((d, i) => {
    if (d === "Massachusetts") {
        return `${d} (highlighted)`;
    }
    return d;
})
```

#### SVG Example: Data-Driven Rectangles

Let's create a simple bar chart using SVG rectangles:

```javascript
const data = [5, 10, 15, 20, 25];

// Create SVG container
const svg = d3.select("body")
    .append("svg")
    .attr("width", 400)
    .attr("height", 200);

// Create rectangles
svg.selectAll("rect")
    .data(data)
    .enter()
    .append("rect")
    .attr("x", (d, i) => i * 70)      // Position horizontally
    .attr("y", d => 200 - d * 4)      // Position vertically (higher values = lower y)
    .attr("width", 60)                // Fixed width
    .attr("height", d => d * 4)       // Height based on data
    .attr("fill", "steelblue");
```

**Key points about SVG positioning:**
- `x` attribute: We multiply the index by 70 to space rectangles apart
- `y` attribute: SVG coordinates start at top-left, so we subtract from total height
- `height` attribute: Multiply data values to make differences visible

*Result:*

![D3 - Bind Data](assets/cs171-svg-d3-barchart-example.png?raw=true "D3 - Bind Data")


#### Activity II

1. **Navigate to 'activity_2' and create a new D3 project inside the folder.**

2. **Append a new SVG drawing area to your HTML document with D3** (Width: 500px, Height: 500px)

3. **Draw circles with D3 dynamically!**

   *use the code snippets that we've provided above to append a new **SVG circle** for every object in the following array:*

   ```javascript
   let sandwiches = [
        { name: "Thesis", price: 7.95, size: "large" },
        { name: "Dissertation", price: 8.95, size: "large" },
        { name: "Highlander", price: 6.50, size: "small" },
        { name: "Just Tuna", price: 6.50, size: "small" },
        { name: "So-La", price: 7.95, size: "large" },
        { name: "Special", price: 12.50, size: "small" }
   ];
   ```
4. **Define dynamic properties**

	- Set the x/y coordinates and make sure that the circles don't overlap each other
	- Radius: *large sandwiches* should be twice as big as small ones
	- Colors: use two different circle colors. One color (```fill```) for cheap products < 7.00 USD and one for more expensive products
	- Add a border to every circle (SVG property: ```stroke```)
   
   
*The result might look like the following:*

![D3 - Result Activity 2](assets/cs171-d3-activity-2.png?raw=true "Result Activity 2")












-----


### Loading External Data

Instead of hardcoding data in variables, real-world visualizations typically load data from external files. D3 provides built-in methods to fetch data from various sources using modern JavaScript promises.

#### Data Format Overview

**CSV (Comma Separated Values)** is ideal for tabular data:
- Each line represents a row
- Columns are separated by commas
- First row typically contains column headers
- Simple, widely supported format

**JSON** is better for hierarchical or nested data:
- Supports complex data structures
- Native JavaScript format
- Ideal for APIs and structured data

> **Choosing the right format**: Use CSV for spreadsheet-like data (rows and columns), and JSON for nested or hierarchical data structures.

#### Creating a CSV File

Let's convert our sandwich data into a CSV file:

*Create `data/sandwiches.csv`:*
```csv
name,price,size
Thesis,7.95,large
Dissertation,8.95,large
Highlander,6.50,small
Just Tuna,6.50,small
So-La,7.95,large
Special,12.50,small
```

#### Loading Data with D3

D3 provides several data loading methods:
- `d3.csv()` - for CSV files
- `d3.json()` - for JSON files  
- `d3.tsv()` - for Tab Separated Values
- `d3.text()` - for plain text files

**Basic data loading:**
```javascript
d3.csv("data/sandwiches.csv").then(function(data) {
    console.log(data);
    // Process your data here
});
```

#### Understanding Promises and Asynchronous Loading

**Why use promises?** Data loading is asynchronous, meaning:
- The page renders immediately while data loads in the background
- Code that doesn't depend on data continues executing
- Data-dependent code waits until loading completes

**Example showing execution order:**
```javascript
console.log("1. This runs first");

d3.csv("data/sandwiches.csv").then(function(data) {
    console.log("3. This runs after data loads");
    console.log(data);
});

console.log("2. This runs second (before data loads)");
```

**Console output:**
```
1. This runs first
2. This runs second (before data loads)  
3. This runs after data loads
[{name: "Thesis", price: "7.95", size: "large"}, ...]
```


#### Data Type Conversion

**Important**: CSV data loads as strings! Convert numeric values explicitly:

```javascript
d3.csv("data/sandwiches.csv").then(function(data) {
    console.log("Before conversion:", typeof data[0].price); // "string"
    
    // Convert strings to numbers
    data.forEach(function(d) {
        d.price = +d.price;  // Convert to number
        // d.price = parseFloat(d.price); // Alternative method
    });
    
    console.log("After conversion:", typeof data[0].price); // "number"
    
    createVisualization(data);
});
```

#### Row Conversion Function

D3 allows data conversion during loading:

```javascript
d3.csv("data/sandwiches.csv", function(d) {
    // This function runs for each row
    return {
        name: d.name,                    // Keep as string
        price: +d.price,                // Convert to number
        size: d.size,                   // Keep as string
        isExpensive: +d.price > 7.0     // Create calculated field
    };
}).then(function(data) {
    console.log("Data already processed:", data);
    createVisualization(data);
});
```


-----

## Activity III

1. **Navigate to 'activity_3' and create a new D3 project inside the folder.**

   *notice that there's already a folder called 'data' that contains your dataset for this exercies, i.e. `cities.csv`*

2. **Use D3 to load the CSV file**

   Write the data to the *web console* and inspect it in your browser:

	- In which format is the information stored now?
	- Which properties are available?
	- Check the types of the variables in the console

3. **Prepare the data**

   *You might have noticed that each value of the CSV file is stored as a string, including numerical values.*

	- Convert all numerical values to *numbers*. (Otherwise you might see unexpected behavior when making calculations.)
	- We recommend iterating over each row to convert strings into floats. You can use this neat line of code:

    ```javascript
            d.age = +d.age;
   ```

4. **Filter the dataset**

   We are only interested in cities that are part of the *European Union (EU)*. In the remainder of the activity use the filtered dataset.

5. **Append a new paragraph to your HTML document**

   Count all elements in the filtered dataset and use D3 methods to write the result (i.e., the number of EU countries) to your webpage.

5. **Draw one SVG circle for each row in the filtered dataset**

	- All the elements (drawing area + circles) should be added dynamically with D3
	- SVG container: width = 700px, height = 550px
	- Use the x/y coordinates from the dataset to position the circles

7. **Dynamic circle properties**

   Change your default radius to a data-dependent value:

	- The radius should be **4px** for all cities with a population lower than 1.000.000.
	- The radius for all the other cities should be **8px**.

8. **Assign labels with the names of the European cities**

	- Use the *SVG text* element
	- All the elements should have the same class: ```city-label```
	- The labels should be only visible for cities with a population equal or higher than 1.000.000. You can use the SVG property ```opacity``` to solve this task.

9. **Styling**

   *Create a new external stylesheet if you have not done it yet.*

   Add proper styles to your webpage but include at least these CSS rules for the class ```city-label```:

	- Font size = 11px
	- Text anchor = middle

*Your result should look similar to this screenshot:*
![Activity 3 Result](assets/cs171-activity-3.png?raw=true "Activity 3 Result")


*Important notice: This example is not intended to be a best practice example of how to work with D3 scales. It was designed to help you to get a better understanding of different basic concepts in D3.*

Next week you will learn how to create real scales for different types of data, you will work with more flexible size measurements and you will learn how to use D3 axes in your visualizations.

&nbsp;

-----

#### Bonus Activities (optional!)

- Add a **D3 click event listener**.

  The d3 method .on() adds or removes a listener to each selected element for the specified event typenames.
  The typenames is a string event type, such as click, mouseover, or submit. When a specified event is dispatched
  on a selected element, the specified listener will be evaluated for the element, being passed the current event
  (event) and the current datum (d), with this as the current DOM element (event.currentTarget). In order to have access
  to this, however, we cannot use arrow functions. Have a look at this event listener:

    ```javascript
    .on("click", function(event, d){
        console.log('check out what you have access to', event, d, this)
    });
    ```

  Of course, you can do more than just writing something to the console here. For example, you could call other functions and pass along
  some information from the current selection.


- Change the **hover style** of the SVG circles.
