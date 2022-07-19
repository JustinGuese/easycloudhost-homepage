---
title: "EasyKube"
description: "Managed Kubernetes in AWS and a custom Cloud"
draft: false
---

# Your custom private cloud 

Are you looking for a way to host your data and applications in a secure, private cloud, out of the hands of big corporations?

**EasyKube is your solution**

## The advantages of a custom private cloud

So, why should you care to create your own cloud, instead of using public cloud providers?

There are several advantages and disadvantages depending on your background.
Let us say you store sensitive, intellectual data, like patents or data that gives you a competitive advantage.


## Serverless functions overview

A "**storage**" function distinguishes itself from a "simple" function, in that it offers **persistence**, meaning that if a function crashes, or restarts, that objects saved in the path **"/mnt/persistent/"** will be saved.

A "**timed**" function distinguishes itself from the "continuous" function, in that the timed one is running at a specific **schedule**, whilst the continuous is running constantly.

These two settings can be combined, resulting in a total of four combinable possibilities for serverless functions:

1. Simple-Continuous function
    - Good for web applications that do not require storage. 
    - Examples: 
        - you want an API or website displayed where data does not have to be stored
        - you want to download current crypto prices and calculate the exchange rate between two pairs
2. Simple-Timed function
    - Good for jobs that you want to have executed, that do not require storage
    - Examples:
        - triggering other endpoints with post requests
        - starting external backups
        - downloading data and writing it into the managed MongoDB
3. Storage-Continuous function
    - Good for web applications that require storage.
    - Examples:
        - An API that receives current users as json and saves them to disk
        - An API or website that needs to save pictures to disk
4. Storage-Timed function
    - Good for jobs that require storage
    - Examples:
        - You want to download price data every hour and save it into a CSV file
        - You want to create backups of a database

## Managed MongoDB overview

In case storage on disk is not enough, you can easily spin up a managed mongodb instance, which you can easily access from your serverless functions.

A managed MongoDB makes sense, if you want to run multiple functions that are all accessing the same information, like if you distributed your workloads into several functions, or you are running functions in parallel.

The big benefits of the managed MongoDB service are, that contrary to other hosting providers it will remain in a custom network, meaning it is not exposed to the internet, but you can still easily access it in your functions.

This means you do not have to worry about SSL connections, strong passwords or other things, and can easily get it up and running in seconds. An example to connect with python is as follows:

```python
from pymongo import MongoClient
client = MongoClient('mongodb://mongodb:27017/')
```
This saves you from a lot of steps compared to other hosting providers, where you need to set up SSL certificates, ports, firewalls and user password combinations.

Example applications for the managed MongoDB are:
- You are saving items as json into MongoDB using custom EasyFAAS functions. If one function is not enough, you can simply scale your function up, and the load will be distributed to two functions automatically.
- You are building an ETL pipeline, where the first function collects data and saves it into the database, the second applies calculations to it and writes it again into the database, and the third one serves the result as an API


# 1. Getting started



## 1.1 The main dashboard

![main dashboard](/assets/images/tutorial/main-dashboard.png)

The main dashboard is the central control system for EasyFAAS. In here, you will se an overview over the different services that are available.
