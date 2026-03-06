=========================================================
DEVSECOPS LOCAL ENVIRONMENT - OPERATIONS MANUAL
=========================================================

This document outlines how to start and stop the local 
infrastructure required for the CI/CD pipeline.

---------------------------------------------------------
PART 1: HOW TO START THE ENVIRONMENT
---------------------------------------------------------
Execute these steps before pushing code to GitHub to 
ensure your local runner and security scanners are ready.

1. Start Container Runtime:
   - Open the "Rancher Desktop" application on your Mac.
   - Wait for the background virtual machine to initialize.

2. Start Local SonarQube Server:
   - If you run SonarQube via Docker:
     Open a terminal and run:
     docker start sonarqube
     (Or whatever name you gave your Sonar container)
   
   - If you downloaded the SonarQube ZIP file:
     Open a terminal, navigate to the SonarQube folder, and run:
     cd bin/macosx-universal-64
     ./sonar.sh start

   - Verification: Go to http://localhost:9000 in your browser.

3. Start GitHub Actions Self-Hosted Runner:
   - Open a NEW terminal window.
   - Navigate to the folder where you installed the runner:
     cd path/to/actions-runner
   - Start the listening service:
     ./run.sh
   - Verification: Terminal should say "Listening for Jobs".

4. Develop and Push:
   - You can now push code to GitHub. The local runner will 
     pick up the jobs and execute the pipeline.


---------------------------------------------------------
PART 2: HOW TO STOP THE ENVIRONMENT
---------------------------------------------------------
Execute these steps to free up your Mac's CPU and memory 
when you are done working.

1. Stop the GitHub Actions Runner:
   - Go to the terminal window running `./run.sh`.
   - Press `Ctrl + C` on your keyboard.
   - The terminal will say "Exiting runner...".

2. Stop the Local SonarQube Server:
   - If you run SonarQube via Docker:
     Open a terminal and run:
     docker stop sonarqube
   
   - If you run SonarQube via the ZIP script:
     Open a terminal, navigate to the SonarQube bin folder:
     ./sonar.sh stop

3. Stop Local Test Containers (If any are running):
   - Check for running app containers:
     docker ps
   - Stop them using their Container ID:
     docker stop <CONTAINER_ID>

4. Stop Container Runtime:
   - Click the Rancher Desktop icon in your Mac's menu bar 
     (top right) and select "Quit Rancher Desktop".

=========================================================