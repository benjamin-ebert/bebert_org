---
title: "How to start building Magento 2 extensions"
date: 2019-09-06T08:49:19+02:00
draft: false
tags: ['Magento']
---

First the most important thing ist that you clearly know what you want to change.
Is it only a frontend change or do you need to implement some logic?

As there is no documentation that clearly explains what every bit of code does and what it depends on, you need to find that out on your own.
Start in the frontend, the dev tools are your best friend here.

1. In the browser, inspect the place you want to change
I inspected the amount of an applied discount code on the checkout summary. Then in the dev tools I copied this:
```
<span class="price" data-bind="text: getValue(), attr: {'data-th': name}" data-th="checkout.sidebar.summary.totals.discount">
```

2. In PhpStorm, hit shift + cmd + f and search for terms that are related to what you want to do
First I searched for what I had copied in the browser, which led me to the html file that displays the discount.
It had a data-bind property "getCouponCode()". I did another search in PhpStorm to find out where the logic was.
I tried different variations and when I reduced the search term to "getCoupon" I finally ended up with Discount.php. A last search for "discount" led me to Validator.php which turned out to be the jackpot. To summarize: start at the frontend, search for promising terms and drill further down with what you find in the results. Open a few files that seem promising and you'll probably find what you were looking for.
\Magento\Quote\Model\Quote.php might be useful too

So in my case, I needed to alter the calculation of discounts, so I started with looking at the coupons in the frontend. Then by searching for terms from the frontend code I figured out where the frontend gets its data from, eg. Validator.php, the place where discounts are calculated, which is what I was looking for.

3. Build your module and get your dependencies straight. 
4. Copy relevant files and their directory structure 
