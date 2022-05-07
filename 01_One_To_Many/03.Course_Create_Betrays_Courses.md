Hmmmmm, so now whenever we create a new `course` we need to add the `Teacher` ID. The easiest way to do that is to pass the `teacher` ID in the request body. But that's not the correct convention, we agreed before that IDs are passed in the request's URL.

1. So we will change our `createCourse` route to `/teachers/:teacherId/courses`. Since it starts with `teachers`, we will move the `createCourse` route and controller to the `teacher`'s routes and controllers files.

2. Since `createCourse` has `teacherId` as a route param, we will save it in `req.body` before passing it to `Teacher.create`.

```js
try {
    [...]
    req.body.teacherId = req.teacher.id;
    const newCourse = await Course.create(req.body);
    [...]
  }
```

3. Let's try creating another course.

4. That Worked!. But look at the inconsistency between the naming convention of all fields and `TeacherId`. So yucky! We can fix that in `models/index` by passing an object to `hasMany` with the key `foreignKey` and the value is the new name:

```js
db.Teacher.hasMany(db.Course, {
  foreignKey: 'teacherId',
});
```

5. Let's make it mandatory that every `course` must have a `teacher` ID. In `models/index`, inside the `foreignKey` object, set `allowNull` to `false`.

```js
db.Teacher.hasMany(db.Course, {
  foreignKey: 'teacherId',
  allowNull: false,
});
```
