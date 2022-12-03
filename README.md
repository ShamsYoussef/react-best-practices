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
* [React Component Best Practices](#react-component-best-practices)
* [React Code Structure Best Practices](#react-code-structure-best-practices)

 ## React Project Structure Best Practices
 While creating a react project, the first step is to define a project structure that is scalable. You can create a new base react application structure by using the npm command `create-react-app`. The below screenshot displays the basic react app folder structure.

  ![image](https://user-images.githubusercontent.com/63429054/205446786-1083bf72-973a-4d3b-8e74-b61555fa119c.png)

   <p> React folder structure may differ based on project specification and complexity. There are various reactjs best practices that can be taken into account while defining project architecture: </p>
   
   ### Folder Layout
   The architecture focuses on reusable components of the react developer architecture so that the design pattern can be shared among multiple internal projects. Hence the idea of component-centric file structure should be used which implies that all the files related to a different component (like test, CSS, JavaScript, assets, etc.) should be kept under a single folder.
   ```jsx
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
  ```jsx
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
  ## React Component Best Practices
  Its components are the building blocks of a react project. Here are some of the React best practices that can be considered while coding with React in the component state and component hierarchy.
  
  ### 1. Decompose into Small Components

  Try to decompose large components into small components such that component performs one function as much as possible. It becomes easier to manage, test, reuse and create a new small components.
  
  ### 2. Use Functional Components with Hooks

After the release of React v16.08, it’s possible to develop function components with the state with the new feature ‘React Hooks’. It reduces the complexity of managing states in Class components. So always prefer to use functional components with React Hooks like useEffect(), useState() etc. This will allow you to repeatedly use facts and logic without much modification in the hierarchical cycle.
### 3. Appropriate Naming and Destructuring Props

To keep readable and clean code, use meaningful and short names for props of the component. Also, use props destructuring feature of function which discards the need to write props with each property name and can be used as it is.

```jsx
const funcDestruct = ({name, title}) => {
return <p>{name} – {title}</p>
}
```

## React Code Structure Best Practices

### 1. Naming Conventions
 - A component name should always be in a Pascal case like ‘SelectButton’, ’Dashboard’ etc. Using Pascal case for components differentiate it from default JSX element tags.
 - Methods/functions defined inside components should be in Camel case like ‘getApplicationData()’, ‘showText()’ etc.
 - For globally used Constant fields in the application, try to use capital letters only. Like const PI = “3.14”;

### 2. Avoid the Use of the State as much as Possible
Whenever using state in the component, keep it centralized to that component and pass it down in the component tree as props.

### 3. Write DRY Code

Try to avoid duplicate code and create a common component to perform the repetitive task to maintain the DRY (Don’t Repeat Yourself) code structure.
For instance: When you need to show multiple buttons on a screen then you can create a common button component and use it rather than writing markup for each button.

### 4. Try to Avoid Unnecessary Div
When there is a single component to be returned, there is no need to use `<div>`. 

❌ Dont't
```jsx
return (
<div>
<Button>Close</Button>
</div>
);
```

✔️ Do:
```jsx
return <Button>Close</Button>
```

When there are multiple components to be returned, use or in shorthand form <> as shown below:

❌ Dont't
```jsx 
//Will throw an error

const InfoText = () => {
  return (
    <h1>Welcome!</h1>
    <p>This our new page, we're glad you're are here!</p>
  )
}
```
	
✔️ Do:
```jsx	
const InfoText = () => {
  return (
        <>
      	   <h1>Welcome!</h1>
      	   <p>This our new page, we're glad you're are here!</p>
    	</>
  )
}
```
