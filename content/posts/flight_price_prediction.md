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

While writing my master's thesis, I also decided to take into account such factors as weather conditions at the departure and destination airports, large events such as Formula-1 or Champion Leages matches or national holidays. Additionally, school vacations in federal land of Germany, where Berlin airport is located.

# Dataset collection

This is the introduction article to the serie “Flight price prediction”, where I on my example will demosntrate how to find interesting features for flight price prediction.
