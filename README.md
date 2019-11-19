## User Story

- the first person who registers with the username 'admin' will have the admin rights
- every other user will be a student

1. user will be brought to the homepage
2. user will register if they do not have an account next
3. user will to select their courses -- a minimum of 3
4. if user has an account they will be brought to the landing page

   # If user is admin

   1. admin will see the 5 pre filled courses that are concurrent with the jedi academny
   2. admin will be able to add, update, and delete courses
   3. admin will be able to see all the students that are in the jedi academny
   4. admin will be able to log out

   # If user is student

   1. user will be brought to the landing page
   2. user will be able to see the courses that they are in
   3. user will be able to click on a course and see the other students that are in the course with them
      - user will not be able to see all the other students that are in the school with them UNLESS they are in the same course
   4. user (student) will be able to log out

## ROUTES

1. register (@users) route -> /register --> POST
2. login (@users) route -> /login --> GET

## MODELS

```
class Student(UserMixin, Model):
    student_id = PrimaryKey
    full_name = CharField(unique = True)
    email = CharField(unique=True)
    password = CharField()

    class Meta:
        database = DATABASE
```

```
class Course(Model):
    course_id = PrimaryKey
    title = CharField()
    description = CharField()
    start_date = DateTimeField(default=datetime.datetime.now)
    end_date = DateTimeField(default=datetime.datetime.now)
    class Meta:
        database = DATABASE
```

```
class Enrollments(Model):
    course_id = ForeignKeyField(Enrollments, backref='courses')
    student_id = ForeignKeyField(Enrollments, backref='students')

    class Meta:
        database = DATABASE
```

```
def initialize():
    DATABASE.connect()
    DATABASE.create_tables([User, Course], safe=True)
    print("Created tables if they weren't already there")
    DATABASE.close()
```

## Stretch goals

- user (student) will be able to create their own lightsaber and battle others whom have the same one
