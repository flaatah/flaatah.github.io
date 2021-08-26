---
layout: post
title: "Web Scraping in R"
subtitle: "Scraping movie data from IMDB with the ravest package"
background: '/img/posts/web-scaraping/bg-index.jpg'
---

<h1>Introduction </h1>

In today’s world, data is being generated at an exponential rate. This massive amount of data and information is essential for many individuals and tech giants in various useful ways.

So, having access to precise data in abundance will serve you just right in any field in gaining insights and performing further analysis. Therefore, Web Scraping has become a must have skill especially if you are a data scientist.

All the data is available on the Internet today. But, how to scrape data that might be useful to you? Well, you have got it all sorted out. With all the advanced tools and programming languages, scraping data out from the web is just one cushy job.

Let’s dive straight to the point.

# Web Scraping?
Web Scraping is just a technique to convert unorganized data that is usually available on the internet to an organized format so that it can be useful to us.

The very basic idea of scraping data is the old school method of COPY AND PASTE . Well, to be honest, this method might sound easy-peasy but is taxing, monotonous, time-dependent and not at all fascinating.

But with a few lines of code it is utterly possible. So, let’s see how can we scrape data.

# Web Scraping using R
Expecting that you all will be having a basic knowledge about how R works and its syntax, lets get straight to this short tutorial where I’ll show you How To Scrape Data using R from multiple pages at once.

For general text data scraping: you can visit: Basic Web Scraping

# About the Data
![Data](/img\posts\web-scaraping\Data.jpg)

From The Numbers, here lies the complete list of movies with their release dates, production budget and gross revenue information. The profit and loss figures are very rough estimates based on domestic and international box office earnings and domestic video sales, extrapolated to estimate worldwide income to the studio, after deducting retail costs.

# Note: The movies’ data is in the tabular format.

Following are the steps you need to follow:
Open R Studio. Then in a new file:
Package Installation
Install the required packages.

xml2: Xml2 is a wrapper around the comprehensive libxml2 C library that makes it easier to work with XML and HTML in R

rvest: rvest helps you scrape information from web. pages.

tibble: The tibble package provides utilities for handling tibbles, where “tibble” is a colloquial term for the S3 tbl_df class. The tbl_df class is a special case of the base data.frame.