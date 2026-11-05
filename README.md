# Django Tutorial (Poll Applications) - Alpha Team

This is a Tutorial application to create in python environment in Django that will be used as a warmup educational effort.

Target versions: *python 3.10.12 / django-5.2.18*

## Configuration
### Some important tips for your setup

* Ensure that you are running the designated python version and is active in your environment. I recommend you to setup venv and activate it with: source venv/bin/activate
* This code will unlikely run as it is in a pythonanywhere or environment without creating a .venv file with the SECRET_KEY environment variable and make sure that it is exported in the terminal session that launches the server. If using zsh in mac you might want to add the variable manually using double quotes: export SECRET_KEY="YOUR KEY"
* The database is not kept until we decided so. For now you have to run the command: __python manage.py migrate__ where the settings.py lives.

## New Feature: Adding a Bar Chart in the List View

### Functional Requirements
-- Requirements definition-- (Paul)

### Technical Design (Components to be adjusted)
Since this is a graphical component we need some data to be propagated to the HTML and be rendered using a simple approach: 

* The simplest can be to add a javascript or CSS function that takes the plain rendered values (can be hidden values). This can be done by taking the context values passed to the `results.html` template as part of the context of each vote.
* The Result View already passes the vote count. We can compute the total sum of the votes to apply the rendering algorithm together with the other values and put it in the context. Other option is to compute the fraction to be rendered and apply a rendering algorithm
* After the data is rendered we can call the javascript function using the `onLoad()` javascript event to trigger the bar chart function. We will explore the possibility of using CSS or other UI/UX tooling. The core principle is to avoid extra coding.

Expected Changes:
- `templates/polls/results.html` Template - To render the computed factor per each answer that will render the size of the bar
- `polls/views.py` Ad an extra computed variable (as a tupple) so that it can be rendered easily
- Extra CSS and Styles in the static `pols/static/polls/style.css` to allocate the style that will shape the bar chart and its surroundings

