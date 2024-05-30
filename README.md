# Git Author Updater

This repository contains two simple Bash scripts designed to update the author and committer information in a Git repository. Use these scripts when you need to change your account name or email address and update this information in your previous projects.

## Usage

### 1. `update_author_info_by_email`
This script updates the author and committer information based on the email address.

#### Instructions
- Replace `{old_email}` with the email address you want to change.
- Replace `{new_username}` with the new username.
- Replace `{new_email}` with the new email address.

#### Example
```bash
#!/bin/bash
git filter-branch -f --env-filter '
OLD_EMAIL="{old_email}"
CORRECT_NAME="{new_username}"
CORRECT_EMAIL="{new_email}"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags

# Sleep for 3 seconds
sleep 3
```

### 2. `update_author_info_by_username`
This script updates the author and committer information based on the username.

#### Instructions
- Replace `{old_name}` with the username you want to change.
- Replace `{new_name}` with the new username.
- Replace `{new_email}` with the new email address.

#### Example
```bash
#!/bin/bash
git filter-branch -f --env-filter '
OLD_NAME="{old_username}"
CORRECT_NAME="{new_username}"
CORRECT_EMAIL="{new_email}"

if [ "$GIT_COMMITTER_NAME" = "$OLD_NAME" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_NAME" = "$OLD_NAME" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags

# Sleep for 3 seconds
sleep 3
```

## Execution
1. Place the desired script in your local repository.
2. Open a terminal in the repository's directory.
3. Make the script executable
4. Run the script:
   ```bash
   ./update_author_info_by_email
   ```
   or
   ```bash
   ./update_author_info_by_username
   ```

## Conclusion
These scripts provide a convenient way to update your Git commit history with new author and committer information. By following the instructions and examples provided, you can ensure that your previous projects reflect your current account details accurately.
