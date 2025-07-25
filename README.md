# Notes
*from stone age*

vim
```
:set wrap
:set nowrap

:set textwidth=80 #then select section to reformat
<g>, <q>
```
python
```py
exec(open('my_script.py').read()) #run python script from shell
```

## Python 

### VENV
1. make venv
```zsh
python3 -mvenv .venv
```

2. to activate
```
source ./.venv/bin/activate
```
```zsh
# install packages pip / pip3
pip install jupyter matplotlib numpy pandas scipy scikit-learn

# upgrade existing package
pip install --upgrade <package_name>

# make requirements.txt file
pip freeze > requirements.txt

# To exit venv
deactivate

# How to use the requirements.txt file
pip install -r requirements.txt

```

 - To specify the interpreter you can use the ```#!``` on the first line of a ```script.py```

```python
#!/Users/mikedeufel/code/python/HuggingFace/venv/bin/python
```
 - Note you must run this as an executable in order for the ```#!``` to work 

```zsh
chmod +x filename.py
ls -la #to verify
./filename.py
```
### SQLite
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

### Basic Python

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

### Pandas

```py
pd.set_option('display.max_rows', None)

```



### Tensorflow
#### Utilities
- One Hot Encode
```py
from tensorflow.keras.utils import to_categorical
y_train = to_categorical(train_labels)
```

#### Models
##### 1 Architecture ```model.Sequential([layers.Dense(16,actyivation="relu"),....])```
 - Simple stacked layers w/ relu activation can solve lots of problems
 - Make last layer ```layers.Dense(1,activation="sigmoid")``` for binary classification
 - Make last layer ```layers.Dense(#_categories, activation="softmax"``` for single label multiclassification

##### 2 Compile ```model.compile(optimizer=_, loss=_,metrics=[_])```
 - Set Optimizer to "rmsprop" for 95% of models
 - if binary classificationWhen then ```loss="binary_crossentropy"```
 - if single label multiclassification with OHE y then ```loss="categorical_crossentropy"``` 
 - if single label multiclassification with int y then ```loss="sparse_categorical_crossentropy"```

##### 3 Fit ```model.fit(x_train, y_train, epochs=_, batch_size=_2^n_)```
 - epochs is number of forward + backward pass the model makes attempting to reduce loss carefull not to overfit

### NbDev
```.py
nbdev_new
nbdev_preview
nbdev_prepare
nbdev_export
# nbdev_watch... 
```


## GIT 

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




## Useful Terminal (Linux/Mac)
 - show ssh keys: ```ls -al ~/.ssh```
 - Copy: ```pbcopy < filename.txt```
 - Copy output: ```ls | pbcopy```




## SSH 
1. create new ssh
```.bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/my_server_key
```
2. Send ssh to server
```
ssh-copy-id -i ~/.ssh/custom_key_name.pub user@server_ip
```
3. Edit ~/.ssh/config
```
Host orange
    HostName server_ip
    User user   # same as step 2
    IdentityFile ~/.ssh/my_server_key
'''
>> ssh my_server_key # Will log you on
'''
```

## CSS
- Conditional Border
```css
border-radius: max(0px, min(8px, calc((100vw - 4px - 100%) * 9999))) / 8px;
```

## Linux 
- Increase font size
```
sudo dpkg-reconfigure console-setup
```

