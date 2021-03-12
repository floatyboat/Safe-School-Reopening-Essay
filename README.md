# Safe Schools Reopening

## Introduction
This project is a map of the school districts in California. It provides information for the status of schools reopening after developing a plan to handle the spread of COVID-19 safely. This map was made to show the progress of the "Covid-19 and Reopening In-Person Learning Framework for K-12 Schools in California, 2020-2021 School Year" developed by the California Department of Public Health. This map is displaying the data reported by each school district. Every other monday (or Tuesday if Monday is a state holiday), school districts will report their level of in-person learning, from distance learning to hybrid learning to in-person classes at each level of education, elementary, middle, and high school levels. The information is provided on the internet to be transparent to the people of California about the information the California Department of Public Health has at its disposal. This project could be useful for anyone trying to gain more information about the state of schooling in California during the pandemic.

There are many web map elements on display here. The map includes a legend showing which colors represent which level of in-person schooling. Statistics that can be viewed are the level of in-person schooling, the eligibility to reopen, the planned date for reopening if it is not already, the prescence of a COVID safety plan with a link to view it, the amount of COVID funds received, the amount (in month supply) of PPE supplies received, the number of outbreaks in 2021, and the prescence of state testing in the school district.

[Legend](img/legend.PNG)

## Critique
The map also includes many interactive elements. The thematic layer can be changed to show the in-person education level of elementary, middle, or high school. The selected layer is highlighted in the selection `div`.

[Thematic layer selection div](img/selectiondiv.PNG)

Specific school districts can be searched on the map as well. The search also has an autocomplete feature to suggest to the user school districts to select based on user input.

[search bar](img/search.PNG)

Each school district can be clicked on to view more in-depth information about the district. The

## Systematic Archetecture
The main services used to make this map functional on the web are provided by ESRI's ArcGIS JavaScript packages, which are loaded into the HTML document in the `<head>` section. Most of the styling as well comes from an ArcGIS CSS file linked in the HTML document. The map does not use all of the functionality provided by these `.js` files. As noted in the source code, some interactive elements were removed--such as the ability for the user to change the source selection of the legend--by setting `Display: none` in the CSS in the HTML document. All of the information is loaded from an ArcGIS server, retrieved using queries `onLoad`.

The map does contain some of its own major functions as well. The `map-selector` element used to select the thematic layer that is displayed has an `EventListener` function that switches which `btn-switch` CSS class has the `active-map` class and calls the `toggleSchoolLayer` function to change the display on the map as well. In other words, this function changes the display of the buttons to show which one is selected and changes the thematic layer displayed when one of the three maps is clicked by the user. The data is received by sending a query to the ArcGIS server hosting the map.

Another major function is the function that provides extra information about the specific school district when clicked. When the user clicks within a school district boundary, a query is  sent to the ArcGIS server to get the geometry for the boundary highlight to indicate which district was clicked and the information conatined in the popup window. When the data is loaded the ID of the popup `<div>` is changed to match the specific district clicked. The information is then populated within the popup with the information returned from the query.

The final major function that provides this web map its functionality is tn the school search bar. This functionality is provided by ESRI JavaScript files linked in the `<head>`. By providing the `<form>` element with the classes `esri-input` and `esri-search_input`, the search bar gains the functionality to not only search for specific school district, but it also gains an autocomplete feature to help the user find the district they are looking for. As the user types, a `div` element with the class `esri-search_suggestions-menu` is created on the page and populated by a `ul` to display the dropdown with the matching school districts, bolding the matching portion of the names to what was inputed by the user. A query is sent to ArcGIS with each user input to retreive the possible matches.

## Analysis


## Reflection
