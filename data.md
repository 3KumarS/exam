Experiment–1
Aim:To demonstrate the use of Wildcard in Java Generics.

code:

import java.util.*;

class WildcardDemo {

    // 1. Unbounded Wildcard
    static void showList(List<?> list) {
        for (Object o : list) {
            System.out.println(o);
        }
    }

    // 2. Upper Bounded Wildcard
    static void showNumbers(List<? extends Number> list) {
        for (Number n : list) {
            System.out.println(n);
        }
    }

    // 3. Lower Bounded Wildcard
    static void addNumbers(List<? super Integer> list) {
        list.add(10);
        list.add(20);
    }

    public static void main(String[] args) {

        List<Integer> intList = new ArrayList<>();
        intList.add(1);
        intList.add(2);

        List<Double> doubleList = new ArrayList<>();
        doubleList.add(10.5);
        doubleList.add(20.5);

        List<Number> numList = new ArrayList<>();

        showList(intList);        // <?>
        showNumbers(doubleList); // <? extends>
        addNumbers(numList);      // <? super>

        System.out.println(numList);
    }
}


Output:

1
2
10.5
20.5
[10, 20]

-----------------
Experiment–2 

Aim : To write a Java program to create a List of items and use ListIterator to print the elements in forward and backward direction.

Code:

import java.util.*;

class ListIteratorDemo {

    public static void main(String[] args) {

        List<String> list = new ArrayList<>();

        list.add("Java");
        list.add("MCA");
        list.add("Generics");
        list.add("Spring");

        // ListIterator
        ListIterator<String> itr = list.listIterator();

        System.out.println("Forward Direction:");
        while (itr.hasNext()) {
            System.out.println(itr.next());
        }

        System.out.println("\nBackward Direction:");
        while (itr.hasPrevious()) {
            System.out.println(itr.previous());
        }
    }
}

Output:

Forward Direction:
Java
MCA
Generics
Spring

Backward Direction:
Spring
Generics
MCA
Java

----------------------

Experiment–3
Write a Java program to create a Set containing list of items of type String and print the items in the list using Iterator interface. Also print the list in reverse / backward direction.

Code:

import java.util.*;

class SetIteratorDemo {

    public static void main(String[] args) {

        Set<String> set = new HashSet<>();

        set.add("Java");
        set.add("MCA");
        set.add("Spring");
        set.add("Generics");

        // Forward direction using Iterator
        System.out.println("Forward Direction:");
        Iterator<String> itr = set.iterator();

        while (itr.hasNext()) {
            System.out.println(itr.next());
        }

        // Convert Set to List for reverse traversal
        List<String> list = new ArrayList<>(set);
        ListIterator<String> listItr = list.listIterator(list.size());

        // Backward direction
        System.out.println("\nBackward Direction:");
        while (listItr.hasPrevious()) {
            System.out.println(listItr.previous());
        }
    }
}


OutPut:

Forward Direction:
Java
MCA
Spring
Generics

Backward Direction:
Generics
Spring
MCA
Java

--------------------

Experiment–4

Write a Java program using Map interface containing list of items having keys and associated values and perform the following operations:
a) Add items in the map
b) Remove items from the map
c) Search specific key from the map

Code:

import java.util.*;

class MapDemo {

    public static void main(String[] args) {

        Map<Integer, String> map = new HashMap<>();

        // a) Add items
        map.put(101, "Ram");
        map.put(102, "Shyam");
        map.put(103, "Mohan");

        System.out.println("Map Elements:");
        System.out.println(map);

        // b) Remove item
        map.remove(102);

        System.out.println("\nAfter Removing Key 102:");
        System.out.println(map);

        // c) Search specific key
        int searchKey = 101;
        if (map.containsKey(searchKey)) {
            System.out.println("\nKey " + searchKey + " found. Value = " + map.get(searchKey));
        } else {
            System.out.println("\nKey not found");
        }
    }
}


Output :

