---
title: "EasyFAAS"
description: "this is meta description"
draft: false
img: "images/logos/EasyFAAS.png"
---

<!-- ![EasyFAAS Logo](images/logos/EasyFAAS.png) -->


{{< notice "tip" >}}
  Did you know, that over 60% of development time is spent on DevOp tasks instead of working on the actual product [1]?
{{< /notice >}}

What if there could be a way to **"just run code" instead of worrying about servers and clusters**?

**EasyFAAS (Easy-Function-as-a-service) lets you run your code in an easy environment, without hidden costs.**

## Why should I choose EasyFAAS over other providers?

Whilst we were working with FAAS services of other providers, we usually ended up having problems with two specific things:
(EU) Data Security
Complexness

### 1. Our problems with (EU) Data Security

Even though FAAS services of other cloud providers are technically secure, they still have the problem of being hosted by an american company. This can be a problem for EU-based companies, as the american ["patriot act"](https://www.congress.gov/107/plaws/publ56/PLAW-107publ56.pdf) states, that the US government can basically request your data from american companies to "intercept and obstruct terrorism".
There have been unconfirmed reports of misuse as well, where industry and intellectual secrets were requested.

{{< notice "tip" >}}
This proves to be especially dangerours for companies in the **finance** industry, or in general where **companies have an intellectual competitive advantage**.
{{< /notice >}}

Of course no one can surely say (yet) that this is really happening, and that it is not only used for the defeat of terrorism, but our company and many others agree that your data should only belong to you.

### 2. Our problems with complexness

Now back to a happier topic: The FAAS services of other cloud providers are amazing. They are versatile, well integrated in their system, and were a technological novelty. Our problem has just been, that if you want to "just get going", meaning just pasting your code, you will often experience that it is not that easy.

The technical interconnections with other services come with a price: You will find yourself setting up API Gateways if you want the service to connect to the outside, where you will need to know about ports, firewalls, security groups and even networking.

Also, if you are using custom packages like Python's numpy and pandas, you will have to create an extra layer, which proves to be quite complex, instead of just listing the packages that are used.

One of our main applications in the past has been to create little APIs that write and read from a database. 
In other FAAS solutions, this requires you to create the networking, the database connection and the custom layer to get started, which involved a lot of repetitive tasks. 

In our EasyFAAS solution this becomes as simple as this:

![EasyFAAS - Create a new function dashboard](/images/easyservices/easyfaas/create-a-new-function.png)

# Contents

1. [Overview](/easyservices/easyfaas#0-inroduction)
2. [Serverless Functions Overview](/easyservices/easyfaas#1-serverless-functions-overview)


## 0. Inroduction

EasyFAAS reduces time to market, and let's your programmers focus on what it important: your code!

To achieve this EasyFAAS currently supports two functions:

#### 1. Serverless functions

- Distinguished into **"simple"** and **"storage"** functions
- Distinguished into **"timed"** and **"continuous"** functions

#### 2. A managed MongoDB NoSQL database

- Easy integration without much setup into your EasyFAAS functions

### 1. Serverless functions overview

A "**storage**" function distinguishes itself from a "simple" function, in that it offers **persistence**, meaning that if a function crashes, or restarts, that objects saved in the path **"/mnt/persistent/"** will be saved.

A "**timed**" function distinguishes itself from the "continuous" function, in that the timed one is running at a specific **schedule**, whilst the continuous is running constantly.

These two settings can be combined, resulting in a total of four combinable possibilities for serverless functions:

#### 1.1 Simple-Continuous function

- Good for web applications that do not require storage. 
- Examples: 
    - you want an API or website displayed where data does not have to be stored
    - you want to download current crypto prices and calculate the exchange rate between two pairs

#### 1.2. Simple-Timed function

- Good for jobs that you want to have executed, that do not require storage
- Examples:
    - triggering other endpoints with post requests
    - starting external backups
    - downloading data and writing it into the managed MongoDB


#### 1.3. Storage-Continuous function

- Good for web applications that require storage.
- Examples:
    - An API that receives current users as json and saves them to disk
    - An API or website that needs to save pictures to disk


#### 1.4. Storage-Timed function

- Good for jobs that require storage
- Examples:
    - You want to download price data every hour and save it into a CSV file
    - You want to create backups of a database

### 2. Managed MongoDB overview

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


## 1. Getting started



### 1.1 The main dashboard

Head over to [https://app.easyfaas.de/](https://app.easyfaas.de/) and register or login.

<center>
    <img src="/images/tutorial/easyfaas/maindashboard.png" style="width:50%" alt="Easyfaas main dashboard">
</center>

The main dashboard is the central control system for EasyFAAS. In here, you will se an overview over the different services that are available.

### 1.2 Create a new function

Next click on **New function**, which takes you to the function type selection screen.

![easyfaas function type selection](/images/tutorial/easyfaas/newfunction.png)

**What is a timed, and what is a continuous function?**


{{< tabs >}}

  {{< tab "Timed Function" >}}
   A timed function is best suited for jobs that do not need to run all the time, but rather run at specific intervals. If you have used Cron in the past, this is pretty much it. 

   You can define Cron schedules as you are used to, like for example


    <table>
        <tr>
            <th>
                Cron expression
            </th>
            <th>
                Meaning
            </th>
        </tr>
        <tr>
            <td>30 2 * * *</td>
            <td>Every day at 2:30</td>
        </tr>
        <tr>
            <td>30 * * * *</td>
            <td>Every day, every hour at :30 (2:30, 3:30, 4:30 ...)</td>
        </tr>
        <tr>
            <td>01 2 1 * *</td>
            <td>2:01 on the first of every month</td>
        </tr>
    </table>


{{< notice "info" >}}
I like to use the website [https://crontab.guru/](https://crontab.guru/) to check my expressions
{{< /notice >}}
  {{< /tab >}}

  {{< tab "Continuous Function" >}}
  A continuous function runs all the time, and is best used if you want a webservice or API to run.
  {{< /tab >}}

{{</ tabs >}}

### 1.3 The create function screen

For this tutorial I went with a continuous function

![Create a new continuous function](/images/tutorial/easyfaas/createfunctioncontinuous.png)

Let us take a look at the differnet elements

**Function name**

This can be whatever you want. The function name will later be converted to a lower-case, "-" seperated form.
Like "My awesome FuNcTiOn" will become "my-awesome-function".

**Function count**

This is where **scalability** comes into play. For now leave function count at 1, but if you later on experience that you need more power, you can easily up-scale your function here.

**PIP requirements**

Now instead of creating a layer for your FAAS function, you can **just enter your pip packages here**, and it will automatically install them. Easy as that.

**Debian requirements**

All functions are build in Debian. Meaning you can easily install any Debian package if you need it. If you have installed it on your local system with "apt install ..." you can list it here. This is useful if you might need some system based tools like imagemagic, wkhtml and others. **This is actually not supported yet in other FAAS services**.

**Visibility**

Your EasyFAAS function comes with security enabled by default. If your function is public, it will be accessible for everyone. If it is private, you will need to send an auth token to the endpoint. 
Does that mean you need to create new users and everything? No, you can just get an auth token using our RestAPI using your **normal user and password**, and then use that token to fire towards your function. 
Easy as that.

