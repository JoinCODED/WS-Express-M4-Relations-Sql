We will do the same in our `students` controller:

```js
exports.studentsGet = async (req, res) => {
  try {
    const students = await Student.findAll({
      include: [
        {
          model: Course,
          as: 'courses',
          through: { attributes: [] },
        },
      ],
    });
    res.json(students);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};
```
