---
layout: post
title: 'Docker EP - 10: Let''s Dockerize a Flask Application'
date: 2024-08-18 11:49:08+00:00
render_with_liquid: false
category: Docker
tags:
- Flask
- Python
- Tutorial
- Development
---



<p class="wp-block-paragraph">Let’s develop a simple flask application, </p><ol class="wp-block-list"><li><strong>Set up the project directory:</strong> Create a new directory for your Flask project.</li></ol><pre class="wp-block-syntaxhighlighter-code">mkdir flask-docker-appcd flask-docker-app</pre><p class="wp-block-paragraph">2. Create a virtual environment (optional but recommended):</p><pre class="wp-block-syntaxhighlighter-code">python3 -m venv venvsource venv/bin/activate</pre><p class="wp-block-paragraph">3. <strong>Install Flask</strong></p><pre class="wp-block-syntaxhighlighter-code">pip install Flask</pre><p class="wp-block-paragraph">4. Create a simple Flask app:</p><p class="wp-block-paragraph">In the <code>flask-docker-app</code> directory, create a file named <code>app.py</code> with the following content, </p><pre class="wp-block-syntaxhighlighter-code">from flask import Flaskapp = Flask(__name__)@app.route('/')def hello_world():    return 'Hello, Dockerized Flask!'if __name__ == '__main__':    app.run(host='0.0.0.0', port=5000)</pre><p class="wp-block-paragraph">5. <strong>Test the Flask app:</strong> Run the Flask application to ensure it’s working.</p><pre class="wp-block-syntaxhighlighter-code">python app.py</pre><p class="wp-block-paragraph">Visit <code>http://127.0.0.1:5000/</code> in your browser. You should see “Hello, Dockerized Flask!”.</p><h3 class="wp-block-heading">Dockerize the Flask Application</h3><ol class="wp-block-list"><li><strong>Create a Dockerfile:</strong> In the <code>flask-docker-app</code> directory, create a file named <code>Dockerfile</code> with the following content:</li></ol><pre class="wp-block-syntaxhighlighter-code"># Use the official Python image from the Docker HubFROM python:3.9-slim# Set the working directory in the containerWORKDIR /app# Copy the current directory contents into the container at /appCOPY . /app# Install any needed packages specified in requirements.txtRUN pip install --no-cache-dir Flask# Make port 5000 available to the world outside this containerEXPOSE 5000# Define environment variableENV FLASK_APP=app.py# Run app.py when the container launchesCMD ["python", "app.py"]</pre><p class="wp-block-paragraph">2. Create a <code>.dockerignore</code> file:</p><p class="wp-block-paragraph">In the <code>flask-docker-app</code> directory, create a file named <code>.dockerignore</code> to ignore unnecessary files during the Docker build process:</p><pre class="wp-block-syntaxhighlighter-code">venv__pycache__*.pyc*.pyo</pre><p class="wp-block-paragraph">3. Build the Docker image:</p><p class="wp-block-paragraph">In the <code>flask-docker-app</code> directory, run the following command to build your Docker image:</p><pre class="wp-block-syntaxhighlighter-code">docker build -t flask-docker-app .</pre><p class="wp-block-paragraph">4. Run the Docker container:</p><p class="wp-block-paragraph">Run the Docker container using the image you just built, </p><pre class="wp-block-syntaxhighlighter-code">docker run -p 5000:5000 flask-docker-app</pre><p class="wp-block-paragraph">5. <strong>Access the Flask app in Docker:</strong> Visit <code>http://localhost:5000/</code> in your browser. You should see “Hello, Dockerized Flask!” running in a Docker container.</p><p class="wp-block-paragraph">You have successfully created a simple Flask application and Dockerized it. The Dockerfile allows you to package your app with its dependencies and run it in a consistent environment.</p>


## Related Posts
- [[🚀 #FOSS: Mastering Superfile: The Ultimate Terminal-Based File Manager for Power Users]]
- [[Docker Ep 9: The Building Blocks – Detailed Structure of a Dockerfile]]
- [[Learning Notes #67 - Build and Push to a Registry (Docker Hub) with GH-Actions]]
- [[Docker EP 11 - Docker Networking &amp; Docker Volumes]]
- [[Problem Statements : Git &amp; Github Session - St. Joseph's GDG Meeting]]

