---
layout: post
title: "Smart Control Groups"
categories: [EmailMarketing]
---
According to the Bing Chat: A **control group** is a subset of the total group of customers being exposed to a test. In marketing segmentation, control groups are used to measure the impact of a specific campaign or customer journey. Specifically, control groups are the customers you are targeting with a particular campaign who will not receive that campaign.

## Smart Control Groups
Most control groups that I stumbled upon were plain random split such as 90/10% or 80/20%. It is a natural, practical implementation of a 10% or 20% subset to be excluded and...measured against the targeted group. Nevertheless, I found a smarter formula for creating a subset which I call a **Smart Control Group**. 

This formula is based on the fact that an organization uses numeric IDs to identify campain members.For example the ACME Company identifies its clients by 6-digits numeric IDs for example: 111111, 123456, 102034, and so on. Let a whole campagin segment contains random clients and a Smart Control Group (SCG) identifies a segment by the last digit only. As a result with a large enough sample (calculations below) the SCG that contains clients who's ID ends with any natural number from 0-9, makes 10% out of the total segment. And similarly, a larger SCG that contains clients who's ID ends with two or three different natural numbers, make 20% and 30% respectively.

## Benefits of Smart Control Groups
*   Easy to use
*   Always predictable
*   No need to keep a record of clients excluded from a campaign
*   Same clients can be excluded from multiple journeys such as onboarding journey series
*   Beautiful math

## Math Behind Smart Control Groups
```python
import random


def control_group_distrib(list_name : list):
  for i in range(10):
    count = sum(1 for num in list_name if num.endswith(str(i)))
    percent = count/len(list_name) * 100
    print(str(i) + " counted " + str(count)  + " | " + str(percent) + "%")


#ClientIDs increment using a regular counter. This creates an array of ClientIDs from 0-... as a main pool of clientList.
clientsList = ["ID_" + str(i).zfill(3) for i in range(10000)]

#Get random Clients from the clientsList to create a random segment
list1 = random.sample(clientsList, 20)
#print("\n\n" + str(list1))
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