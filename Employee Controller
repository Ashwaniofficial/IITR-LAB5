package com.greatlearning.ems.controller;


import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;

import com.greatlearning.ems.service.EmployeeService;
import com.greatlearning.ems.entity.Employee;


@Controller
public class EmployeeController {


    private EmployeeService employeeService;


    public EmployeeController(EmployeeService employeeService) {
        this.employeeService = employeeService;
    }
   
    @GetMapping("/employees")
    public String listEmployees(Model model) {
        model.addAttribute("employees", employeeService.getAllEmployees());
        return "employees";
    }  
    
    @GetMapping("/employees/new")
   public String createEmployeeForm(Model model) {
       // create employee object to hold employee form data
       Employee employee = new Employee();
       model.addAttribute("employee", employee);
       return "create_employee";
   }


   @PostMapping("/employees")
   public String saveEmployee(
           @ModelAttribute("employee") Employee employee) {
       employeeService.saveEmployee(employee);
       return "redirect:/employees";
   }  
   
   @GetMapping("/employees/edit/{id}")
	public String editEmployeeForm(@PathVariable Long id, Model model) {
		model.addAttribute("employee", employeeService.getEmployeeById(id));
		return "edit_employee";
	}
   
   @PostMapping("/employees/{id}")
	public String updateEmployee(
			@PathVariable Long id, 
			@ModelAttribute("employee") Employee employee, 
			Model model) {

		// get employee from database by id
		Employee existingEmployee = employeeService.getEmployeeById(id);
		existingEmployee.setId(id);
		existingEmployee.setFirstName(employee.getFirstName());
		existingEmployee.setLastName(employee.getLastName());
		existingEmployee.setEmail(employee.getEmail());

		// save updated employee object
		employeeService.updateEmployee(existingEmployee);
		return "redirect:/employees";
	}	

   
   @GetMapping("/employees/{id}")
   public String deleteEmployee(@PathVariable Long id) {
       employeeService.deleteEmployeeById(id);
       return "redirect:/employees";
   }

   

   
   

   
}
