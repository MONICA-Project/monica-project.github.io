# Monica Tutorials
<!-- Short description of the project. -->

Monica tutorials is the repository of all the tutorials for MONICA artifacts. 

<!-- A teaser figure may be added here. It is best to keep the figure small (<500KB) and in the same repo -->

## Getting Started
The website generated from this repository can be found at https://monica-project.github.io/

<!-- Instruction to make the project up and running. -->
### Adding New Sections 
In order to add a new section on the tutorial, please add your markdown (your_tutorial.md) to [contents/_sections folder.](https://github.com/MONICA-Project/monica-project.github.io/tree/master/contents/_sections) 
The markdown should have following format
```markdown
---
layout: default
title: <Title of the Tutorial>  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">Title of the Tutorial</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->
Few words about the tutorial

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## First
Contents 
## Second
Contents
```

### Adding Images to the Sections
You can add image to [assets/img folder](https://github.com/MONICA-Project/monica-project.github.io/tree/master/assets/img) and directly link it in the markdown file.

## Affiliation
![MONICA](https://github.com/MONICA-Project/template/raw/master/monica.png)  
This work is supported by the European Commission through the [MONICA H2020 PROJECT](https://www.monica-project.eu) under grant agreement No 732350.


[The code is taken from the minimal theme](https://pages-themes.github.io/minimal/) by [orderedlist](https://github.com/orderedlist)


