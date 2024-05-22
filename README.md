# Notes
Personal Notes / Reminders
## Python 

### VENV

```zsh
# to create a virtual enviorment named "venv"
python3 -m venv venv

# to activate
source ./venv/bin/activate

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
 - if single label multiclassification then ```loss=categorical_crossentropy``` 

##### 3 Fit ```model.fit(x_train, y_train, epochs=_, batch_size=_2^n_)```
 - epochs is number of forward + backward pass the model makes attempting to reduce loss carefull not to overfit


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
```bash
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
```bash
git branch "new_feature" # Makes the branch
git checkout "new_feature" # Moves you over the the branch
git add -A
git commit -m "small_new_feature" # uploads teh change ONLY to the branch
git push -u origin "new_feature" # slightly complex command that associates the brance with main
git branch -a # To verify
# Ready to merge with Master Branch
git checkout master
git pull origin master
git merge "new_feature" # Merges the changes 
git push origin master # Uploads the changes to remote repo
#Delete the Branch
git branch -d "new_feature" # will delete localy
git push origin --delte "new_feature" # will delete from remote repo
git branch -s # to verify
```
