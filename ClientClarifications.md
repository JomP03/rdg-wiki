# Client Clarifications

## Introduction

This document is intended to serve as a hub for all the clarifications that the client has made regarding the project 
in the forum and during the meetings.

All the relevant information provided by the client in the forum will be summarized here.

The information will be organized and aggregated by requirement.

### 150 - Create a building

- A building has a mandatory code, an optional name and an optional description, and has the maximum dimensions of each
floor in terms of cells (e.g., 10 x 10).
- The building code is mandatory and unique, up to 5 characters, letters and digits, and may contain spaces in the middle.
- The building name is optional, up to 50 alphanumeric characters.
- The building description is optional, up to 255 characters.

Sources: 
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25047),
[2](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25016)

### 160 - Edit a building

- All the building information can be edited, except for the building code.

Source: 
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25168)

### 190 - Create a floor

- A floor is created and associated with a building, has a number (e.g., floor number 1), and has a brief description
- The floor number is unique within the building, and is an integer.
- The floor description is optional, up to 250 characters.

Sources: 
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25016), 
[2](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25248)

### 200 - Edit a floor information

- All the floor information can be edited, except for the building to which it is associated.

Source:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25168)

### US230 - Load Floor Plan

- The floor plan format could be adapted according to the requirements and design decisions.
- The floor plan is assumed to be introduced with coherent information and without errors. In the future there will be a
  floor editor that will ensure the coherence of the floor plan with the persisted data.

Sources:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25070),
[2](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25069)


### 240 - Create a passage between buildings

- A passage connects two floors of two different buildings.
- It is possible to have a multiple passages in one floor, each for different buildings.
- In the same building it is possible to have multiple passages to the same building, but in different floors.
- A passage has two points, each point has the association to a floor and the coordinates of the point in the floor.

Source:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25082)

### 250 - Edit a passage between buildings

- All information about a passage can be edited.

Source:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25168)

### 270 - Create an elevator in a building

- An elevator has an association to a building, an identification number, a list of floors that it serves, a brand,
a model, a serial number and a brief description.
- The elevator identification number is unique within the building and mandatory.
- The elevator brand is optional, up to 50 alphanumeric characters.
- The elevator model is optional, up to 50 alphanumeric characters, but if the brand is specified, the model is mandatory.
- The elevator serial number is optional, up to 50 alphanumeric characters.
- The elevator description is optional, up to 250 characters.

Source:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25298#p32051)

### 280 - Edit an elevator in a building

- All information about an elevator can be edited, except for the building to which it is associated.

Source:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25168)

### 310 - Create a room

- A room has a nome, a description, a category, the dimensions, a position for the door and a floor.
- The room name is mandatory, up to 50 alphanumeric characters.
- The room description is mandatory, up to 250 characters.
- The floor's minimum dimensions are 1 x 1.

Sources:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25016),
[2](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25276)

### 350 - Add a mew robot type

- There only two types of tasks a robot type can have: "transport" and "surveillance".
- The robot type is mandatory, up to 25 alphanumeric characters.
- The robot brand is mandatory, up to 50 alphanumeric characters.
- The robot model is mandatory, up to 100 alphanumeric characters.

Sources:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25045),
[2](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25101),
[3](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25171)

### US360 - Add Robot To The Fleet

- The robot should be of a given Robot Type.
- The robot must have an id code, mandatory, unique and with a maximum of 30 characters.
- The robot must have a nickname, which must be unique with a maximum of 30 characters.
- The robot must have a serial number, mandatory, unique and with a maximum of 50 characters. Unique for a given Robot Type.
- The robot must have a description, optional, with a maximum of 250 characters.

Sources:
[1](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25101),
[2](https://moodle.isep.ipp.pt/mod/forum/discuss.php?d=25265)

### US10 - Create End-user

"If you use an IAM provider, e.g. google, to register users, you can do this in steps, starting with authentication in the IAM and then collecting the data mentioned."

"The use of an IAM system is primarily for users but can be used for all users of the system. regarding the creation/registration of users, please refer to the previous answers in the forum."

"The email will be the username that identifies each user."

"At the moment the initial password must be entered by the administrator when creating the account. the password policy is as follows:
* minimum 10 characters;
* at least 1 capital letter;
* at least 1 lowercase letter;
* at least 1 digit;
* at least 1 symbol."

"Creating users and registering users are two different use cases with different needs.
User creation is for system administrators to create the system's various backoffice users in one of the designated roles, e.g. campus manager, fleet manager, task manager."

"User registration is used to register users with the user role.
In both cases it will be necessary to obtain a name, email address and telephone number."

"When registering users, the tax number must also be collected for invoicing services."

"Only emails from the organization will be accepted, e.g. isep.ipp.pt."

NOTE: the parameterization of the accepted email domain must be kept out of the project's source code, e.g. properties file or environment variable.

"The administrator assigns the role when creating users."

"Users who use the registration functionality will always be of the "user" type"