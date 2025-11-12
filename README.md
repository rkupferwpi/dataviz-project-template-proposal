# Data Visualization Project

## Introduction

The visualization (viz) project I propose to create is on that shows by state the number of National Instant Check System (NICS) background checks that occured during selected years.  The data NICS background check data was obtained from https://github.com/BuzzFeedNews/nics-firearm-background-checks.  My primary goal is a map of the US that shows the NICS background check data for that state as a pop up when the user hovers over a state.  Simultaneously, I'm working on a stacked bar chart to show the NICS background check data to present as my visualization if I'm not successful with my primary goal visualization.


## Questions & Tasks

The following tasks and questions will drive the visualization and interaction decisions for this project:
## Questions
 * What are the total number of background checks performed for the selected state?
 * How many background checks are performed for each category of background check for each state?
 * How do the background check totals vary over time?
## Tasks
 * How to convert the provided month-years to useable date formats
 * How to load in a map of the US that shows each state
 * How to associate the state names data with the map boarders
 * How to hover over or click on a state and obtain the data
 * How to make that data appear in a bubble over the state
 * How to make the data show the total for each year and by type of check (without having do modify the csv data to include totals)
 * How to make a legend with years that are selectable such that the data for each state appears for the selected year

 

## Sketches

![Sketch 1](https://github.com/user-attachments/assets/86a18823-b548-4693-985d-c8444ea128ce)

![Sketch 2](https://github.com/user-attachments/assets/c2deb32d-e055-4cba-9ea9-b99cb1e4b413)

Sketch 1 shows the data as I would like to present it, as a map of the US where the user can hover over a state (or click on a state) and have a bubble appear that shows the total background checks in the state and the total of each type of background check.  On the right hand side is a legend that allows the user to select from the available years the data is available for.

Sketch 2 shows the data in stacked bar chart form with each state on the x-axis and total on the y-axis.  The stacked bars form the total of each type of check with the total bar lenght the sum of the stacked bar.  On the right hand side is a legend that allows the user to select from the available years the data is available for.  As a bonus, if I went with this visualization, it would be interesting if it could play each year on it's own so one could see the changes in numbers of background checks over time.



## Prototypes

Currently I only have one year of data that I've loaded which was the exercise about how to load csv data.
import { csvParse, select } from 'd3';

export const viz = (container, { state, setState }) => {
  select(container)
    .selectAll('pre')
    .data([null])
    .join('pre')
    .text(JSON.stringify(state.data, null, 2));

  // state.data could be:
  // * undefined
  // * 'LOADING'
  // * An array of objects
  const { data } = state;

  if (data === undefined) {
    setState((state) => ({
      ...state,
      data: 'LOADING',
    }));
    fetch('data.csv')
      .then((response) => response.text())
      .then((csvString) => {
        const data = csvParse(csvString);

        for (const d of data) {
          d.month = d.month;
          d.state = d.state;
          d.handgun = +d.handgun;
          d.long_gun = +d.long_gun;
          d.other = +d.other;
          d.multiple = +d.multiple;
        }

        setState((state) => ({
          ...state,
          data,
        }));
      });
  }
};

The result was:
[
  {
    "month": "2023-09",
    "state": "Alabama",
    "handgun": 15421,
    "long_gun": 12848,
    "other": 1156,
    "multiple": 1052
  },
  {
    "month": "2023-09",
    "state": "Alaska",
    "handgun": 2429,
    "long_gun": 2543,
    "other": 262,
    "multiple": 197
  },
  .
  .
  .
  

## Open Questions

I’m not sure where to get the geographic shapes to build a map from this data nor am I confident that I'll be able to associate the state name in the csv to the map data.  I'm also not confident about making the data selectable by year.

## Milestones

By the end of week six I would like to at least get the date in the csv into a working date in d3 and I would like to get the entire data set loaded and to figure out the coding to at least get the total number of checks by state.

## UPDATE 1

I loaded the map of the US showing just the state borders.  I was about to give up on the map idea and just do the bar chart but then I remembered to use the AI.  I would not have been able to do this without the use of AI.  I find this extremely discouraging.  Here is a picture of the map.

<img width="962" height="501" alt="US Map With States" src="https://github.com/user-attachments/assets/4e179e32-bb64-4696-9215-b1be71f8df73" />

## Here is the index.js code

import { select } from 'd3';
import topojson from 'topojson-client';
import { map } from './map';

const worldAtlasURL =
  'https://unpkg.com/visionscarto-world-atlas@0.1.0/world/110m.json';

const usStatesURL =
  'https://unpkg.com/us-atlas@3.0.0/states-10m.json';

export const main = (container, { state, setState }) => {
  const width = window.innerWidth;
  const height = window.innerHeight;

  const svg = select(container)
    .selectAll('svg')
    .data([null])
    .join('svg')
    .attr('width', width)
    .attr('height', height);

  // state.data could be:
  // * undefined
  // * 'LOADING'
  // * An array of objects
  const { data } = state;

  if (data && data !== 'LOADING') {
    svg.call(map, {
      data,
    });
  }

  if (data === undefined) {
    setState((state) => ({
      ...state,
      data: 'LOADING',
    }));
    fetch(usStatesURL)
      .then((response) => response.json())
      .then((topoJSONData) => {
        const data = topojson.feature(
          topoJSONData,
          topoJSONData.objects.states,
        );
        setState((state) => ({
          ...state,
          data,
        }));
      });
  }
};

## Here is the link to the file on VizHub:
https://vizhub.com/rkupferwpi/1362d30acea64463912d010ce1fa7b5f

## UPDATE 2 Week 7
I have updated my NICS stacked bar chart to include all the years in the dataset.  I've added a drop down to make the year shown selectable by the user.  I added an addtional drop down to allow the user to show the top 10 states, the top 25 states, or all states.  I've also added a pop up that appears when a user hovers over a bar to show the totals of each type of background check for that state.  Here are some pictures:

<img width="1259" height="577" alt="Top 25 States 2023" src="https://github.com/user-attachments/assets/ddefbe92-c2fa-460b-859a-613f47e758e6" />
<img width="1251" height="575" alt="Top 25 States 2009" src="https://github.com/user-attachments/assets/ac28069e-2641-4dc0-8938-d6a8fa1fb937" />
<img width="1262" height="563" alt="Top 10 States 2023" src="https://github.com/user-attachments/assets/d09188cf-573d-45dd-9913-90639365170e" />
<img width="1261" height="568" alt="Top 10 States 2009" src="https://github.com/user-attachments/assets/3fd8f306-dd81-446d-a63e-0e774b29e62e" />
<img width="1263" height="577" alt="Pop up" src="https://github.com/user-attachments/assets/8e999d08-efb6-4994-95bb-3d906d4673c4" />
<img width="1264" height="573" alt="All States 2023" src="https://github.com/user-attachments/assets/951acc7b-1ffb-43bf-b32a-39de76d22470" />
<img width="1259" height="576" alt="All States 2009" src="https://github.com/user-attachments/assets/ea158a7b-7f51-416d-a1f2-9c7e6eae743d" />

This is the link to this iteration the bar chart viz: https://vizhub.com/rkupferwpi/bbb53529f42e425285b5f0e67fc74664

I've also updated my map viz to show a pop up with the name of the state the user is hovering over.  The goal is to get the background check types and totals to show up in the pop up.  Additionally, I updated the viz such that the state that the user hover over fills in with red color.  This is the viz that I would prefer to use for my project.  However, I feel like the most challenging step will be getting the NICS background data to associate with each state.  Here is a picture of what I did:

<img width="966" height="502" alt="US Map with Pop up and Red Fill on Hover" src="https://github.com/user-attachments/assets/594e8624-0f69-41df-83d3-0da38d3724a2" />

This is the link to this iteration of the map viz: https://vizhub.com/rkupferwpi/b20439bfcbd04d27bdd0ac0b1f7f2966

## UPDATE Week 9

I've added interactivity with the legend on my bar chart such that when the user hovers over the specific type of NICS check the opacity of the other types changes.  When the user moves away from the legend the opacity returns to 1 for all types.  Additionally, I've repositioned the legend, the year selector, and the top counts.  The other viz I'm working on for my project does not really lend itself to multiple colors and a legend.  I thought about filling in the states with different colors but that will just look confusing as it doesn't correspond to any data that I'd be trying to relay.  My bar chart was a much better candidate for this tasking.

Here is the link to the viz in vizhub:
https://vizhub.com/rkupferwpi/5f7d5f65164c4f2e8d9355f42a40df43

Here is the result when I hover over handguns:

<img width="1264" height="573" alt="Handguns" src="https://github.com/user-attachments/assets/eb2541e2-8c19-423a-9636-0d9c3d16b500" />

When I hover over long guns:

<img width="1262" height="570" alt="Long guns" src="https://github.com/user-attachments/assets/a9d57ddf-c7fc-4374-9e7b-b0811fb4652f" />

When I hover over multiple:

<img width="1263" height="573" alt="Multiple" src="https://github.com/user-attachments/assets/6781116b-fcd8-411a-ba78-4b9d8f83568b" />

When I hover over other:

<img width="1266" height="571" alt="Other" src="https://github.com/user-attachments/assets/4ef943f3-8312-4726-914a-d798f3aa803f" />

## Update Week 10

I've added the following interactivity to my US map.  When the user clicks on a state, they get a zoomed in view of the state.  When the user clicks off of the state it will zoom out.  However, if the user clicks on another state the viz zooms into that state.  So I've added a reset view button to the bottom right of the viz to restore the view to the default zoom level which shows the entirety of the United States.

Here is a screen shot of this effect:
<img width="1232" height="587" alt="Zoomed In On Missouri" src="https://github.com/user-attachments/assets/dfd0465d-f3e0-4731-bdb7-77a708419999" />

Here is a link to this iteration:  https://vizhub.com/rkupferwpi/fb169b7e4c5d4f55bc8aa424ff0a1d85

I've added the following interactivity to my bar chart vis of NICS background checks.  I've added a sort drop down menu that allows the user to organize the bar chart by most to least checks, least to most checks, and alphabetical by state.  I've also added code to move the legend when least to most checks is selected so the bars don't interfere with the legend.

Here are screenshots of these effects.
Most to least:
<img width="1263" height="573" alt="Most to Least" src="https://github.com/user-attachments/assets/9cb5c51d-25b9-4e47-94c1-3fe4c6db65fc" />

Least to most:
<img width="1263" height="578" alt="Least to Most" src="https://github.com/user-attachments/assets/e2512458-2767-4d4f-996c-3e874ccd91cb" />

Alphabetical by state:
<img width="1262" height="577" alt="Alphabetical by State" src="https://github.com/user-attachments/assets/27c0947c-6593-420d-b218-620c7c1a2a30" />

Here is the link to the current iteration: https://vizhub.com/rkupferwpi/767dedbf8ecc45959057128399e4d899

## Update Week 11
I've updated the bar chart with a title, adjusted the drop down selector positioning, and the legend positioning.  I've also changed the background color to a softer color.

Here is an image of the viz:
<img width="1261" height="577" alt="Bar Chart Polishing" src="https://github.com/user-attachments/assets/13c3b5c4-0c8f-4fb8-a1e6-bd82051fd3b9" />

Here is the link to the VIZ: https://vizhub.com/rkupferwpi/ea9f228118024d6a83ce94d9a6c05843

I've updated the map by adding a title, removing the black border around the continental US, Alaska, and Hawaii, changed the background around the US to a light blue with an opacity of .4, and changed the background color of the states to a light gray.

Here is an image of this viz: 
<img width="1273" height="556" alt="US Map Polishing" src="https://github.com/user-attachments/assets/9b11198b-fb3e-4f09-be92-c7797ea28dcf" />

Here is a link to the viz: https://vizhub.com/rkupferwpi/91099e4e0c2c4f259b39f9ad9384a909
