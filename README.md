# Method for multi-task level visualization of access to active transportation infrastructure and demographics

## Introduction

Transportation safety is an issue that impacts everyone, but it is especially important for those of use who walk, bike, use a wheelchair, or otherwise mix with car traffic without the safety afforded by a car. These road users are dubbed ‘Vulnerable Road Users’ ( VRUs) in transportation circles [1]. In the past year, over 200 pedestrians and 150 cyclists have been involved in collisions in Seattle, with at least 12 pedestrian fatalities in 2021 [2, 3]]  This is despite the city’s stated ‘vision zero’ goal of reducing traffic deaths to zero by 2030 [4]. 
    One important factor in reducing VRU collisions is infrastructure. Infrastructure items like crosswalks and bike lanes have been shown to reduce collisions and fatalities [5]. But not every intersection has a crosswalk, and not every road has a bike lane in Seattle. This raises questions about where these infrastructure items are located in Seattle, and who has access to them. Are these items distributed equitably around the city so that all may benefit, or is access to life-saving infrastructure a privilege granted to a subset of Seattleites? Are there specific locations that lack crosswalks where installing one would improve the day -to- day life of nearby residents? These are important questions to answer in considering how to allocate new transportation infrastructure. A 2015 report from People for Bikes, a US bicycling advocacy organization, explored the intersection of cycling and equity [6]. Findings in the report show that people of color are leading a surge in bicycling in the US, but are also more likely to be killed riding their bikes. This report cites survey data showing that people of color are more interested in riding bikes for transportation, and are also more likely to ride if they have access to infrastructure like protected bike lanes. This report specifically calls out south Seattle for lacking safe cycling infrastructure. In this project, our team has set out to design a visualization that can address these sorts of questions. We seek to find an answer to the research question: How can we best visualize how alternative transportation infrastructure distributions in Seattle intersect with population distributions?

## Background, Previous Work, and Motivation

Manaswi Saha, a PhD Candidate at UW, has identified the role of a visualization’s user or stakeholder, and how this impacts the necessary level of granularity, as a key design parameter in geo-visual representations of urban accessibility data [7]. In her recent paper and in personal conversations, she describes how different stakeholders in the infrastructure process have different needs around how to use a visualization, corresponding to different task levels. Task levels range from macro or high-level to micro or low-level. A user's task level is driven by the tasks they perform relative to the infrastructure. For example, they found that wheelchair users are interested in seeing very detailed and hyperlocal visualizations, as they tend to think of infrastructure in terms of how they are getting from point A to point B. This is an example of a micro task level. On the other hand, policy makers prefer visualizations that abstract data at the city level to better understand trends that drive policy decisions. This is an example of a macro task level. People filling the role of advocates strike a balance between these two positions: They make use of city-level visualizations for understanding broad trends and communicating with policy makers, but also expect the detailed, local visualizations to drill into specific problems and communicate with infrastructure users. These findings were distilled down into a set of best practices for designing geovisualization of urban accessibility data. These include designing visualizations that target the sensemaking process of the target user and include the details that are relevant to that process. Users should be able to access multiple map types to view data from different perspectives. People need to trust the data that is being visualized. Her work focused on infrastructure accessibility issues (i.e. wheelchair passability) in particular, but we believe that these insights are directly transferable to the similar issue of alternative transportation infrastructure.
In our review of existing work on the question of alternative transportation infrastructure distribution and equity, we found that most communications involving visualization tend to fall into two broad categories. The first is to plot infrastructure on a google-maps type interface using some sort of GIS (geographic information system) based tool. The best example we have come across is from the Puget Sound Regional Council [8]. While these tools do allow a hyper-local exploration of data, they do not allow a user to easily understand city-wide trends. They also do not allow the incorporation of other relevant information, such as demographic or collision datasets. In our subjective opinions, they also are not visually appealing and do not invite one to explore and understand the data. The second visualization approach is to explore infrastructure vs. equity data at a city-wide and up level. The report on equity and cycling from People for Bikes mentioned above [6] looks at this issue at a city -to - national level, using plots of aggregate statistics when visualizations are used.  This is great for demonstrating the existence of a problem, but it does not allow one to explore local issues to suggest solutions.  
We believe there is a gap that needs to be filled in providing a visualization that represents pedestrian and bike infrastructure and allows comparisons with demographic and other datasets. This visualization tool should allow the user to explore this data at a variety of granularity levels, as Saha suggests. It is also important to allow for the inclusion of specific context information showing how conditions affect real people, or explaining why things are the way they are. By designing a visualization that addresses these shortcomings and follows best practices laid out in previous work for communicating on these issues, we hope to build a tool that advances the conversation around the advancement of alternative transportation infrastructure in an equitable manner. 

