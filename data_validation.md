## create the collection with the validator

db.createCollection("messages", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         // the required fields, no message without any of these fields
         required: [ "text", "user", "likes"],
         properties: {
            text: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            user: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            likes: {
               bsonType: "int",
               minimum: 0,
               description: "must be an integer greater or equal to 0 and is required"
            },
            //Array definition
            comments: {
                bsonType: ["array"],
                items: {
                    bsonType: ["object"],
                    //Comments are not mandatory but if there is a comment it needs these two fields
                    required: ["comment", "user"],
                    additionalProperties: false,
                    description: "'items' must contain the stated fields.",
                    properties: {
                        comment: {
                            bsonType: "string",
                            description: "must be a string and is required"
                        },
                        user: {
                            bsonType: "string",
                            description: "must be a string and is required"
                        }
                    }
                }
            }
         }
      }
   }
})