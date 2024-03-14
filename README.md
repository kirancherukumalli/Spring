package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class KiranprojectApplication {

	public static void main(String[] args) {
		SpringApplication.run(KiranprojectApplication.class, args);
	}

}


package com.example.demo;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name="student")
public class Student {
	@Id
	@GeneratedValue(strategy= GenerationType.IDENTITY)

   private  int id;
	@Column(name="student_name")
   private String name;
	@Column(name="student_percentage")
   private double percentage;
	@Column(name="student_grade")
   private String grade;
	@Column(name="student_branch")
   private String branch;
	
	public Student() {
		
	}
	
	public Student(String name, double percentage, String grade, String branch) {
		super();
		this.name = name;
		this.percentage = percentage;
		this.grade = grade;
		this.branch = branch;
	}

	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public double getPercentage() {
		return percentage;
	}
	public void setPercentage(double percentage) {
		this.percentage = percentage;
	}
	public String getGrade() {
		return grade;
	}
	public void setGrade(String grade) {
		this.grade = grade;
	}
	public String getBranch() {
		return branch;
	}
	public void setBranch(String branch) {
		this.branch = branch;
	}
	@Override
	public String toString() {
		return "Student [id=" + id + ", name=" + name + ", percentage=" + percentage + ", grade=" + grade + ", branch="
				+ branch + "]";
	}
   

	}




spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:3306/sohan
spring.datasource.username=root
spring.datasource.password=***
spring.datasource.driver-class-name =com.mysql.jdbc.Driver
spring.jpa.show-sql=true


package com.example.demo;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class Studentcontroller {
	private static final String Name = null;
	@Autowired
	StudentRepository repo;
	@GetMapping("/allstudents")
public  List<Student> getAllstudents(){
		List<Student>students = repo.findAll();
	return students;
}
	@GetMapping("/allstudents/{id}")
	public Student getStudent(@PathVariable int id) {
		Student student =repo.findById(id).get();
		return student;
	}
	@PostMapping("/allstudent/add")
	@ResponseStatus(code=HttpStatus.CREATED)
	public void createStudent(@RequestBody Student student) {
		repo.save(student);
	}
	@PutMapping("/student/update/{id}")
	public Student updateStudents(@PathVariable int id) {
		Student student=repo.findById(id).get();
		student.setName("Sohan");
		student.setBranch("AEO");
		student.setPercentage(99);
		repo.save(student);
		return student ;
		
	}
	
	@DeleteMapping("/student/delete/{id}")
	public void removeStudent(@PathVariable int id) {
		Student student= repo.findById(id).get();
		repo.delete(student);
	}
	
}



package com.example.demo;

import java.util.Optional;

import org.springframework.data.jpa.repository.JpaRepository;
import org.yaml.snakeyaml.events.Event.ID;

public interface StudentRepository  extends JpaRepository<Student, Integer>{

	

	
}
