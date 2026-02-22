### CS572-Homework-02-CRUD

Given the following Schema:
```typescript
import { Schema, model, InferSchemaType } from 'mongoose';

const EnrollmentSchema = new Schema({
    student: {
        email: { type: String, required: true },
        name: { type: String, required: true }
    },
    grade: { type: Number, min: 0, max: 100 },
    status: { 
        type: String, 
        enum: ['enrolled', 'completed', 'dropped'], 
        default: 'enrolled' 
    }
}, { timestamps: true });

const CourseSchema = new Schema({
    title: { type: String, required: true },
    code: { type: String, required: true, unique: true },
    description: { type: String, required: true },
    active: { type: Boolean, default: true },
    enrollments: [EnrollmentSchema],
}, { timestamps: true });

type CourseWithTimestamps = InferSchemaType<typeof CourseSchema>;
type EnrollmentWithTimestamps = InferSchemaType<typeof EnrollmentSchema>;

export type Course = Partial<CourseWithTimestamps>;
export type Enrollment = Partial<EnrollmentWithTimestamps>;

export const CourseModel = model<Course>('course', CourseSchema);
```
* Write a function to create a new course (with an empty enrollments[] array).
* Write a function to enroll a student in a specific course (by course id).
* Write a function to return all enrollments for a specific course id, with pagination.
* Write a function to update a student’s grade (identified by course id and enrollment id).
* Write a function to remove (delete) an enrollment by enrollment id for a specific course id.
