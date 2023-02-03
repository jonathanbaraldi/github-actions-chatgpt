


python /main.py --openai_api_key "$1" --github_token "$2" --github_pr_id "$3" --openai_engine "$4" --openai_temperature "$5" --openai_max_tokens "$6"



# Pipeline with ChatGPT

This project aims to automate code review using the ChatGPT language model. It integrates  with Github Actions, and upon receiving a Pull Request, it automatically sends each code review to ChatGPT for an explanation.

# Setup

The following steps will guide you in setting up the code review automation with ChatGPT.

## Prerequisites
Before you begin, you need to have the following:

- An OpenAI API Key. You will need a personal API key from OpenAI which you can get here: https://openai.com/api/. To get an OpenAI API key, you can sign up for an account on the OpenAI website https://openai.com/signup/. Once you have signed up, you can create a new API key from your account settings.
- A Github account and a Github repository where you want to use the code review automation.

### Step 1: Create a Secret for your OpenAI API Key

Create a secret for your OpenAI API Key in your Github repository or organization with the name `openai_api_key`. This secret will be used to authenticate with the OpenAI API.

You can do this by going to your repository/organization's settings, navigate to secrets and create a new secret with the name `openai_api_key` and paste your OpenAI API key as the value.

### Step 2: Adjust Permissions

Then you need to set up your project's permissions so that the Github Actions can write comments on Pull Requests. You can read more about this here: [automatic-token-authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#modifying-the-permissions-for-the-github_token)

### Step 3: Create a new Github Actions workflow in your repository in `.github/workflows/chatgpt-review.yaml. A sample workflow is given below:

```
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: ChatGPT explain code
    steps:
      - name: ChatGTP explain code
        uses: jonathanbaraldi/github-actions-chatgpt@v1.2
        with:
          openai_api_key: ${{ secrets.openai_api_key }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
          github_pr_id: ${{ github.event.number }}
          openai_engine: "text-davinci-002" #optional
          openai_temperature: 0.5 #optional
          openai_max_tokens: 2048 #optional
```
