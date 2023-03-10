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
