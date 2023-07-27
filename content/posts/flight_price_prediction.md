---
title: To buy or not to buy? (Part I)
description:
toc: true
authors:
tags:
    - price prediction
    - regression
    - tree-based algorithms
categories:
series:
    - flight price prediction
date: '2021-04-18'
lastmod: '2021-05-19'
featuredImage: images/ryanair.jpg
draft: false
---
In this blog series, we'll discuss how to use machine learning to predict the price of travel itineraries.

<!--more-->

## Introduction

Predicting the cost of a trip can be tricky, even with the help of machine learning. This is especially true when trying to predict the prices of flights from low-cost airlines. These airlines use a flexible pricing system to fill up their planes with as many passengers as possible, which helps them make more money from each flight.

There are many factors that can influence the price of a flight route. Some of these include how many seats are filled on the plane (passenger load factor), the price of kerosene fuel, the competition between airlines on that specific route, and the overall competition among airlines in the market. Other factors, like the costs of airport services and government subsidies, can also play a role.

When I was writing my master's thesis, I took into account additional factors that can impact flight prices. These factors included the weather conditions at both the departure and destination airports, any major events happening at those locations (such as Formula-1 races or UEFA Champion League football games), and national holidays. I also considered school vacations in the federal state of Germany where the Berlin airport is located.

Considering all of these factors can help improve the accuracy of predicting flight prices and make it easier to plan and budget for your travel expenses.



## Dataset collection

<details>
  <summary>Overview of features</summary>

| Feature name                                            | Description                                               | Source                                                       |
| ------------------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| fr_price                                                | *float*, price of ryanair flight on observation date (ts) |                                                              |
| days_until_departure                                    | *int*                                                     | = observation date (ts) - departure date                     |
| day_of_week                                             | *int*, encoded as 0-6                                     |                                                              |
| year                                                    | *int,* 2018-2020                                          |                                                              |
| month                                                   | *int*, 1-12                                               |                                                              |
| day                                                     | *int*, 1-31                                               |                                                              |
| weekend                                                 | *boolean*, 0 or 1                                         |                                                              |
| holiday                                                 | *boolean*, 0 or 1                                         | [public holiday calendar](https://www.schulferien.org/Kalender_mit_Ferien/kalender_2021_ferien_Berlin.html) (in German) |
| school vacation                                         | *boolean*, 0 or 1                                         | [calendar of school vacation](https://www.schulferien.org/Berlin/berlin.html) (in German) |
| event                                                   | *boolean*, 0 or 1                                         | Calendar of UEFA Champion League  games and etc.             |
| HHI (monthly)                                           | *float*                                                   | [flightstats](flightstats.com) (with subscription)           |
| crude oil (monthly)                                     | *float*                                                   | [quandl.com](quandl.com)                                     |
| temprerature features (e.g. avg_temp_bcn, avg_temp_ber) | *float*                                                   | [wunderground.com](wunderground.com)                         |

</details>

### Gather weather data

If you want to gather past weather information, you can use the website [wunderground.com](wunderground.com). As far as I know, it's the only website that offers historical temperature data for free. To automatically collect the temperatures of your departure and arrival cities, a special tool called a 'crawler' was created to do the job for you.


<details>
  <summary>Weather crawler code</summary>
<p>

<script src="https://gist.github.com/max-kuk/8037447a425d3bb53e58a374397839d7.js"></script>

</p>
</details>

### Gather flight route statistics and calculate HHI

The Herfindahl-Hirschman Index, or HHI, is a way to measure how big companies are compared to the market they operate in. It also shows how much competition exists between these companies.

$HHI = \sum_{i=1}^{N} s_{i}^{2},$

where:

- $s_{i}$  is the market share of firm $i$ in the market,
- $N$ is the number of firms on the market.


<details>
  <summary>Flightstats crawler code</summary>
<p>

<script src="https://gist.github.com/max-kuk/6d161d3b6372bda3f5c4294c826e103e.js"></script>

</p>
</details>

{{< mermaid >}}
pie
    title Average market share of airlines on the BER-BCN route (2017-2020)
    "ASL Airlines France" : 0.02
    "easyJet" : 39.76
    "Eurowings" : 3.17
    "Germanwings" : 4.24
    "Ryanair" : 33.14
    "Vueling" : 19.68
{{< /mermaid >}}


## Conclusion