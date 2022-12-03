<h1 align="center">React Best Practices <a href="https://reactnative.dev/" target="_blank" rel="noreferrer">
    <img
      src="https://reactnative.dev/img/header_logo.svg"
      alt="reactnative"
      width="40"
      height="40"
    />
  </a>
  </h1>
  
 ## Table of contents
* [React Project Structure Best Practices](#react-project-structure-best-practices)

 ## React Project Structure Best Practices
 <p> While creating a react project, the first step is to define a project structure that is scalable. You can create a new base react application structure by using the npm command ‘create-react-app’. The below screenshot displays the basic react app folder structure.</p>

  ![image](https://user-images.githubusercontent.com/63429054/205446786-1083bf72-973a-4d3b-8e74-b61555fa119c.png)

   <p> React folder structure may differ based on project specification and complexity. There are various reactjs best practices that can be taken into account while defining project architecture: </p>
   
   ### 1. Folder Layout
   The architecture focuses on reusable components of the react developer architecture so that the design pattern can be shared among multiple internal projects. Hence the idea of component-centric file structure should be used which implies that all the files related to a different component (like test, CSS, JavaScript, assets, etc.) should be kept under a single folder.
   ```
   Components
	|
	--Login
		|
		--tests--
		--Login.test.js
		--Login.jsx
		--Login.scss
		--LoginAPI.js
   ```
  This is another approach used in grouping the file types. In this, the same type of files is kept under one folder. For example:
  ```
  APIs
  |	
  --LoginAPI
  --ProfileAPI
  --UserAPI

Components
  |	 
  --Login.jsx
  --Login.test.js
  --Profile.jsx
  --Profile.test.js
  --User.jsx
  ```
