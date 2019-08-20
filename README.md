# 3D Recipe Viewer

## Usage

To run the flask app:
 - Run `python app.py`
 - Go to `http://localhost:5000/` from a browser

OR go to [this link](https://dsc-flask-api-heroku.herokuapp.com/) to check a slightly older version of the app running on Heroku. (It might take some time to load if it has been inactive for a while)

## Requirements 

 - Python 3.5.6
 - See `requirements.txt` in Flask-app submodule for requirements of the Flask app

## Objective

People who are new to cooking often find it difficult to understand and recognize certain parts of the recipe. For example, the person may not recognize the name of some of the ingredients but they can identify it with images, or they may not know how to execute a certain step the way it is described. Our primary objective is to ease the process of cooking with recipes.
Additionally we are also trying to convert recipes which are present on paper, into digital form. 

## Basic Working

First upload a recipe image in the website. It extracts text from the image, then splits the text into sentences. Each sentence is classified into either an ingredient or a step. The ingredient sentences are further split into unit, quantity and ingredient name. The corresponding image for each ingredient is extracted from a google image search by a scraper. For each step, a YouTube video is shown and verbs are extracted from the sentence. A GIF is shown for each verb in each step.

## Technical Details

This project consists of several modules. Most of it was implemented in Python 3 with the help of external modules including Flask, Pytesseract, Scrapy, NLTK and OpenCV. The modules of this project are given below.
1. **Image to Text converter**: This module uses the user uploaded image and extracts text from it. This is done with the help of modules like OpenCV and Tesseract OCR (pytesseract module). OpenCV is used to read the image, resize it, remove noise from it and to convert it to grayscale. Tesseract is an optical text recognition software and pytesseract is a python module to use tesseract in python. It recognises characters and extracts text from an image.
2. **Sentence Classifier**: This module takes a list of sentences as input and classifies them as either a step/instruction or an ingredient. This is achieved by training a Maximum Entropy Classifier on a limited set of ingredients and steps extracted from a [recipe dataset](https://eightportions.com/datasets/Recipes/#fn:1). The data is preprocessed by extracting features from it (the features include POS tags, unigrams, bigrams and trigrams). The training is done only once and the model is saved. This trained model is used to classify the sentences. 
	- If the sentence is classified as an ingredient, it is passed through an ingredient parser which splits the ingredient into quantity, unit and ingredient name. For example, "2 cloves garlic, crushed" is split into {'name': 'garlic, crushed', 'unit': 'cloves', 'quantity': '2'}.
	- If the sentence is identified as a step/instruction, part-of-speech (POS) tagging is done on it and a list of all verbs in the sentence is returned along with the sentence.
3. **Web Scraper/Crawlers**: These scrapers are used to get images, videos and GIFs relevant to the recipe. Images of each ingredient is scraped from Google Image Search. Video links of every step is scraped from YouTube search and are embedded into the website. Scrapy python module is used to implement these scrapers. Each scraper/spider has a start URL which it scrapes first. XPath selectors are used to get the relevant URL or image. The google images scraper saves each image to disk. The GIFs scraper returns a list of URLs to the GIFs given a list of search term. The YouTube scraper returns a list of video IDs given a list of search terms.
4. **Flask App**: The website uses Flask as its backend. It handles all the inputs including uploaded files, checkboxes and buttons using forms. It calls the relevant function based on the input and displays output using HTML templates. Jinga2 template engine is used by flask to display the templates which allows us to use expressions and variable names instead of hardcoding values. CSS is used to make the HTML appear more attractive and responsive.

## Future Work

 - Build a cloud API and a mobile app.
 - Making a more pleasant experience for the user by improving the UI and making it more responsive.
 - Create a user management system (users can create and save their recipes).
 - With the users data we can create and make a database which other users can view and use.
 - Extracting recipe directly from websites instead of using images.
 - Using 3D models and animations to show the recipes in 3D.
 - Finding more relevant videos and GIFs which show the steps more clearly.
 - Creating and using bigger datasets to increase the accuracy of text recognition and classification of sentences.