# ldap_printer
LDAP based printer 

## Installation
- Make sure you have sudo permissions and python 2 installed. This project is written only for linux based OS
- Make sure firefox is installed in system and can be triggered using `firefox` command
- Make sure your internet connection is ready before installation starts
- Install dependencies

  ```bash
  sudo apt-get install python-dev python-pip libcups2-dev
  ```
- Install python dependencies by running `sudo pip install -r requirements.txt`
- Run installation script as `bash install.sh` or `./install.sh`
- Add `/usr/local/ldap_printer` in `/etc/sudoers` secure path.
- Delete this directory

## Usage
- Add the list of roll numbers who are enlisted in the hostel mess to data/roll\_no\_list.txt
- Edit data/printer.cfg file. There you have to rename PDF to the desired printer's name
- To print a file run command `ldap_print`
- To get account information of all users run `sudo rootaccount.py`. You need to be a sudo user. 
You will find the resultant file in `data/printer\_account.csv`.
    - Pass first argument as filename. If it is not present then filename `printer_account.csv` will be used.
    - Pass second argument as month for which you want accounting info. This should be integer. By default it is 
    current month
    - It generates two files `filename` and `verbose_filename`. `filename` has compact data i.e. total prints per user. 
  `verbose_filename` has details of all individual print events.

- Configure cups log-rotate rotation and deletion period for appropriate timespan. We recomment rotation period as 1 
month and deletion period 3-4 months. Learn how to do it using Google ;-)
- To prevent the local accounts from unauthorised use of the printer from browsers or pdf reader, do the following
    - To add the local accounts in the blacklist for the printer, do the following
      - Type system-config-printer on terminal and press Enter
      - Right click your desired printer and select properties
          - Select Access Control
          - Select Deny printing for everyone, except these users option
          - Add root as username here and click apply
  
        


## Development
- Install python development kit by 

  ```bash
     sudo apt-get install python-dev python-pip libcups2-dev
  ```

### virtualenv configuration
- **Ignore these steps if you're familiar with virtualenv**
- Install necessary dependencies by running `sudo pip install virtualenv virtualenvwrapper`
- Add following lines to your `~/.bashrc`

  ```bash
    
  export WORKON_HOME=~/.envs
  mkdir -p $WORKON_HOME
  source /usr/local/bin/virtualenvwrapper.sh
  ```
- Create virtualenv by `mkvirtualenv ldap-printer`. Deactivate by `deactivate` and again activate by `workon ldap-printer`

### Installation for development
- Install Python dependencies by running `pip install -r requirements.txt`
- cpp wrapper is generated by running `python generate_wrapper.py`. Compile it with `g++` to get executable file
- Directly run application by `python printmain.py`


## Uninstall
- Delete project directory from `/usr/local/ldap_printer`
- Remove environment variable from `/etc/profile.d/ldap_printer.sh`
