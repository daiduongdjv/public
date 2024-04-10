> assign
```javascript
function assign(targetObj, ...sourceObjects) {
  return sourceObjects.reduce((finalObj, currentObj) => {
    return { ...finalObj, ...currentObj }
  }, targetObj);
}

const duck = {
  hasBill: true,
  feet: 'orange'
};

const beaver = {
  hasTail: true
};

const otter = {
  hasFur: true,
  feet: 'webbed'
};

const result = assign({}, duck, beaver, otter);

console.log(result);
```


> cloneDeep
```javascript
function cloneDeep(originalObj) {
  if (typeof originalObj !== "object") {
    return originalObj;
  }
  if (Array.isArray(originalObj)) {
    return originalObj.map((item) => cloneDeep(item));
  }
  let copy = {};
  for (let [key, value] of Object.entries(originalObj)) {
    copy = { ...copy, [key]: cloneDeep(value) }
  }
  return copy;
}

const movie = {
  name: 'F&F9',
  cast: [
    {
      id: 1,
      name: 'Vin Diesel'
    }
  ],
  ratings: {
    count: 4.5,
    reactors: [
      {
        userId: '12309',
        name: 'Taran'
      }
    ]
  }
}

const deepCopyOfMovie = cloneDeep(movie);

console.log(deepCopyOfMovie === movie);

deepCopyOfMovie.ratings.count = 4.3;

console.log(JSON.stringify(movie));

console.log(JSON.stringify(deepCopyOfMovie));
```

>curry
```javascript
function curry(func) {
  return function recursiveCurry(...args) {
    if (args.length >= func.length) {
      return func.apply(this, args);
    }
    return recursiveCurry.bind(this, ...args)
  }
}

function getMultiplication(a, b, c, d) {
  return a * b * c * d;
}

const curriedMul = curry(getMultiplication);

console.log(curriedMul(2)(3)(4, 1));

console.log(curriedMul(2)(3)(4)(1));
```

> debounce
```javascript
function debounce(func, delay) {
  let timer = "";
  return function() {
    const context = this;
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(context, arguments), delay);
  }
}

const printText = function() {
  console.log(`Hello, I'm ${this.name}`)
}

const debouncedFunc = debounce(printText, 4000);

debouncedFunc();  // this is undefined

const myself = {
  name: 'Jaynil',
  intro: debounce(printText, 3000)
};

myself.intro();  // this is myself object
```

> once
```javascript
function callMeOnce(fn) {
  const context = this;
  let called = false;
  return function (...args) {
    if (called) {
      return;
    }
    called = true;
    return fn.apply(context, args);
  };
}

const printText = () => console.log("Called!");

const once = callMeOnce(printText);

once();
once();
once();
once();
```

> throttle
```javascript
function throttle(func, delay) {
  let flag = true;
  return function() {
    let context = this, args = arguments;
    if (flag) {
      flag = false;
      func.apply(context, args);
      setTimeout(() => flag = true, delay);
    }
  }
}

const printText = function() {
  console.log(`Hi, I'm ${this.name || 'logger'}`);
}

const throttled = throttle(printText, 2000);

console.log("Test One");
throttled();
throttled();
throttled();
throttled();
setTimeout(throttled, 2000);

const myself = {
  name: 'Jaynil',
  intro: throttle(printText, 2000)
};

console.log("Test Two");
setTimeout(() => myself.intro(), 2000);
```

> sum
```javascript
var sum = function(arr) {    
    var sum = 0;    
    for (i = 0; i < arr.length; i++) {        
        sum += arr[i];           
    }    
console.log(sum);
}
```

> clamp
```javascript
//Lodash Number 
var clamp = function(number,lower,upper) {    
    if (number >= lower && number <= upper) {
        console.log(number);
    }
    else if (number < lower) {
        number = lower;
        console.log(number);
    }
    else if (number > upper) {
        number = upper;
        console.log(upper);
    }
}
```