## Visualization Design

### Data sources
Many types of transportation and street-related infrastructure could fall under the realm of alternative transportation infrastructure and be relevant to this work. Sidewalks, crosswalks, and bike lanes are some of the more mainstream and objective examples. Other important examples include traffic calmed streets and intersections, low-traffic streets like Seattle’s Stay Healthy Streets, or accessibility specific infrastructure like that tracked by Project Sidewalk [9]. We focus in this work on bike lanes and crosswalks as these have a large impact on VRU safety and are easily quantified. The City of Seattle publishes geo-tagged datasets of marked crosswalk and bike lane locations. We based our infrastructure visualizations on this data. To show demographic trends, we are using data from the 2020 Census that has been aggregated at the neighborhood level by the City. We will be dividing the city based on neighborhoods, as this provides a reasonable sized unit of area to consider in our visualizations. We also rely on Seattle street data and Seattle city border data to construct our visualizations. 

### Layout and Encodings
In designing our visualization structure, we focused on a hypothetical ‘advocate’ user of the tool. We consider an advocate to be someone who is not necessarily personally involved in the issue at hand, but who cares deeply about it and works to solve it. As identified in Saha, the key aspect in designing a visualization for use by advocates is to support multiple analysis tasks at multiple length scales and granularity levels. We expect a user to start an exploration by looking at the city-wide level of granularity, then find interesting regions to dive into and view in detail. To support this, we provide two main visualizations, and interactions to navigate between them. When first visiting the page, a choropleth of the city, broken into neighborhoods, loads. This map supports a macro task level. This choropleth plots the demographics and composite accessibility score for that neighborhood. The demographic quantity plotted is the ratio of people of color for each neighborhood, as calculated by the city of Seattle. We decided to encode this value using a linear mapping of POC ratio to circle area.  This means that areas with a larger population of people of color have a larger circle, which we find intuitive to understand. Our accessibility score is computed by averaging the normalized miles of bike lanes and number of crosswalks per mile of road in the neighborhood. This metric is somewhat arbitrary, and we discuss alternatives in following sections. We chose to encode the transportation index using color. We selected a sequential continuous colormap using Colorbrewer. [10]. A sequential colormap allows the user to make distinctions between areas that have similar index values. We chose the orange colormap so that the more saturated hues connote with ‘bad’, but don’t invoke blood like the red color schemes used in gun violence graphics we talked about in the course. In this city-wide map, road details are included, as Saha found that including geographic information helps users place themselves in the map.  When users click on a neighborhood, detailed granular information about that neighborhood is displayed in a composite visualization below. This detailed view supports a micro task level. A map plots the detailed transportation infrastructure for the neighborhood, allowing users to see exactly what infrastructure is within the neighborhood. All of the streets or roads in the neighborhood are plotted in gray. Bike lanes within the neighborhood are plotted over the streets in green. Crosswalks are plotted on top of everything using blue circles.  This supports the fine-grained visualization Saha identified as important for advocates in identifying specific problems and in working with local user stakeholder. This local view also plots the racial breakdown of residents of that neighborhood using a stacked bar chart. We intend for this bar chart to appear next to the neighborhood  map, but it appears below in our Observable implementation due to restrictions on chart placements in Observable. 

## Future work and room for improvement

