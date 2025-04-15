---
layout: post
title: "Web Payments by First Principles: Data Architecture"
date: 2017-10-25 20:22
comments: true
published: true
categories: Software Payments APIs Database
---

Once you start receiving payments on your site, congratulations! You are likely building something people want. But now you are at the point of having to manage payments data. Developers are generally aware that handling payments data should be done with care, but it is not immediately obvious what the different considerations are. In this blog post, we will go over strategies that you can follow to future proof your payments stack from the point of a fledgeling startup to a mature, stable business.

With storing payments data, there are quite a few considerations. What you should store and shouldn’t. In the event of a security breach on your site, you want your users financial information to be protected. Moreover, you want to architect your data storage for any current and future stakeholder requests. When it comes to payments, there are generally many stakeholders, let’s talk about a handful of them.

You are going to have technical stakeholders: your managers and other product teams who have questions about payments. Business entities that have to report their earnings for filing taxes and reporting earnings to shareholders who will need their data from you. As someone buying/selling online, your data needs to be stored in a way to make sure you don’t break compliance (PCI/SOX etc). Support/operations will be your stakeholders when customers have problems paying and come to you for help. Let’s get into how we can address these asks.

1. **Avoid storing sensitive personal information**: Any application sending payments information such as credit card numbers, cvv to their server will have to become PCI compliant. This a financial and logistics burden which you can avoid for the most part by using a gateway provider such as Braintree/Stripe/Adyen. Usually your browser/mobile app will authenticate with the gateway and get back a token, which you can relay back to your server. This removes the danger of accidentally logging payments data, since the only data your server will see is a payments token. Even if you do get data breached, these tokens would not be useful to the attacker. This also removes the need for you to be PCI compliant which is tens of thousands of dollars in yearly expenses.  More data you should avoid storing include any plaintext passwords and secret keys, common web best practices.

2. **Freeze request/response from external providers**: You need to store every single request/response that you are making to your external providers, ideally in an append-only data storage. One of the common requests that we get in payments is to recreate the transaction as it happened. This is hard to do without storing the data at point in time of the transaction. Moreover, the business logic related to transaction such as taxes, fees calculations also need to be versioned and stored so that you can recreate the transaction at a certain point in time.  

3. **Encourage immutability and lower side effects**: Similar to the point above, you should never destroy payments or charging data. There are easy ways to archive and hide the data from users. This is very useful for historical financial reporting, triaging potential inefficiencies in your charging/billing process, and dealing with any disputes with your payments provider.
 
4. **Denormalize and index for searchability**: Payments data is generally more write heavy but needs to be stored in a way for ease of triaging. Most payments providers provide unique request ids with their calls, and you should supply your own if that is possible. That way, you can set up bidirectional tracking, so that each individual call to payments is trackable from both sides. Setting indices on those unique ids is helpful for search. If the table is growing too large, it is useful to only keep upto a certain limit in your app and store the rest in a data warehouse such as AWS Redshift or Google Bigquery. The data warehouse strategy also enables you to normalize the data if you want easier access to data in one place and avoid expensive joins.

5. **Prefer cents as units instead of dollars**: You can avoid a whole class of floating point bugs by storing in cents and using integers as opposed to float for all your arithmetic. Since floats in computing are really a representation of an infinite number, the can only be approximation and lead to hideous rounding errors. This is a good read on that topic https://stackoverflow.com/questions/3730019/why-not-use-double-or-float-to-represent-currency. Using established tools such as the money gem for currency in ruby is also very useful.

The above strategies will be useful for both internal and external users of your payments stack and help to protect your money and time when it comes to payments data. Please reach out via comments or [email with feedback!](mailto:avi@aviadas.com).
