```plantuml
@startuml
package "Student Portal - Client" {
  [Đăng ký học phần]
  [Xem thời khóa biểu]
  [Xem điểm]
}

package "Create data - Client" {
  [Tạo dữ liệu sinh viên]
  [Tạo dữ liệu môn học]
}

package "Server" {
  [Lưu trữ đăng ký học phần API]
  [Lưu trữ sinh viên API]
  [Lưu trữ môn học API]
}

database "postgres"

[Đăng ký học phần] --> [Lưu trữ đăng ký học phần API]
[Xem thời khóa biểu] --> [Lưu trữ đăng ký học phần API]
[Xem điểm] --> [Lưu trữ đăng ký học phần API]

[Tạo dữ liệu sinh viên] --> [Lưu trữ sinh viên API]
[Tạo dữ liệu môn học] --> [Lưu trữ môn học API]

[Lưu trữ đăng ký học phần API] --> postgres
[Lưu trữ sinh viên API] --> postgres
[Lưu trữ môn học API] --> postgres
@enduml
```

```
@startuml

Interface StudentStorage {
    Student()
    Save()
    Delete()
}

Interface SubjectStorage {
    Subject()
    Save()
    Delete()
}

Interface EnrollStorage {
    Enroll()
    EnrollByStudent()
    EnrollBySubject()
    TryEnroll()
    TryEnrollByStudent()
    TryEnrollBySubject()
    Save()
    SaveTry()
    Delete()
    DeleteTry()
}

class StudentGorm {
    db *gorm.DB
}

class SubjectGorm {
    db *gorm.DB
}

class EnrollGorm {
    db *gorm.DB
}

class StudentService {
    Student()
    Save()
    Delete()
    TryEnroll()
    DeleteTryEnroll()
}

class SubjectService {
    Subject()
    Save()
    Delete()
}

class EnrollService {
    RealEnroll()
}

class StudentTransport
class SubjectTransport
class EnrollTransport

StudentStorage <|.. StudentGorm
SubjectStorage <|.. SubjectGorm
EnrollStorage <|.. EnrollGorm

StudentStorage <.. StudentService
EnrollStorage <.. StudentService
SubjectStorage <.. SubjectService
EnrollStorage <.. SubjectService
EnrollStorage <.. EnrollService

StudentService <.. StudentTransport
SubjectService <.. SubjectTransport
EnrollService <.. EnrollTransport

@enduml
```
