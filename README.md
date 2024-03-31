# QUESTIONS TO ANSWER
- How many users are active/not active?

```
TODO...

```

- What is the average age of all users?
``` 
[
    {
        $group: {
        _id: null,
        averageAge: {
                $avg: "$age"
            }
        }
    }
]
```
- Liist the top 2 most common favourite fruits among the users

```
[
  {
    $group: {
      _id: "$favoriteFruit",
      count: {
        $sum: 1
      }
    },
  },
  {
    $sort: {
      count: -1
    }
  },
  {
    $limit: 2
  }
]

```
- find the total number of males and females

```

[
  {
    $group: {
      _id: "$gender",
      count: {
        $sum: 1
      }
    }
  }
]

```

- Which country has the highest number of registered user

```

[
  {
    $group: {
      _id: "$company.location.country",
      totalUsers: {
        $sum: 1
      }
    }
  },
  {
    $sort: {
      totalUsers: -1
    }
  },
  {
    $limit: 1
  }
]

```

- List all the unique eye colors present in the collection

```

[
  {
    $group: {
      _id: "$eyeColor",
    },
  },
]

```


- What is the average number of tags per user

```

[
  {
    $unwind: {
      path: "$tags"
    }
  },
  {
    $group: {
      _id: "$_id",
      numberOfTags: {
        $sum: 1
      }
    }
  },
  {
    $group: {
      _id: null,
      averageNumberOfTags: {
        $avg: "$numberOfTags"
      }
    }
  }
]

```

```
Another Solution:

[
  {
    $addFields: {
      numberOfTags: {
        $size: {
          $ifNull: ["$tags", []]
        }
      }
    }
  },
  {
    $group: {
      _id: null,
      averageNumberOfTags: {$avg: "$numberOfTags"}
    }
  }
]

```


- How many users have specific tag like "enim"

```

[
  {
    $match: {
      tags: "enim"
    }
  },
  {
    $count: 'userWithEnimTag'
  }
]

```

- What are the names and age of users who are inactive and have 'velit' as a tag

```
[
  {
    $match: {
      // isActive: false, tags: "velit"
      $and: [
        {
          isActive: false,
        },
        {
          tags: "velit",
        }
      ],
    },
  },
  {
    $project: {
      name: 1,
      age: 1,
    },
  }
]
```


- How many user have phone number starting with '+1(940)'

```
[
  {
    $match: {
    	"company.phone": /^\+1 \(940\)/
    }
  },
  {
    $count: 'count'
  }
]
```
- Who has registered most recently

```
[
  {
    $sort: {
      registered: -1
    }
  },
  {
    $limit: 2
  },
  {
    $project: {
      name: 1,
      registered: 1,
      
    }
  }
]
```
- Catagorize users by their favourite fruit

```
[
  {
    $group: {
      _id: "$favoriteFruit",
      users: {
        $push: "$name",
      },
    },
  },
  {
    $addFields: {
      userCount: {
        $size: "$users",
      },
    },
  },
]
```


- How many users have 'ad' as the second tag in their list of tags

```
[
  {
    $match: {
      "tags.1": "ad",
    },
  },
  {
    $group: {
      _id: null,
      users: {$push: "$name"}
    }
  },
  {
    $addFields: {
      howMany: {$size: "$users"}
    }
  }
]
```
- Find users who have bot 'enim' and 'id' as their tags

```
[
  {
    $match: {
      tags: {
        $all: ["enim", "id"],
      },
    },
  }
]
```
- List all the companies in the USA with their corresponding user account
```
[
  {
    $match: {
      "company.location.country": "USA",
    },
  },
  {
    $group: {
      _id: "$company.title",
      // _id: null,
      users: {$push: "$name"}
      // userCount: {$sum: 1}
    }
  }
]
```

- 

```

```