## Continuos Integration 

Continuous integration automates the building, testing and deploying of applications.

#### Why is continuous integration important?

When continuous integration (CI) is established as a step in a software project's development process it can dramatically reduce deployment times by minimizing steps that require human intervention.

#### Automated testing

Another major advantage with CI is that testing can be an automated step in the deployment process. Broken deployments can be prevented by running a comprehensive test suite of unit and integration tests when developers check in code to a source code repository.

CI combined with unit and integration tests check that any code modifications do not break existing tests to ensure the software works as intended.

## Continuous integration example

The following picture represents a high level perspective on how continuous integration and deployment can work.

![alt text](https://raw.githubusercontent.com/RubypyCoding/continuos-integration--Python/images/continuous-integration.png)

- When new code is committed to a source repository there is a hook that notifies the continuous integration server that new code needs to be built (the continuous integration server could also poll the source code repository if a notification is not possible).

- The continuous integration server pulls the code to build and test it. 

- If all tests pass, the continuous integration server begins the deployment process. 

- The new code is pulled down to the server where the deployment is taking place. 

- Finally the deployment process is completed via restarting services and related deployment activities.

There are many other ways a continuous integration server and its deployments can be structured. The above was just one example of a relatively simple setup. [CI](https://www.fullstackpython.com/continuous-integration.html).

## Heroku Configuration for CI

We'll use Heroku to deploy our project.

#### Step 1

Create a Heroku account.

#### Step 2

Install Heroku CLI.

```python
$ brew install heroku/brew/heroku
```

#### Step 3

In terminal go to your project folder and login to heroku:

```python
$ heroku login
```

#### Step 4

Create your project name:

```python
$ heroku create <appname>>
```

#### Step 5

Inside your heroku dashboard, go to "Deploy", search for "Deployment method" and then select the GitHub option.

#### Step 6

At Deploy tab on the “Automatic deploys” section don't forget to check the "Wait for CI to pass before deploy" option and enable the Automatic Deploys.

#### Step 7

Inside your heroku dashboard, go to "Setting" section and enable heroku builpacks, select python option.

#### Step 8

You can verify in your github repository on the Webhooks Settings. You have linked your app heroku account through webhooks. A webhook in web development is a method of augmenting or altering the behaviour of a web page, or web application, with custom callbacks.


## CI Configuration in Python


We will use Travis CI to test various components of our software stack before releasing it to customers. This will allow us to make improvements without breaking existing functionality.

#### Step 1

Install [PIP](https://www.w3schools.com/python/python_pip.asp) in your system PIP is a package manager for Python packages, or modules. 

Check if you have installed PIP:

```python
$ pip --version
```

If not:

```python
$ sudo easy_install pip
```

[In case of error](https://stackoverflow.com/questions/20082935/how-to-install-pip-for-python-3-on-mac-os-x).

#### Step 2

Create `requirements.txt` in the folder of your program:

```python
django
gunicorn
django-heroku
```

#### Step 3 - Link Travis CI and GitHub


Create a Travis CI account and flick the repository switch on for your repo.


#### Step 4 - Build Configuration

Create a file called `.travis.yml` in the folder of your program:

```python
language: python
python:
  - "3.6"
cache: pip
install:
  - pip install -r requirements.txt
script:
  - python test_primes.py
```

- The `language` section is used to specify the language of the software.
- The `python` section is used to specify the version or versions of Python to use for testing.
- The `install` section is used to specify commands to run before testing, such as the installation of dependencies or the compilation of required packages.
- The `script` section is used to specify the command to test your software. Typically, this command will find all tests in your project and run them. The specified command must exit with a status code of 0 if the test is successful; otherwise the test will be considered a failure.


For advanced build configuration, see the Travis CI documentation on [Configuring your build](https://docs.travis-ci.com/user/customizing-the-build/).

#### Step 5 - Trigger builds
To trigger builds,  push the commit that adds “.travis.yml” to the project.

```python
$ git status
$ git add .
$ git commit -m "Adding travis yml"
$ git push origin master
```

#### Step 6 - Restart Build

Go to your Travis CI dashboard and click on `Restart build` or simply wait the reload of your repository.

#### Step 7 - Deploy it automatically

Go to your Heroku Dashboard and check the lastest activity. Now everytime you update your project in github repository, Travis CI will be running the tests and when this tests were passed Heroku will deploy it automatically!

CI SUPER POWER!!!!




