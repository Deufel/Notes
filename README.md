# Notes
Personal Notes / Reminders

## Python 

### VENV
1. make venv
```
python3 -mvenv .venv
```

2. to activate
```
source ./.venv/bin/activate
```
```
# install packages pip / pip3
pip install jupyter matplotlib numpy pandas scipy scikit-learn

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

### Data Basics
#### Shuffle data
```py
import numpy as np

data = np.arange(10)

indicies_permutation = np.random.permutation(len(data))
shuffled_data = data[indicies_permutation]

print(f"data: \t\t{data}")
print(f"shuffled: \t{shuffled_data}")

'''
----- OUTPUT -----
data: 		[0 1 2 3 4 5 6 7 8 9]
shuffled: 	[2 9 8 1 5 7 3 0 4 6]
'''
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
```


## GIT 

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
git branch "new_feature" # Makes the branch
git checkout "new_feature" # Moves you over the the branch
git add -A
git commit -m "small_new_feature" # uploads teh change ONLY to the branch
git push -u origin "new_feature" # slightly complex command that associates the brance with main
git branch -a # To verify
git add -A && git commit -m "small new feature..."
git push
# Ready to merge with Master Branch
git checkout master
git pull origin master
git merge "new_feature" # Merges the changes 
git push origin master # Uploads the changes to remote repo
#Delete the Branch
git branch -d "new_feature" # will delete localy
git push origin --delte "new_feature" # will delete from remote repo
git branch -s # to verify
# To go back to an old version and branch off
git log --graph --oneline --all --decorate # to see all committs # 
git checkout -b new-branch-name 4f8d768 # Creating a new branch from an old commit
```

### Rolling back to a previous commit
#### Step 1: Reset to the desired commit
```
git log -1                # Find commit 
git reset --hard <....>   # Step 1: Roll Back
git clean -n              # Step 2: Perform a dry run to see what will be removed
git clean -f              # Step 3: Remove untracked files
git clean -fd             # Step 4: Remove untracked directories
git clean -fX             # Optional Step 5: Remove ignored files
git clean -fdx            # Optional Step 6: Remove all untracked files, directories, and ignored files
```

### Easy


One Line init, add, commit
```
git init && git add -A && git commit -m "Initial commit"
```

Link To a repo
```
git remote add origin https://github.com/<username>/<repo>.git
## This is not a good way to do this ...
git branch -M master
git push -u origin master
```

Abandon all changes and remove all files not explicitly tracked
```
git reset --hard HEAD && git clean -fdx
```

Visual CLI Commit Tree
```
git log --oneline --graph --decorate --all
```

Note if you put any file in the git hub upon creation it will not like the push; to force it you can
Force push to the remote repository
Be CAREFUL when you do this. It will wipe out the remote repo should only be done on set up.
```
#----CAUTION
git push --force origin master
#----CAUTION
```


## Useful Terminal (Linux/Mac)
show ssh keys: ```ls -al ~/.ssh```

## Podman CLI
1. Start the Podman machine ```podman machine start```

2. Verify the Podman machine is running ```podman machine list```

3. Pull a Node.js image ```podman pull node:latest```

5. Create and run a container```podman run -it -p 8080:8080 --name node-dev-container -v $(pwd):/usr/src/app -w /usr/src/app node:latest /bin/bash```
 - 8080 access
 - shared Volume

5. Inside the container, install Node.js dependencies and start the development server ```npm install;npm start```
