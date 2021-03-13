# Safe Schools Reopening

![Full map](/img/fullmap.PNG)

## Introduction
This project is a map of the school districts in California. It provides information for the status of schools reopening after developing a plan to handle the spread of COVID-19 safely. This map was made to show the progress of the "Covid-19 and Reopening In-Person Learning Framework for K-12 Schools in California, 2020-2021 School Year" developed by the California Department of Public Health. This map is displaying the data reported by each school district. Every other monday (or Tuesday if Monday is a state holiday), school districts will report their level of in-person learning, from distance learning to hybrid learning to in-person classes at each level of education, elementary, middle, and high school levels. The information is provided on the internet to be transparent to the people of California about the information the California Department of Public Health has at its disposal. This project could be useful for anyone trying to gain more information about the state of schooling in California during the pandemic.

There are many web map elements on display here. The map includes a legend showing which colors represent which level of in-person schooling. Statistics that can be viewed by school are the level of in-person schooling, the eligibility to reopen, the planned date for reopening if it is not already, the prescence of a COVID safety plan with a link to view it, the amount of COVID funds received, the amount (in month supply) of PPE supplies received, the number of outbreaks in 2021, and the prescence of state testing in the school district.

![Legend](/img/legend.PNG)

## Critique

### Responsive Design
This map does support responsive design. The map can be zoomed in and out to change the view, which is especially useful for smaller screens. Elements like the legend and the popup window can be hidden to view more of the map as well.

![mobile with legend](/img/mobilelegend.jpeg)

![mobile no legend](/img/mobilenolegend.jpeg)

### Basemap and Thematic Layers

The basemap used here appears to be one of the default ESRI maps. The basemap is grey and includes state boundaries, city labels, and water features. The basemap is the same color as the `No Status Available` label on the map. It is a simple but effective basemap that works for its purpose.

There are three thematic layers for the map. Each layer overlays the school districts for the state of California. The three colors--dark blue, light blue, and pale yellow--used to represent the three levels of in-person schooling are distinct and easy to tell apart.

### Interactive Elements

The map also includes many interactive elements. The thematic layer can be changed to show the in-person education level of elementary, middle, or high school. The selected layer is highlighted in the selection `div`.

![Thematic layer selection div](/img/selectiondiv.PNG)

Specific school districts can be searched on the map as well. The search also has an autocomplete feature to suggest to the user school districts to select based on user input. A users current location can also be retrieved to display the local school district.

![search bar](/img/search.PNG)

![Search with current location](/img/serachcurrloc.PNG)

Each school district can be clicked on to view more in-depth information about the district. The statitics diplayed were mentioned in the introduction. If different schools within the district have different levels of openess, the view within the popup window can be changed to view information on each different school within the district.

![Info Popup](/img/popup.PNG)

## Systematic Archetecture
The main services used to make this map functional on the web are provided by ESRI's ArcGIS JavaScript packages, which are loaded into the HTML document in the `<head>` section. Most of the styling as well comes from an ArcGIS CSS file linked in the HTML document. The map does not use all of the functionality provided by these `.js` files. As noted in the source code, some interactive elements were removed--such as the ability for the user to change the source selection of the legend--by setting `Display: none` in the CSS in the HTML document. All of the information is loaded from an ArcGIS server, retrieved using queries `onLoad`.

The map does contain some of its own major functions as well. The `map-selector` element used to select the thematic layer that is displayed has an `EventListener` function that switches which `btn-switch` CSS class has the `active-map` class and calls the `toggleSchoolLayer` function to change the display on the map as well. In other words, this function changes the display of the buttons to show which one is selected and changes the thematic layer displayed when one of the three maps is clicked by the user. The data is received by sending a query to the ArcGIS server hosting the map.

Another major function is the function that provides extra information about the specific school district when clicked. When the user clicks within a school district boundary, a query is  sent to the ArcGIS server to get the geometry for the boundary highlight to indicate which district was clicked and the information conatined in the popup window. When the data is loaded the ID of the popup `<div>` is changed to match the specific district clicked. The information is then populated within the popup with the information returned from the query.

The final major function that provides this web map its functionality is tn the school search bar. This functionality is provided by ESRI JavaScript files linked in the `<head>`. By providing the `<form>` element with the classes `esri-input` and `esri-search_input`, the search bar gains the functionality to not only search for specific school district, but it also gains an autocomplete feature to help the user find the district they are looking for. As the user types, a `div` element with the class `esri-search_suggestions-menu` is created on the page and populated by a `ul` to display the dropdown with the matching school districts, bolding the matching portion of the names to what was inputed by the user. A query is sent to ArcGIS with each user input to retreive the possible matches.

## Analysis and Reflection
This map shows a clear divide in the age groups that are allowed to have in-person schooling. It is much more frequent for elementary schools in the state to have in-person or hybrid schooling when compared to the frequency of the same for high schools. The [Covid-19 School Reopening Status Report](https://www.cdph.ca.gov/Programs/CID/DCDC/Pages/COVID-19/School-Reopening-Status-Reporting-Directive.aspx) mentioned that the evidence we have so far shows that it is safer for youngest demographic and becomes less so the older one gets. This was encouraging to me that the state government recognized this trend because it is the young children who stand to lose the most from online-only learning.

This is map is a great way for the government of California to remain transparent in their efforts to reopen schools for in-person lessons. It can help give people hope that their schools will soon be open because they can see that some of the schools in the state are, in fact, open. With the vaccine starting to make the rounds, this map is a sign that normalcy--whatever that may mean in 2021--is just around the corner. In a state with one of the most strict lockdown policies in the country, it is encouraging to see that at least the more sparsely populated areas of the state have been allowed to educate their kids and that common sense has at least partrially returned to the people running things in Sacramento. It is however discouraging that the school district where I currently reside--San Dieguito Unified School District--is still marked eligible to reopen despite the goal posts recently being moved. The county approved the opening of the schools starting this week, but the state shot it down. The same organization that made this map and marked the school district as eligible to be open just denied the opening of the secondary schools this week, citing the need for a students to stay in one classroom with one teacher for the entire day. That is a clearly unreasonable request given the way public secondary schools are set up in this country. However, the end is still in sight, this is just a bump in the road towards reopening the schools thorughout the state.

The closure of schools due to the pandemic has definitely exacerbated the digital divide not only in California, but around the country. As schools moved online, children without access to technology and an adequate working space have been falling behind for the past year. Opening schools as soon and as safely as possible is very important in order to lessen the blow to an entire generation's education. While socioeconomic status has been hindering children during this time, there are some parallels between the racial makeup of counties in California and the school districts that are open currently. Here is a map I made last quarter for a project in another class:

![Map of non-white percentages by California counties](/img/Non-White_Cali.png)

Referencing the current school reopening map, it appears that the counties with the most non-white residents also have the least open school districts. Towards the northern part of California, where there are majority white residents, the schools are the most open. While these areas are also the least populated areas of the state, it still speaks to the growing racial inequality as a result of the pandemic.
