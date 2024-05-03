# Repository for the Course Data Visualization
Containing two Projects which make up the course mark

- [Repository for the Course Data Visualization](#repository-for-the-course-data-visualization)
- [1. Assignment1 (Creating Visualization)](#1-assignment1-creating-visualization)
  - [The Question](#the-question)
  - [The Creation](#the-creation)
  - [The Database](#the-database)
  - [The Code](#the-code)
  - [The Visualization](#the-visualization)
  - [The Answer](#the-answer)
- [2. Electricity Price and its Suppliers in Germany](#2-electricity-price-and-its-suppliers-in-germany)
  - [Abstract](#abstract)
  - [Method](#method)
  - [Topic Identification (Compile)](#topic-identification-compile)
  - [Cleaning](#cleaning)
  - [Context](#context)
  - [Combining](#combining)
    - [Code of the Visuals](#code-of-the-visuals)
    - [Pricing](#pricing)
      - [Price per state](#price-per-state)
      - [Price per State (Map)](#price-per-state-map)
      - [Amount and Type of power plant per state](#amount-and-type-of-power-plant-per-state)
      - [Supplier Zones](#supplier-zones)
    - [Power Suppliers](#power-suppliers)
      - [Power plants on the Map](#power-plants-on-the-map)
      - [Marketshare per supplier](#marketshare-per-supplier)
      - [Plant Type per supplier](#plant-type-per-supplier)
      - [Plant Type by supplier](#plant-type-by-supplier)
      - [Capacity 2015 vs. 2024](#capacity-2015-vs-2024)
      - [Type of Energy over time](#type-of-energy-over-time)
      - [Production vs Consumption](#production-vs-consumption)
  - [Conclusion](#conclusion)
  - [Citations](#citations)

# 1. Assignment1 (Creating Visualization)
## The Question
How significant is the bias of a face recognition algorithm, when it's trained on smiling women and neutral looking men and the test group only has neutral looking women and smiling men (*how often are the predictions wrong for men and women, showing which emotion*).
## The Creation
The Database for this project was created in the [Face Recognition Bias](https://wandb.ai/elsaesserniklas/4facesbias/reports/Face-Recognition-Bias-Report---Vmlldzo1NjUzNDg3?accessToken=ko7n0bkuhe2512rf4rz2zwfi6njqygqbi6a4ltw4d1sz97bxtj6ttw2hmla78iic) Project.

The Project had the goal to analyze the sex based bias when a face recognition algorithm is trained on Pictures of men and women, in which women smile all the time and men show neutral emotions.

For further information about the underlying data please check [Face Recognition Bias](https://wandb.ai/elsaesserniklas/4facesbias/reports/Face-Recognition-Bias-Report---Vmlldzo1NjUzNDg3?accessToken=ko7n0bkuhe2512rf4rz2zwfi6njqygqbi6a4ltw4d1sz97bxtj6ttw2hmla78iic).
## The Database
The resulting Database from the project looked like this:

![test_img](Data/readme_img/Bildschirmfoto%2024-05-03%um%15.41.55.png)


## The Code
## The Visualization
## The Answer

# 2. Electricity Price and its Suppliers in Germany
## Abstract
This report approaches the subject of data journalism by telling a story about the German electricity market (suppliers), while also focusing on the art of digital (data) journalism as laid out in "Digitaler Journalismus in der Praxis" [1]\
From 2010 onward, the use of data in journalism increased [1], caused by the wider availability of data (big data) and the ability to connect more subjects, among others, with machine learning.

EU regulation initiated the ENTSO-E transparency platform, which is a main provider of data used in this report. 


## Method
As laid out in Bradshaw's "The Online Journalism Handbook" and explained in "Digitaler Journalismus in der Praxis" by Tim Osing, five steps (Compile, Clean, Context, Combine, and Communicate)[1] are recommended to tell a story based on data with visuals in an online medium. These steps were used to approach the problem and answer the questions asked in the following chapter.

## Topic Identification (Compile)
The Report tries to answer the following two questions:
1. The cause for the price difference of one kWh per state.
2. What are the distinguishable factors regarding the energy suppliers, and how do they tie up with the price?

The price for electricity in German states increased about 65% over 10 years (from 29.14 to 42.22 € cent per kilowatt-hour [kWh]).
To answer the questions this report poses - and to understand the German energy market, this report focused on four data sources:
- SMARD[A] (Strommarktdaten), an information hub of the German Bundesnetzagentur. The data published on SMARD provides an up-to-date and comprehensive overview of what is happening on the electricity market but is mainly based on data from ENTSO-E.
- Kraftwerksliste from the Bundesnetzagentur[C], the highest German regulatory authority, whose tasks consist of maintaining and promoting competition in so-called network markets.
- ENTSO-E[B] (The European Network of Transmission System Operators for Electricity)  a European association in which all transmission system operators are compulsory members.
- StromAuskunft[D], a value-oriented and consumer-friendly comparison portal with a free switching service for electricity and gas.

## Cleaning
To see which files had the necessary data and which steps were needed to get the data in a form that could be used to answer the questions while generating enticing visuals, a lot of data was imported and cleaned—more than even needed for the final result.

The Code in [Data Prep](dataPrep.ipynb) contains all steps taken to get the imported data, mostly in **.csv** files, in a form which could later be used to create the desired visuals and therefore answer the initial posed questions.

The Code is rather extensive due to the fact that more data was cleaned and prepared than later used to create visuals.

To create the data relevant for the Folium Map, like converting Addresses to GPS-Coordinates, each code block for this task has a loading time of about 2 minutes.

Furthermore it is necessary to note that some code blocks throw errors at the current code state, due to later taken changes to the data.

The final data is here:
- [Price combined with power plat](Data/Preis_cKW.csv)
- [Net Genaration Capacity](Data/NGC.csv)
- [Price per State](Data/PreisLand.csv)
- [Power plants output greater 100 MW](Data/BNetza/KW100Mw-3.csv)
- [Prodcution and Consumption from 2015 - 2024 ](Data/SMARD/combined_2015_2024.csv)

Interesting things in the raw data were that, although most of the time the raw data was imported as **.csv** columns like *Date* and other columns containing *numeric values* were not formatted natively in a way in which they were manipulable out of the box. \
Multiple times, data was split over various **.csv** files, which then needed to be formatted to have the same structure and be merged into a new **.csv** containing all single files.\
Not needed data was deleted, and not missing data, like the full name of an abbreviation, was added.

## Context
To give some context to the data the following Questions are advised: *Who gathered it? When was it compiled? What methodology was used?*[1]

These Questions are fairly easy to answer for the used data, since it's mostly from a government agency. SMARD accesses data from the Übertragungsnetzbetreiber (Transmission system operator) and ENTSO-E, Bundesnetzagentur also uses data from ENTSO-E but extends it with its own parameters, which it acquires directly from the Energy suppliers and other market participants.\
The data from SMARD is collected on an hourly basis on the basis of the German Energy Industry Act.

## Combining
By definition of Bradshaw and Tim Osing, combining is the step in which all data falls into place and in this case the visuals are created, and it is possible to tell a story.

The first sub-chapter **Pricing** focuses on the direct correlation between the price and potential reasons for the differences per state. 

The second sub-chapter focuses on the effect of renewable and conventional power plants regarding the generation of electricity regarding the generation of electricity in comparison to consumption and the general effect on the price.

### Code of the Visuals
The complete code which used to create the visuals is at [Data Journalism](DataJournalism.ipynb)

### Pricing
This Chapter tries to answer the first Question: 

*The cause for the price difference of one kWh per state.*

The used data is from Bundesnetzagentur and the StromAuskunft. [C][D]
#### Price per state


#### Price per State (Map)


#### Amount and Type of power plant per state


#### Supplier Zones


### Power Suppliers


#### Power plants on the Map


#### Marketshare per supplier


#### Plant Type per supplier


#### Plant Type by supplier


#### Capacity 2015 vs. 2024


#### Type of Energy over time


#### Production vs Consumption


## Conclusion
To conclude the two threads, analyzed in this report:

1. Why is the price for one kWh per state so different
2. What are the differences of Energy Suppliers, how does this tie up with the price

To the **1st** Question:\
The price per state is mostly dependent on the supplier for the state. States which were part of *East* Germany and are now in the zone of Vattenfall have the lowest amount of any power plant and generally higher prices than states in *West* Germany. The two biggest suppliers by gross installed capacity have the best (lowest) prices, while the two smaller suppliers have the higher (more expensive) prices.

To the **2nd** Question:\
There are definitely some small correlations between the supplier and its power plant portfolio and the price per state. States with a bigger supplier and therefore generally more power plants have, on average, lower prices than states with a smaller supplier. But the direction the overall production is taking—more focus on renewables and an increase in overproduction compared to consumption—shows that the availability of electricity is only increasing.

The general conclusion of this report has to state that the cleaning and data preparation consumed about 70% of the time spent to create this report, especially the visuals. The necessary work was very detail-focused and repetitive, only showing how important it is to have a good data foundation and ideally already import good data.

The "framework" from Bradshaw formulated in *The Online Journalism Handbook* and explained in *Digitaler Journalismus in der Praxis*[1] helped a lot by structuring this report.


## Citations
[1]@Book{<br />
title = {Digitaler Journalismus in der Praxis: Grundlagen von Onlinerecherche, Storytelling und Datenjournalismus},<br />
editor = {Osing, Tim [Verfasser/in]},<br />
publisher = {Springer VS},<br />
year = {2022},<br />
isbn = {9783658391058},<br />
language = {Deutsch}<br />
}<br />
[A]-[SMARD](https://www.smard.de/page/home/marktdaten/78?marketDataAttributes=%7B%22resolution%22:%22hour%22,%22from%22:1713564000000,%22to%22:1714514399999,%22moduleIds%22:%5B5000410,6000411,1004066,1001226,1001225,1004067,1004068,1001228,1001224,1001223,1004069,1004071,1004070,1001227%5D,%22selectedCategory%22:5,%22activeChart%22:true,%22style%22:%22color%22,%22categoriesModuleOrder%22:%7B%7D,%22region%22:%22DE%22%7D), last Access: 30.04.2024<br />
[B]-[ENTSO-E](https://www.entsoe.eu/data/power-stats/), last Access: 30.04.2024<br />
[C]-[Bundesnetzagentur](https://www.bundesnetzagentur.de/DE/Fachthemen/ElektrizitaetundGas/Versorgungssicherheit/Erzeugungskapazitaeten/Kraftwerksliste/start.html), last Access: 30.04.2024 <br />
[D]-[StromAuskunft](https://www.stromauskunft.de/stromversorger/), last Access: 30.04.2024 <br />
[I.]-[ShapeFile for Map](https://github.com/stepheneb/jsxgraph/tree/master), last Access: 30.04.2024 <br />
