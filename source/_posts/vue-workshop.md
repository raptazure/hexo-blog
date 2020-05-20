---
title: Vue Workshop
date: 2020-05-18 22:40:22
categories: 编程
tags: ["JavaScript", "Vue.js"]
---

<img src="vue-workshop/vue.jpeg" width="950px">

&nbsp; &nbsp; &nbsp; 最近在看尤大的 `Vue Workshop: Advanced Features from the Ground Up`，为了便于总结与复习，把对应的笔记放在这里～

<!--more-->

# Reactivity

### 1.1 Getters and Setters

- 实现一个 `convert` 函数，其参数为一个对象， 使用 [Object.defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 将对象的属性原位转换为 `getter/setters`，转换过的对象应该保持原有行为，但同时输出所有 `get/set` 操作，如：
  ```js
  const obj = { foo: 123 }
  convert(obj)

  obj.foo // should log: 'getting key "foo": 123'
  obj.foo = 234 // should log: 'setting key "foo" to 234'
  obj.foo // should log: 'getting key "foo": 234'
  ```
- 可能的实现：
  ```js
  function convert (obj) {
    // get a list of existing properties and iterate
    Object.keys(obj).forEach(key => {
      // remember to assign it to the initial value of that original property
      let internalValue = obj[key]
      // store internalValue in this closure
      Object.defineProperty(obj, key, {
        get () {
          console.log(`getting key "${key}": ${internalValue}`)
          // retain the original access behavior
          return internalValue
        },
        set (newValue) {
          console.log(`setting key "${key}" to: ${newValue}`)
          internalValue = newValue
        }
      })
    }) 
  }
  ```

### 1.2 Dependency Tracking

- 创建一个 `Dep` 类，包含方法 `depend` 和 `notify`，创建一个 `autorun` 函数，传入一个 updater 函数，在 updater 函数里，可通过调用 `dep.depend()` 显式依赖于一个 `Dep` 的实例，随后，可通过调用 `dep.notify()` 来再次运行 updater 函数，如：
  ```js
  const dep = new Dep()

  autorun(() => {
    dep.depend()
    console.log('updated')
  })
  // should log: "updated"

  dep.notify()
  // should log: "updated"
  ```
- 可能的实现：
  ```js
  // a class representing a dependency
  class Dep {
    constructor () {
      this.subscribers = new Set()
    }

    depend () {
      if (activeUpdate) {
        // register the current active update as a subscriber
        this.subscribers.add(activeUpdate)
      }
    }

    notify () {
      // run all subscriber functions
      this.subscribers.forEach(sub => sub())
    }
  }

  let activeUpdate

  function autorun (update) {
    function wrappedUpdate () {
      activeUpdate = wrappedUpdate
      update()
      activeUpdate = null
    }
    wrapperUpdate()
  }
  ```