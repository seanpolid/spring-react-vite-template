<h1>Overview</h1>
This project will demonstrate how we can combine React with Spring Boot. To accomplish this, we will use Node.js, npm, Vite, and Maven. The advantages of this approach are:

<br/>
<br/>
<ul>
  <li>We can write our React-based frontend as JSX files without having to manually compile them into JavaScript</li>
  <li>Our compiled JavaScript will automatically be placed into our src/main/resources/static folder</li>
  <li>We can take advantage of Spring Boot's hot reload feature (with one caveat)</li>
  <li>Our backend and frontend can operate on the same port (so we don't have to label our REST controller with @CrossOrigin nor change the port of our frontend; If you want to be able to use the Vite dev server, use the annotation @CrossOrigin(origins={"http://localhost:5173"}) above the necessary controllers)</li>
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
<blockquote>npm run watch</blockquote>

8. Edit the App.jsx file in the frontend/src folder and save. <br/>

9. Refresh your project and look in src/main/resources/static. You should see an index.html file and an assets folder (confirming that vite is now tracking our changes).

Pre App.jsx edit:

![static folder before](https://github.com/seanpolid/spring-react-vite-images/blob/main/resources-before.png?raw=true)

Post App.jsx edit:

![static folder after](https://github.com/seanpolid/spring-react-vite-images/blob/main/resources-after.png?raw=true)

10. Run the whole project as a Spring Boot Application. Using your preferred browser, navigate to the path indicated by your controller (for me it's http:localhost:8080/). You should see the following:

![react display](https://github.com/seanpolid/spring-react-vite-images/blob/main/react-served.png?raw=true)

** If you don't see it, make sure to refresh your project.

11. Create a simple REST controller that returns "Hello world!" from the endpoint '/api/hello'

![rest controller](https://github.com/seanpolid/spring-react-vite-images/blob/main/simple-rest-controller.png?raw=true)

12. In the App component, create a new state to track our "Hello world!". Additionally, create a hook that fetches data from our endpoint:

![rest controller](https://github.com/seanpolid/spring-react-vite-images/blob/main/use-effect.png?raw=true)

13. Place the 'hello' variable into the App's JSX:

![App's JSX](https://github.com/seanpolid/spring-react-vite-images/blob/main/app-jsx.png?raw=true)

14. Refresh the project and check your browser. It should look like the following:

![hello world!](https://github.com/seanpolid/spring-react-vite-images/blob/main/hello-world.png?raw=true)

15. To deploy the application, right click on your project (if using Eclipse; may be different for other IDEs) and click 'Run as' then 'Maven Build...'.

16. Specify 'package' as a goal and click run. Check the 'target/' folder in your project to confirm you see a file called 'spring-react-vite-template-0.0.1-SNAPSHOT.jar'.

![Maven build](https://github.com/seanpolid/spring-react-vite-images/blob/main/maven-build.png?raw=true)

![target folder](https://github.com/seanpolid/spring-react-vite-images/blob/main/target-folder.png?raw=true)

17. Make sure that the Spring Boot server from before isn't still running. If it isn't, then navigate to the target folder using the terminal and run the following command:
<blockquote>java -jar spring-react-vite-template-0.0.1-SNAPSHOT.jar</blockquote>

![java jar deploy](https://github.com/seanpolid/spring-react-vite-images/blob/main/java-jar-deploy.png?raw=true)

If you go into a browser and check the same path from before, you should see our React app. 

<h2>Important Notes</h2>
As mentioned above, there is one caveat to this approach. You may have noticed this already, but to see the changes you've made to the frontend, you need to refresh the whole project each time. The reason for this is because Vite creates new files on each build. If it were only modifying them, then a refresh would not be necessary (since Spring Boot's hot reload would make the necessary adjustments). 
<br/>Also, prior to going with this approach, I did try to use the frontend-maven-plugin instead of a locally installed version of Node.js. I was able to adjust the plugin executions so I could run the necessary npm commands, but I kept running into build issues. Since the script 'Vite build --watch --emptyOutDir' runs indefinitely, whenever Maven would automatically build the project (thus executing the script) it would get stuck. This became too problematic since I would have to forcefully close the IDE each time.
