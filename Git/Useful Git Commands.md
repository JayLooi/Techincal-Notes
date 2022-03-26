# Useful Git Commands

These notes presented git commands that I used frequently and personally found really useful. 

1. `git checkout`

   * To switch to existing branch
   
       ```
       $ git checkout <branch-name>
       ```

   * To switch to new branch
   
      ```
      $ git checkout -b <new-branch-name>
      ```

2. `git add`

   * To stage all modified/added/deleted file(s) to index

      ```
      $ git add .
      ```

    * To stage some modified/added/deleted file(s) to index

      ```
      $ git add <file-path-1> <file-path-1> ... <file-path-n>
      ```

    * To stage part of the changes in file(s) to index

      ```bash
      # Apply to all changed file(s)
      $ git add -p

      # Apply to selected file(s)
      $ git add -p -- <file-path-1> <file-path-2> ... <file-path-n>
      ```

      This command will show one hunk at a time and prompt user for action by  character input from the list [y,n,q,a,d,j,J,g,/,e,?]. 
      
      Inputting 'y' will stage current hunk and 'n' will not stage current hunk.   
      Refer to [Git documentation page](https://git-scm.com/docs/git-add#Documentation/git-add.txt-patch) or more information regarding the  options. 
      
      Example output:   
      ```diff
      diff --git a/repo/Hello.c b/repo/Hello.c
      index 2da0555..5b69571 100644
      --- a/repo/Hello.c
      +++ b/repo/Hello.c
      @@ -1,4 +1,6 @@
       #include <stdio.h>
      
      +char name[256];
      +
       int main()
       {
      (1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]?
      ```  
      ```diff
      @@ -3,6 +5,9 @@
       int main()
       {
      -    printf("Hello, World! \n");
      +    printf("What is your name? \n >> ");
      +    scanf("%s", name);
      +
      +    printf("Hello, %s. \n", name);
      
           return 0;
       }
      \ No newline at end of file
      (2/2) Stage this hunk [y,n,q,a,d,K,g,/,e,?]?
      ```

3. `git commit`
    * To make a commit

      Single line commit message: 
    
      ```
      $ git commit -m "This is commit message"
      ```

      Multi-paragraph commit message:

      ```
      $ git commit -m "This is commit message. " -m "you can make more paragraphs with multiple -m <commit-message>" -m "This is last paragraph. "
      ```
    
    * To amend latest commit
      
      ```
      $ git commit --amend
      ```

      This command can be used to modify the commit message of latest commit. 

      If staged changes exist when running this command, the latest commit will be replaced by a new commit by combining staged changes with the latest commit. 

4. `git cherry-pick`

    * To apply a commit onto HEAD
      
      ```
      $ git cherry-pick <commit>
      ```

      Let's say we would like to apply some changes that were committed in branch-A onto branch-B, we could use `cherry-pick` command to "pick" the desired commits from branch-A and apply onto branch-B. 

5. `git reset`

    This command is used to undo changes in commit tree, staging index and working directory. 
    
    There are three primary modes in `git reset` command which correspond to the command arguments `--hard`, `--mixed` and `--soft`. The default argument is `--mixed`. 

    * Undo changes in staging index

      ```bash
      # Equivalent to git reset HEAD --mixed
      $ git reset
      ```

      This command will unstage the file(s) from index. 

    * Undo changes in staging index and working directory

      ```bash
      # Equivalent to git reset HEAD --hard
      $ git reset --hard
      ```

      This command will undo all the changes in staged and unstaged files but not untracked file. 
    
    * Undo commit(s) by moving current branch HEAD to previous commit

      ```
      $ git reset [mode] <commit>
      ```

      To keep the existing changes untouched, and also keep the changes from the undone commits(s) in staging area: 

      ```
      $ git reset --soft <commit>
      ```

      To keep the existing changes untouched, and also keep the changes from the undone commit(s) in working directory: 

      ```
      $ git reset --mixed <commit>
      ```

      To remove all the existing changes and those from undone commit(s):

      ```
      $ git reset --hard <commit>
      ```

6. `git revert`

    Reverting changes in a commit by creating a new commit. 

    ```
    $ git revert <commit>
    ```
