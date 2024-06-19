# MongoDbQueries

## Table of Contents
1. [Query 12](#query-12)
2. [Query 13](#query-13)
3. [Query 14](#query-14)
4. [Query 15](#query-15)
5. [Query 16](#query-16)
6. [Query 17](#query-17)
7. [Query 18](#query-18)
8. [Query 20](#query-20)
9. [Query 22](#query-22)
10. [Query 23](#query-23)
11. [Query 24](#query-24)
12. [Query 25](#query-25)
13. [Query 26](#query-26)
14. [Query 27](#query-27)
15. [Query 28](#query-28)
16. [Query 29](#query-29)
17. [Query 30](#query-30)
18. [Query 31](#query-31)
19. [Query 32](#query-32)

---

### Query 12

```javascript
db.getCollection('restaurants').find({
  'cuisine': { $nin: ['American'] },
  'address.coord.1': { $lt: -65.754168 },
  'grades.score': { $gt: 70 }
});
```

**Description:**  
This query retrieves all restaurants that do not serve American cuisine, are located at a longitude less than -65.754168, and have at least one grade with a score greater than 70.

---

### Query 13

```javascript
db.getCollection('restaurants')
  .find({
    cuisine: { $nin: ['American'] },
    'grades.grade': 'A',
    borough: { $nin: ['Brooklyn'] }
  })
  .sort({ cuisine: -1 });
```

**Description:**  
This query finds restaurants that do not serve American cuisine, have received an 'A' grade, and are not located in Brooklyn. The results are sorted by cuisine in descending order.

---

### Query 14

```javascript
db.getCollection('restaurants').find(
  { name: { $regex: '^Wil' } },
  {
    restaurant_id: 1,
    borough: 1,
    name: 1,
    cuisine: 1
  }
);
```

**Description:**  
This query retrieves restaurants whose names start with "Wil". The output includes the restaurant ID, borough, name, and cuisine.

---

### Query 15

```javascript
db.getCollection('restaurants').find(
  { name: { $regex: 'ces$' } },
  {
    restaurant_id: 1,
    borough: 1,
    name: 1,
    cuisine: 1
  }
);
```

**Description:**  
This query retrieves restaurants whose names end with "ces". The output includes the restaurant ID, borough, name, and cuisine.

---

### Query 16

```javascript
db.getCollection('restaurants').find(
  { name: { $regex: 'Reg' } },
  {
    restaurant_id: 1,
    borough: 1,
    name: 1,
    cuisine: 1
  }
);
```

**Description:**  
This query retrieves restaurants whose names contain "Reg". The output includes the restaurant ID, borough, name, and cuisine.

---

### Query 17

```javascript
db.getCollection('restaurants').find({
  borough: 'Bronx',
  cuisine: { $in: ['American', 'Chinese'] }
});
```

**Description:**  
This query finds all restaurants in the Bronx that serve either American or Chinese cuisine.

---

### Query 18

```javascript
db.getCollection('restaurants').find(
  {
    borough: {
      $in: [
        'Bronx',
        'Brookyln',
        'Staten Island',
        'Queens'
      ]
    }
  },
  {
    name: 1,
    borough: 1,
    cuisine: 1,
    restaurant_id: 1
  }
);
```

**Description:**  
This query retrieves the names, boroughs, cuisines, and restaurant IDs of all restaurants located in the Bronx, Brooklyn, Staten Island, or Queens.

---

### Query 20

```javascript
db.getCollection('restaurants').find(
  { 'grades.score': { $not: { $gt: 10 } } },
  {
    cuisine: 1,
    borough: 1,
    _id: 0,
    restaurant_id: 1,
    name: 1
  }
);
```

**Description:**  
This query finds all restaurants that have no grade score greater than 10. The output includes cuisine, borough, restaurant ID, and name.

---

### Query 22

```javascript
db.getCollection('restaurants').find(
  {
    grades: {
      $elemMatch: {
        grade: 'A',
        score: 11,
        date: ISODate('2014-08-11T00:00:00.000Z')
      }
    }
  },
  { restaurant_id: 1, name: 1, grades: 1, _id: 0 }
);
```

**Description:**  
This query retrieves restaurants that have at least one grade entry with grade 'A', score 11, and date '2014-08-11'. The output includes the restaurant ID, name, and grades.

---

### Query 23

```javascript
db.getCollection('restaurants').find(
  {
    'grades.1.grade': 'A',
    'grades.1.score': 9,
    'grades.1.date': ISODate('2014-08-11T00:00:00.000Z')
  },
  { restaurant_id: 1, name: 1, grades: 1, _id: 0 }
);
```

**Description:**  
This query retrieves restaurants where the second grade entry (index 1) is an 'A' with a score of 9 and date '2014-08-11'. The output includes the restaurant ID, name, and grades.

---

### Query 24

```javascript
db.getCollection('restaurants').find(
  { 'address.coord.1': { $gte: 42, $lt: 52 } },
  {
    restaurant_id: 1,
    name: 1,
    address: 1,
    _id: 0
  }
);
```

**Description:**  
This query retrieves restaurants located at a latitude between 42 and 52. The output includes the restaurant ID, name, and address.

---

### Query 25

```javascript
db.getCollection('restaurants')
  .find({})
  .sort({ name: -1 });
```

**Description:**  
This query retrieves all restaurants and sorts them by name in descending order.

---

### Query 26

```javascript
db.getCollection('restaurants')
  .find({})
  .sort({ name: 1 });
```

**Description:**  
This query retrieves all restaurants and sorts them by name in ascending order.

---

### Query 27

```javascript
db.getCollection('restaurants')
  .find({})
  .sort({ cuisine: 1, borough: -1 });
```

**Description:**  
This query retrieves all restaurants and sorts them first by cuisine in ascending order, then by borough in descending order.

---

### Query 28

```javascript
db.getCollection('restaurants').find(
  { 'address.street': { $exists: false } },
  { address: 1 }
);
```

**Description:**  
This query finds all restaurants that do not have a street address field. The output includes the address.

---

### Query 29

```javascript
db.getCollection('restaurants').find({
  'address.coord': { $type: 'double' }
});
```

**Description:**  
This query retrieves all restaurants where the address coordinates are of type double.

---

### Query 30

```javascript
db.getCollection('restaurants').find(
  { 'grades.score': { $mod: [7, 0] } },
  { restaurant_id: 1, name: 1, 'grades.grade': 1 }
);
```

**Description:**  
This query retrieves all restaurants where the grades score is a multiple of 7. The output includes the restaurant ID, name, and grades.

---

### Query 31

```javascript
db.getCollection('restaurants').find(
  { name: { $regex: 'mon' } },
  {
    name: 1,
    borough: 1,
    'address.coord': 1,
    cuisine: 1
  }
);
```

**Description:**  
This query retrieves restaurants whose names contain "mon". The output includes the name, borough, address coordinates, and cuisine.

---

### Query 32

```javascript
db.getCollection('restaurants').find(
  { name: { $regex: '^Mad' } },
  {
    name: 1,
    borough: 1,
    'address.coord': 1,
    cuisine: 1
  }
);
```

**Description:**  
This query retrieves restaurants whose names start with "Mad". The output includes the name, borough, address coordinates, and cuisine.
