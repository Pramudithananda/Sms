import React, { useState } from 'react';
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';

const StudentManagementSystem = () => {
  const [students, setStudents] = useState([
    { id: 1, name: 'John Doe', age: 20, grade: 'A' },
    { id: 2, name: 'Jane Smith', age: 22, grade: 'B+' }
  ]);

  const [newStudent, setNewStudent] = useState({
    name: '',
    age: '',
    grade: ''
  });

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setNewStudent(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const addStudent = () => {
    if (!newStudent.name || !newStudent.age || !newStudent.grade) return;
    
    const student = {
      id: students.length + 1,
      ...newStudent,
      age: parseInt(newStudent.age)
    };

    setStudents([...students, student]);
    setNewStudent({ name: '', age: '', grade: '' });
  };

  const deleteStudent = (id) => {
    setStudents(students.filter(student => student.id !== id));
  };

  return (
    <Card className="w-full max-w-md mx-auto">
      <CardHeader>
        <CardTitle>Student Management System</CardTitle>
      </CardHeader>
      <CardContent>
        <div className="space-y-4">
          <Input
            name="name"
            value={newStudent.name}
            onChange={handleInputChange}
            placeholder="Student Name"
            className="w-full"
          />
          <Input
            name="age"
            type="number"
            value={newStudent.age}
            onChange={handleInputChange}
            placeholder="Age"
            className="w-full"
          />
          <Input
            name="grade"
            value={newStudent.grade}
            onChange={handleInputChange}
            placeholder="Grade"
            className="w-full"
          />
          <Button onClick={addStudent} className="w-full">
            Add Student
          </Button>

          <div className="mt-4">
            <h3 className="font-bold mb-2">Student List</h3>
            {students.map(student => (
              <div 
                key={student.id} 
                className="flex justify-between items-center p-2 border-b"
              >
                <div>
                  {student.name} (Age: {student.age}, Grade: {student.grade})
                </div>
                <Button 
                  variant="destructive" 
                  size="sm"
                  onClick={() => deleteStudent(student.id)}
                >
                  Delete
                </Button>
              </div>
            ))}
          </div>
        </div>
      </CardContent>
    </Card>
  );
};

export default StudentManagementSystem;
