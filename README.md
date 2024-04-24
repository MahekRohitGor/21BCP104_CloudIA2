# 21BCP104_CloudIA2
Cloud Computing Lab IA2

Create any three-tier application using Docker, using a multi-container setup. Build at least one docker image using Dockerfile. You are free to use your old projects, build new projects or take any project from GitHub. However, if you are using a project from Github, properly cite the original author of the code in your blog. 


1. Write a blog post in a tutorial-like manner, documenting every little step of your work. This blog should include screenshots and explanations. You can include some diagrams, too, if necessary. You are free to make the tutorial in parts. But in such case, part 1 should have a link to part 2 and so on.  
2. The blog post should be posted on your own GitHub pages blog. (Search for "How to set up a blog using GitHub pages and Jekyll". )
3. The Dockerfile(s) should be uploaded to a Github repository, with a Readme file explaining each line of the Dockerfile.  
4. As usual, append your roll number to the image/container name. Also, make sure to display your roll number in your presentation tier (front end). 
5. You can use any DBMS you like, but I encourage you to use a Database management software which you have not used before. 

Node.js application follows a three-tier architecture:
Database Tier: Utilizing MongoDB for data storage and management.
Frontend and Backend Tier: HTML and CSS for frontend and Node.js is used for backend development.
Management Server: mongo-express serves as a web-based interface for managing the MongoDB database.

## Step by Step Procedure
**Step 1:** Clone the Project<br>
To begin, clone the project from the repository hosted by Nana Janashia.<br> You can access the project via the following Git URL:
https://gitlab.com/nanuchi/developing-with-docker.git<br>
Once cloned, navigate to the directory where the project has been downloaded.
Open a terminal window and change the directory to the one where the project was cloned.
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/c7a8f050-9f8b-4049-b23b-2699efd5e2f2)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/813debc8-af8f-4638-a8a6-c0665709b5ce)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/ab8dae8a-1946-40e6-ab02-3cdf63a100ae)

**Step 2:** Create a Docker Network <br>
Create a Docker network to ensure container isolation. This will help in managing communication between containers.
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/2ab1f2d1-172b-40cf-ba37-7686a847f3f0)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/6b87598b-14fe-4f74-b2b2-4ef638d1e9f0)

**Step 3:** Run the Database Container<br>
Run the MongoDB container with the following command:
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/a78d0a10-7274-474a-bcc2-fa92e84d352e)

- Creates a detached MongoDB container.
- Connects it to a specified Docker network.
- Maps host port 27017 to container port 27017 for MongoDB client connections.
- Sets the MongoDB root username to "admin" and password to "password".
- Uses the official MongoDB Docker image.

**Step 4:** Run the mongo-express Server<br>
Run the mongo-express server container using the following command:
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/43896d9e-7d00-4ac1-b663-5c8a3ca53f21)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/d39bbb6d-534e-499f-a400-40b631c56e44)
Access the mongo-express interface by navigating to http://localhost:8081 in a web browser.<br> You will be prompted to enter the username and password. Use the provided credentials: username - admin, password - pass.<br>
Once logged in, you will be able to see the mongo-express dashboard.<br>
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/dc14efd4-0f79-4d1f-ac6e-8505816933fb)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/4e1d65ac-1a18-4afb-8aed-55ecb170a930)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/671463ca-78f1-49ee-a4fa-2e7cb5bc934b)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/e578ccfd-7a5f-405e-be30-0d08620b42c2)

**Step 5:** Create Docker Image for the Application<br>
Navigate to the 'app' folder of the project and create a Dockerfile. Add the below instructions to the Dockerfile for building the Docker image for the application.
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/067055b9-a1cd-442e-a5c7-9ba9589e8995)
- **FROM node**: This line specifies the base image to use for building the Docker image. In this case, it uses the official Node.js image from Docker Hub.<br>
- **WORKDIR /app**: This sets the working directory inside the container to /app. It means that any subsequent commands will be executed from this directory.<br>
- **COPY . .** : This copies the contents of the current directory (where the Dockerfile is located) into the /app directory within the container. The first . refers to the source directory (the current directory), and the second . refers to the destination directory (the /app directory inside the container).<br>
- **ENV MONGO_DB_USERNAME=admin** : This sets an environment variable named MONGO_DB_USERNAME with the value admin inside the container. This variable will be accessible to the application running in the container.
- **ENV MONGO_DB_PWD=password** : Similar to the previous line, this sets an environment variable named MONGO_DB_PWD with the value password inside the container.
- **RUN npm install** : This command install the Node.js dependencies for the application. It executes the npm install command inside the container's /app directory.
- **EXPOSE 3000**: This instruction informs Docker that the container listens on port 3000 at runtime. However, it does not actually publish the port. It's a way to document which ports the container is designed to use.
- **CMD [ "node", "server.js" ]** : This specifies the command to run when the container starts. It runs the Node.js application by executing node server.js. This assumes that server.js is the entry point file for the Node.js application.

![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/09531bc6-9ca8-4614-8406-2e00dbebaefe)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/9c1e3eed-45d4-4c65-b0d9-885bbd9b82cc)


**Step 6:** Update server.js and Build Docker Image<br>
Make the necessary changes to the 'server.js' file to replace occurrences of 'localhost' with the name of the MongoDB container.<br>
Once the changes are made, build the Docker image using the provided Dockerfile and run the container with the following command:<br>
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/f7b4e754-d152-4fc8-8dca-f8ea86879355)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/d7bf393e-a8d3-4410-9904-3c35f74a507a)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/0df89e9d-d3c3-4e66-9c8f-4b1118918d85)
![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/5768a8d5-5fcf-4601-a9fc-4df50f411acc)


Upon successful execution, you can access the website at http://localhost:3000 and interact with it. <br>

![image](https://github.com/MahekRohitGor/21BCP104_CloudIA2/assets/101034649/72aa425f-a5c0-4f92-acf4-a909c57b89ba)
