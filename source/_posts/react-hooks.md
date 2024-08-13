---
title: 1个组件使用10 react hooks
date: 2022-01-11 09:33:17
updated: 2022-01-11 09:33:17
tags: react
categories:
---

尝试使用1个组件使用10个常见的hooks

### App.tsx 需要实现一个父组件

``` typescript
import { createContext, useCallback, useRef, useState } from "react"
import Count from "./Count";
import './App.css'


enum Theme {
  LIGHT = 'light',
  DARK = 'dark'
}

export const ThemeContext = createContext(Theme.LIGHT); // 创建一个context对象

const App = () => {
  const [theme, setTheme] = useState(Theme.LIGHT);
  const childRef = useRef<{changeNum: (num: string) => void}>(null);

  const handleButtonClick = useCallback(() => {
    childRef.current?.changeNum('99');
  }, []);

  return <ThemeContext.Provider value={theme}>
    <button onClick={() => setTheme(theme === Theme.LIGHT ? Theme.DARK : Theme.LIGHT)}>
      Toggle Theme
    </button>
    <Count ref={childRef} />

    <button onClick={handleButtonClick}>Change Text</button>
  </ThemeContext.Provider>
}

export default App;
```

### Count.tsx 用了10 react hooks

``` typescript
import { useState, useEffect, useLayoutEffect, useMemo, useCallback, useRef, useContext, useReducer, useDebugValue, useImperativeHandle,  forwardRef } from "react"
import { ThemeContext } from "./App";

function counterReducer(state, action) {
  switch (action.type) {
      case 'INCREMENT':
          return { count: state.count + 1 };
      case 'DECREMENT':
          return { count: state.count - 1 };
      case 'RESET':
          return { count: 0 };
      default:
          throw new Error();
  }
}
  
  
  const Count = forwardRef((props, ref) => {
    const [num, setNum] = useState(''); // 组件状态
    const input = useRef<HTMLInputElement>(null); // 获取组件实例，或者获取一个不变的钩子
    const context = useContext(ThemeContext); // 上下文爷孙及更深组件传值
    const [state, dispatch] = useReducer(counterReducer, { count: 0 }); // redux思想，修改状态需要发布action



    useEffect(() => { // 副作用，调用函数，解绑定
      console.log('init')
      return () => {
        console.log('destroy')
      }
    },[])

    const handleChange = useCallback((event: React.ChangeEvent<HTMLInputElement>) => { // 根据依赖缓存函数
      setNum(event.target.value);
    }, []);

    useLayoutEffect(() => { // useEffect的组件渲染完后版本
        input.current?.focus();
    }, [])
  
    const pow = useMemo(() => { // 缓存一个值
      const inputNum = Number(num);
      if (isNaN(inputNum)) return '';
      return inputNum ** 2;
    }, [num]);
  
    useDebugValue(pow) // 控制台打印调试信息

    useImperativeHandle(ref, () => { // 给父组件传递一个值，允许父组件调用自己
      return {
        changeNum: (nextNum: string) => { // 父组件调用
          setNum(nextNum);
        }
      }
    })

    return <>
      <div className="main" style={{backgroundColor: context === 'light' ? 'white' : 'black'}}>
        {pow}
        <input type="text" value={num} onInput={handleChange} ref={input} />

        <div>
            Count: {state.count}
            <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
            <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
            <button onClick={() => dispatch({ type: 'RESET' })}>Reset</button>
        </div>
      </div>
    </>
  });
  
  export default Count;
```