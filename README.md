# DEVELOP A DJANGO-BASED CRUD APPLICATION

## AIM

To develop a Django-based web application that performs CRUD (Create, Read, Update, and Delete) operations on student records.

## ALGORITHM

1. Create a Django project and an application.
2. Define the `Student` model with the required fields (Name and Email).
3. Run migrations to create the database table.
4. Configure URL routing for Home, Add, Update, and Delete operations.
5. Create the `home()` view to retrieve and display all student records.
6. Create the `add()` view to insert a new student record into the database.
7. Create the `update()` view to modify an existing student record using its ID.
8. Create the `delete()` view to remove a student record using its ID.
9. Design the HTML page with separate forms/buttons for Add, View, Update, and Delete operations.
10. Run the Django development server and perform all CRUD operations through the web browser.

## PROGRAM
views
```.py
from django.shortcuts import render, redirect
from .models import Student


def home(request):
    res = Student.objects.all()
    return render(request, 'crud.html', {'result': res})


def create(request):
    if request.method == "POST":
        na = request.POST.get("nam")
        em = request.POST.get("emai")

        Student.objects.create(
            Name=na,
            Email=em
        )

    return redirect("home")


def update(request):
    if request.method == "POST":
        di = request.POST.get("id")

        stud = Student.objects.get(Idno=di)

        stud.Name = request.POST.get("nam")
        stud.Email = request.POST.get("emai")

        stud.save()

    return redirect("home")


def delete(request):
    if request.method == "POST":
        di = request.POST.get("id")

        Student.objects.get(Idno=di).delete()

    return redirect("home")
```

crud.html
```
<!DOCTYPE html>
<html>
<head>
    <title>Student CRUD</title>
</head>

<body>

    <h1>Student CRUD</h1>

    <h3>Add Student</h3>

    <form action="{% url 'crea' %}" method="POST">
        {% csrf_token %}

        <label>Name:</label>
        <input type="text" name="nam" placeholder="Enter Name" required>

        <br>

        <label>Email:</label>
        <input type="email" name="emai" placeholder="Enter Email" required>

        <br>

        <button type="submit">Add</button>
    </form>

    <hr>

   <h3>View Students</h3>

<table border="1">
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Email</th>
    </tr>

    {% for i in result %}
    <tr>
        <td>{{ i.Idno }}</td>
        <td>{{ i.Name }}</td>
        <td>{{ i.Email }}</td>
    </tr>
    {% endfor %}
</table>

<br>

<form action="{% url 'home' %}" method="GET">
    <button type="submit">View</button>
</form>

    <h3>Update Student</h3>

    <form action="{% url 'up' %}" method="POST">
        {% csrf_token %}

        <label>ID:</label>
        <input type="text" name="id" placeholder="Enter ID" required>

        <br>

        <label>Name:</label>
        <input type="text" name="nam" placeholder="Enter New Name" required>

        <br>

        <label>Email:</label>
        <input type="email" name="emai" placeholder="Enter New Email" required>

        <br>

        <button type="submit">Update</button>
    </form>

    <hr>

    <h3>Delete Student</h3>

    <form action="{% url 'del' %}" method="POST">
        {% csrf_token %}

        <label>ID:</label>
        <input type="text" name="id" placeholder="Enter ID" required>

        <br>

        <button type="submit">Delete</button>
    </form>

</body>
</html>
```

## OUTPUT
<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/3d1dd342-1694-4b26-a3a7-c81a2fa600b1" />



## RESULT

A Django-based CRUD web application was successfully developed to perform Create, Read, Update, and Delete operations on student records using SQLite as the backend database.


