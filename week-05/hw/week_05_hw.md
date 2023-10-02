<!-----
layout: lab
exclude: true
----->

<img src="cs171-logo.png" width="200">

&nbsp;

# Week 05 | Homework

&nbsp;

![Homework 5](cs171-hw5-banner.png?raw=true "Homework 5")

# CS171 - Homework 5

This homework requires that you have read and programmed along with chapters 7 and 8 in *D3 - Interactive Data Visualization for the Web*.

&nbsp;

## 1) Za'atari Refugee Camp (8 points)

Za’atari is a refugee camp in Jordan that opened in 2011 to host people fleeing from the Syrian civil war. With around 80,000 refugees it is one of the largest UN-supported camps and over the past few years it transformed from a tent camp to a real city with water and sewage systems, markets, coffee shops etc.


*In this homework you will create two charts to present data from Za'atari in a meaningful way.*

### Data

#### Population

As part of this homework assignment we provide a CSV file with population statistics between January 2013 and November 2015. The statistics are based on active registrations in the UNHCR database.

[zaatari-refugee-camp-population.csv](https://www.cs171.org/Homework_instructions/week-05/hw/assets/zaatari-refugee-camp-population.csv)

#### Type of Shelter

The REACH initiative and Unicef evaluated the type of shelters in the Za'atari refugee camp. Although, the camp is gradually transforming into a real city, a lot of people still have to live in tents:

> The vast majority of households (79.68%) were recorded as living in caravans. That number was followed by 10.81% of households recorded as living in a combination of tents and caravans, while 9.51% were observed to be living in tents only.

&nbsp;

### Implementation

1. **Download the data**

	Please download the CSV data: [zaatari-refugee-camp-population.csv](https://www.cs171.org/Homework_instructions/week-05/hw/assets/zaatari-refugee-camp-population.csv)

2. **Set up a new D3 project and create a two-column layout in your HTML file**
	During the course of this homework you will add an area chart to the left column and a bar chart to the right column.

	![Homework 5 - Preview](cs171-hw5-preview.png?raw=true "Homework 5 - Preview")

3. **Load the CSV file and prepare the data for the area chart**

	The *dates* are loaded as string values. Similar to numeric values (e.g. ```d.price = +d.price```) you have to convert these values. You will need *Date Objects* to create flexible *time scales* later.

	*This website should help you to convert the data into the right format: [https://github.com/d3/d3-time-format/blob/master/README.md](https://github.com/d3/d3-time-format/blob/master/README.md). Make sure to test your results before continuing.*

4. **From now on, your charts should implement the D3 margin convention**

	Create ```margin```, ```height```, and ```width``` variables and append a new SVG drawing space for the area chart to the HTML document via JavaScript.

5. **Area chart: Before you create the actual area chart, create linear scales for the x- and y-axes**

	Use the ***D3 time scale function*** for the x-axis.  It is an extension of *d3.scaleLinear()* that uses JS date objects as the domain representation.

	*Read more about D3's time scales: [https://github.com/d3/d3-scale/blob/master/README.md#time-scales](https://github.com/d3/d3-scale/blob/master/README.md#time-scales). You can (and should) always google for additional examples, if you are still unclear on the usage of D3 elements we require you to include.*

6. **Area chart: Map the population data to the area (using SVG path)**

	*Compared to a simple line chart you should fill the whole area between the data points and the x-axis.*

	To create an area chart, follow the steps below:

	a. Define a function that generates the area:

	See [https://github.com/d3/d3-shape/blob/master/README.md#areas](https://github.com/d3/d3-shape/blob/master/README.md#areas) (```d3.area()```) for details.

	b. Draw the area (using an SVG path element)

	```javascript
	let path = svg.append("path")
      .datum(data)
      .attr("class", "area")
      .attr("d", area);
	```

	c. Change the style with CSS

	If any of these steps are unclear, study some D3 area chart examples online. Make sure you understand the code before you implement it yourself!

	d. Bonus (optional): Render the actual boundary (upper line of the area chart) as line, with different visual properties.

7. **Area chart: Append the x- and y-axes and add a chart title**

	From now on, we expect that you will always label your charts, display meaningful axes, and provide a legend if necessary. Also, make sure your axes start at appropriate values.
	In data visualization we aim to create meaningful, easy-to-understand visualizations to provide insight into the data. Missing labels or axes are often a main cause for misunderstanding data!

	* Format the labeling of the x-axis to display the month and year in text format (e.g. April 2013).
	* Make sure that the labels don't overlap each other, by rotating the text labels of the x-axis.

8. **Create a compound JS data structure to store information about the shelter types**

	Store the information you have about the different shelter types in your own data structure. (As a reminder, 79.68% of households were recorded as living in caravans. 10.81% of households live in a combination of tents and caravans, while 9.51% live in tents only.)

	* Store the *type of shelter* and *percentage values*.
	* You will have to use your data structure for your bar chart afterwards, so make sure that it is as simple and efficient as possible. The actual implementation is up to you.

9. **Create a vertical bar chart for the camp's three shelter types**

	* Append a new SVG drawing area for the bar chart (using D3 margin conventions) to the right column of your webpage.
	* Map the data from your new dataset to SVG rectangles to create a vertical bar chart (refer to the screenshot in Section Implementation.1 for how it should look). The y-axis represents the percentage of people living in one of the three shelter types.
	* Usa a linear scale for the y axis.
	* For the x dimension you may choose to use either an ordinal scale or no explicit D3 scale function, as there are only 3 categories. (Note, however, that in one of the next steps you will have to add labels for each bar. Your scale implementation here affect the way you add labels later.)
	* Add a chart title.

10. **Bar chart: Draw x- and y-axes**

	*The ticks of the y-axis should be formatted as percentages.*

	[https://github.com/d3/d3-axis/blob/master/README.md](https://github.com/d3/d3-axis/blob/master/README.md)

11. **Bar chart: Append labels at the top of each bar to indicate the actual percentages**

	* Each bar should have a label to indicate the percentage, directly above the bar.
	* Each bar should also have a label with the name of the shelter type. This can be done either by using a categorical x axis, or by manually adding text labels.

12. **Create dynamic tooltips for your area chart**

	![Area Chart Tooltips](cs171-hw4-tooltips.gif?raw=true "Area Chart Tooltips")

	*There are many different ways to include tooltips. Follow the steps below for one approach, but feel free to experiment with others*

	Make sure the tooltip shows the camp's population for the current mouse position, as shown in the above animation.

	Note: This step is relatively complex, compared to the earlier steps. Add individual elements step-by-step and make sure they are working before adding on more elements. Debugging tip: during development, add color to your elements through css styles to ensure they are being rendered properly.

	* Create a group for all the tooltip elements and hide it by setting the style attribute 'display' to 'none' (Skip this step during development to make sure you are rendering things correctly). Save this element as a variable, which you will use to append text elemenet and later update the tooltip position. Give it a class name.

    * Append a vertical tooltip line to the leftmost position of the group (x=0) and that spans the full height of the svg.  Don't forget to assign the 'stroke' attr for it to render properly!

	* Append an empty SVG text element for the tooltip population value. place it 10px away from the top left corner of the group, and don't forget to give it a class or id!

    *  Append an empty SVG text element for the tooltip date value. Position this text just below
   the population text holder. Give it a unique class or id name.

	* Append a rectangle over the whole chart to capture 'mouse events'. Add listeners to 'mouseover', 'mouseout', and 'mousemove' events. On mouseover, set the display style of the tooltip group to 'null, on mouseout set it to 'none', and on mousemove, trigger a new 'mousemove' function that will handle the positioning of the tooltip.

	* ```d3.bisector```is a function that finds the closest index in an array for a given value, specifying an accessor function.  You can read more about it here: [https://github.com/d3/d3-array#bisector](https://github.com/d3/d3-array#bisector)

	* For this homework, you will need to define a bisector that returns the date attribute, such as the example below. This can then be applied as bisectDate(array, d), returning the index of  the array which contains the closest value to 'd'.

        ```javascript
        let bisectDate = d3.bisector(d=>d.date).left;
        ```

    * Write a mousemouve function with the following signature:

        ```javascript
        function mousemove(event){
            //code goes here
        }
        ```

	* Inside this function implement the following steps:

		* Use d3.pointer(event)[0] to get the x position of the mouse pointer.

	    * Use .invert on the xscale to find the equivalent date value for the x position of the
	     mouse pointer.

		* Call the previsously declared bisector function to get the index of the closest date in
		 the original data array.

		* Use the index from the previous step to grab the data element at that location.  

	    * Shift the whole tooltip group on the x-axis to the position of the mouse.

	    * Update the tooltip text properties with the date and population values

13. **Use CSS to style the webpage**

	*Spacing between charts, font size, color scheme, ...*

	This is your space to be creative! Please use at least 3 CSS styles, and keep the design guidelines you have learned so far in lecture in mind. But you don't need to go overboard. (Required are 3 different CSS styles)

&nbsp;

Congratulations on finishing your homework! Up until now, all your visualizations have been static (i.e., the initial visualization did not change after first rendering). Over the next couple of weeks you will learn how to dynamically update visualizations, and how to create dynamic transitions. You will also learn how to link two or more visualizations together, so that the interaction in one view will automatically trigger an update of the second view!

## 2) Visual Vocabulary (2 points)
Use the [visual vocabulary](https://bit.ly/miro-visual-vocabulary) to decide which visualization types would best fit the following prompt:

```
Compare available houses on the market in regards to size, price, number of amenities, and distance to the closest supermarket.
```

* Pick 3 visualizations that you could use to answer parts or all of the above prompt.
* Create a hand-drawn sketch for each of the 3 visualizations (3 sketches overall). Make sure to add titles, axes, axis labels, and labels.
* Add a short paragraph for each visualization where you describe why you picked a certain visualization, why it works well for the above prompt, and how you encode the data in the visualization.

## 3) Optional: `Dear Data' Competition: Visualizing Personal Data


If you collected data for your personal Dear Data project last week, you can sketch a visualization this week that encodes the personal data you collected last week using creative, artistic, and whimsical visual encodings inspired by the Dear Data project. Similar to Georgia Lupi and Staphanie Posavec, we want you to sketch your visualizations by hand, either using pen and paper or a tablet and electronic pencil. As you know from last week's homework, the student with the best Dear Data visualization, as determined by our TFs, will **win a copy of the Dear Data book**!

**Why sketches?**

We previously talked about the various advantages of sketches. They are cheap, easy to create, easy to throw away, and they seem to increase the depth of discussions and reflections. Another advantage is that sketches allow you to **iterate on your visualization ideas**. It is never the case that your first sketch is the best you can come up with. As Nadieh Bremer, accomplished visualization designer, says:

It makes me feel more human/normal to think that the people I admire also didn’t come up with their final dataviz in one perfect go. - Nadieh Bremer


Sketching allows you to reflect and refine your visualizations. Take a look at some of the blog posts that Nadieh and Shirley Wu wrote for their [Data Sketches](https://www.datasketch.es) project, and you will see many iterations of hand-drawn in addition to code sketches. As an aside, the Data Sketches book would also be a great addition to your visualization library.

**Final sketch**

Once you got your inspiration, sketched a few ideas, and iterated on them, it is time to create your final sketch. Again, you can use pen and paper or a tablet and electronic pencil for this. We do not want you to be constrained, so you can **use any page size or format** that you like. Please use thick strokes and bold colors that are easy to see from a distance and that will reproduce well once you take a photo of your sketch (assuming it was done on paper). As before, we want you to use **at least five** of your data attributes in your final sketch.

Similar to the Dear Data project, we also want you to **create a legend that explains how each of your data attributes is visually encoded**. The legend can be drawn on a separate piece of real or electronic paper. Again, make sure to use thick strokes or large fonts to make the writing easy to read. If you like, you can also add the legend directly to your sketch using lines and arrows that make the connection from your visuals to your data. Please also **add a paragraph where you briefly explain your sketch to us** (e.g., what data you collected, what you show, and why you chose that encoding).

**How to submit your project**

If you drew using pen and paper, take pictures of your sketches and legends, and if you used a tablet and electronic pencil you can export the electronic pages. Combine all of the images in a pdf and label them to make it clear what they show. You can use a google doc to collect everything and then export it to a pdf). Please make sure that your images are big enough to make the visuals and text easily legible. You can include your reflection as typed text after the embedded images in your homework document.

## 4) Submit Homework in Canvas

Submission instructions:

*  Use the following recommended folder structure to submit your hw:

```
/submission_FirstnameLastname 	
	hw/
	    implementation/ ...folder for your code
   	        index.html
	        css/ 		...folder with all CSS files
	        js/ 		...folder with all JavaScript files
			dear_data/
					dear_data_submission.pdf

```

*  Make sure to keep the overall size of your submission under 5MB! Sketches don't have to be in the highest resolution, but should still be readable.

*  Upload a single .zip file.

**Congratulations for finishing Homework 5! See you in class!**
