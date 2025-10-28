<h1> Mike's Notepad </h1>
<small>Random Notes - mostly obsolete - </small>
<hr>





<details><summary> <H2> Python </H2></summary> 

 <details><summary><h3> .venv </h3></summary>

 ** uv **

```bash
uv pip compile requirements.in         # easy way to visualize dependencies on legacey python projects
```


 **Basic**
 ```zsh
 python3 -m venv .venv                 # Create Virtual Enviorment
 source ./.venv/bin/activate           # Activate Virtual Enviorment
 pip install numpy pandas              # Install Package(s)
 pip install --upgrade <package_name>  # Upgrade Package
 pip freeze > requirements.txt         # make requirements.txt file
 deactivate                            # To exit .venv
 pip install -r requirements.txt       # How to use the requirements.txt file

 # ----- Additional usefull commands ----- 
 echo ".venv/" >> .gitignore           # Don't commit venv to git
 pip list                              # Show installed packages
 pip show <package_name>               # Show package info/dependencies
 pip uninstall <package_name>          # Remove a package
 pip install -e .                      # Install current project in editable mode
 pip install -e '.[dev]'               # Install current project in editable mode with dev packages 
 which python                          # Verify you're using venv Python
 rm -rf .venv                          # Delete virtual environment
 ```
 
 </details>

 <details><summary><h3> general </h3></summary>

 <ol>
  <li> To specify the interpreter you can use the ```#!``` on the first line of a ```script.py``` </li>
  <li> Note you must run this as an executable in order for the ```#!``` to work </li>

  
 </ol>

 </details>


 <details><summary><h3> SQL Lite </h3></summary>
  
 ```.py
 import sqlite3
 import pprint
 ''' Inspect '''
 print(db.execute("select sqlite_version()").fetchall()) # sqlite version
 db = sqlite3.connect("your_datebase.db")
 db.execute("select name from sqlite_master where type='table'").fetchall()  # tables
 for row in db.execute("SELECT * FROM any_table LIMIT 10"): print(row)       # rows (tuples)
 db.row_factory = sqlite3.Row              # will convert rows to dict (easier to work with)
 for row in db.execute("SELECT * FROM any_table LIMIT 10"): print(dict(row)) # rows (dictionaries)
 for row in db.execute("select name from sqlite_master where type='table'").fetchall(): pprint.pprint(dict(row)) # tables (pprint)
 for row in db.execute("SELECT * FROM stats LIMIT 10"): pprint.pprint((dict(row))) # rows (pprint)
 ''' Create '''
 db.execute("CREATE TABLE events(id integer primary key, name text, start_date text, end_date text, description text);")
 ```
 </details>

 <details><summary><h3> Usefull </h3></summary>
 
 ```py
 # Shuffle data
 import numpy as np
 data = np.arange(10)
 
 indicies_permutation = np.random.permutation(len(data))
 shuffled_data = data[indicies_permutation]
 
 # F-string tricks
 print(f'{n:,}')                 # 1,000s seperator with ',' (can also use _)
 print(f'{n:>20}:')              # Rt align w/ 20 spaces; '<' for left, '^' for center
 print(f'{datetime.now(): %c}')  # Date formatting lots more optins available ..
 print(f'{n = }')                # Will output "n = ...." much nicer way to check vars
 ```

 </details>
 
 <details><summary><h3> Pandas </h3></summary>
 
 ```py
 pd.set_option('display.max_rows', None)
 ```

 </details>




  <details><summary><h3> Tensorflow </h3></summary>
  **Utilities**
     
  ```py
  # One Hot Encode
  from tensorflow.keras.utils import to_categorical
  y_train = to_categorical(train_labels)
  ```

  ** Models **
```py
''' 1. Architecture: a Simple stacked layers w/ relu activation can solve lots of problems '''
model.Sequential([layers.Dense(16,actyivation="relu"),....])   # Simple stacked layers
layers.Dense(1,activation="sigmoid"                            # last layer for binary classification
layers.Dense(#_categories, activation="softmax"                # last layer for multiclass classification
''' 2. Compile: '''
model.compile(optimizer=_, loss=_,metrics=[_])   # Optimizer to "rmsprop" for 95% of models
                                                 # loss="binary_crossentropy"             binary classification
                                                 # loss="categorical_crossentropy"        multiclassification w/ OHE y
                                                 # loss="sparse_categorical_crossentrop"  sing. label multiclass. w/ int y
''' 3. Fit: Run the model '''
model.fit(x_train, y_train, epochs=_, batch_size=_2^n_)  # epochs is number of forward + backward pass the model
                                                         # makes attempting to reduce loss carefull not to overfit
```

  </details>

  <details><summary><h3> nb dev </h3></summary>
    ```.py
    nbdev_new
    nbdev_preview
    nbdev_prepare
    nbdev_export
    # nbdev_watch... 
    ```
  </details>
