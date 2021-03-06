#WDI Singapore Install Fest

For the first portion of the class, we'll be working exclusively inside of the browser and Node. We'll be installing the following tools.

* Slack
* Homebrew
* Git
* Node
* Oh my ZSH
* iTerm
* Postgres.app
* Ruby
* Rails

##Slack

We will be using slack to communicate throughout the course. You should've received an invite to our channels via e-mail. You can login via the web browser, but downloading / installing the app is highly recommended.

[Download Slack](https://slack.com/downloads)

##Homebrew

Homebrew is a package manager that we will use to install various command line tools in our class.

Open up terminal, and paste the following command to install Homebrew. You might be prompted to install XCode Command Line Tools during the install process.

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

You may be prompted to installed XCode command line tools. When prompted, click and install through that, and you're homebrew installation will continue.

After the installation process, run the command `brew doctor`. If any warnings or errors are displayed, we will need to resolve them before proceeding with the rest of the install fest.

##Xcode

Speaking of Xcode, install Xcode through the App Store. [Link here](https://itunes.apple.com/us/app/xcode/id497799835?mt=12)

##GIT
Before we do this process, please make sure you have signed up for an account on [Github](http://www.github.com). We will be installing a version of GIT from home brew and also configuring it.

To install GIT
```
brew install git
```

####Configuring GIT

Using your email credentials for GIT, run these commands with your user and email configured.

```
git config --global user.name "YOUR-USERNAME"
git config --global user.email "YOUR-EMAIL-ADDRESS"
git config --global push.default simple
git config --global credential.helper osxkeychain
```

You should probably install the command line prompt and autocompletition plugins:
https://git-scm.com/book/en/v2/Git-in-Other-Environments-Git-in-Bash

#### Caching Github Login
We'll mainly be using HTTPS, so use a credential helper to cache our keys. You should already be setup if you used homebrew to install git, else follow these steps: https://help.github.com/articles/caching-your-github-password-in-git/#platform-mac

For SSH Keys you can cache them too if needed:
https://help.github.com/articles/generating-ssh-keys/

##Node

To install Node
```
brew install node
```

Verify the installation afterwards by running

```
node -v
npm -v
```

The above should display without any errors.

To finish up your installation, run this command to allow for global installations of npm tools.

```
sudo chown -R $USER /usr/local/lib
```


##Sublime
We'll be running **Sublime**, as our text editor of choice.

Download and install the latest version [https://www.sublimetext.com/](https://www.sublimetext.com/)

## (optional) Pimp your Terminal with iTerm & Oh My ZSH

A shell is an interface into our computer, and we will be using a lot to run commands. You can 'make it hipper' by installing some packages:

https://gist.github.com/kevin-smets/8568070

## [Postgres](#postgres)

### Postgres.app
We will be using a relational database called Postgres for Node and Rails portion our class.

Download and install from [http://postgresapp.com/](http://postgresapp.com/)

Get the version of Postgres being installed on your system:
```
ls -la /Applications/Postgres.app/Contents/Versions
```

There should be only one version in this directory, or take the highest version.

Create the export path command with that version number/directory name
```
export PATH=$PATH:/Applications/Postgres.app/Contents/Versions/9.5/bin
```

Type `which psql` at which point should display

```
/Applications/Postgres.app/Contents/Versions/9.5/bin/psql
```

###Install Postgres GUI

We'll be using **Postico**. Install here:

https://eggerapps.at/postico/

##Installing Ruby on Rails

###Install rbenv
rbenv lets us change ruby verions on the fly, useful for working with diffrent versions.

```
brew update
brew install rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
source ~/.zshrc

sudo chown -R $USER ~/.rbenv
```

###Configuring rbenv
```
brew update

brew install ruby-build

rbenv install 2.2.2
rbenv global 2.2.2
```

###Install Rails

```
echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

Restart your terminal. The command above will install gems without documentation (which can take up time when installing Rails)

```
sudo gem update
sudo gem install rails
```
You may need to press "yes" for various entries

###Verify your installation

Make sure to restart your terminal and then run each of these commands. Finally call someone over to validate your installation is correct.

```
rails -v
ruby -v

which ruby
which rails
which bundle
which gem

node -v
npm -v

git --version
psql --version

```

###OSX

```
alias srv="_srv(){open \"http://localhost:\${1-8000}\" && python -m SimpleHTTPServer \$1}; _srv"
```


3.) Close and restart your terminal, or run `sublime ~/.zshrc` to reload the file.

Now you should be able to navigate to the folder of your project (the folder containing index.html), type `srv`, and hit enter. This will start a HTTP server and open your browser to that URL.

You can go back to the site at anytime by going to `http://localhost:8000`. You can quit the server by typing `CTRL + C`


#### Aside: Wildcard Protocols and HTTP

You'll notice that Bootstrap and other CDN URLs may start with `//`. This is a wildcard protocol, which means it will use whatever protocol your site is using (`http://` or `https://`). When we're loading a file locally, our protocol is `file:///`, meaning we're accessing a file on our harddrive. Therefore, the default CDN will look for the file on our computer (instead of on the CDN) and won't find it. To fix this, we need to run a HTTP server.
