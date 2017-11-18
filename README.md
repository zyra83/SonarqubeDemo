	Pour le moment avant de fair e lien entre les 2 taches bien lancer 
	  ./gradlew jacocoTestReport
	  ./gradlew sonarqube   -Dsonar.host.url=http://127.0.0.1:9000   -Dsonar.login=211b9a42f50be9e51aefd0a6072b5d4e25080880


# SonarqubeDemo

#### Installing SonarQube
The installation is pretty straightforward, you have just to download an archive and extract it in a folder of your choice.

1. Go to http://www.sonarqube.org/downloads/ and download the latest release.
2. Unzip the archive

#### Starting SonarQube
1. Go to sonarqube-4.3/bin (or whatever version you downloaded)
2. Open a corresponding folder according to your operating system (linux-x86-64 in my case). There you should see a file called sonar.sh (or StartSonar.bat for Windows)
3. Open up a terminal window and execute: sonar.sh start (or just double click StartSonar.bat on windows). This command will start sonar listening on localhost:9000.
4. Open a browser and enter localhost:9000. The sonar web page should open.
Note that it may take some time until sonar loads, so if you get “page not found” in your browser, try to refresh the page later.

#### Activate the scanner in your build
For Gradle 2.1+:
# build.gradle
plugins {
  id "org.sonarqube" version "2.5"
}
#### SonarQube Configuration
Now we should start and configure SonarQube. Therefore you need to login into the administrator account. On the top right you see the login link. Login using “admin” and “admin” which is the default. For a non local server I highly recommend to change the password immediately!

Next we install all necessary plugins. Go to the “Administrator” page and select “Update Center” in the “System” dropdown. Select now the “Available” tab and install the following plugins:

- Android
- Checkstyle
- Findbugs
- Git
- Java
- XML
It could be possible that some of them are already installed. You can check if they are there when you activate the “Installed” tab. The installations are currently just pending, you need to restart or stop/start the SonarQube server with the previously mentioned scripts.

#### Analysing source code of a project
1. Navigate to the root directory of your project and create a file called sonar-project.properties, which will specify the project settings such as the code source directory, language used, and the project name:

- sonar.projectKey=myproject
- sonar.projectName=My Project
- sonar.projectVersion=1.0
- sonar.sources=src
- sonar.language=java
- sonar.sourceEncoding=UTF-8

Note: for Android Studio, which follows the gradle directory structure, set the sourses as:

- sonar.sources=src/main/java

2. Run ./gradlew sonarqube command to start the analysis.
3. Once the analysis complets, head to localhost:9000 to see the results for your project.


