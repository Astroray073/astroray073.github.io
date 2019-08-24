---
title               : "Slime Kingdom"
startDate           : 2017-03 
endDate             : 2017-09
lastModifiedAt      : 2016-03-09T16:20:02-05:00
excerpt             : "Casual tower defence game development"
header:
    overlay_image   : /assets/images/portfolio/slimekingdoms/main.png
previewImage        : /assets/images/portfolio/slimekingdoms/main.png

image_location      : /assets/images/portfolio/slimekingdoms
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

- Members : 2 game designers, 2 programmers, 3 graphic designers.
- Duration : about 6 months.

Role : Main programmer and Animator

### Development environment

The list of tools was used in development.

- Windows 10
- [Unity (5.6.03f)](https://unity.com)
- [Spine](http://esotericsoftware.com/)
- [Spine-unity](https://github.com/EsotericSoftware/spine-runtimes/tree/3.7/spine-unity)
- Git hosted by [Bitbucket](https://bitbucket.org)
- [NPOI](https://archive.codeplex.com/?p=npoi)

## Requirements

- Our goal was making sample 5 stages.
- To test game balance, external data layer was needed.
- It makes game designers easier to manipulate game specific data.

## Implementation

### Data control via Microsoft Excel

<figure class="align-center" style = "padding: 0em 2em;">
  <img src="{{ site.url }}{{ page.image_location }}/excel-flowchart.png" alt="">
  <figcaption>Data flow from Excel to Unity</figcaption>
</figure> 

When excel file is modified, the file will be parsed into ScriptableObject instance.

<figure class="align-center" style = "padding: 0em 2em;">
  <img src="{{ site.url }}{{ page.image_location }}/excel-parsing.png" alt="">
  <figcaption>Parsing result</figcaption>
</figure> 

As figure shown above, it is capable to manage game data through Excel.

### Stage editor

<figure class="align-center" style = "padding: 0em 2em;">
  <img src="{{ site.url }}{{ page.image_location }}/editor.png" alt="">
  <figcaption>Stage Editor inside Unity</figcaption>
</figure> 

Stage editor is most important feature to generate the contents of this type of game.

Capable of

- Edit tiles of a stage
- Setting wave information
- Save and load a stage
