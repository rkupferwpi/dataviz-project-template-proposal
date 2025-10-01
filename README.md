# Data Visualization Project

## Data

The data I propose to visualize for my project is NICS background check data obtained from https://github.com/BuzzFeedNews/nics-firearm-background-checks.


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

