1. To enroll a `student` in a `course`, we need to create a new route in `courses` routes:

```js
router.post('/:courseId/:studentId', courseEnroll);
```

We need the `course` id and the `student` id as params.

2. Let's create the `courseEnroll` function in our `courses` controller:

```js
exports.courseEnroll = async (req, res, next) => {
  try {
    const { studentId } = req.params;
    res.status(204).end();
  } catch (error) {
    next(error);
  }
};
```

3. OK, so we have the data we need, now we need to insert this `student` into the `course`. When creating a many to many relationship sequelize creates `get`, `set` and `add` methods to each model.

So by creating this relation, we have `getStudent`, `addStudent` and `setStudent`.

4. Let's use the `addStudent` method to add the 'student':

```js
exports.courseEnroll = async (req, res, next) => {
  try {
    const { studentId } = req.params;
    await req.course.addStudent(studentId);
    res.status(204).end();
  } catch (error) {
    next(error);
  }
};
```

5. Check your database, it works!
