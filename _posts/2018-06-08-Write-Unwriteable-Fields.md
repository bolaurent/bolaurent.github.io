---
layout: post
title: Apex: Write to unwriteable SObject fields
date:   2018-06-06 21:16:00 -0800
categories: schema apex
---

Have you ever wanted to create an SObject in memory, and write to one or more fields that are normally unwriteable? For instance,
CreatedDate, or a formula field. You might want to do this in a unit test class. Or you might have a formula field in an SObject
held by a VisualForce controller that you want
to update before committing to the database. Normally, Apex won't let you do that. Here's a workaround.

{% highlight apex %}
public static SObject makeSObjectFromFields(Map<String, String>fields, System.Type targetType) {
    String jsonrep = json.serialize(fields);
    return (SObject)json.deserialize(jsonrep, targetType);
}
{% endhighlight %}

Here's an example of calling that method:

{% highlight apex %}
OpportunityLineItem oli = (OpportunityLineItem)SchemaUtility.makeSObjectFromFields(
    new Map<String,String>{
        'ListPrice' => String.valueOf(pbe.UnitPrice)
    },
    opportunityLineItem.class
);
{% endhighlight %}
