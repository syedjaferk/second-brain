---
layout: post
title: Docker Directives - Env Directive
date: 2024-07-09 01:45:15+00:00
render_with_liquid: false
category: Docker
tags:
- ENV Directive
- Dockerfile
- Environment Variables
- Linux Commands
- Unix
---



<p class="wp-block-paragraph">The <strong>ENV</strong> directive in a <strong>Dockerfile</strong> can be used to set environment variables. </p><p class="wp-block-paragraph">Environment variables are key-value pairs that provide information to applications and processes running inside the container. </p><p class="wp-block-paragraph">They can influence the behavior of programs and scripts by making dynamic values available during runtime.</p><p class="wp-block-paragraph">Environment variables are defined as key-value pairs as per the following format:</p><pre class="wp-block-syntaxhighlighter-code">ENV &lt;key&gt; &lt;value&gt;</pre><p class="wp-block-paragraph">For example, we can set a path using the <strong>ENV</strong> directive as below,</p><pre class="wp-block-syntaxhighlighter-code">ENV PATH $PATH:/usr/local/app/bin/</pre><p class="wp-block-paragraph">We can set multiple environment variables in the same line separated by spaces. However, in this form, the <strong>key</strong> and <strong>value</strong> should be separated by the equal to (<code>=</code>) symbol:</p><pre class="wp-block-syntaxhighlighter-code">ENV &lt;key&gt;=&lt;value&gt; &lt;key=value&gt; ...</pre><p class="wp-block-paragraph">Below, we set two environment variables configured. </p><p class="wp-block-paragraph">The <strong>PATH</strong> environment variable is configured with the value of <code>$PATH:/usr/local/app/bin</code>, and </p><p class="wp-block-paragraph">the <strong>VERSION</strong> environment variable is configured with the value of <code>1.0.</code>0.</p><pre class="wp-block-syntaxhighlighter-code">ENV PATH=$PATH:/usr/local/app/bin/ VERSION=1.0.0</pre><p class="wp-block-paragraph">Once an environment variable is set with the <strong>ENV</strong> directive in the <strong>Dockerfile</strong>, this variable is available in all subsequent Docker image layers. </p><p class="wp-block-paragraph">This variable is even available in the Docker containers launched from this Docker image.</p><p class="wp-block-paragraph">Below are some of the examples of using ENV file, </p><h3 class="wp-block-heading">Example 1: Setting a single environment variable</h3><pre class="wp-block-syntaxhighlighter-code"># Use an official Node.js runtime as a parent image
FROM node:14

# Set the environment variable NODE_ENV to "production"
ENV NODE_ENV=production

# Copy package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install app dependencies using the NODE_ENV variable
RUN if [ "$NODE_ENV" = "production" ]; then npm install --only=production; else npm install; fi

# Copy app source code to the container
COPY . .

# Expose the port the app runs on
EXPOSE 8080

# Define the command to run the app
CMD ["node", "app.js"]
##</pre><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">Example 2: Using Environment Variables in Application Configuration</h3><pre class="wp-block-syntaxhighlighter-code">
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set environment variables
ENV APP_HOME=/usr/src/app
ENV APP_CONFIG=config.ProductionConfig

# Create application directory and set it as the working directory
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

# Copy the current directory contents into the container at /usr/src/app
COPY . .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Use the environment variable in the command to run the application
CMD ["python", "app.py", "--config", "$APP_CONFIG"]
</pre><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">Example 3: Passing Environment Variables to the Application</h3><pre class="wp-block-syntaxhighlighter-code">
# Use an official nginx image as a parent image
FROM nginx:alpine

# Set environment variables
ENV NGINX_HOST=localhost
ENV NGINX_PORT=8080

# Copy custom configuration file from the current directory
COPY nginx.conf /etc/nginx/nginx.conf

# Replace placeholders in the nginx.conf file with actual environment variable values
RUN sed -i "s/NGINX_HOST/$NGINX_HOST/g" /etc/nginx/nginx.conf &amp;&amp; \
    sed -i "s/NGINX_PORT/$NGINX_PORT/g" /etc/nginx/nginx.conf

# Expose ports
EXPOSE 8080

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
</pre>


## Related Posts
- [[Docker Directives - ARG Directive]]
- [[PYTHON-FUNDAMENTALS: Constants Variables aNd Data Types]]
- [[Effortless Data Storage with LocalBase and IndexedDB]]
- [[Top Command in Linux: Tips for Effective Usage]]
- [[Git Stash Explained: Save Your Work Efficiently]]

