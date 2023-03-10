<h1>Overview</h1>
This project will demonstrate how we can combine React with Spring Boot. To accomplish this, we will use Node.js, npm, Vite, and Maven. The advantages of this approach are:

<br/>
<br/>
<ul>
  <li>We can write our React-based frontend as JSX files without having to manually compile them into JavaScript</li>
  <li>Our compiled JavaScript will automatically be placed into our src/main/resources/static folder</li>
  <li>We can take advantage of Spring Boot's hot reload feature (with one caveat)</li>
  <li>Our backend and frontend can operate on the same port (so we don't have to label our REST controller with @CrossOrigin nor change the port of our frontend)</li>
</ul>

Although the current project works as is, the following instructions will show how we can create it from scratch (I will assume that you have Node.js installed locally on your machine). 

<h2>Instructions</h2>
1. Create a Spring Starter Project. We will only need Spring Web and Spring Boot DevTools as dependencies.<br/><br/>

![spring dependencies](https://github.com/seanpolid/spring-react-vite-images/blob/main/spring-dependencies.png?raw=true)

2. Either create a controller or configure the class entry point so your endpoint (i'm using '/') returns "index.html" (we state the file type since we're serving static content).

![controller](https://github.com/seanpolid/spring-react-vite-images/blob/main/controller.png?raw=true)

3. Open up the terminal in your IDE or on your computer and navigate to the project so you're at the root level.

![root directory](https://github.com/seanpolid/spring-react-vite-images/blob/main/root-dir.png?raw=true)

4. Run the npm commands below in the given order:
<blockquote>
npm create vite@latest frontend -- --template react <br/>
cd frontend <br/>
npm install
</blockquote>

![npm commands](https://github.com/seanpolid/spring-react-vite-images/blob/main/npm-commands.png?raw=true)


5. Open the vite.config.js file in the frontend folder and specify the outDir so it points to our static resources folder:

![vite config](https://github.com/seanpolid/spring-react-vite-images/blob/main/vite-config.png?raw=true)

6. Open the package.json file in the frontend folder and add the 'watch' script (this will automatically compile our jsx on each new save):

![package.json](https://github.com/seanpolid/spring-react-vite-images/blob/main/package-json.png?raw=true)

7. While you're in the frontend folder (terminal), run the following command:
<blockquote>npm run watch</blockquote><br/>

8. Edit the App.jsx file in the frontend/src folder and save. <br/>

9. Refresh your project and look in src/main/resources/static. You should see an index.html file and an assets folder (confirming that vite is now tracking our changes).

Pre App.jsx edit:

![package.json](https://github.com/seanpolid/spring-react-vite-images/blob/main/resources-before.png?raw=true)

Post App.jsx edit:

![package.json](https://github.com/seanpolid/spring-react-vite-images/blob/main/resources-after.png?raw=true)


Run the whole project as a Spring Boot Application. Using your preferred browser, navigate to the path indicated by your controller (for me it's http:localhost:8080/). You should see the following (if not, make sure to refresh your project):
To deploy the application, right click on your project (if using Eclipse; may be different for other IDEs) and click 'Run as' then 'Maven Build...'.
Specify 'package' as a goal and click run. Check the 'target/' folder in your project to confirm you see a file called 'spring-react-vite-cli-0.0.1-SNAPSHOT.jar'.
Make sure that the Spring Boot server from before isn't still running. If it isn't, then navigate to the target folder using the terminal and run the following command:
java -jar spring-react-vite-cli-0.0.1-SNAPSHOT.jar
If you go into a browser and check the same path from before, you should see our React app. (Congrats if you made it this far!)
