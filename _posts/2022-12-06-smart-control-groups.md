---
layout: post
title: "Smart Control Groups"
categories: [EmailMarketing]
---
Most control groups that I stumbled upon were plain random splits such as 90/10% or 80/20%. It is a natural and practical implementation of an excluded subset. Nevertheless, I found a smarter formula for creating a control group.

## Smart Control Groups
According to the **Bing Chat**:
> "A control group is a subset of the total group of customers being exposed to a test. In marketing segmentation, control groups are used to measure the impact of a specific campaign or customer journey. Specifically, control groups are the customers you are targeting with a particular campaign who will not receive that campaign."


This formula assumes that an organization uses numeric IDs to identify campain members. For example the ACME Company identifies its clients using 6-digit (or more) IDs such as: 111111, 123456, 102034, and so on. This could also be any alphanumeric combination such as ID_123456 or Client-111111.

Let a whole campagin segment contains 10000 random clients. A Smart Control Group (SCG) identifies a subset using the **last digit** from the ID that is: 11111**1**, 12345**6**, 10203**4**. In other words, a subset contains clients whose ID ends with **1** or...in fact any natural number from 0-9.

As per calculations below, with a large enough sample (over 1000), each subset represents **10%** of the entire campaign segment.

## Benefits of Smart Control Groups
*   Easy and predictable as opposed to random splits
*   Pick a number or two from 0-9 to represent a 10% or 20% subset - a control group to exclude from a campaign
*   No need to keep a record of randomly excluded clients for each campaign or a journey
*   Easy to track a contact lifecycle through multiple journeys knowing that the ID was a part of the segment or excluded in a subset
*   Beautiful math

## Math Behind Smart Control Groups
This Python script generates a clients list, then randomizes for a segment and pulls subset for a control group. Smaller samples are quite random but larger samples approximate almost evenly toward 10% for each subset. In other words it does not matter whether a subset contains IDs that end with 3 or 7 or 0. With samples large enough, each control group is close to 10% of the segment.
```python
import random
def control_group_distrib(list_name : list):
  for i in range(10):
    count = sum(1 for num in list_name if num.endswith(str(i)))
    percent = count/len(list_name) * 100
    print(str(i) + " counted " + str(count)  + " | " + str(percent) + "%")

#ClientIDs increment using a regular counter. This creates an array of ClientIDs from 0-... as a main pool of clientList.
clientsList = ["ID_" + str(i).zfill(6) for i in range(10000)]

#Get random Clients from the clientsList to create a random segment
list1 = random.sample(clientsList, 20)
list2 = random.sample(clientsList, 129)
list3 = random.sample(clientsList, 1483)

#Control Groups even distribution
print(f"Total number of global Clients is: {len(clientsList)}\n\
A random sample that represents a segment is: {str(len(list1))}\n\
In such a small, randomized segment, it is impossible to use a control group\n", end="\n\n")

control_group_distrib(list1)

#Control Groups even distribution
print(f"\nTotal number of global Clients is: {len(clientsList)}\n\
A random sample that represents a segment is: {len(list2)}\n\
In a larger segment, Control Groups created using the last digit are still not well distributed.", end="\n\n")

control_group_distrib(list2)

#Control Groups even distribution
print(f"\nTotal number of global Clients is: {len(clientsList)} \n\
A random sample that represents a segment is: {len(list3)} \n\
In a segment over 1000 randomized ClientIDs, Control Groups created using the last digit are almost evenly distributed for each digit.\n", end="\n\n")

control_group_distrib(list3)
```

## Resources
*   [Replit - Pyton Online Sandbox](https://replit.com/@karolcholewa/ControlGroups#main.py)
*   [Control Groups in Marketing](https://www.optimove.com/resources/learning-center/control-groups-in-marketing#The_Guide_to_Control_Groups_in_Marketing)