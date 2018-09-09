# code-challenge-ui

### Introduction 
This repository contains the UI automation code for the challenge . It has a self contained automation framework that was build atop of selenium java binding . It also has a docker file Which installs all the dependencies and runs the test cases(In Chrome at the moment)
### Running the test cases 
There are two ways to run the test cases , you can use the provided dockerFile or follow the steps given in the section 'Running the Test Locally'
#### __Using the provided DockerFile__  
The easiest way is to use the DockerFile provided with this project. Here are the steps 
1. Please make sure that you have docker installed in your PC. This can be downloaded from https://www.docker.com/products/docker-desktop
2. Download the contents of the docker folder . You will see two files (DockerFile and startup_script.sh) 
3. Open a Command prompt and navigate to the folder and type __`docker build -t execution_env:latest .`__ (Notice a dot(.) in the command)
4. Once the image is built , type __`docker run execution_env:latest`__ ,Now the latest code will be downloaded from the github and the automation will run . The script output will be shown in the commandline , However you cannot see the tests running in the browser or download the reports 

#### __Running the Test locally__
__Prerequisites:__
1. The project requires maven(3.X) to be installed and configured . For more details please refer to https://maven.apache.org/install.html
2. The automation needs selenium server running in standalone mode or grid mode, Either locally or at an IP that is visible  

__Configuation Steps:__

1. Download Selenium server : Download the selenium standalone server jar from https://www.seleniumhq.org/download/
2. Download Chrome driver : Download the latest version of the chrome driver from http://chromedriver.chromium.org/downloads ,extract the contents and __copy the chromedriver binary to the same folder containing the selenium standalone server jar file__
3. Download the firefox driver from https://github.com/mozilla/geckodriver/releases, extract the contents and __copy the firefoxdriver binary to the same folder containing the selenium standalone server jar file__
4. Launch the selenium server in standalone mode with the command __`java -jar <path to the selenium standalone.jar>`__

__Running the Tests:__

The tests can be launched from the command line, First Navigate to the automation-code-challenge base folder 
1. To run the automation in chrome type __`mvn clean test -Dbrowser=chrome`__
2. To run the automation in firefox type __`mvn clean test -Dbrowser=firefox`__

#### __Configurable Parameters(Or System Properties)__
The Framework has three configurable parameters 
1. __-Dbrowser__(The browser to run the automation on ). The default value is chrome and the allowed options are chrome and firefox) 
2. __-Denv__(The evironment to run the automaton on). The Default and only allowed value is prod
3. __-Dserver__(The selenium server URL) . The Default value is http://localhost:4444/wd/hub

For example the command __`mvn clean test -Dbrowser=chrome -Denv=prod -Dserver=http://10.0.192.112:4444/wd/hub`__ will run the automation on chrome , with prod evnironment URL (http://automationpractice.com/index.php) with a selenium server running on the host 10.0.192.112
