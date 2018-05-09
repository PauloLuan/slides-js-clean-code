---?image=assets/images/css.jpg&opacity=20
@title[Code Talking]

### Clean 
## @css[shoutout](Code)
#### Good Practices for modern @fa[magic] @css[gold](JS) Applications
#### by @pauloluan

---
@title[WTF per minute]

#### Code review measure

@div
![](assets/images/wtf.jpg)
@divend

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

@size[0.5em](@color[gray](How should I write my functions?))
#### @css[gold]("Functions should do one thing. They should do it well. They should do it only.") 
— Robert C. Martin (Uncle Bob)

---
##### How should I write my functions?
#### @color[#e43d36](DON'T)
```javascript
// DON'T
async function getUserRouteHandler (req, res) {
  const { userId } = req.params
  // inline SQL query
  let user = await find('user')
    .where({ id: userId })
    .first()
  res.json(user)
}
```
---

#### @color[#00ff00](DO)
```javascript
// DO
// User model (eg. models/user.js)
const tableName = 'user'
const User = {
  getOne (userId) {
    return find(tableName)
      .where({ id: userId })
      .first()
  }
}

// route handler (eg. server/routes/user/get.js)
async function getUserRouteHandler (req, res) {
  const { userId } = req.params
  let user = await User.getOne(userId)
  res.json(user)
}
```

---

##### Use long, descriptive names
#### @color[#e43d36](DON'T)
```javascript
/**
 * Invite a new user with its email address
 * @param {String} user email address
 */
function inv (user) { /* implementation */ }
```

#### @color[#00ff00](DO)
```javascript
function inviteUser (emailAddress) { /* implementation */ }
```
---

##### Avoid long argument list
#### @color[#e43d36](DON'T)
```javascript
function getRegisteredUsers (fields, include, fromDate, toDate) { /* implementation */ }
getRegisteredUsers(['firstName', 'lastName', 'email'], ['invitedUsers'], '2016-09-26', '2016-12-13')
```

#### @color[#00ff00](DO)
```javascript
function getRegisteredUsers ({ fields, include, fromDate, toDate }) { /* implementation */ }
getRegisteredUsers({
  fields: ['firstName', 'lastName', 'email'],
  include: ['invitedUsers'],
  fromDate: '2016-09-26',
  toDate: '2016-12-13'
})
```
---

##### Avoid else's
#### @color[#e43d36](DON'T)
```javascript
if(v){
   let x = v;
} else {
   let x =10;
}
```

#### @color[#00ff00](DO)
```javascript
let x = v || 10;
```
---

##### Reduce side effects 
#### @color[#e43d36](DON'T)
```javascript
function addItemToCart (cart, item, quantity = 1) {
  const alreadyInCart = cart.get(item.id) || 0
  cart.set(item.id, alreadyInCart + quantity)
  return cart
}
```

#### @color[#00ff00](DO)
```javascript
// not modifying the original cart
function addItemToCart (cart, item, quantity = 1) {
  const cartCopy = new Map(cart)
  const alreadyInCart = cartCopy.get(item.id) || 0
  cartCopy.set(item.id, alreadyInCart + quantity)
  return cartCopy
}
```
---

##### Organize your functions in a file according to the stepdown rule 
#### @color[#e43d36](DON'T)
```javascript
// "I need the full name for something..."
function getFullName (user) {
  return `${user.firstName} ${user.lastName}`
}

function renderEmailTemplate (user) {
  // "oh, here"
  const fullName = getFullName(user)
  return `Dear ${fullName}, ...`
}
```

---
##### Organize your functions in a file according to the stepdown rule 
#### @color[#00ff00](DO)
```javascript
function renderEmailTemplate (user) {
  // "I need the full name of the user"
  const fullName = getFullName(user)
  return `Dear ${fullName}, ...`
}

// "I use this for the email template rendering"
function getFullName (user) {
  return `${user.firstName} ${user.lastName}`
}
```
---

##### How to write nice async code? 
#### @color[#e43d36](DON'T)
```javascript
// AVOID
asyncFunc1((err, result1) => {
  asyncFunc2(result1, (err, result2) => {
    asyncFunc3(result2, (err, result3) => {
      console.lor(result3)
    })
  })
})
```
---

#### @color[#e43d36](DON'T)
```javascript
// AVOID 2
asyncFuncPromise1()
  .then(asyncFuncPromise2)
  .then(asyncFuncPromise3)
  .then((result) => console.log(result))
  .catch((err) => console.error(err))
```
---

#### @color[#00ff00](DO)
```javascript
// NICEEEEE
try {
    let result1 = await asyncFuncPromise1()
    let result2 = await asyncFuncPromise2(result1)
    let result3 = await asyncFuncPromise3(result2)
    let result = console.log(result)
} catch (error) {
    console.error(error)
}
```

---
##### How to write nice async code? Real Example! 
#### @color[#e43d36](DON'T)
```javascript
// AVOID
function handler (done) {
  validateParams((err) => {
    if (err) return done(err)
    dbQuery((err, dbResults) => {
      if (err) return done(err)
      serviceCall((err, serviceResults) => {
        done(err, { dbResults, serviceResults })
      })
    })
  })
}
```
---

#### @color[#e43d36](DON'T)
```javascript
// AVOID 2
function handler () {
  return validateParams()
    .then(dbQuery)
    .then(serviceCall)
    .then((result) => {
      console.log(result)
      return result
    })
}
```
---

#### @color[#00ff00](DO)
```javascript
// NICEEEEE
async function handler () {
  await validateParams()
  const dbResults = await dbQuery()
  const serviceResults = await serviceCall()
  return { dbResults, serviceResults }
)
```

---?image=assets/images/css.jpg&opacity=20
@title[Clean Code]

#### @size[0.5em](@color[gray](click to view the reference article that this slides were inspired of))
### [Rising Stack Article](https://blog.risingstack.com/javascript-clean-coding-best-practices-node-js-at-scale/)

---?image=assets/images/css.jpg&opacity=20
@title[Follow me]

#### @size[0.5em](@color[gray](Follow me at @))
#### Github.com/@css[gold](pauloluan)

#### @size[0.5em](@color[gray](Linkedin))
#### linkedin.com/in/@css[gold](pauloluan)
