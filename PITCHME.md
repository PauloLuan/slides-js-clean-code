# JS Clean Code 

Good practices for modern Javascript Applications

---

### Flux Design

- Best Practices: Improving your code quality

---

### 

NO
```javascript
// DON'T
let d
let elapsed
const ages = arr.map((i) => i.age)
```

YES
```javascript
// DO
let daysSinceModification
const agesOfUsers = users.map((user) => user.age)
```
