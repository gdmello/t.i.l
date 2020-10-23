# Modify Old Commit Messages (Already Pushed)
1. go back 20 commits in history, in interactive mode
    
        git rebase -i HEAD~20

2. when the list of commits appear in the text editor, change 'pick' -> 'edit' for each commit which needs to be modified.
3. save & exit

4. proceed with modifying each commit
        
        git rebase --continue

5. if git rebase prompts, go ahead and modify the commit message in the text editor with this command

        git commit --amend

6. Run the above 2 steps for each commit which needs to be amended.

7. Push changes to the upstream repository

        git push --force

Great [source](https://www.git-scm.com/book/en/v2/Git-Tools-Rewriting-History)

# Change Local Commit Author

        git commit --author <first.last@domain.com> --amend
