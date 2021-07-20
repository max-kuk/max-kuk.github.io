---
title: To buy or not to buy? (Part I)
description:
toc: true
authors:
    - Maksim Kukushkin
tags:
    - price prediction
    - regression
    - tree-based algorithms
categories:
    - price prediction
series:
    - flight price prediction
date: '2021-04-18'
lastmod: '2021-05-19'
featuredImage: images/ryanair.jpg
draft: false
---

In this article serie  we will talk on how to predict a ticket price with machine learning.

<!--more-->

# Introduction

The prediction of itinerary price could be challenging even if you use machine learning. Especially, when you predict the prices of low-cost airline companies. Low-cost airlines use dynamic pricing systems to ensure high passenger loads thereby maximising revenue on the flight.

Factors affecting the price of a route can be manifold: passenger load factor, carosine price, competition between airlines on the route and competition between airlines in the market in general. Other factors may be airport services prices, government subsidies and etc.

While writing my master's thesis, I also decided to take into account such factors as weather conditions at the departure and destination airports, large events such as Formula-1 or Champion Leages football matches and national holidays. Additionally, I considered school vacations in federal land of Germany, where Berlin airport is located.



# Dataset collection



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
| HHI (monthly)                                           | *float*                                                   | [Flightstats](flightstats.com) (with subscription)           |
| crude oil (monthly)                                     | *float*                                                   | [quandl.com](quandl.com)                                     |
| temprerature features (e.g. avg_temp_bcn, avg_temp_ber) | *float*                                                   | [wunderground.com](wunderground.com)                         |

## Gather weather data



## Gather flight route statistics and calculate HHI

This is the introduction article to the serie “Flight price prediction”, where I on my example will demonstrate how to find interesting features for flight price prediction.

