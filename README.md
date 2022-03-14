# SQL PRACTICE

### SQL Practice №6 | Scientists

#### Relational shema
![Relation shema](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Scientists-schema.png/300px-Scientists-schema.png)

#### The creation code
``` sql
CREATE TABLE scientists (
  SSN int,
  Name CHAR(30) NOT NULL,
  PRIMARY KEY (SSN)
);

CREATE TABLE projects (
  Code CHAR(4),
  Name CHAR(50) NOT NULL,
  Hours INT,
  PRIMARY KEY (Code)
);
	
CREATE TABLE assignedTo (
  Scientist INT NOT NULL,
  Project CHAR(4) NOT NULL,
  PRIMARY KEY (Scientist, Project),
  FOREIGN KEY (Scientist) REFERENCES scientists (SSN),
  FOREIGN KEY (Project) REFERENCES projects (Code)
);
```
#### Sample database
``` sql
 INSERT INTO scientists(SSN, Name) 
  VALUES (123234877,'Michael Rogers'),
         (152934485,'Anand Manikutty'),
         (222364883, 'Carol Smith'),
         (326587417,'Joe Stevens'),
         (332154719,'Mary-Anne Foster'),	
         (332569843,'George ODonnell'),
         (546523478,'John Doe'),
         (631231482,'David Smith'),
         (654873219,'Zacary Efron'),
         (745685214,'Eric Goldsmith'),
         (845657245,'Elizabeth Doe'),
         (845657246,'Kumar Swamy');

 INSERT INTO projects (Code, Name, Hours)
 VALUES ('AeH1','Winds: Studying Bernoullis Principle', 156),
        ('AeH2','Aerodynamics and Bridge Design',189),
        ('AeH3','Aerodynamics and Gas Mileage', 256),
        ('AeH4','Aerodynamics and Ice Hockey', 789),
        ('AeH5','Aerodynamics of a Football', 98),
        ('AeH6','Aerodynamics of Air Hockey',89),
        ('Ast1','A Matter of Time',112),
        ('Ast2','A Puzzling Parallax', 299),
        ('Ast3','Build Your Own Telescope', 6546),
        ('Bte1','Juicy: Extracting Apple Juice with Pectinase', 321),
        ('Bte2','A Magnetic Primer Designer', 9684),
        ('Bte3','Bacterial Transformation Efficiency', 321),
        ('Che1','A Silver-Cleaning Battery', 545),
        ('Che2','A Soluble Separation Solution', 778);

 INSERT INTO assignedTo (scientist, project)
   VALUES (123234877,'AeH1'),
          (152934485,'AeH3'),
          (222364883,'Ast3'),	   
          (326587417,'Ast3'),
          (332154719,'Bte1'),
          (546523478,'Che1'),
          (631231482,'Ast3'),
          (654873219,'Che1'),
          (745685214,'AeH3'),
          (845657245,'Ast1'),
          (845657246,'Ast2'),
          (332569843,'AeH4');
```
#### Exercises
1. List all the scientists' names, their projects' names, and the hours worked by that scientist on each project, in alphabetical order of project name, then scientist name.

``` sql
1. SELECT S.Name, P.Name, P.Hours FROM Scientists AS S INNER JOIN AssignedTo AS A ON S.SSN = A.Scientist INNER JOIN Projects AS P ON A.Project = P.Code ORDER BY P.Name ASC, S.Name ASC;
```
