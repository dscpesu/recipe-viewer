# 3D Recipe Viewer

## Flask App
The flask app runs a flask website. First upload a recipe image in the website. It extracts text from the image, then splits the text into sentences. Each sentence is classified into either an ingredient or a step. The ingredient sentences are further split into unit, quantity and ingredient name. The corresponding image for each ingredient is extracted from a google image search by a scraper. For each step, a YouTube video is shown and verbs are extracted from the sentence. A GIF is shown for each verb.
To run the flask app:
 - Run `python app.py`
 - Go to `http://localhost:5000/` from a browser

OR go to [this link](https://dsc-flask-api-heroku.herokuapp.com/) to check a slightly older version of the app running on Heroku. (It might take some time to load if it has been inactive for a while)

## Requirements 

 - Python 3.5.6
 - See `requirements.txt` in Flask-app submodule for requirements of the Flask app
