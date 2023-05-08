# [GitHub Stats Visualization](https://github.com/jstrieb/github-stats)

<!--
https://github.community/t/support-theme-context-for-images-in-light-vs-dark-mode/147981/84
-->
<a href="https://github.com/riolubruh/github-stats">
<img src="https://github.com/riolubruh/github-stats/blob/master/generated/overview.svg#gh-dark-mode-only" />
<img src="https://github.com/riolubruh/github-stats/blob/master/generated/languages.svg#gh-dark-mode-only" />
<img src="https://github.com/riolubruh/github-stats/blob/master/generated/overview.svg#gh-light-mode-only" />
<img src="https://github.com/riolubruh/github-stats/blob/master/generated/languages.svg#gh-light-mode-only" />
</a>

Generate visualizations of GitHub user and repository statistics with CircleCI.
Visualizations can include data for both private repositories, and for
repositories you have contributed to, but do not own.

Generated images automatically switch between GitHub light theme and GitHub
dark theme.

## Background

When someone views a profile on GitHub, it is often because they are curious
about a user's open source projects and contributions. Unfortunately, that
user's stars, forks, and pinned repositories do not necessarily reflect the
contributions they make to private repositories. The data likewise does not
present a complete picture of the user's total contributions beyond the current
year.

This project aims to collect a variety of profile and repository statistics
using the GitHub API. It then generates images that can be displayed in
repository READMEs, or in a user's [Profile
README](https://docs.github.com/en/github/setting-up-and-managing-your-github-profile/managing-your-profile-readme).

Since the project runs on CircleCI, no server is required to regularly
regenerate the images with updated statistics. Likewise, since the user runs
the analysis code themselves via CircleCI, they can use their GitHub
access token to collect statistics on private repositories that an external
service would be unable to access.

## Disclaimer

If the project is used with an access token that has sufficient permissions to
read private repositories, it may leak details about those repositories in
error messages. For example, the `aiohttp` library—used for asynchronous API
requests—may include the requested URL in exceptions, which can leak the name
of private repositories. If there is an exception caused by `aiohttp`, this
exception will be viewable in the CircleCI project tab of the repository, and
anyone may be able to see the name of one or more private repositories.

Due to some issues with the GitHub statistics API, there are some situations
where it returns inaccurate results. Specifically, the repository view count
statistics and total lines of code modified are probably somewhat inaccurate.
Unexpectedly, these values will become more accurate over time as GitHub
caches statistics for your repositories. Additionally, repositories that were
last contributed to more than a year ago may not be included in the statistics
due to limitations in the results returned by the API.

For more information on inaccuracies, see issue
[#2](https://github.com/jstrieb/github-stats/issues/2),
[#3](https://github.com/jstrieb/github-stats/issues/3), and
[#13](https://github.com/jstrieb/github-stats/issues/13).

## Introduction

This guide provides instructions for setting up github-stats, a tool that generates statistics for your GitHub profile. By following these steps, you'll be able to create images to display your GitHub contributions and language usage on your GitHub profile.

## Installation Steps

1. **Create a personal access token:** Follow the instructions [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) to create a personal access token with the `read:user` and `repo` permissions. Copy the access token when it is generated, as you will need it in later steps. Note that it may take a few minutes for the token to become active.
2. **Create a copy of the repository:** Click [here](https://github.com/riolubruh/github-stats/generate) to create a fresh copy of the repository. This is different from forking the repository because it copies everything fresh, without the commit history.
3. **Connect your GitHub account to CircleCI:** Go to CircleCI, connect your GitHub account, and add the repository you just created. Select the "Fastest: Use the .circleci/config.yml in my repository" option.
4. **Add environment variables:** In CircleCI, go to the `Project Settings > "Environment Variables"` page. Create a new environment variable with the name `ACCESS_TOKEN` and paste the copied personal access token as the value. Then, create another new environment variable with the name `GITHUB_ACTOR` and put your GitHub username.
5. **Customize your statistics (optional):** You can change the type of statistics reported by adding other repository secrets. To ignore certain repos, add them (in owner/name format e.g., `jstrieb/github-stats`) separated by commas to a new secret—created as before—called `EXCLUDED`. To ignore certain languages, add them (separated by commas) to a new secret called `EXCLUDED_LANGS`. For example, to exclude HTML and TeX, you could set the value to `html,tex`. To show statistics only for "owned" repositories and not forks with contributions, add an environment variable called `EXCLUDE_FORKED_REPOS` with a value of `true`. These other values are added as secrets by default to prevent leaking information about private repositories. If you're not worried about that, you can change the values directly in the CircleCI config file itself.
6. **Generate the images:** Go to the github-stats Project page in CircleCI and press "Rerun Workflow from start" on the right side of the screen to generate images for the first time. In step 9, we will set it up to be automatically regenerated every 24 hours, but they can be regenerated manually by running the workflow this way.
7. **View the images:** Take a look at the images that have been created in the `generated` folder.
8. **Add the images to your GitHub profile:** To add your statistics to your GitHub Profile README, copy and paste the following lines of code into your markdown content. Change the `username` value to your GitHub username.

```md
![](https://raw.githubusercontent.com/username/github-stats/master/generated/overview.svg#gh-dark-mode-only)
![](https://raw.githubusercontent.com/username/github-stats/master/generated/overview.svg#gh-light-mode-only)
```
```md
![](https://raw.githubusercontent.com/username/github-stats/master/generated/languages.svg#gh-dark-mode-only)
![](https://raw.githubusercontent.com/username/github-stats/master/generated/languages.svg#gh-light-mode-only)
```
9. **Set up automatic updates:** To have the images update automatically, go to Project Settings > Triggers, click Add Trigger, and configure how frequently you want the images to update!
10. **Star the repo:** If you like github-stats, don't forget to star the repo!

## Troubleshooting Tips

- If the personal access token doesn't work, wait a few minutes and try again.
- If there are issues with CircleCI, check the CircleCI documentation for troubleshooting tips or reach out to their support team.
- If the images aren't generating or updating as expected, check the CircleCI logs for errors or reach out to the github-stats team for help.


# Support the Project

There are a few things you can do to support the project:

- Star the repository (and follow me on GitHub for more)
- Share and upvote on sites like Twitter, Reddit, and Hacker News
- Report any bugs, glitches, or errors that you find

These things motivate me to to keep sharing what I build, and they provide
validation that my work is appreciated! They also help me improve the
project. Thanks in advance!

If you are insistent on spending money to show your support, I encourage you to
instead make a generous donation to one of the following organizations. By advocating
for Internet freedoms, organizations like these help me to feel comfortable
releasing work publicly on the Web.

- [Electronic Frontier Foundation](https://supporters.eff.org/donate/)
- [Signal Foundation](https://signal.org/donate/)
- [Mozilla](https://donate.mozilla.org/en-US/)
- [The Internet Archive](https://archive.org/donate/index.php)


# Related Projects

- Inspired by a desire to improve upon
  [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
- Makes use of [GitHub Octicons](https://primer.style/octicons/) to precisely
  match the GitHub UI