</details>

<details><summary><h2> VIM </h2></summary>
 
 ```vim
 :set wrap
 :set nowrap
 
 :set textwidth=80 #then select section to reformat <g>,<q>
 ```
 
</details>


<details><summary><h2> GIT </h2></summary>

```bash
# GLOBAL SETTIGNS to change
git config --global pull.rebase true
```

```zsh
# ARCHIVE
git fetch origin
git checkout -b main-backup origin/main

# SAVE
git add -A && git commit -m "save" && git push 
```

### Basics
```bash
# Verify installed
git --version 
# Set up
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"

# Confirm
git config --list

# navigate to location
git init
ls -la # to verify
rm -rf .git # to stop tracking project with .git
git status # to see current status
touch .gitignore # add file names to ignore (can also use wildcards ex *.txt)

git add "file_name" # add a single file to staging area
git add -A # add all files to Staging Area
git reset # Remove files from the Staging Area
git status # to verify   

git add -A
git commit -m "Initial Commit" # try to make better Messages
git log # will show the History
```

### Remote Repo
```zsh

git clone <url> <where to clone> # will also work for local files
git remote -v # Lists Repo information
git branch -a # List all of the Branches of the Repo
# ..make some changes to code...
git diff
git status
git add -A
git commit -m "message"
# When ready to commit changes do a git pull -> git push (to capture any other changes)
git pull origin master
git push origin master
```

### Branching
```zsh

git switch -c new_feature # Creates and switches to branch
git add -A
git commit -m "small_new_feature" # commits to branch
git push -u origin new_feature # pushes and sets upstream
git branch -a # verify branches
git add -A && git commit -m "small new feature..."
git push
# Ready to merge
git switch master
git pull origin master
git merge new_feature # merges changes 
git push origin master # pushes to remote
# Delete branch
git branch -d new_feature # delete locally
git push origin --delete new_feature # delete from remote
git branch -a # verify deletion
# Branch from old commit
git log --oneline --graph --all # see commits
git switch -c new-branch-name 4f8d768 # create branch from old commit
```

### Rolling back to a previous commit
#### Step 1: Reset to the desired commit
```zsh

git init && git add -A && git commit -m "Initial commit"
git reset --hard origin/main # Roll back to last commit
git log --oneline --graph --decorate --all                  # With Page
git --no-pager log --oneline --graph --decorate --all       # No page

```

</details>



<details><summary><h2> Linux </h2></summary>

 ```bash
sudo dpkg-reconfigure console-setup  # Change Font Size
ls -al ~/.ssh                        # list ssh keys
mise settings add idiomatic_version_file_enable_tools python # for uv warning..

 ```

</details>

<details><summary><h2> SSH </h2></summary>

```bash
# 1. Generate Key Pair (use Ed25519 for better security; add passphrase for protection)
ssh-keygen -t ed25519 -f ~/.ssh/my_key -C "your_email@example.com"

# 2. Set Secure Permissions (SSH requires this to use the keys)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/my_key
chmod 644 ~/.ssh/my_key.pub

# 3. Copy Public Key to Server (initially uses password; replace user@server_ip)
ssh-copy-id -i ~/.ssh/my_key.pub user@server_ip

# 4. Configure SSH Client (~/.ssh/config; create if needed, chmod 600 after)
# Host my_server
#     HostName server_ip
#     User user
#     IdentityFile ~/.ssh/my_key  # Private key (not .pub)
#     IdentitiesOnly yes  # Optional: Restrict to this key

# 5. Connect (uses config alias; enter passphrase if set)
ssh my_server

# 6. (Optional) Disable Password Auth on Server (after key works; requires sudo)
# Edit /etc/ssh/sshd_config:
# PasswordAuthentication no
# PubkeyAuthentication yes
# Then: sudo systemctl restart sshd

# 7. (Optional) Revoke Key (if compromised; on server)
# Remove line from ~/.ssh/authorized_keys; generate new pair
```
</details>

<details><summary><h2> CSS </h2></summary> 
 
- Conditional Border
```css
border-radius: max(0px, min(8px, calc((100vw - 4px - 100%) * 9999))) / 8px;
```

</details>



