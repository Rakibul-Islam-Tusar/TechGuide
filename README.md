# TechGuide
Database For TechGuide
CREATE DATABASE TechGuide;
GO

-- Drop database TechGuide;

USE TechGuide;
GO

CREATE TABLE Chapters (
    ChapterID INT PRIMARY KEY IDENTITY(1,1),
    ChapterName NVARCHAR(50) NOT NULL, -- Chapter name
    ChapterVideo NVARCHAR(MAX) -- Chapter video
);

CREATE TABLE Subjects (
    SubCode INT PRIMARY KEY, -- Subject code
    SubName NVARCHAR(50) NOT NULL, -- Subject name
    ChapterID INT NULL, -- References Chapters
    FOREIGN KEY (ChapterID) REFERENCES Chapters(ChapterID) ON DELETE CASCADE
);

CREATE TABLE Department (
    DepID INT PRIMARY KEY IDENTITY(1,1),
    DepName NVARCHAR(30) NOT NULL, -- Department name
    SubCode INT NULL, -- References Subjects
    FOREIGN KEY (SubCode) REFERENCES Subjects(SubCode) ON DELETE CASCADE
);

CREATE TABLE Semester (
    SemesterID INT PRIMARY KEY IDENTITY(1,1),
    SemesterName NVARCHAR(40) NOT NULL, -- Semester name
    DepID INT NULL, -- References Department
    FOREIGN KEY (DepID) REFERENCES Department(DepID) ON DELETE CASCADE
);

CREATE TABLE Types (
    TypeID INT PRIMARY KEY IDENTITY(1,1),
    TypeName NVARCHAR(20) NOT NULL -- Type name
);

CREATE TABLE Course (
    CourseID INT PRIMARY KEY IDENTITY(1,1),
    CourseName NVARCHAR(40), -- Course name
    SemesterID INT NULL, -- References Semester
    TypeID INT NULL, -- References Types
    StartDate DATE DEFAULT GETDATE(), -- Default start date
    EndDate DATE, -- End date
    FOREIGN KEY (SemesterID) REFERENCES Semester(SemesterID) ON DELETE CASCADE,
    FOREIGN KEY (TypeID) REFERENCES Types(TypeID) ON DELETE CASCADE
);
