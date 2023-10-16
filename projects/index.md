---
layout: page
title: Projects
description: otho's constructs
permalink: /projects/
---


<!-- Here are some of the non-trivial projects I built for the past few years.  My
definition of a *project* is a bit fuzzy; for now, these are things that I have
worked on with a tangible outcome like a library, website, or a game.

<ul>
  {% for post in site.categories.projects %}
    <li>
        <span>{{ post.date | date_to_string }}</span> » <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
        <meta name="description" content="{{ post.summary | escape }}">
        <meta name="keywords" content="{{ post.tags | join: ', ' | escape }}"/>
    </li>
  {% endfor %}
</ul>

<h4>Others</h4> -->

**DC v Marvel deep learning superhero classifier**  
The power of FastAI, PyTorch and ResNet18 with this deep learning neural network model that accurately classifies DC and Marvel superheroes/characters - making it a must-have tool for any comic book database and fandom

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Python&color=3776AB&logo=Python&logoColor=FFFFFF&label=" alt="Python" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=PyTorch&color=EE4C2C&logo=PyTorch&logoColor=FFFFFF&label=" alt="PyTorch" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Jupyter&color=F37626&logo=Jupyter&logoColor=FFFFFF&label=" alt="Jupyter" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=🤗+Hugging+Face&color=FFCB4C&l&label=" alt="Hugging Face" style="padding-top: 3px;">}}

* [View code on Colab](https://colab.research.google.com/drive/1XSerXrQUfuNg3A6fpxEa4NUtL8XmokMN?usp=sharing)
* [View deployed model on HuggingFace](https://huggingface.co/spaces/troublledwaters/comicsClassifier)



**AI startup writing assistant**  
I developed an AI writing assistant that leverages OpenAI's GPT-3 model to generate high-quality writing for emails, social media posts, and memos, streamlining communication and boosting productivity.

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Python&color=3776AB&logo=Python&logoColor=FFFFFF&label=" alt="Python" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=OpenAI&color=412991&logo=OpenAI&logoColor=FFFFFF&label=" alt="OpenAI" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=GPT-3&color=412991&logo=OpenAI&logoColor=FFFFFF&label=" alt="GPT-3" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Streamlit&color=FF4B4B&logo=Streamlit&logoColor=FFFFFF&label=" alt="Streamlit" style="padding-top: 3px;">}}

* [View app on StreamLit](https://inkwell.streamlit.app/)
* [View code in GitHub](https://github.com/heytomiwa/startup-writing-assistant)


**Volcano Eruptions in the 21st Century: Interactive Visualization**  
A data-driven project that uses Tableau to create an interactive and informative visualization of volcano eruptions that have occurred in the 21st century.

{{< image src="/img/Data_viz - New Design.png" alt="Volcani Eruption data viz" position="left" style="width: 85%;" >}}

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Tableau&color=E97627&logo=Tableau&logoColor=FFFFFF&label=" alt="Tableau" style="padding-top: 3px;" >}}

[View viz in Tableau](https://public.tableau.com/app/profile/tommy.adedokun/viz/VolcanoEruptionsinthe21stCentury/DataViz_)


**Predicting House Prices using Machine Learning**  
technical mastery in data cleaning, exploratory data analysis, and feature engineering by implementing several machine learning algorithms using Python libraries like Pandas, NumPy, and ScikitLearn, culminating in a real-time prediction Flask API endpoint that showcases my end-to-end ability

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Python&color=3776AB&logo=Python&logoColor=FFFFFF&label=" alt="Python" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=NumPy&color=013243&logo=NumPy&logoColor=FFFFFF&label=" alt="NumPy" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=pandas&color=150458&logo=pandas&logoColor=FFFFFF&label=" alt="Pandas" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=scikit-learn&color=222222&logo=scikit-learn&logoColor=F7931E&label=" alt="Scikit-Learn" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Flask&color=000000&logo=Flask&logoColor=FFFFFF&label=" alt="Flask" style="padding-top: 3px;" >}}


[View code in GitHub](https://github.com/heytomiwa/house-price-prediction-with-flask-serving)


**Global Diversity in the NBA Draft**  
Scraped and cleaned data from Wikipedia on the NBA draft to analyze the diversity of foreign nationals in the drafts.

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Python&color=3776AB&logo=Python&logoColor=FFFFFF&label=" alt="Python" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Jupyter&color=F37626&logo=Jupyter&logoColor=FFFFFF&label=" alt="Jupyter" style="padding-top: 3px;">}}

[View code in github](https://github.com/heytomiwa/NBA-Drafted-Players-2009-2021-Analytics)


**Bike-share User Analytics Case Study**  
To help in creating a new marketing strategy to help convert casual users to subscribers, I analyzed a year’s worth of data
on a fictional bike-share company - Cyclistic, with SQL on a PostgreSQL database to understand the differences and
similarities in the behaviour of user types.

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=PostgreSQL&color=4169E1&logo=PostgreSQL&logoColor=FFFFFF&label=" alt="PostgreSQL" style="padding-top: 3px;">}}

[View code in GitHub](https://github.com/heytomiwa/Bike-share-Analytics)


**World Happiness Report: Regional Health Analytics**  
This project utilizes data from the World Happiness Report to provide insights on the relationship between happiness and health at the regional level. This data-driven analysis sheds light on the factors that contribute to the happiness and well-being of people in different regions, informing public health policies and initiatives.

{{< image src="/img/projects_2-copy.png" alt="Correlation map" style="width: 85%;" >}}
{{< image src="/img/projects_5.png" alt="Chart 1" style="width: 85%;" >}}

{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Excel&color=217346&logo=Microsoft+Excel&logoColor=FFFFFF&label=" alt="Microsoft Excel" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=PowerPoint&color=B7472A&logo=Microsoft+PowerPoint&logoColor=FFFFFF&label=" alt="Microsoft PowerPoint" style="float: left; margin-right: 3px; padding-top: 3px;" >}}
{{< image src="https://img.shields.io/static/v1?style=for-the-badge&message=Tableau&color=E97627&logo=Tableau&logoColor=FFFFFF&label=" alt="Tableau " style="padding-top: 3px;">}}

[View presentation in google drive](https://drive.google.com/file/d/1TztOhuCcGftp1DyDm8gzwCfJUKzwNrBS/view)