---
layout: post
title: 'Learning Notes #2 - Automate Email Notifications in GitHub Actions'
date: 2024-12-20 07:07:03+00:00
render_with_liquid: false
category: Automation
tags:
- GitHub Actions
- Email Notifications
- SMTP
- Google Authentication
---



<p class="wp-block-paragraph">Today, i was checking youtube videos on github actions. I came across a video on sending a mail via a Github Action <a href="https://www.youtube.com/watch?v=SkD7KQ3KzZs&amp;t=108s">https://www.youtube.com/watch?v=SkD7KQ3KzZs&amp;t=108s</a>. This blog is just an implementation of the video. </p><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">What am i going to do ?</h3><p class="wp-block-paragraph">I need to send a mail using my gmail id via Github</p><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">What prior information you need ?</h3><ol class="wp-block-list"><li>Gmail SMTP Server address – smtp.gmail.com</li><li>Gmail SMTP port – 465</li><li>Email username – your mail id.</li><li>Email password – App Password from Google. <a href="https://support.google.com/accounts/answer/185833?hl=en">https://support.google.com/accounts/answer/185833?hl=en</a>.  </li></ol><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">YAML File</h3><pre class="wp-block-syntaxhighlighter-code">name: "Send Mail"on:  workflow_dispatch:jobs:  mail:    runs-on: ubuntu-latest    steps:      - name: Print Name        run: echo "Sending Mail"          - name: Send Mail        if: ${{ always() }}        uses: dawidd6/action-send-mail@v3        with:          server_address: smtp.gmail.com          server_port: 465          username: ${{ secrets.EMAIL_USERNAME }}          password: ${{ secrets.EMAIL_PASSWORD }}          subject: ${{ github.job }} job of ${{ github.repository }} has  ${{ github.status }}          body: "Test Message in Github"          to:  syedjafer1997@gmail.com          from: Syed Jafer K</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">My Github Run: <a href="https://github.com/syedjaferk/gh_actions_templates/actions/runs/12426929593">https://github.com/syedjaferk/gh_actions_templates/actions/runs/12426929593</a></p><p class="wp-block-paragraph"></p>


## Related Posts
- [[ML Notes #1 - Linear Regression from Scratch]]
- [[RSVP for RabbitMQ: Build Scalable Messaging Systems in Tamil]]
- [[Learning Notes #44 - Initial Steps on Distributed Tracing and Observability]]
- [[Learning Notes #01 - Github Actions]]
- [[Learning Notes #58 - Command Query Responsibility Segregation - An Idea Overview]]

