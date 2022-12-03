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
* 🗄️ [Project Structure Best Practices](#project-structure-best-practices)
* 🧱 [Component Best Practices](#component-best-practices)
* ✍️ [Code Structure Best Practices](#code-structure-best-practices)
* 📚 [Additional Resources](#additional-resources)

 ## Project Structure Best Practices
 While creating a react project, the first step is to define a **scalable** project structure. You can create a new react application structure by using the npm command `create-react-app`. Below is the basic react app folder structure.
 
```jsx
└── /src
  ├── /assets - ==> images, svgs, company logo etc.
  ├── /components ==> reusable components like navigation bar, buttons, forms
  ├── /services
  ├── /store ==> redux store
  ├── /utils ==> utilities, helpers, constants.
  ├── /pages ==> majority of the app pages would be here
  ├── index.js
  └── App.js
```

React folder structure may vary based on project specifications and complexity. There are several ReactJs best practices that can be considered when defining a project's architecture:
   
### Folder Layout
The architecture focuses on reusable components of the react developer architecture so that the design pattern can be shared among multiple internal projects. Hence the idea of a component-centric file structure should be used which means that all the files related to a different component (like test, CSS, JavaScript, assets, etc.) should be kept in one folder.

   ```jsx
   Components
	|
	--Profile
		|
		--Profile.test.ts
		--Profile.tsx
		--Profile.scss
		--ProfileAPI.ts
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
  --Profile.tsx
  --Profile.test.ts
  --User.tsx
  --User.test.ts
  --Login.tsx
  --Login.test.ts
  ```
  ## Component Best Practices
  Components are the building blocks of a react project. Here are some of the React best practices that can be considered while coding with React in the component state and component hierarchy.
  
### 1. Decompose into Small Components

  Try to decompose large components into small components such that component performs one function as much as possible. It becomes easier to manage, test, reuse and create a new small components.
  
### 2. Use Functional Components with Hooks

After the release of React v16.08, it’s possible to develop function components with the state with the new feature **React Hooks**’. It reduces the complexity of managing states in Class components. So always prefer to use functional components with React Hooks like `useEffect()`, `useState()` etc. This will allow you to repeatedly use facts and logic without much modification in the hierarchical cycle.
### 3. Appropriate Naming and Destructuring Props

To keep readable and clean code, use meaningful and short names for props of the component. Also, use props destructuring feature of function which discards the need to write props with each property name and can be used as it is.

```jsx
const FuncDestruct = ({name, title}) => {
return <p>{name} – {title}</p>
}
```

## Code Structure Best Practices

### 1. Naming Conventions
Use **PascalCase** in components, interfaces, or type aliases 👇
```jsx
// React component
const UserProfile = () => {...}

// Typescript interface
interface AdminUser {
  name: string;
  id: number;
  email: string;
}

// Typescript Type Alias
type TodoList = {
    todos: string[];
    id: number;
    name: string;
}
```
Use **camelCase** for JavaScript data types like variables, arrays, objects, functions, and so on 👇

```jsx
const getLastDigit = () => { ... }

const userTypes = [ ... ]
```

### 2. Use shorthand for boolean props
There are scenarios where you pass boolean props to a component.

❌ Don't
```jsx
<RegistrationForm hasPadding={true} withError={true} />
```
You don't need to do it necessarily like this because the occasion of the prop itself is either truthy (if the prop is passed) or falsy (if the prop is missing).A cleaner approach would be:

✔️ Do:
```jsx
<RegistrationForm hasPadding withError />
```

### 3. Write a fragment when a div is not needed
A React component can only render one single HTML tag at its root. So if you'd like to render two adjacent elements, you'll get the famous error called `Adjacent JSX elements must be wrapped in an enclosing tag`. 

❌ Don't
```jsx 
//Will throw an error
const LandingPage = () => {
  return (
    <h1>Hello!</h1>
    <p>This is our main page!</p>
  )
}
```
So, what can you do? You just wrap the rendered output into a fragment, which satisfies React and doesn't render an extra HTML element in the browser. 
	
✔️ Do:
```jsx	
const LandingPage = () => {
  return (
        <>
      	   <h1>Hello!</h1>
      	   <p>This is our main page!</p>
    	</>
  )
}
```
Of course you could have solved this with a div tag as well. But using div after div will create something like **div hell** in the browser where you got many deep nested div tags without any sense.

### 4. Use Destructuring to Get Props

Destructuring was introduced in ES6. This type of feature in the javascript function allows you to easily extract the form data and assign your variables from the object or array. Also, destructuring props make code cleaner and easier to read.

❌ Don't
```jsx 
const UserProfile = props => {
const firstName = props.firstName
const lastName = props.lastName
const city = props.city
  return (....)
}
```
	
✔️ Do:
```jsx	
const UserProfile = ({firstName, lastName, cit}) => {
  return (....)
}
```

### 5. Try to Avoid Unnecessary Div
When there is a single component to be returned, there is no need to use `<div>`. 

❌ Don't
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

### 6. Integrate self closing tags when no children are needed
when there are no children needed, try to use the component as a self closing element like the input tag in HTML, that doesn't take children as well.

❌ Don't
```jsx 
<UserProfile></UserProfile>
```

✔️ Do:
```jsx	
<UserProfile />
```

### 7. Sanitize your code to prevent XSS Attacks
Maybe you've found yourself in a scenario where you have to use the property dangerouslySetInnerHTML on an element in React. Basically it's React's equivalent to innerHTML you might know from Javascript. So using it, you can set HTML directly from React.

Let's consider the following example, where we'd like to render an HTML string inside a div. The string could come from a rich text editor where it's already formatted HTML.
```jsx
const Markup = () => {
  const htmlString = "<p>This is set via dangerouslySetInnerHTML</p>"
  
  return (
    <div dangerouslySetInnerHTML={{ __html: htmlString }} />
  )
}
```
The term dangerously is chosen with intention. Using this property can open you up to a cross-site-scripting (XSS) attack. So it's mandatory that the code that gets set is sanitized first. (A great library is [dompurify](https://www.npmjs.com/package/dompurify). that can help you out with this).

### 8. Take Advantage of Object Literals

Object literals can help make our code more readable. Let’s say you want to show three types of users based on their roles. You can’t use ternary because the number of options exceeds two.

❌ Don't
```jsx 
const {role} = user

switch(role){
  case ADMIN:
    return <AdminUser />
  case EMPLOYEE:
    return <EmployeeUser />
  case USER:
    return <NormalUser />
}
```
	
✔️ Do:
```jsx	
const {role} = user

const components = {
  ADMIN: AdminUser,
  EMPLOYEE: EmployeeUser,
  USER: NormalUser
};

const Component = components[role];

return <Componenent />;
```

### 9. Don't Define a Function Inside Render
Don’t define a function inside render. Try to keep the logic inside render to an absolute minimum.

❌ Don't
```jsx 
return (
    <button onClick={() => dispatch(ACTION_TO_SEND_DATA)}>    // NOTICE HERE
      This is a bad example 
    </button>  
)
```
	
✔️ Do:
```jsx	
const submitData = () => dispatch(ACTION_TO_SEND_DATA)

return (
  <button onClick={submitData}>  
    This is a good example 
  </button>  
)
```
### 10. Use Memo
`React.PureComponent` and `Memo` can significantly improve the performance of your application. They help us to avoid unnecessary rendering.

❌ Don't
```jsx 
import React, { useState } from "react";

export const TestMemo = () => {
  const [userName, setUserName] = useState("Shams");
  const [count, setCount] = useState(0);
  
  const increment = () => setCount((count) => count + 1);
  
  return (
    <>
      <ChildrenComponent userName={userName} />
      <button onClick={increment}> Increment </button>
    </>
  );
};

const ChildrenComponent =({ userName }) => {
  return <div> {userName} </div>;
};
```
Although the child component should render only once because the value of count has nothing to do with the ChildComponent . But, it renders each time you click on the button.

✔️ Do:
```jsx	
import React ,{useState} from "react";

const ChildrenComponent = React.memo(({userName}) => {
    return <div> {userName}</div>
})
```
Now, no matter how many times you click on the button, it will render only when necessary.

### 11. Put CSS in JavaScript
Avoid raw JavaScript when writing React applications because organizing CSS is far harder than organizing JS.

❌ Don't
```jsx 
// CSS FILE
.body {
  height: 10px;
}

//JSX
return <div className='body'> </div>
```
	
✔️ Do:
```jsx	
const bodyStyle = {
  height: "10px"
}

return <div style={bodyStyle}></div>
```

### 12. String Props Don’t Need Curly Braces
When passing string props to a children component.

❌ Don't
```jsx 
return <UserProfile name={"Shams"} />
```
	
✔️ Do:
```jsx	
return  <UserProfile name="Shams" />  
```

### 13.  Import in Order
Always try to import things in a certain order. It improves code readability.

❌ Don't
```jsx
import React from 'react';
import ErrorImg from '../../assets/images/error.png';
import styled from 'styled-components/native';
import colors from '../../styles/colors';
import { PropTypes } from 'prop-types';
```
The rule of thumb is to keep the import order like this:
 - Built-in
 - External
 - Internal

✔️ Do:
```jsx	
import React from 'react';

import { PropTypes } from 'prop-types';
import styled from 'styled-components/native';

import ErrorImg from '../../assets/images/error.png';
import colors from '../../styles/colors';
```
### 14. Write DRY Code

Try to avoid duplicate code and create a common component to perform the repetitive task to maintain the DRY (Don’t Repeat Yourself) code structure.
For instance: When you need to show multiple buttons on a screen then you can create a common button component and use it rather than writing markup for each button.

### 15. Use snippet extensions

In Visual Studio Code, for example, there are certain extensions available that increase your productivity a lot. One type of these extensions are snippet extensions. Here are some recommendations:

![image](https://user-images.githubusercontent.com/63429054/205458209-d5d1f1dc-c9cc-49ee-a4d1-12bb115b5f85.png)

![image](https://user-images.githubusercontent.com/63429054/205458218-24c3b9a3-13dc-40e8-8717-91543882fbed.png)

<img src="https://user-images.githubusercontent.com/63429054/205458222-fee6f2f5-dea1-429f-a0af-c4a67ab247ef.png" width="960"/>

## Additional Resources
- [Official Documentation](https://reactjs.org/docs/getting-started.html)
- [The Beginner's Guide to React](https://egghead.io/courses/the-beginner-s-guide-to-react)
- [patterns.dev](https://www.patterns.dev/)
- [Tao Of React](https://alexkondov.com/tao-of-react/)
- [React Patterns](https://reactpatterns.com/)
 
