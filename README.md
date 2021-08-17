<h1 align="center">Final Report for Google Summer of Code 2021</h1>
<h1 align="center">Python Battery Mathematical Modelling (PyBaMM), NumFOCUS</h1>
<img align="center" src="https://user-images.githubusercontent.com/74055102/129663465-75fa46b7-b3a8-4be7-bec9-a1c51e5ff70a.png">
</br>
<h2 align="center">An Automated Twitter Bot to run PyBaMM Simulations</h2>
<!-- <img align="center" src="https://user-images.githubusercontent.com/74055102/129664338-49831d30-336d-45db-9c5e-f7abbbb46e15.jpg"> -->
</br>

## Details

Name: [Saransh Chopra](https://www.linkedin.com/in/saransh-chopra-3a6ab11bb/) </br>
Organization: [NumFOCUS](https://numfocus.org/) </br>
Sub-Organization: [PyBaMM](https://www.pybamm.org/) </br>
Mentors: [Robert Timms](https://www.robertwtimms.com/), [Valentin Sulzer](https://github.com/Saransh-cpp/BattBotTest/edit/main/README.md), [Ferran Brosa Planella](https://www.brosaplanella.com/) </br>

## Abstract
 > PyBaMM (Python Battery Mathematical Modelling) solves physics-based electrochemical DAE models by using state-of-the-art automatic differentiation and numerical solvers. The Doyle-Fuller-Newman model can be solved in under 0.1 seconds, while the reduced-order Single Particle Model and Single Particle Model with electrolyte can be solved in just a few milliseconds. Additional physics can easily be included such as thermal effects, fast particle diffusion, 3D effects, and more. All models are implemented in a flexible manner, and a wide range of models and parameter sets (NCA, NMC, LiCoO2, ...) are available. There is also functionality to simulate any set of experimental instructions, such as CCCV or GITT, or specify drive cycles. </br>
\- [pybamm.org](https://pybamm.org)

PyBaMM or Python Battery Mathematical Modelling is a Python library that is centered around the science of batteries. The library is being extensively used in research and is a big part of Twitter's battery community.

The main aim of this project was to extend PyBaMM's code to Twitter, in a way that users can directly see PyBaMM's wide range of abilities like plug-and-play physics in action. A stretch goal was to accept requests from Twitter and reply with the appropriate simulation without the need of writing code.

More formally, the project aimed to create an automated Twitter bot that can -
 - Tweet random battery simulations (with/without degradation) regularly.
 - Reply to a Twitter simulation request with an appropriate plot.

Both of these functionalities should have had minimum or no human inputs (except for the tweet texts).

This in turn would have also helped PyBaMM by -
 - Stumbling upon undetected bugs
 - Increasing the overall visibility and publicity of the ilbrary itself

## Work done

Some quick links -

 - **Original project idea** - [Twitter bot to run simulations](https://github.com/pybamm-team/PyBaMM/wiki/GSoC-2021-Projects#twitter-bot-to-run-simulations) </br>
 - **Project repository** - [BattBot](https://github.com/pybamm-team/BattBot) </br>
 - **Twitter account (bot)** - [@battbot_](https://twitter.com/battbot_) </br>
 - **Previous blogs (detailed progress) on [Medium](https://whiteviolin.medium.com/)** - [Community Bonding](https://whiteviolin.medium.com/my-gsoc21-experience-community-bonding-f31ea7bb624c), [Week 1-2](https://whiteviolin.medium.com/gsoc21-week-1-and-2-twitter-api-github-actions-and-sensitive-parameters-9d7e79de183a), [Week 3-4](https://whiteviolin.medium.com/gsoc21-week-3-and-4-getting-the-bot-ready-for-official-deployment-3c56c06844be), [Week 5-6](https://whiteviolin.medium.com/gsoc21-week-5-and-6-battbot-is-live-91831dd2e5a4), [Week 7-8](https://whiteviolin.medium.com/gsoc21-week-7-and-8-setting-up-the-reply-functionality-be5ac6897a9d) </br>
 - **Merged pull requests** - label - [GSOC21: Twitter Bot](https://github.com/pybamm-team/BattBot/pulls?q=is%3Apr+is%3Aclosed+label%3A%22GSOC21%3A+Twitter+Bot%22) </br>
 - **Closed issues** - label - [GSOC21: Twitter Bot](https://github.com/pybamm-team/BattBot/issues?q=is%3Aissue+is%3Aclosed+label%3A%22GSOC21%3A+Twitter+Bot%22) </br>

Below are all the pull requests (with some details) that were made during Google Summer of Code 2021. The number of pull requests may seem greater than other GSoC projects as the BattBot repository was created from scratch. For further reference, a good amount of documentation, available in the README.md and CONTRIBUTING.md files, has also been added to the bot's repository.

 - **Cleaning up the already written code** - I created a simple working prototype of the bot before GSoC, these PRs were made to add and clean up that code (which acted as a base for the bot), thus making it ready for test driven development. After these PRs were merged, the bot started tweeting some simple plots using GitHub Actions (Note: In the starting, the bot was hosted on my twitter account and this repository was on my GitHub account) - </br>
[#1](https://github.com/pybamm-team/BattBot/pull/1) - Refactor the code and add a basic template for experiments. </br>
[#4](https://github.com/pybamm-team/BattBot/pull/4) - Restructure the bot, add tests and update the workflows to extract `Twitter API keys` from repository secrets. </br>
 - **Adding degradation and implementing GIF tweets** - Adding degradation in the bot aligned with the original project proposal, that was, creating random battery degradation plots. Implementing GIF tweets was something that my mentors suggested, as it would have been better to tweet the whole simulation in a GIF instead of tweeting a PNG at some with some random value of time (x-axis).
[#5](https://github.com/pybamm-team/BattBot/pull/5) - Add degradation, restructure the tests for codecov, add a timeout for simulations. </br>
[#8](https://github.com/pybamm-team/BattBot/pull/8) - Implement GIF tweets, remove tweepy, minor refactor and add a way to upload large files to the Twitter API endpoint in chunks. </br>
 - **Running tests in a subprocess, covering the same and adding a small workaround for a Twitter API error** - Some of tests were running on the functions which were solving some random simulations, and these functions often crashed. Hence it was necessary to add a time-out to these tests and re-run them if the time-out is hit. This however, created a code coverage issue, as the coverage library cannot run tests in subprocesses by default which was also fixed in these PRs. </br>
[#9](https://github.com/pybamm-team/BattBot/pull/9) - Implement timeout and use coverage to run tests in subprocesses. </br>
[#12](https://github.com/pybamm-team/BattBot/pull/12) - Fix Twitter API internal error bug. </br>
 - **Adding non-degradation comparisons, removing some simple plots and adding some parameters to vary** - The simple plots that were initally implemented in the bot were removed and some comparison (comparing 2 or more models or parameter values) plots were added to the bot. </br>
[#10](https://github.com/pybamm-team/BattBot/pull/10) - Added comparisons with no degradation involved. </br>
[#17](https://github.com/pybamm-team/BattBot/pull/17) - Removed some simple plots. </br>
[#18](https://github.com/pybamm-team/BattBot/pull/18) - Shortlisted and added some sensitive parameters to vary. </br>
 - **Adding tweet status for different possible configurations and a minor bug fix** - Dynamic tweet statuses/texts were added to the bot, that would be tweeted with the GIFs. A bug where some images were never deleted from the bot was fixed.</br>
[#20](https://github.com/pybamm-team/BattBot/pull/20) - Add tweet statuses. </br>
[#21](https://github.com/pybamm-team/BattBot/pull/21) - Delete leftover plots. </br>
 - **Adding documentation** - Updated README.md, added CONTRIBUTING.md and CODE_OF_CONDUCT.md. </br>
[#23](https://github.com/pybamm-team/BattBot/pull/23) - Create CODE_OF_CONDUCT.md. </br>
[#24](https://github.com/pybamm-team/BattBot/pull/24) - Create CONTRIBUTING.md. </br>
[#28](https://github.com/pybamm-team/BattBot/pull/28) - Update README.md. </br>
 - **Store the random configurations and let users play with it** - Till now, the random configurations that were being tweeted out were not stored anywhere, they could only be extracted from a the tweet's text, and hence, users might've found reproducing that simulation a bit difficult. The following PRs updated the workflows to automatically save the the configurations and added a notebook that could be used to run and play with the saved configurations</br>
[#23](https://github.com/pybamm-team/BattBot/pull/23) - Create CODE_OF_CONDUCT.md. </br>
[#24](https://github.com/pybamm-team/BattBot/pull/24) - Create CONTRIBUTING.md. </br>
[#28](https://github.com/pybamm-team/BattBot/pull/28) - Update README.md. </br>
