## Create a model:

```js
const Developer = mongoose.model('Developer', {
    name: String,
    skills: [String]
});
```

The Developer model defined above means that we can make documents in the Developer collection that will each have two properties:

name, which will be a string

skills, which will be an array of strings

----

## Create an instance of that model:

```js
    let newDev = new Developer({
        name:"Alex",
        skills:["HTML", "CSS", "JavaScript"]
    });
    
    await newDev.save().then(() => {
        console.log("Save successful!");
    }).catch(error => {
        console.log("Some error occurred saving data!:\n" + error)
    });
```

**This doesn't open or close the database itself, just a representation of this single instance creation.**

----

Full code would look like:

```js
const mongoose = require('mongoose');

async function dbConnect(){
    try {
        await mongoose.connect('mongodb://localhost:27017/CoderIsAwesome');
        console.log("Database connected!");
    } catch (error) {
        console.log(`dbConnect failed! Error:\n${JSON.stringify(error)}`);
    }
}

async function dbClose(){
    await mongoose.connection.close();
    console.log("Database disconnected!");
}

const Developer = mongoose.model('Developer', {
    name: String,
    skills: [String]
});

async function someAppFunction(){
    await dbConnect();

    let newDev = new Developer({
        name:"Alex",
        skills:["HTML", "CSS", "JavaScript"]
    });
    
    await newDev.save().then(() => {
        console.log("Save successful!");
    }).catch(error => {
        console.log("Some error occurred saving data!:\n" + error)
    });
    
    console.log("Closing the DB now so the app doesn't hang open for ages...");
    await dbClose();
}

someAppFunction();
```