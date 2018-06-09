---
layout: post
title: Apex: Write to unwriteable SObject fields
---

Have you ever wanted to create an SObject in memory, and write to one or more fields that are normally unwriteable? For instance,
CreatedDate, or a formula field. You might want to do this in a unit test class. Or you might have a formula field in an SObject
held by a VisualForce controller that you want
to update before committing to the database. Normally, Apex won't let you do that. Here's a workaround.

