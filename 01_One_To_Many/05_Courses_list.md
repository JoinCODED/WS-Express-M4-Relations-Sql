We'll fix our `courses` list to return all `courses`, but to also add the `teacher`'s name to display it in the `courses` list.

1. Now let's include the `teacher` details in the `courses` list! In `courses` Controller:

```js
Course.findAll({
  attributes: { exclude: ['createdAt', 'updatedAt'] },
  include: {
    model: Teacher,
  },
});
```

2. Oops. We got an error saying that `Course` has no relationship with `Teacher`. So `hasMany` is a one-sided relationship! We need to create a relationship from `Course`'s side.

3. In `models/index` we will use `belongsTo` which completes the `one-to-many` relationship. It indicates that every `course` has one `teacher`.

```js
db.Course.belongsTo(db.Teacher);
```

4. Let's try fetching our list of `courses` again. It works! But let's cleanup a bit starting with excluding `teacherId`. In `course` Controller:

```js
Course.findAll({
  attributes: { exclude: ['teacherId', 'createdAt', 'updatedAt'] },
  include: {
    model: Teacher,
  },
});
```

5. Also let's give `Teacher` an alias and set the foreign key again. In `models.index`:

```js
db.Course.belongsTo(db.Teacher, {
  as: 'teacher',
  foreignKey: 'teacherId',
});
```

6. And in `course` Controller:

```js
Course.findAll({
  attributes: { exclude: ['teacherId', 'createdAt', 'updatedAt'] },
  include: {
    model: Teacher,
    as: 'teacher',
  },
});
```

7. The only field we'll send is the `teacher`'s name:

```js
Course.findAll({
  attributes: { exclude: ['teacherId', 'createdAt', 'updatedAt'] },
  include: {
    model: Teacher,
    as: 'teacher',
    attributes: ['name'],
  },
});
```
