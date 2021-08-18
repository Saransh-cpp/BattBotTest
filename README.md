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
Mentors: [Robert Timms](https://www.robertwtimms.com/), [Valentin Sulzer](https://sites.google.com/view/valentinsulzer), [Ferran Brosa Planella](https://www.brosaplanella.com/) </br>

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
 - Increasing the overall visibility and publicity of the library itself

## Work done

Some quick links -

 - **Original project idea** - [Twitter bot to run simulations](https://github.com/pybamm-team/PyBaMM/wiki/GSoC-2021-Projects#twitter-bot-to-run-simulations) </br>
 - **Project proposal** - [My proposal](https://github.com/Saransh-cpp/Saransh-cpp/blob/main/PyBaMM_-_Automated_Twitter_bot_to_run_PyBaMM_Simulations_-_Saransh_Chopra.pdf) </br>
 - **Project repository** - [BattBot](https://github.com/pybamm-team/BattBot) </br>
 - **Twitter account (bot)** - [@battbot_](https://twitter.com/battbot_) </br>
 - **Previous blogs (detailed progress) on [Medium](https://whiteviolin.medium.com/)** - [Community Bonding](https://whiteviolin.medium.com/my-gsoc21-experience-community-bonding-f31ea7bb624c), [Week 1-2](https://whiteviolin.medium.com/gsoc21-week-1-and-2-twitter-api-github-actions-and-sensitive-parameters-9d7e79de183a), [Week 3-4](https://whiteviolin.medium.com/gsoc21-week-3-and-4-getting-the-bot-ready-for-official-deployment-3c56c06844be), [Week 5-6](https://whiteviolin.medium.com/gsoc21-week-5-and-6-battbot-is-live-91831dd2e5a4), [Week 7-8](https://whiteviolin.medium.com/gsoc21-week-7-and-8-setting-up-the-reply-functionality-be5ac6897a9d) </br>
 - **Merged pull requests** - label - [GSOC21: Twitter Bot](https://github.com/pybamm-team/BattBot/pulls?q=is%3Apr+is%3Aclosed+label%3A%22GSOC21%3A+Twitter+Bot%22) </br>
 - **Closed issues** - label - [GSOC21: Twitter Bot](https://github.com/pybamm-team/BattBot/issues?q=is%3Aissue+is%3Aclosed+label%3A%22GSOC21%3A+Twitter+Bot%22) </br>

Below are all the pull requests (with some details) that were made during Google Summer of Code 2021. The number of pull requests may seem greater than other GSoC projects as the BattBot repository was created from scratch. For further reference, a good amount of documentation, available in the [README.md](https://github.com/pybamm-team/BattBot#readme) and [CONTRIBUTING.md](https://github.com/pybamm-team/BattBot/blob/main/CONTRIBUTING.md) files, has also been added to the bot's repository.

 - **Cleaning up the already written code** - I created a simple working prototype of the bot before GSoC, these PRs were made to add and clean up that code (which acted as a base for the bot), thus making it ready for test driven development. After these PRs were merged, the bot started tweeting some simple plots using GitHub Actions (Note: In the starting, the bot was hosted on my twitter account and this repository was on my GitHub account) - </br>
[#1](https://github.com/pybamm-team/BattBot/pull/1) - Refactor the code and add a basic template for experiments. </br>
[#4](https://github.com/pybamm-team/BattBot/pull/4) - Restructure the bot, add tests and update the workflows to extract `Twitter API keys` from repository secrets. </br>
 - **Adding degradation and implementing GIF tweets** - Adding degradation in the bot aligned with the original project proposal, that was, creating random battery degradation plots. Implementing GIF tweets was something that my mentors suggested, as it would have been better to tweet the whole simulation in a GIF instead of tweeting a PNG at some with some random value of time (x-axis). </br>
[#5](https://github.com/pybamm-team/BattBot/pull/5) - Add degradation, restructure the tests for codecov, add a timeout for simulations. </br>
[#8](https://github.com/pybamm-team/BattBot/pull/8) - Implement GIF tweets, remove tweepy, minor refactor and add a way to upload large files to the Twitter API endpoint in chunks. </br>
 - **Running tests in a subprocess, covering the same and adding a small workaround for a Twitter API error** - Some of tests were running on the functions which were solving some random simulations, and these functions often crashed. Hence it was necessary to add a time-out to these tests and re-run them if the time-out is hit. This however, created a code coverage issue, as the coverage library cannot run tests in subprocesses by default which was also fixed in these PRs. </br>
[#9](https://github.com/pybamm-team/BattBot/pull/9) - Implement timeout and use coverage to run tests in subprocesses. </br>
[#12](https://github.com/pybamm-team/BattBot/pull/12) - Fix Twitter API internal error bug. </br>
 - **Adding non-degradation comparisons, removing some simple plots and adding some parameters to vary** - The simple plots that were initally implemented in the bot were removed and some comparison (comparing 2 or more models or parameter values) plots were added to the bot. </br>
[#10](https://github.com/pybamm-team/BattBot/pull/10) - Add comparisons with no degradation involved. </br>
[#17](https://github.com/pybamm-team/BattBot/pull/17) - Remove some simple plots. </br>
[#18](https://github.com/pybamm-team/BattBot/pull/18) - Shortlist and added some sensitive parameters to vary. </br>
 - **Adding tweet status for different possible configurations and a minor bug fix** - Dynamic tweet statuses/texts were added to the bot, that would be tweeted with the GIFs. A bug where some images were never deleted from the bot was fixed.</br>
[#20](https://github.com/pybamm-team/BattBot/pull/20) - Add tweet statuses. </br>
[#21](https://github.com/pybamm-team/BattBot/pull/21) - Delete leftover plots. </br>
 - **Adding documentation** - Updated README.md, added CONTRIBUTING.md and CODE_OF_CONDUCT.md. </br>
[#23](https://github.com/pybamm-team/BattBot/pull/23) - Create CODE_OF_CONDUCT.md. </br>
[#24](https://github.com/pybamm-team/BattBot/pull/24) - Create CONTRIBUTING.md. </br>
[#28](https://github.com/pybamm-team/BattBot/pull/28) - Update README.md. </br>
 - **Store the random configurations and let users play with it** - Till now, the random configurations that were being tweeted out were not stored anywhere, they could only be extracted from a the tweet's text, and hence, users might've found reproducing that simulation a bit difficult. The following PRs updated the workflows to automatically save the the configurations and added a notebook that could be used to run and play with the saved configurations.</br>
[#22](https://github.com/pybamm-team/BattBot/pull/22) - Update the workflows to store configurations and add a notebook. </br>
[#30](https://github.com/pybamm-team/BattBot/pull/30) - Fix a bug where the configurations were not getting stored, updated some parameters which were giving errors. </br>
[#35](https://github.com/pybamm-team/BattBot/pull/28) - Add a personal github token to push to protected branches. </br>
 - **Tweet twice a day, vary C-rate and Ambient temperature, and scale functions** - Tweet frequency and the time at which the tweets were sent out (with some randomness obviously) were updated. A bug, where functions were being replaced by float values, was fixed. To make the GIFs more random, `C-rate` and `"Ambient temperature [K]"` were now varied in every `model comparison`. At this point the repository was moved to `pybamm-team`'s account and the CI started failing because of some accessibility issues, some documentation errors also surfaced up, which were also fixed in the following PRs. </br>
[#34](https://github.com/pybamm-team/BattBot/pull/34) - Update the tweet time and frequency to store configurations and fix the broken links in documentation. </br>
[#38](https://github.com/pybamm-team/BattBot/pull/38) - Refactor `parameter_generator` and get it working for functional parameters, split the tests into 2 directories - `with_keys` and `without_keys` and update workflows to run `without_keys` tests on a PR from a fork. </br>
[#40](https://github.com/pybamm-team/BattBot/pull/40) - Vary `"Current function [A]"` and `"Ambient temperature [K]"` in all model comparisons. </br>
 - **Some minor bug fixes** - For some random configurations, the generated tweet text was too long and for some random configurations, the tweet text had an extra (wrong) term which was fixed. The bug where sometimes the workflows, where the changes made to data.txt and config.txt files was being pushed, failed because of extra code in the repository, was also fixed. </br>
[#44](https://github.com/pybamm-team/BattBot/pull/44) - Fix the tweet text while varying `"Current function [A]"` and `"Ambient temperature [K]"`. </br>
[#45](https://github.com/pybamm-team/BattBot/pull/45) - Pull the latest code before pushing. </br>
[#46](https://github.com/pybamm-team/BattBot/pull/46) - Fix the long tweet text bug. </br>
 - **Some more bug fixes + documentation changes** - The tweeting functionality was almost ready and now it was time to implement the replying functionality. For this, I started wby adding a `Reply` class where all the reply stuff will occur and then refactored all the random part of the codebase into a sinle function (seperating the random part from the simulation and solving part) so now, a configuration could either be randomly generated (tweet) and solved or could be read from a tweet text (reply) and solved using the same code. At the end, I decided to create a super class for `Tweet` and `Reply` classes which would have all of the common code (the code where  GIF is uploaded to Twitter API's endpoint). </br>
[#41](https://github.com/pybamm-team/BattBot/pull/41) - Add all the required files for `Heroku`, and added the `Reply` class. </br>
[#48](https://github.com/pybamm-team/BattBot/pull/48) - Refactor randomness out of the codebase to a single function, and transform `comparison_generator` function to a class (`ComparisonGenerator`) . </br>
[#58](https://github.com/pybamm-team/BattBot/pull/58) - Create a super class for `Tweet` and `reply`, and add `"model comparison"` replies for testing the added code. </br>
