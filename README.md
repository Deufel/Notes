# Notes

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
 - Note you must run this as an executable in order for the #! to work 

```zsh
chmod +x filename.py
ls -la #to verify
./filename.py
```
