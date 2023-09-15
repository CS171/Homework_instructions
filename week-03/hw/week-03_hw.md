<!-----
layout: lab
exclude: true
----->

<img src="cs171-logo.png" width="200">

&nbsp;

# Week 03 | Homework

In this assignment, you’ll use HTML, CSS and JavaScript to create a small dashboard for a local pizza delivery company. It should help the company to get meaningful insights into their collected data and to evaluate their performance. We provide a template that will serve as your point of departure code.


This homework assumes that you have read and programmed along with chapter 3 (up to page 53) in *D3 - Interactive Data Visualization for the Web* (Second Edition) by Scott Murray.

![Homework Week 03](week-03-hw-banner.png?raw=true)

&nbsp;

&nbsp;

## 1. PizzaWorld - Insights & Statistics (4 points)

### Template

We are providing a small template (*Bootstrap* already included) for this homework. It is quite similar to the framework which we have used in this week's lab and should help you to get started. You can download the framework for this week's homework via canvas:
 [here's the link](https://www.cs171.org/Homework_instructions/week-03/hw/week-03_hw_template.zip)

When exploring the folder structure and its contents you will notice that we are providing all the files you need. Your only job is to 1) understand the code and 2) to extend the following files:

- ```index.html```
- ```css/style.css```
- ```js/main.js```


### Data

We have included two datasets from *PizzaWorld* in the framework. One table has 1198 rows with pizza deliveries and the other table has 200 rows with corresponding customer feedback.

The data (arrays with JSON objects) are already stored in these two global variables:

- ```deliveryData```
- ```feedbackData```

*The variables are accesible in the JS file ```main.js```*

*To get started, write the variables to the web console and inspect them.*

#### Delivery Data

- ```delivery_id```
- ```date```
- ```area``` (Boston | Cambridge | Somerville)
- ```price``` (in USD)
- ```count``` (number of delivered pizzas)
- ```driver```
- ```delivery_time``` (minutes)
- ```temperature```
- ```drinks_ordered``` (true | false)
- ```order_type``` (web | phone)


#### Feedback Data

- ```delivery_id``` (matches the deliveries)
- ```punctuality``` (medium | low | high)
- ```quality ``` (medium | low | high)
- ```wrong_pizza ``` (true | false)



### Implementation

1. **Download template**

	If you haven't done so already, please download the template [here](https://www.cs171.org/Homework_instructions/week-03/hw/week-03_hw_template.zip)

2. **Display dataset summary**

	Open ```main.js```. You'll find an empty function ```createVisualization()``` that you'll populate in order to update the DOM dynamically.
	Start by extracting the following numbers from the provided data and append them with
	meaningful labels to the HTML document:
	* Number of pizza deliveries
	* Number of all delivered pizzas (*count*)
	* Average delivery time
	* Total sales in USD
	* Number of all feedback entries
	* Number of feedback entries per quality category: *low*, *medium*, *high*

	→ You should do all of that (extracting numbers and adding labels to HTML) directly in JavaScript. Update the DOM dynamically with JavaScript!

	*Make sure you test your code after you have implemented this part! Once your code is working
	, consider your code structure and code design:*
	- *If your code is already longer than a couple of lines, extract it into a separate
	 function and call that function within *createVisualization()*.*
	- *Think about calculating the above numbers at the same time (e.g., inside a single loop), if
	 possible. That will make the code shorter and easier to read, as well as faster.*
	- *Make sure you use consistent spacing, layout, self-explanatory variable names, and code
	      comments! If you do this as you progress in your coding project, this will save you a
	       lot of time later!*

	**Hint:** Javascript has a number of native methods and properties that make interacting with HTML elements easy. For instance

	* ```document.getElementById('some_id')``` returns an element by its ID. You can then manipulate that element.
	* Once you've selected an element, you can get and set its text through the ```innerText``` property. So if you'd like to assign the current value to a variable do something like ```let elemText = document.getElementById('some_id').innerText``` and if you want to change that value do ```document.getElementById('some_id').innerText = 'New Value'```.
	* To add or retrieve the HTML within an element, use the ```innerHTML``` property (e.g. ```document.getElementById('some_id').innerHTML = '<h1>Title</h1>'```.)
	* The ```value``` property get and sets the value of ```input```, ```select```, and ```button``` elements.



