---
layout: post
comments: true
title: Common Redux Mistakes
---

I wanted to document a few of the mistakes I have seen, and likely committed myself, that you can avoid in order to keep your Redux implementation clean. Most of these will likely also translate to another state management framework as well.

## Don’t put state into Redux unnecessarily

### Problem

There is a complexity cost to elevating state to Redux. Don’t take on the cost unless it is necessary.

### Solution

Use local state when possible. Avoid the urge to put state in Redux because you think you’ll need it in another component later. It is easy enough to promote local state to Redux once needed. Local state and Redux can coexist.

## Don’t put calculated or modified data into the Redux store

### Problem

If you call an api and then manipulate the response data before storing it in redux (most likely in your reducer) it could cause issues later down the line. You may later find that you also need a slightly different version of the data. If you then store a different version of the modified data, you will most likely run into issues keeping those 2 different values in sync.

### Solution

Store your raw source data in the Redux store and use selectors to perform any modifications. This ensures that any and all modifications of the data are kept in sync any time the source data is updated in the Redux store. It also leads to smaller, simpler reducers.

## Don’t comingle entity data and presentation state

### Problem

If a single node in your redux store holds both entity data and presentation state things can get overcomplicated. When I refer to entity data I am referring to data usually retrieved from an api. When I refer to presentation state, I am referring to the state of UI controls. For example, isLoading is a common piece of presentation state.

### Solution

Store entity data and presentation state in separate nodes in your redux store. For example, I’ve seen this separation at the very top level, where there are 2 nodes, entities and presentation state and then everything is under one of those two nodes.

## Avoid heavy frameworks on top of redux

### Problem

I’ve seen multiple heavy handed frameworks built on top of redux. Usually, in an effort to reduce syntactical duplication (or typing). In most cases, I have found that these obscure the simplicity of Redux and make the code harder to read.

## Solution

Avoid the large frameworks built on top of Redux. Especially, if you are new to redux and are just starting a new project. Feel free to use smaller libraries like Reselect where applicable.
