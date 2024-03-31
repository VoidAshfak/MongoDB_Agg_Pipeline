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


- 

```



```


- 

```



```


- 

```



```


- 

```



```


- 

```



```


- 

```



```


- 

```



```