3. **Call the function:** ***renderBarChart(deliveryData)***

	So far, you should have done all your DOM manipulation inside of ```createVisualization()```. If you call *renderBarChart()* our script will automatically group (and count) the deliveries per day. Subsequently a bar chart will be added to the container: ```#chart-area```.

	Requirements:
	- You need a div-container with the id ```#chart-area``` in your HTML document
	- As a **function parameter**, you have to include a JSON array with deliveries (each delivery is an object and must include at least the property: ```date```). Try to call *renderBarChart()* (inside ```createVisualization```) with the argument ```deliveryData```.

	→ You should now see a basic bar chart on your page.

4. **Filter the data before drawing the bar chart**

	In the next task, you should filter the ```deliveryData``` array depending on the selected options, before calling *renderBarChart()*.

	a. Add two **select-boxes** to your HTML document. The user should be able to select:

	- ```area``` (*All*, *Boston*, *Cambridge* or *Somerville*)
	- ```order type``` (*All*, *Web* or *Phone*).

	Make sure to set the callback function of the select boxes to the function that updates and creates our visualization!

	b. If the user selects an option, filter the variable ```deliveryData``` accordingly and then call *renderBarChart()* again. Every time you call this function, it will analyze all changes in your array and update the chart with D3.

	>It is good practice to do a sanity check on the result you get after filtering or processing data. Take a look at the original data, do the numbers make sense? Are there missing values? This is especially important when dealing with real-world data that has not been cleaned and prepared for easy use in a homework ;-)

5. **Global data filtering**

	In the previous step you have implemented a function which reacts to the user input (change of a select-box value) and updates the chart immediately.

	Additionally, these filter options should also affect the displayed dataset summary that you implemented earlier.

	→ If the user filters the data by a specific ```area``` or ```order type``` you should **update the bar chart and the display of the summary data** from step (2).

	*Hint: The data are stored in two separate variables. Make sure your filtering algorithm influences customer feedback as well as order data.*

6. **Style your webpage using CSS.**

	We already provided a simple css file in our template. Adjust either the CSS or the html elements you dynamically generate to create a visually pleasing and easy to read webpage.
	Lastly, make sure to include a tooltip ```div``` in your DOM. Check out  ```barchart.js``` and  ```style.css``` to understand why ```#tooltip``` is already working.
	```
        <div id="tooltip" class="hidden">
            <p><strong>Deliveries</strong></p>
            <p><span id="value"></span></p>
        </div>
	```   

&nbsp;

## 2. Infographic Design Critique  (5 points)

a. **First read the Design Critique Overview in Canvas.**

b. **Then look at this visualization of the top 10 salaries at Google:**  [![Creative Commons License](cs171-hw2-infographic.png)](https://www.jobvine.co.za/what-does-it-take-to-get-a-job-at-google/)

c. **Extend your previously created** `index.html` **file and add the following:**

- A screenshot of the salary visualization in the left column.
- An analysis of the visualization with answers to the following questions in the right column:
  - Who is the audience?
  - What questions does it answer?
  - What is the data? be specific, including data types (N,O,Q).
  - For each data type, how is it visually encoded?
  - Do you consider this to be a 'good' visualization? Why or why not?


***Add this information at the bottom of the website you created in step 1, below the Pizza World Visualization.*** *Use a two-column layout, where in the left column you show the screenshot and in the right column you add the answers to the questions above.*


## 3. Submit Homework in Canvas
a. Add your lab work in ```submission_FirstnameLastname/lab``` and add a text file telling us who your lab partner was called ```lab_partner.txt```

b. Put your JS homework in the folder structure ```submission_FirstnameLastname/hw/implementation```.


c. Zip your folder and upload it on Canvas for your homework submission.


Use the following recommended folder structure:

```
/submission_FirstnameLastname
	lab_partner.txt
	lab/
	hw/
	    implementation/
   	        index.html
	        css/ 		...folder with all CSS files
	        js/ 		...folder with all JavaScript files
	    ...
```
Note that you should add your name to the filename using CamelCase style, e.g., `submission_JohnDoe.zip` if your name is John Doe.

**Congratulations for finishing the homework for this week! See you in class!**

<!--

For your final submission you will have to:

- Click the 'submit' button
Double-check your 'latest submission', check that all the visualizations are working as you expect. You can run them directly in Vocareum and look at them in a new window
- Upload a teaser image of your homework (under 'Action'/'upload gallery thumbnail'. This teaser will show up in the classes gallery and should motivate other students to look at your solution in more detail.

After the homework deadline you will be able to:

- Look at the gallery with all other student submissions
- Give peer feedback or comments to other students (Please use proper manners and constructive criticism!)
- Give stars to other students' work (this will not influence grading!)
-->