Map Elements:
{101=Ram, 102=Shyam, 103=Mohan}

After Removing Key 102:
{101=Ram, 103=Mohan}

Key 101 found. Value = Ram

----------------------

Experiment–5
Write a Java program using Lambda Expression with multiple parameters to add two numbers.

Code:

interface Addable {
    int add(int a, int b);
}

class LambdaDemo {

    public static void main(String[] args) {

        Addable obj = (a, b) -> a + b;

        System.out.println("Addition = " + obj.add(10, 20));
    }
}




Output:

Sum = 30

-----------------------


Experiment–6
Write a JSP page to display the Registration Form (Make your own assumptions)
Code:

<%@ page language="java" contentType="text/html" %>

<html>
<head>
    <title>Registration Form</title>
</head>
<body>

<h2>Student Registration</h2>

<form action="success.jsp" method="post">

    Name: <input type="text" name="name" /><br><br>

    Email: <input type="email" name="email" /><br><br>

    Password: <input type="password" name="password" /><br><br>

    Course:
    <select name="course">
        <option>MCA</option>
        <option>BCA</option>
        <option>BSc</option>
    </select><br><br>

    Gender:
    <input type="radio" name="gender" value="Male">Male
    <input type="radio" name="gender" value="Female">Female<br><br>

    <input type="submit" value="Register" />

</form>

</body>
</html>

Output:
Student Registration
Name → textbox


Email → textbox


Password → password field


Course → dropdown (MCA, BCA, BSc)


Gender → radio buttons (Male / Female)


Register → submit button

------------------------


Experiment–7
Write a JSP program to add, delete and display the records from StudentMaster
 (RollNo, Name, Semester, Course) table.

1️⃣ Database Table (Exam Assumption ✔️)
CREATE TABLE StudentMaster (
    RollNo INT PRIMARY KEY,
    Name VARCHAR(50),
    Semester INT,
    Course VARCHAR(20)
);

2️⃣ JSP to INSERT record
📄 insert.jsp


<%@ page import="java.sql.*" %>

<%
int roll = Integer.parseInt(request.getParameter("roll"));
String name = request.getParameter("name");
int sem = Integer.parseInt(request.getParameter("sem"));
String course = request.getParameter("course");

Class.forName("com.mysql.jdbc.Driver");
Connection con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/mca", "root", "root");

PreparedStatement ps = con.prepareStatement(
    "INSERT INTO StudentMaster VALUES(?,?,?,?)");

ps.setInt(1, roll);
ps.setString(2, name);
ps.setInt(3, sem);
ps.setString(4, course);

ps.executeUpdate();

out.println("Record Inserted Successfully");

con.close();
%>



3️⃣ JSP to DISPLAY records
📄 display.jsp

<%@ page import="java.sql.*" %>

<table border="1">
<tr>
    <th>Roll No</th>
    <th>Name</th>
    <th>Semester</th>
    <th>Course</th>
</tr>

<%
Class.forName("com.mysql.jdbc.Driver");
Connection con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/mca", "root", "root");

Statement st = con.createStatement();
ResultSet rs = st.executeQuery("SELECT * FROM StudentMaster");

while(rs.next()) {
%>
<tr>
    <td><%= rs.getInt(1) %></td>
    <td><%= rs.getString(2) %></td>
    <td><%= rs.getInt(3) %></td>
    <td><%= rs.getString(4) %></td>
</tr>
<%
}
con.close();
%>
</table>



4️⃣ JSP to DELETE record
📄 delete.jsp

<%@ page import="java.sql.*" %>

<%
int roll = Integer.parseInt(request.getParameter("roll"));

Class.forName("com.mysql.jdbc.Driver");
Connection con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/mca", "root", "root");

PreparedStatement ps =
    con.prepareStatement("DELETE FROM StudentMaster WHERE RollNo=?");

ps.setInt(1, roll);
ps.executeUpdate();

out.println("Record Deleted Successfully");

con.close();
%>


