We will work on this courses api.

Fork and clone [this](https://github.com/JoinCODED/Demo-Express-M4-Sql-Courses) into your development folder.

1. Let's add some fields to our `Teacher` model that represents the `Courses` that's taught by this `Teacher`.

```js
const TeacherModel = (sequelize, DataTypes) => {
  const Teacher = sequelize.define('Teacher', {
    name: {
      type: DataTypes.STRING,
    },
    courseName: {
      type: DataTypes.STRING,
    },
  });
  return Teacher;
};

module.exports = TeacherModel;
```

2. Does this make sense? To add those fields to the `Teacher` model? A `teacher` can have 100 different `courses`, does that mean that those fields will be repeated in all 100 rows?! Nonsense! What we need to do is link the `Teacher` model to the `Course` model.
