# Data Visualization Project

## Introduction

This visualization (viz) project will show by state the number of National Instant Check System (NICS) background checks that occured during selected years.  The NICS background check data was obtained from https://github.com/BuzzFeedNews/nics-firearm-background-checks.  The visualization will be a stacked bar chart of the NICS background check data for each state along the horizontal axis.  The vertical axis will provide the totals.  The stacked bar chart will be formed from the four types of background checks presented in the data.  

Here is some information on the data.  The data contains four categories of background checks:
1. Handguns
2. Long guns
3. Other
4. Multiple

Categories 1, 2, and 4 are self explanatory.  Category 3 is not self explanatory.  What Other consists of are items that are frames (instead of completed firearms), National Firearms Act (NFA) weapons (ie, silencers, machine guns, etc...), and other firearms that are neither handguns nor long guns.  The data ranges from years 1998 to 2023.


## Questions the VIZ will Answer

The following questions drove the visualization and interaction decisions for this project:

 * What are the total number of background checks performed for the selected state?
 * How many background checks are performed for each category of background check for each state?
 * How do the background check totals vary over time?
   
## Anticipated Challenges

These are some of the challenges I forsaw in creating this viz.

 * How to convert the provided month-years to useable date formats
 * How to make the data show the total for each year and by type of check (without having do modify the csv data to include totals)
 * How to make a legend with years that are selectable such that the data for each state appears for the selected year

## Putting Ideas to Paper

The following sketch conceptualized the direction the visualization would go.

![Sketch 2](https://github.com/user-attachments/assets/c2deb32d-e055-4cba-9ea9-b99cb1e4b413)


The sketch shows the data in stacked bar chart form with each state on the horizontal axis and totals on the vertical axis.  The stacked bars form the total of each type of check with the total bar length being the sum of the stacked bar.  On the right hand side of this conceptualization is a legend that allows the user to select from the available years the data is available for.  


## Barchart
The initial work on the NICS stacked bar chart includes all the years in the dataset.  There is a drop down menu to make the year shown above the legend on the right hand side of the viz, selectable by the user.  There is an addtional drop down to allow the user to show the top 10 states, the top 25 states, or all states.  A pop up as been added to the viz that appears when a user hovers over a bar to show the totals of each type of background check for that state.  The following pictures show these visualization actions:

<img width="1259" height="577" alt="Top 25 States 2023" src="https://github.com/user-attachments/assets/ddefbe92-c2fa-460b-859a-613f47e758e6" />
<img width="1251" height="575" alt="Top 25 States 2009" src="https://github.com/user-attachments/assets/ac28069e-2641-4dc0-8938-d6a8fa1fb937" />
<img width="1262" height="563" alt="Top 10 States 2023" src="https://github.com/user-attachments/assets/d09188cf-573d-45dd-9913-90639365170e" />
<img width="1261" height="568" alt="Top 10 States 2009" src="https://github.com/user-attachments/assets/3fd8f306-dd81-446d-a63e-0e774b29e62e" />
<img width="1263" height="577" alt="Pop up" src="https://github.com/user-attachments/assets/8e999d08-efb6-4994-95bb-3d906d4673c4" />
<img width="1264" height="573" alt="All States 2023" src="https://github.com/user-attachments/assets/951acc7b-1ffb-43bf-b32a-39de76d22470" />
<img width="1259" height="576" alt="All States 2009" src="https://github.com/user-attachments/assets/ea158a7b-7f51-416d-a1f2-9c7e6eae743d" />

This is the link to this iteration the bar chart viz: https://vizhub.com/rkupferwpi/bbb53529f42e425285b5f0e67fc74664

## Barchart Interactivity

Interactivity has been added to the legend on the bar chart such that when the user hovers over the specific type of NICS check the opacity of the other types changes.  When the user moves away from the legend the opacity returns to 1 for all types.  Additionally, the legend, the year selector, and the top counts have been repositioned.  

This is the link to this iteration of the viz in vizhub:
https://vizhub.com/rkupferwpi/5f7d5f65164c4f2e8d9355f42a40df43

Here is the result when I hover over handguns:

<img width="1264" height="573" alt="Handguns" src="https://github.com/user-attachments/assets/eb2541e2-8c19-423a-9636-0d9c3d16b500" />

When I hover over long guns:

<img width="1262" height="570" alt="Long guns" src="https://github.com/user-attachments/assets/a9d57ddf-c7fc-4374-9e7b-b0811fb4652f" />

When I hover over multiple:

<img width="1263" height="573" alt="Multiple" src="https://github.com/user-attachments/assets/6781116b-fcd8-411a-ba78-4b9d8f83568b" />

When I hover over other:

<img width="1266" height="571" alt="Other" src="https://github.com/user-attachments/assets/4ef943f3-8312-4726-914a-d798f3aa803f" />

## Additional Barchart Interactivity

The following interactivity has been added to the bar chart vis of NICS background checks.  A sort drop down menu that allows the user to organize the bar chart by most to least checks, least to most checks, and alphabetical by state.  Also, code has been added to move the legend when least to most checks is selected so the bars don't interfere with the legend.

Here are screenshots of these effects.
Most to least:
<img width="1263" height="573" alt="Most to Least" src="https://github.com/user-attachments/assets/9cb5c51d-25b9-4e47-94c1-3fe4c6db65fc" />

Least to most:
<img width="1263" height="578" alt="Least to Most" src="https://github.com/user-attachments/assets/e2512458-2767-4d4f-996c-3e874ccd91cb" />

Alphabetical by state:
<img width="1262" height="577" alt="Alphabetical by State" src="https://github.com/user-attachments/assets/27c0947c-6593-420d-b218-620c7c1a2a30" />

Here is the link to the current iteration: https://vizhub.com/rkupferwpi/767dedbf8ecc45959057128399e4d899

## Barchart Polishing

I've updated the bar chart with a title, adjusted the drop down selector positioning, and the legend positioning.  I've also changed the background color to a softer color.

Here is an image of the viz:
<img width="1261" height="577" alt="Bar Chart Polishing" src="https://github.com/user-attachments/assets/13c3b5c4-0c8f-4fb8-a1e6-bd82051fd3b9" />

Here is the link to the VIZ: https://vizhub.com/rkupferwpi/ea9f228118024d6a83ce94d9a6c05843

## Barchart Further Polishing

After additional polishing of the stacked barchart, the total number of NICS background checks for each state is shown by stacking the total of each of the four categories of background checks - handgun, long gun, other, and multiple.  The default ordering of states is descending from most to least number of NICS checks.  However, the ordering is user selectable from least to most, most to least, and alphabatized by state name.  Additionally, the user can select the year they want to view from 1998 to 2023 and the can also narrow the view to the top 10, top 25, or all states.  The user can hover over each category in the legend to highlight that category in each bar.

This is the link to this polished version: https://vizhub.com/rkupferwpi/ea9f228118024d6a83ce94d9a6c05843

## Barchart Final Product

The link to the final product barchart is: https://vizhub.com/rkupferwpi/83fd0ab4095847ef8e445f1e09595633

