# FAQ Bot Framework

A chatbot framework which organically learns to handle the most frequently asked questions.

![Editor](resources/editor.png?raw=true "Editor")

## Description

This code was developed by the [AXA REV research team](https://axa-rev-research.github.io/) to serve as prototype for a chatbot framework to handle frequently asked questions about a topic or a product.

Main features:

- Built-in NLP engine based on [fastText](https://fasttext.cc/) for text classification
- Seamless WebSocket integration using [Action Cable](https://guides.rubyonrails.org/action_cable_overview.html)
- Instant embedding of chat window on any page thanks to customizable widget code
- Dynamic answers using global variables, user variables and external APIs
- Optional connection with [Facebook messenger](https://www.messenger.com/)
- Optional feedback loop for auto-approvements
- Multi-tenancy: Operate multiple chatbots within one framework
- User authentication using [Devise](https://github.com/plataformatec/devise) and role-based user authorization using [cancancan](https://github.com/CanCanCommunity/cancancan)

## Installation

### 0. Requirements
- Ruby 2.4.1+
- [bundler](https://bundler.io/), `gem install bundler`
- A database, e.g. MySQL, PostgreSQL, Oracle

### 1. Web Application

Clone the respository and install the required gems:
```
bundle install
```

Generate secret keys for the `development` and `test` sections in [config/secrets.yml](config/secrets.yml):

```
rake secret
```

Create the database and load the schema:
```
rake db:setup
```

Open the Rails console with `rails c` and create your admin account: 
```
User.create(email: "name@domain.com", password: "TOPSECRET_PASSWORD", password_confirmation: "TOPSECRET_PASSWORD", role: "admin")
```
Startup your local web server:
```
rails s
```
Login in at http://localhost:3000 and create your first FAQ bot project.

### 2. Text Classifier Integration

- Install [fastText](https://github.com/facebookresearch/fastText) in your environment
- In [config/classifiers.yml](config/classifiers.yml), provide the path to the binary, the path to the directory of pretrained vectors, and the path to the directory where you would like to save the classifiers
- Download the *text* files of [pretrained vectors](https://github.com/facebookresearch/fastText/blob/master/pretrained-vectors.md) for all languages of your interest to the directory of pretrained vectors

### 3. Facebook Connection (optional)

- Create a Facebook page and [setup a Facebook app](https://developers.facebook.com/docs/messenger-platform/getting-started/app-setup) 
- In the Messenger section, create a *page access token* and add it to the settings of your FAQ bot project
- In the Webhooks section, edit the page subscription and provide your app's callback url and a random *verification token*
- Add the token to your FAQ bot project's settings to complete the integration

For testing in your development environment, you will need to expose the Webhook url of your local server to the internet. This can be achieved using [Ngrok](https://ngrok.com/).

## Usage

![Schema](resources/schema.png?raw=true "Schema")
Most FAQ knowledge bases are static. In the present chatbot framework, the knowledge base grows organically based on real user demand. The workflow is semi-automated: In the beginning the questions are handled by an agent. The answer to a new question which has never been asked before is manually provided by a human (1). In the following, similar questions by other users are addressed by the agent by selecting the answer from a list (2). Over time the chatbot learns and eventually replies automatically (3).

Additional information about how to configure the chatbot framework can be found in the [wiki](https://github.com/axa-rev-research/faq-bot-framework/wiki).

## Contact

For questions, please contact boris.ruf@axa.com.

## MIT License

Copyright (c) AXA Group Operations SAS

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
