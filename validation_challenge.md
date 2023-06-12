An events website needs a database to handle all the events they publish. Those are the required task by them:

Create the my_events database in MongoDB

The events collection is required. From each event the database would like to know their name, summary, organiser, date and address. First four fields are required, the address is not required (online events exist as well) but if it's included make sure that all the addresses have the same structure. From each organiser the database would like to know their full name, email and years of experience. There is no interest on the website to get more information about organisers, or getting lists of organisers either.


```js
db.createCollection("events", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         required: [ "name", "summary", "organiser", "date"],
         properties: {
            name: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            summary: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            organiser: {
               bsonType: "object",
               required: [ "name","email", "years" ],
               properties: {
                  name: {
                    bsonType: "string",
                    description: "must be a string if the field exists"
                  },
                  email: {
                     bsonType: "string",
                     description: "must be a string and is required"
                  },
                  years: {
                    bsonType: "int",
                    minimum: 0,
                    description: "must be an integer greater or equal to 0 and is required"
                  }
               }
            },
            date: {
               bsonType: "date",
               description: "must be a date and is required"
            },
            address: {
               bsonType: "object",
               required: [ "street","city", "state" ],
               properties: {
                  street: {
                     bsonType: "string",
                     description: "must be a string if the field exists"
                  },
                  city: {
                     bsonType: "string",
                     description: "must be a string and is required"
                  },
                  state: {
                     bsonType: "string",
                     description: "must be a string and is required"
                  }
               }
            }
         }
      }
   }
})
```