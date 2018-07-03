# Reminders

## Turning an Existing Directory into a New Repository

1. Navigate to the directory you want to turn into a repo
2. Type `git init`
3. Use `git add` to add all the relevant files.
4. Type `git commit` to commit these additions.
5. Go to the GitHub website
6. Press the `+` button in the upper-right corner and select *New repository* from the drop-down menu that appears
7. Fill the information in (don't create a README) and create the repo
8. Back on the command line, type `git remote add <the HTML address of the Git repo you just created>`
9. Then type `git push -u origin master`