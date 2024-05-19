---
layout: post
title: AWS Cloud Resume Challenge
subtitle: Create and host a cloud resume website
gh-repo: https://github.com/kai-ion/aws-cloud-resume
gh-badge: [star, fork, follow]
tags: [AWS, Cloud, Web Development]
comments: true
---

This is a demo post to show you my progress in the [AWS Cloud Resume Challange](https://cloudresumechallenge.dev/docs/the-challenge/aws/)

**Steps**

1. Static website
2. Custom Domain
3. S3 bucket
4. Cloudfront
5. SSL Certificate
6. Route53 DNS Management
7. Javascript - Visitor Counter
8. DynamoDB
9. AWS Lambda_Function
10. AWS Lambda_Function connection
11. Git and CI/CD

## Static Website

1. I created my static website based on a template

![website](/assets/img/img-AWS-Cloud-Resume/website.PNG)

## Custom Domain

1. I used namecheap to purchase one domain and then I also used AWS Route 53 to purchase a domain
- https://www.namecheap.com/
- https://aws.amazon.com/route53/ 


Here's a useless table:

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |


How about a yummy crepe?

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

It can also be centered!

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .mx-auto.d-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
