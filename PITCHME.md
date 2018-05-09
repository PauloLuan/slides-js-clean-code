---?image=assets/images/css.jpg&opacity=20
@title[Code Talking]

### Clean 
## @css[shoutout](Code)
#### Good Practices for modern @fa[desktop-alt] JS Applications

---

## @color[#e49436](Clean)Code
#### Good @color[#e49436](Practices) for modern @fa[desktop-alt] JS Applications

---

### JS Clean Code

- Best Practices: Improving your code quality

---?image=assets/images/wtf.jpg&size=55% 55%
@title[WTF's / minute]

---
##### How should I name my variables?
#### @color[#e43d36](DON'T)
```javascript

let d
let elapsed
const ages = arr.map((i) => i.age)
```

#### @color[#00ff00](DO)
```javascript
// DO
let daysSinceModification
const agesOfUsers = users.map((user) => user.age)
```


---

##### How should I name my variables?
#### @color[#e43d36](DON'T)
```javascript
let fName, lName
let cntr

let full = false
if (cart.size > 100) {
  full = true
}
```

#### @color[#00ff00](DO)
```javascript
// DO
let firstName, lastName
let counter

const MAX_CART_SIZE = 100
// ...
const isFull = cart.size > MAX_CART_SIZE
```
---

##### How should I write my functions?
#### @color[#e43d36](DON'T)
```javascript

```

#### @color[#00ff00](DO)
```javascript

```


