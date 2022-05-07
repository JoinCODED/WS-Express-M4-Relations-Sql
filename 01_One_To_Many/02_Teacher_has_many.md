1. Now let's create the relationship between our two models, `Teacher` and `Course`. Let's think about it, every `Teacher` can have many `courses`, but every `course` can have one `teacher` only. So, it's a one-to-many relationship.

2. We will define our relationships in `models/index.js` at the bottom, right before exporting db. Let's translate the following phrase to code "A teacher has many courses". Every model has a method called hasMany that creates a link between the two models.

```js
db.sequelize = sequelize;
db.Sequelize = Sequelize;

// Relations
db.Teacher.hasMany(db.Course);

module.exports = db;
```

3. Since we made change to our database, let's drop it and create a new one. In `app.js`, force `db.sync`:

```js
db.sequelize.sync({ force: true });
```

4. Then let's add some `courses`, note that a field called `TeacherId` was added! Let's try this in Postman. Fetch all `courses`. The field `TeacherId` is there, but it's set to null.
