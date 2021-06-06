# I. Step-Wise Deployment on Heroku (Streamlit)

1. Build your Python App and test on local server
2. Build `requirements.txt`
   ```
   pipreqs <directory-path>
   ```
3. Build `setup.sh` file and paste the following code snippet : 
   In the setup.sh file we will create a streamlit folder with a credentials.toml and a config.toml file.
   ```
   mkdir -p ~/.streamlit/

   echo "\
   [general]\n\
   email = \"your-email@domain.com\"\n\
   " > ~/.streamlit/credentials.toml

   echo "\
   [server]\n\
   headless = true\n\
   enableCORS=false\n\
   port = $PORT\n\
   " > ~/.streamlit/config.toml
   ```
   
4. Build `Procfile`. **Remember not to add extension**
   ```
   web: sh setup.sh && streamlit run app.py
   ```
   
5. Now run the following commands : 
   **Note - Make sure you have an account on Heroku and Heroku CLI is installed on your system.**

  ```
  git init
  heroku login 
  heroku create app-name
  git add .
  git commit -m "message"
  git push heroku master
  ```
  To check if your app is running, enter the following command : 
  ```
  heroku ps:scale web=1
  ```
  It should return : 
  ```
  scaling dynos... done, now running web at 1:Free
  ```
6. **Voila...**


# II. Step-Wise Deployment of Node Website on Heroku (with Database)

## Note - Make sure you are in you project directory :

1. git init
2. git add .
3. git commit -m "message"
4. heroku login
5. heroku create app-name
6. Add a Procfile. **Make sure not to add extension**
   ```
   web: node app.js
   ```
7. Add dynamic port in your **app.js** or add the following snippet :
   
   ```
   let port = process.env.PORT;
   if (port==null || port==""){
   port=3000;
   }
   app.listen(port,function(){
    console.log("Server has started successfully.");
   });
   ```
 8. Specifiying the version of Node in **package.json** : 
 
    ```
    ....
    "license": "ISC",
    "engines": {
    "node" : "Node Version of your application"
    },
    ```
  9. Make **.gitignore** file  and add the following (edit as per your will):

     ```
     /node_modules
     npm-debug.log
     .DS_Store
     /*.env
     ```
  10. Finally run the following commands : 
      
      ```
      git add .
      git commit -m "message"
      git push heroku master
      ```
     
# III. Step-Wise Deployment via GitHub Pages (Static Pages)

## Important - make a repository for your project on GitHub

1. Either upload project folder directly to your repository

2. Use Command Line - 

  * git init
  * git add <folder1> <folder2> <etc.> (or use git add .  to add all files)
  * git commit -m "Your message about the commit"
  * git remote add origin https://github.com/yourUsername/yourRepository.git
  * git push -u origin master
  * git push origin master
