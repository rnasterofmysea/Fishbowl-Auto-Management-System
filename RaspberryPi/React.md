# Install Nodejs & React.js in Ubuntu/Debian
(https://github.com/nodesource/distributions)

## NodeJs 19.X version install

```
curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

```
sudo apt-get install build-essential
```

## Build React

### npm install react build library

```
sudo npm install -g create-react-app
```

### make a project

```
 create-react-app [project-name]
```

### Start Project

```
npm start
```

## App.js

```

import './App.css';
import axios from 'axios';
import React, {useEffect} from 'react';
import { createGlobalStyle } from 'styled-components';
import Template from './Component/Template';
import ButtonTemplate from './Component/ButtonTemplate';
import { useState
 } from 'react';
const GlobalStyle = createGlobalStyle`
  body {
    background: #e9ecef;
  }
`;

function App() {
  
  const [result, setResult] = useState("defult");
  
  function requestAPI(route){
    // e.preventDefault();
    console.log("버튼 동작 테스트");
    axios.get('http://192.168.85.136:8080/'+route)
        .then(response => {
          console.log(response)
          setResult(response.data)
        });
  }

  return (
    <>
      <GlobalStyle />
      <Template>
        <div onClick={()=>requestAPI("temperature_management")}><ButtonTemplate>수온</ButtonTemplate></div>
        <div onClick={()=>requestAPI("filtering_management")}><ButtonTemplate>탁도</ButtonTemplate> </div>
        <div onClick={()=>requestAPI("feeding_management")}><ButtonTemplate>먹이</ButtonTemplate> </div>
        </Template>
        <div>{result}</div>
    </>
  );
}

export default App;
```

## Component

## ButtonTemplate.js
```
import React from 'react';
import styled from 'styled-components';

const ButtonTemplateBlock = styled.button`
  width: 160px;
  height: 160px;

  color : black;
  font-size: 30px;
  font-weight: 800;
  position: relative; /* 추후 박스 하단에 추가 버튼을 위치시키기 위한 설정 */
  background: white;
  border-radius: 16px;
  border-style:solid;
  border-color:#20c997;
  border-width: 3px;
  box-shadow: 0 0 8px 0 rgba(0, 0, 0, 0.04);

//   margin: 0 auto; /* 페이지 중앙에 나타나도록 설정 */
  margin-top:150px;
  margin-bottom: 20x;
  margin-left: 30px;
  margin-right:20px;
  display: flex;
  flex-direction: row;

  &:active,
  &:hover,
  &:focus {
    color : white;
    background: var(--button-hover-bg-color, #20c997);
  }

  &:disabled {
    cursor: default;
    opacity: 0.5;
    background: var(--button-bg-color, #20c997);
  }
`;

function ButtonTemplate({ children }) {
  return <ButtonTemplateBlock>{children}</ButtonTemplateBlock>;
}

export default ButtonTemplate;
```

## Template.js

```
import React from 'react';
import styled from 'styled-components';

const TemplateBlock = styled.div`
  width: 640px;
  height: 480px;

  position: relative; /* 추후 박스 하단에 추가 버튼을 위치시키기 위한 설정 */
  background: white;
  border-radius: 16px;
  box-shadow: 0 0 8px 0 rgba(0, 0, 0, 0.04);

  margin: 0 auto; /* 페이지 중앙에 나타나도록 설정 */

  margin-top: 96px;
  margin-bottom: 32px;
  display: flex;
  flex-direction: row;
`;

function Template({ children }) {
  return <TemplateBlock>{children}</TemplateBlock>;
}

export default Template;
```
