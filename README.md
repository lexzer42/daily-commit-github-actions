# github-actions
This project sets up a GitHub Actions workflow to automatically make commits to a repository at a specific time every day


# Daily Commit with Inspirational Quote

This GitHub Action sets up a workflow to automatically make daily commits to a repository at a specific time, incorporating a random inspirational quote with each commit. The commits occur at 12:00 UTC (noon), but you can adjust the schedule to your timezone.

## Usage

To use this GitHub Action in your repository, follow these steps:

1. Create a `.github/workflows` directory in your repository if it doesn't already exist.

2. Inside the `.github/workflows` directory, create a YAML file (e.g., `daily-commit.yml`).

3. Copy and paste the following workflow definition into the YAML file:

```yaml
name: Daily Commit with Inspirational Quote

on:
  schedule:
    - cron:  '0 12 * * *' # Runs every day at 12 PM (noon)

jobs:
  commit:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2
      with:
        ref: 'main' # Specify the branch here

    - name: Set up Git
      run: |
        git config --local user.email "action@github.com"
        git config --local user.name "GitHub Action"

    - name: Fetch Inspirational Quote
      run: |
        QUOTE=$(curl -s 'https://zenquotes.io/api/random' | jq -r '.[0].q')
        COMMIT_TIME=$(date '+%d %B of %Y in %H hours %M minutes')
        echo "$COMMIT_TIME - \"$QUOTE\"" >> example.txt

    - name: Commit Changes
      run: |
        git add example.txt
        git commit -m "Auto commit with inspirational quote $(date +%F)"
        git push origin main # Assuming the branch name is main, change if needed
```

4. Customize the workflow as needed. You can change the filename (`example.txt`) or modify the commit message format.

5. Commit and push the changes to your repository.

Now, the workflow will run daily at the specified time, making commits with a random inspirational quote added to the `example.txt` file.

## Inspiration

This GitHub Action was inspired by the desire to automate daily commits with a touch of positivity, using random inspirational quotes to inspire and uplift developers.

## Credits

- This workflow uses the [Zen Quotes API](https://zenquotes.io/api/random) to fetch random inspirational quotes.

Feel free to customize and adapt this workflow to suit your needs!

```
Feel free to customize this `README.md` with additional information or formatting according to your preferences.
