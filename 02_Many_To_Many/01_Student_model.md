We have'nt touched the `student` model, because we will apply another type of relationship to it.

A `student` can enroll in many `courses`, and a `course` can have many `student`s, hence the name, `many to many` relation.

1. To create this relation, in `models/index.js` using the `belongsToMany` method:

```js
db.Student.belongsToMany(db.Course);
db.Course.belongsToMany(db.Student);
```

2. There's an extra step here, Sequelize needs to create a **Junction** table which will store those relations, you can name it `student_course` or anything you like, in this case, it makes sense to name it `enrollments`.

3. Pass an object to the `belongsToMany` method:

```js
db.Student.belongsToMany(db.Course, { through: 'Enrollments' });
db.Course.belongsToMany(db.Student, { through: 'Enrollments' });
```

4. Let's also define our `alias` and `foreignKey`:

```js
db.Student.belongsToMany(db.Course, {
  through: 'Enrollments',
  as: 'courses',
  foreignKey: 'studentId',
});
db.Course.belongsToMany(db.Student, {
  through: 'Enrollments',
  as: 'students',
  foreignKey: 'courseId',
});
```
