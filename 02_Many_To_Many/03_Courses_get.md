We want our `courses` list to include all `students` enrolled.

1. In `courses` controller, change the `include` attribute to an array:

```js
exports.coursesGet = async (req, res) => {
  try {
    const courses = await Course.findAll({
      attributes: { exclude: ['teacherId', 'createdAt', 'updatedAt'] },
      include: [
        {
          model: Teacher,
          as: 'teacher',
          attributes: ['name'],
        },
      ],
    });

    res.json(courses);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};
```

2. Now add the `Student` model:

```js
exports.coursesGet = async (req, res) => {
  try {
    const courses = await Course.findAll({
      attributes: { exclude: ['teacherId', 'createdAt', 'updatedAt'] },
      include: [
        {
          model: Teacher,
          as: 'teacher',
          attributes: ['name'],
        },
        {
          model: Student,
          as: 'students',
        },
      ],
    });

    res.json(courses);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};
```

3. We are getting the `enrollments` data nested in there, to get rid of it:

```js
exports.coursesGet = async (req, res) => {
  try {
    const courses = await Course.findAll({
      attributes: { exclude: ['teacherId', 'createdAt', 'updatedAt'] },
      include: [
        {
          model: Teacher,
          as: 'teacher',
          attributes: ['name'],
        },
        {
          model: Student,
          as: 'students',
          through: { attributes: [] },
        },
      ],
    });

    res.json(courses);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};
```
