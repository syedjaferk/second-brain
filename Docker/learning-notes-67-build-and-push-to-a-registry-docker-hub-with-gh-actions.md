---
layout: post
title: 'Learning Notes #67 - Build and Push to a Registry (Docker Hub) with GH-Actions'
date: 2025-01-28 02:30:14+00:00
render_with_liquid: false
category: Docker
tags:
- GitHub Actions
- Docker Hub
- CI/CD
- Automation
- Registry
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">GitHub Actions is a powerful tool for automating workflows directly in your repository.In this blog, we’ll explore how to efficiently set up GitHub Actions to handle Docker workflows with environments, secrets, and protection rules.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Why Use GitHub Actions for Docker?</h2><p class="wp-block-paragraph">My <a href="https://github.com/syedjaferk/gh_action_docker_build_push_fastapi_app">Code base</a> is in Github and i want to tryout gh-actions to build and push images to docker hub seamlessly.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Setting Up GitHub Environments</h2><p class="wp-block-paragraph">GitHub Environments let you define settings specific to deployment stages. Here’s how to configure them:</p><p class="wp-block-paragraph">1. <strong>Create an Environment</strong></p><p class="wp-block-paragraph">Go to your GitHub repository and navigate to <strong>Settings &gt; Environments</strong>. Click <strong>New environment</strong>, name it (e.g., <code>production</code>), and save.<br/><br/>2. <strong>Add Secrets and Variables</strong></p><p class="wp-block-paragraph">Inside the environment settings, click <strong>Add secret</strong> to store sensitive information like <code>DOCKER_USERNAME</code> and <code>DOCKER_TOKEN</code>.</p><p class="wp-block-paragraph">Use <strong>Variables</strong> for non-sensitive configuration, such as the Docker image name.</p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">3. <strong>Optional: Set Protection Rules</strong></p><p class="wp-block-paragraph">Enforce rules like requiring manual approval before deployments. Restrict deployments to specific branches (e.g., <code>main</code>).</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Sample Workflow for Building and Pushing Docker Images</h2><p class="wp-block-paragraph">Below is a GitHub Actions workflow for automating the build and push of a Docker image based on a minimal Flask app.</p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Workflow: <code>.github/workflows/docker-build-push.yml</code></p><pre class="wp-block-syntaxhighlighter-code">name: Build and Push Docker Imageon:  push:    branches:      - main  # Trigger workflow on pushes to the `main` branchjobs:  build-and-push:    runs-on: ubuntu-latest    environment: production  # Specify the environment to use    steps:      # Checkout the repository      - name: Checkout code        uses: actions/checkout@v3      # Log in to Docker Hub using environment secrets      - name: Log in to Docker Hub        uses: docker/login-action@v2        with:          username: ${{ secrets.DOCKER_USERNAME }}          password: ${{ secrets.DOCKER_TOKEN }}      # Build the Docker image using an environment variable      - name: Build Docker image        env:          DOCKER_IMAGE_NAME: ${{ vars.DOCKER_IMAGE_NAME }}        run: |          docker build -t ${{ secrets.DOCKER_USERNAME }}/$DOCKER_IMAGE_NAME:${{ github.run_id }} .      # Push the Docker image to Docker Hub      - name: Push Docker image        env:          DOCKER_IMAGE_NAME: ${{ vars.DOCKER_IMAGE_NAME }}        run: |          docker push ${{ secrets.DOCKER_USERNAME }}/$DOCKER_IMAGE_NAME:${{ github.run_id }}</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">To Actions on live: <a href="https://github.com/syedjaferk/gh_action_docker_build_push_fastapi_app/actions">https://github.com/syedjaferk/gh_action_docker_build_push_fastapi_app/actions</a></p><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-3100" data-recalc-dims="1" decoding="async" height="656" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/01/image-115.png?resize=1904%2C656&amp;ssl=1" width="1904"/></figure>


## Related Posts
- [[Learning Notes #01 - Github Actions]]
- [[🚀 #FOSS: Mastering Superfile: The Ultimate Terminal-Based File Manager for Power Users]]
- [[Problem Statements : Git &amp; Github Session - St. Joseph's GDG Meeting]]
- [[Git Stash Explained: Save Your Work Efficiently]]
- [[Top Command in Linux: Tips for Effective Usage]]

