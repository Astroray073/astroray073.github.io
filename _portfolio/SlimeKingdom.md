---
title               : "Slime Kingdom"
startDate           : 2017-03 
endDate             : 2017-09
lastModifiedAt      : 2016-03-09T16:20:02-05:00
excerpt             : "Casual tower defence game development"
header:
    overlay_image   : /assets/images/portfolio/slimekingdom/main.png
previewImage        : /assets/images/portfolio/slimekingdom/main.png

image_location      : /assets/images/portfolio/slimekingdom
---

{% include video id="1RswM8XEVh6_HeCPqWpyF7EIGcv9qwCjY" provider="google-drive" %}

## Introduction

Slime Kingdom is tower defence game to defend the kingdom of slimes from deadly hostiles.
The objective fo the game is to protect King slime during each waves.

Unique points of this game are...

- The king slime which is protect target can attack nearby enemies.
- Towers can move!
- Can duplicates a tower.

### Team members & responsibilites

Disclaimer : My main role was programmer but as we are small team, I needed to take other responsibilites.
{: .notice--info}

- No. of people : 2 game designers, 2 programmers, 3 graphic designers.
- Duration : about 6 months.

Role : *Main programmer*, *Project manager*, and *Animator*

### Development environment

The list of tools was used in development.

- Windows 10
- [Unity (5.6.03f)](https://unity.com)
- [Spine](http://esotericsoftware.com/)
- [Spine-unity](https://github.com/EsotericSoftware/spine-runtimes/tree/3.7/spine-unity)
- Git hosted by [Bitbucket](https://bitbucket.org)
- [NPOI](https://archive.codeplex.com/?p=npoi)

## Implementation

There are number of features to develop through the project.

### Data control via Microsoft Excel

**Requirements**

1. To test game balance, external data layer was needed.
2. It makes game designers easier to manipulate game specific data.

**Implementation**

<figure class="align-center" style = "padding: 2em 2em;">
  <img src="{{ site.url }}{{ page.image_location }}/excel-flowchart.png" alt="">
  <figcaption>Data flow from Excel to Unity</figcaption>
</figure> 

When excel file is modified, the file will be parsed into ScriptableObject instance.

<figure class="align-center" style = "padding: 2em 2em;">
  <img src="{{ site.url }}{{ page.image_location }}/excel-parsing.png" alt="">
  <figcaption>Parsing result</figcaption>
</figure> 

As figure shown above, it is capable to manage game data through Excel.

### Stage editor

Stage editor is most important feature to generate the contents of this type of game.

<figure class="align-center" style = "padding: 2em 2em;">
  <img src="{{ site.url }}{{ page.image_location }}/editor.png" alt="">
  <figcaption>Stage Editor inside Unity</figcaption>
</figure> 

**Limitations & Improvements**

Tile informations are stored in list. Because serializing Dictionary is tricky on Unity.
Tile informations are accessed frequently. Dictionary(Hashtable) is better choice for the container.