As it stands, we view our project as a prototype of a tool for exploring the data and performing the tasks described above. We’ve identified a few key improvements that would be needed to move this from ‘prototype’ to ‘minimum viable product’.

### Explore different metrics

Our visualization currently plots a transportation infrastructure index that we defined to distill the 2 infrastructure datasets we are working with into a single-value metric. Our current metric is an average of the normalized ratios of miles of bike lanes per mile street and crosswalks per mile of street in each neighborhood. Having worked through this project, we have identified a few problems with this metric. Most importantly, our metric indiscriminately counts miles of street in each neighborhood. This means that neighborhoods with lots of slow-speed residential streets will have a worse index than those with lots of high-speed arterials, even though the former might be better for biking or walking. A simple fix for this would be to base our metric on miles of arterial streets per neighborhood instead of overall miles of streets. We looked for a dataset to do this with, but did not find one readily available. Our metric also does not take connectivity into account at all. An important aspect of bike and pedestrian infrastructure is how connected it is, as this determines how easy it is to move around. However, quantifying connectivity would be a difficult task. Any further work on this project should involve talking with transportation advocates and transportation engineers to identify the most useful metrics for them.

### Add individual context:
One important consideration from our discussions with Saha was that including individual context in a visualization is a powerful way to engage and motivate viewers. The idea here is to incorporate non-quantitative data and stories, such as highlighting the stories of individuals who have been impacted by alternative transportation infrastructure or a lack thereof. This would especially support using our visualization tool for storytelling. We considered ways of including this information, but felt that if poorly implemented this element could be at best chartjunk and at worst distasteful or offensive. Given the scope of this project, we left this for future work. 

### Make it a tool:
There are some user-interface aspects that need to be added to move this project from prototype to usable tool.  First, this tool would have to be extended  to work for other cities. Technically this is feasible. As long as infrastructure data, neighborhood data, and street map data are available for a city in geoJSON format, our data prep workflow could be easily wrapped into a few functions and applied to a new location. Adding support for custom metrics, and possibly swapping between metrics, would also broaden the appeal of this tool. 



## Bibliography (Written) 
Data references in notebook
1. Revised Code of Washington Section 43.61.526
2. Seattle Collisions Dataset, accessed from https://data-seattlecitygis.opendata.arcgis.com/datasets/SeattleCityGIS::collisions/about
3. Ryan Packer. "Seattle On Pace to Record Highest Number of Traffic Fatalities Since 2006", The Urbanist. September 9, 2021. https://www.theurbanist.org/2021/09/09/seattle-on-pace-for-record-traffic-fatalities-in-2021/
4. Seattle Department of Transportation Vision Zero Landing Page. https://www.seattle.gov/transportation/projects-and-programs/safety-first/vision-zero
5. Safe Transportation For Every Pedestrian Pamphlet, US DOT, Accessed from https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjlp4u24f33AhUroI4IHVUQAWAQFnoECBUQAw&url=https%3A%2F%2Ftrec.pdx.edu%2Fsites%2Fdefault%2Ffiles%2FPeter%2520Eun%2520FHWA%2520STEP.pdf&usg=AOvVaw2kBNOnDLZBbZOhK33biEb3
6. Building Equity: Race, Ethnicity, Class, and Protected Bike Lanes: An Idea Book for Fairer Cities. People for Bikes and Alliance for Biking and Walking. 2015. 
7. Saha, Manaswi, et al. "Visualizing Urban Accessibility: Investigating Multi-Stakeholder Perspectives through a Map-based Design Probe Study." CHI Conference on Human Factors in Computing Systems. 2022.
8. Puget Sound Regional Council Transportation System Visualization Tool. “https://www.psrc.org/our-work/featured-work/regional-transportation-plan/transportation-system-visualization-tool”
9. Saha, Manaswi, et al. "Project sidewalk: A web-based crowdsourcing tool for collecting sidewalk accessibility data at scale." Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems. 2019.
10. Brewer, Cynthia. https://colorbrewer2.org/#

