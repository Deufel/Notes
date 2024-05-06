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
#!/opt/homebrew/Caskroom/miniconda/base/envs/mathenv
```
 - Note you must run this as an executable in order for the ```#!``` to work 

```zsh
chmod +x filename.py
ls -la #to verify
./filename.py
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
