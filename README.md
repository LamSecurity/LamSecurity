<div style="background-color:#121212; color:white; padding:20px; border-radius:8px; font-family:Arial, sans-serif;">

# 🔐 **Arsenal de Segurança**  
### *Onde scripts viram escudos e exploits viram lições.*

<div>
  <a href="https://github.com/LamSecurity">
    <img height="180em" src="https://github-readme-stats.vercel.app/api?username=LamSecurity&show_icons=true&theme=dark&include_all_commits=true&count_private=true"/>
  </a>
</div>

![Snake animation](https://raw.githubusercontent.com/LamSecurity/LamSecurity/refs/heads/output/github-contribution-grid-snake.svg)

<div align="center">
  <img src="https://user-images.githubusercontent.com/74038190/213844619-03ff75a1-593b-4c0f-8a7d-eb4b57ed6f7d.gif" width="500" />
</div>



name: GitHub Snake Game



on:

  # Schedule the workflow to run daily at midnight UTC

  schedule:

    - cron: "0 0 * * *"



  # Allow manual triggering of the workflow

  workflow_dispatch:



  # Trigger the workflow on pushes to the main branch

  push:

    branches:

      - main



jobs:

  generate:

    runs-on: ubuntu-latest

    timeout-minutes: 10



    steps:

      # Step 1: Checkout the repository

      - name: Checkout Repository

        uses: actions/checkout@v3



      # Step 2: Generate the snake animations

      - name: Generate GitHub Contributions Snake Animations

        uses: Platane/snk@v3

        with:

          # GitHub username to generate the animation for

          github_user_name: ${{ github.repository_owner }}



          # Define the output files and their configurations

          outputs: |

            dist/github-snake.svg

            dist/github-snake-dark.svg?palette=github-dark

            dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9

        env:

          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}



      # Step 3: Deploy the generated files to the 'output' branch

      - name: Deploy to Output Branch

        uses: peaceiris/actions-gh-pages@v3

        with:

          github_token: ${{ secrets.GITHUB_TOKEN }}

          publish_dir: ./dist

          publish_branch: output

          # Optionally, you can set a custom commit message

          commit_message: "Update snake animation [skip ci]"
