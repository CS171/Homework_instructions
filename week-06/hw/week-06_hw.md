
<!-----
layout: lab
exclude: true
----->

<img src="cs171-logo.png" width="200">

&nbsp;

# Homework 6

This homework requires that you have read Case 1 of the article:
[https://medium.com/@mbostock/what-makes-software-good-943557f8a488](https://medium.com/@mbostock/what-makes-software-good-943557f8a488)

Optional reading: [Mike Bostock's 'Thinking with Joins'](http://bost.ocks.org/mike/join/), and chapters 9-10 in *D3 - Interactive Data Visualization for the Web*.

## 1) FIFA World Cup™ - All Time Statistics (7 points)

> The FIFA World Cup™ is the biggest single-event sporting competition in the world and is played by the senior men's national teams from the 209 Member Associations of FIFA. The competition has been played every four years since the inaugural tournament in 1930, except in 1942 and 1946 when it was not held because of the Second World War.
> 
> The 20 FIFA World Cup tournaments have been won by eight different national teams.
> 
> *FIFA ([http://www.fifa.com/fifa-tournaments/statistics-and-records/worldcup](http://www.fifa.com/fifa-tournaments/statistics-and-records/worldcup))*

### Template

To help you get started with this homework assignment we have prepared a template that you can use. It is based on the front-end framework *Bootstrap* and it includes *D3*,
Furthermore, a CSV file (```fifa-world-cup.csv```) is stored in the folder *"data"*. Of course, you can also start with an empty project and just copy the dataset.

[week-6\_hw\_template.zip](https://www.cs171.org/Homework_instructions/week-06/hw/week-6_hw_template.zip)

### Overview

A D3 line chart will be the core component of your visualization. The x-axis represents the time period and the y-axis will show the attribute of the current user selection: **goals**, **average goals**, **matches**, **teams** or **average attendance.** Additional input fields allow the user to limit the time frame that is shown. If you click on an event, detailed information is visible in a separate container to the right of the chart.

*You can use the following mockup as a guide:*

![Homework 5 Mockup](cs171-hw5-mockup.png?raw=true "Homework 5 Mockup")

### Implementation

1. **Download the resources**

	Please download the template and the CSV file as a ZIP file: [week-6\_hw\_template.zip](https://www.cs171.org/Homework_instructions/week-06/hw/week-6_hw_template.zip)
	
2. **Familiarize yourself with the provided framework and the FIFA World Cup data**

	*main.js*
	
	- The script creates a new SVG drawing area inside the container ```#chart-area```
	- We have separated the loading of the CSV file and the update sequence. The function ```loadData()``` reads the data and saves it in the variable ```data```. The function ```updateVisualization()``` should include all the dynamic chart elements and should be called every time something changes. Beyond that, feel free to customize the structure according to your preferences.
	- We have used the D3 time formatting function to parse string values (year the world cup was held) to *date objects*. You can read more about D3 time formatting here: [https://github.com/d3/d3-time-format/blob/master/README.md](https://github.com/d3/d3-time-format/blob/master/README.md).

		If you want to convert it back - to a year value with four digits - you can use: *formatDate(d.YEAR)*
		
		```javascript
		let formatDate = d3.timeFormat("%Y");
		let parseDate = d3.timeFormat("%Y");
		
		let newDate = parseDate("2020");
		newDate  // Returns: Wed Jan 01 2020 00:00:00 GMT-0500 (EST)
		let year = formatDate(newDate);
		year 	 // Returns: "2020"
		```
		
3. **Create scales and axis functions**

	- Create the inital scales and axes. Make sure to pick appropriate scales, especially for the x axis!
	- Keep in mind that you should update the input domains each time the data changes.
	- We recommend that you first implement the y-axis for showing the data attribute *"goals"*. After you have implemented the initial line chart, you will then connect your visualization with a select box to create a dynamic y-axis (in Activity II, part 6). This will allow the user to interactively change the attribute that is being visualized on the y axis.


4. **Use the ```d3.line``` function to map the data to an SVG path and draw the line chart**

	- Read more about D3's path generator: [https://github.com/d3/d3-shape/blob/master/README.md#lines](https://github.com/d3/d3-shape/blob/master/README.md#lines)
	- Create a path by using the d3.line function. 
	- Try different values for the ***curve*** property (e.g., *d3.curveLinear*, ...) and choose a setting that fits best.
	- Make sure that you can update the path with new data afterwards
	- Debugging hint: Make sure you only draw a single path!

	*Important: Usually, in D3 you map your data elements to the same number of visual elements (e.g., circles). Here, you will map all your data elements to a single path. This is reflected in a different way to create and update your path, different to the standard enter/update/exit methods. Also, you might want to look at the difference between data and datum in D3.*
	
5. **Draw the axes**

	- Append the axis components to the drawing area only once
	- The axis functions must be called every time the data changes

6. **Emphasize the data points on the D3 line graph**

	- Append an SVG circle on each x/y intersection *(20 tournaments = 20 circles)*
	- The points are meant to highlight the individual events.
	- Use the D3 update pattern: enter, update, exit

7. **Implement a dynamic y-axis**

	The user should be able to switch between different data attributes for the y-axis:
	- Goals
	- Average Goals
	- Matches
	- Teams
	- Average Attendance

	Create an HTML select box and react to changes in your JS code (update scale → redraw visual elements). The default value should be the *number of goals*. The x-axis shows the time frame and always stays the same.
	
	*Make sure that your code stays well-structured and understandable, especially after these types of modifications.*

8. **Include smooth, animated transitions whenever something in the visualization changes**

	Instead of jumping from one state to another, perform a smooth transition when the user selects a different mode (y-axis value). The duration of the transition should be *800ms*.
	- Add transitions to the path, the overlayed circles, and the axes
	

9. **Implement a time period filter**

	*Enable the user to limit the visible FIFA World Cups to a specific time frame.*
	
	- Create two HTML input fields (lower and upper bound) and a button to update the visualization. Optionally, if you feel confident in JavaScript and were able to finish the last steps quickly, you can also implement a range slider.
	- The default values should cover the whole time period of the data (20 FIFA World Cups).
	- After the user modifies the time frame you have to filter the dataset, update the scales/axes and redraw the SVG elements (```updateVisualization()```).
	- You don't need to worry about error handling here. We expect that the user enters a valid time frame.
	- Adjust the transition of the circles and the path in the line chart: Think about how you can best visually represent the filtering action in the transition. The transition should be intuitive and not break the mental model the user has of the data. Use the animation below as guidance.
	
	![Time Filtering](time_filtering.gif?raw=true "Time Filtering")

10. **Show the details for a single FIFA World Cup edition**

	*If the user clicks on an SVG circle on the line graph, the invidual statistics for this specific event should be displayed in a separate container beside the chart.*
	
	- Extend your HTML structure to display the additional information
	- Create a ***click listener*** for the SVG circles.
	- We have prepared an empty function ```showEdition(d)```. You can call it with the data of the selected event and implement the logic there. Re-factoring code into separate functions is a crucial factor for maintaining the readability and extensibility of your programs. Your D3 update sequence remains compact and you can reuse the functions.
	- Use *JS functions* and *D3* to update the HTML content with all the available information for a FIFA World Cup edition: *title, winner, goals, average goals, matches, teams, average attendance*.

11. **Create a proper style for your webpage**

	Maintain good spacing between UI components, overall layout, font size, color scheme, etc. Also, make sure that transitions are intuitive and clear.


## 2) Design Creation and Explanation (3 points)

In a previous homework, you had a chance to familiarize yourself with the following infographic. This week, we want you to get creative!

[![Creative Commons License](cs171-hw2-infographic.png)](https://www.jobvine.co.za/what-does-it-take-to-get-a-job-at-google/)

- **Create 2 sketches that redesign the Google salary visualization.**
- For each of your two sketches write down which questions your sketch answers
- Both sketches should cover different aspects of the visual vocabulary (class material of week 5), explain your choices.
- Name and justify all your changes you made using C.R.A.P. and Gestalt principles that you've learned class.
- We expect you to write a text in the range of 200-400 words.
- Write the text with your computer.
- Take a picture of your sketch or scan it.
- Create a PDF (creation.pdf) that contains both the sketch and your explanation/justification.
ß

## 3) Bonus Task (1 point)

Please make sure to finish all previous tasks before you start with the bonus activity. Extra credits are only given if the rest of the homework has been completed and the full possible points have been received. This task is intended for those of you who have already more experience with web development and JS libraries.

Implement a range slider in your project, instead or in addition to the input fields. The user should be able to select a specific time period and the line chart should get updated automatically. If you want to explore more facets of the powerful D3 library you can try to implement the slider either with D3 or you can use another JS library, such as NoUiSlider ([http://refreshless.com/nouislider/](http://refreshless.com/nouislider/)). The range of the slider should be extracted dynamically from the dataset. Please use labels or tooltips to indicate the chosen time period.

*Example:*

![Homework 5 Range Slider](cs171-hw5-range-slider.gif?raw=true "Homework 5 Range Slider")



## 4) Submit Homework in Canvas

Submission instructions:

1. Use the following recommended folder structure:

```
/submission_FirstnameLastname	
	lab_partner.txt	
	hw/
	    implementation/ ...folder for your code
   	        index.html
	        css/ 		...folder with all CSS files
	        js/ 		...folder with all JavaScript files
		design/ ... folder for your design partß 
		
	lab/
	    ...
```

2. Make sure to keep the overall size of your submission under 5MB! 
3. Upload a single .zip file.


**Congratulations for finishing Homework 6! See you in class!**

