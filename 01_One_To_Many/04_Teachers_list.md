1. Let's fetch the list of `teachers` in Postman. Okay, nothing special about it. But what if we can add to every `teacher` the list of its `courses`!

2. To do that we will pass property called include and pass it your model:

```js
Teacher.findAll({
  attributes: ['id', 'name'],
  include: {
    model: Course,
  },
});
```

3. But does it make sense to have the `teacher` ID in this response when it's already there with the `teacher` fields? Nope. The only fields we want are the `id` and `name`. We can easily add an attribute in our controller method:

```js
Teacher.findAll({
  attributes: ['id', 'name'],
  include: {
    model: Course,
    attributes: ['id', 'name'],
  },
});
```

4. One more thing. The `Courses` field name is so disturbing. Let's change it to `courses` for consistency with the other fields. To do that we need to create an `alias` for our model. In `models/index`, we will pass an object to `hasMany` with the key as and the value is your alias.

```js
db.Teacher.hasMany(db.Course, {
  foreignKey: 'teacherId',
  as: 'courses',
  allowNull: false,
});
```

5. We need to pass the alias to `findAll` as well.

```js
Teacher.findAll({
  attributes: ['id', 'name'],
  include: {
    model: Course,
    as: 'courses',
    attributes: ['id', 'name'],
  },
});
```

6. Test again. Yaas all is working properly!!
