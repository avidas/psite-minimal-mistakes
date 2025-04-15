---
layout: post
title: "Web Payments by First Principles: Testing"
date: 2017-05-19 16:21
comments: true
published: true
categories: Software Payments APIs
---

In recent years, payment API providers have made integrating payments much easier than it used to be. Instead of dealing with banks and exchanges, ecommerce apps can integrate with payment gateways that will allow accepting any form of credit cards, and most payment methods such as Apple Pay and PayPal. Large pdfs with instructions manuals are replaced by intelligent documentation sites with walkthroughs and tutorials. Despite that, it is not uncommon to hear developers referring payments as their least favorite part of the development process. Payments integrations are often seen as a necessary evil, to be done once, and hopefully be forgotten thereafter. Often the reasoning is that investing in better payments integration is often not a profit center for companies.

I have worked the last few years in the online payments industry, building APIS, sdks and reliability tools. While payments integration has gotten easier, developers still do make mistakes which are easily avoidable. Here are some of the best practices I would recommend for testing payments in your applications.

1. **Isolate interation between application code and payment gateway in a package**: Once an app grows to a certain size, it may have different ways of interacting with payments gateways. You may be accepting recurring payments and accepting webhooks from the payments provider, just in time checkout or interact with point of sales systems. Having your own package that abstracts out interaction with the payments APIs can help centralize all outgoing requests back and forth with the payments API. You can add your own logging and monitoring, stub out the interaction with payments API to have faster unit tests and centralize knowledge about how you serialize and deserialize messages from and to your payments provider.

2. **Sandbox Testing**: Most payment API/gateways expose a sandbox environments where you can test out a real integration with the API without moving any money. Ideally your integration tests running continously in Jenkins/Travis/Circle CI should be hitting those endpoints.

3. **Monitoring**: You should monitor your sandbox integration as well as your live system. What does the graph of 200s vs 400s HTTP response codes from the payments API look like? Are you getting unexpected 400s? How about 500s? What does the response times look like?

4. **Automated QA**: To avoid putting undue stress on your computation and database resources, background tasks are common strategies to do break down calculations for common payments needs such as reporting and analytics. When calculations are done in partial chunks, automated jobs that test whether those calculations have been done properly can reduce a lot of load for your support and developers when something goes wrong midway between a job, or failure.

5. **Negative/Failure Testing**: Special card numbers provided by payments providers can help you recreate payment declines due to potential denial from processors for reasons such as not enough funds in account. You may also be able to test for rejections due to fraud and compliance. This helps lower the range of potential unknown errors your site may run into, especially when expanding to new markets or accepting more payment methods.

6. **Live testing**: Live testing against payment providers is often tricky, and can led to accounts getting shut down if there is undue load on the API. Despite that, some testing in live is absolutely necessary before you can be confident that on release day, your integration is working as expected.

7. **Test for absence of sentive information**: Storing user information such as credit card number or passwords is a very common way of violation of PCI compliance. Regex patterns can be used to make sure that neither your logs nor your database is storing sensitive information.

I intend to write more posts in this series, covering topics such as considerations before and after going live with payments, when scaling up and so on. If you liked this post, please share or comment.

If you have feedback on this blog post or integrating payments, please [feel free to reach out!](mailto:avi@aviadas.com).
