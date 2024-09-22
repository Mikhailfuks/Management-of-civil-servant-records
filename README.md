using System;
using System.Collections.Generic;
using System.Linq;

namespace CivilServantManagement
{
    // Civil Servant Class
    public class CivilServant
    {
        public int Id { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime DateOfBirth { get; set; }
        public string Department { get; set; }
        public string Position { get; set; }
        public decimal Salary { get; set; }

        public CivilServant(int id, string firstName, string lastName, DateTime dateOfBirth, string department, string position, decimal salary)
        {
            Id = id;
            FirstName = firstName;
            LastName = lastName;
            DateOfBirth = dateOfBirth;
            Department = department;
            Position = position;
            Salary = salary;
        }
    }

    // Civil Servant Management System
    public class CivilServantManagementSystem
    {
        private List<CivilServant> civilServants = new List<CivilServant>();
        private int nextId = 1;

        // Add a new civil servant
        public void AddCivilServant(string firstName, string lastName, DateTime dateOfBirth, string department, string position, decimal salary)
        {
            civilServants.Add(new CivilServant(nextId++, firstName, lastName, dateOfBirth, department, position, salary));
            Console.WriteLine("Civil servant added successfully.");
        }

        // Update a civil servant's details
        public void UpdateCivilServant(int id, string firstName = null, string lastName = null, DateTime? dateOfBirth = null, string department = null, string position = null, decimal? salary = null)
        {
            CivilServant civilServant = civilServants.FirstOrDefault(c => c.Id == id);

            if (civilServant != null)
            {
                if (firstName != null) civilServant.FirstName = firstName;
                if (lastName != null) civilServant.LastName = lastName;
                if (dateOfBirth != null) civilServant.DateOfBirth = (DateTime)dateOfBirth;
                if (department != null) civilServant.Department = department;
                if (position != null) civilServant.Position = position;
                if (salary != null) civilServant.Salary = (decimal)salary;

                Console.WriteLine("Civil servant updated successfully.");
            }
            else
            {

                Console.WriteLine("Error: Civil servant not found.");
            }
        }

        // Delete a civil servant
        public void DeleteCivilServant(int id)
        {
            CivilServant civilServant = civilServants.FirstOrDefault(c => c.Id == id);

            if (civilServant != null)
            {
                civilServants.Remove(civilServant);
                Console.WriteLine("Civil servant deleted successfully.");
            }
            else
            {
                Console.WriteLine("Error: Civil servant not found.");
            }
        }

        // Display all civil servants
        public void DisplayAllCivilServants()
        {
            Console.WriteLine("Civil Servants:");
            foreach (CivilServant civilServant in civilServants)
            {
                Console.WriteLine($"ID: {civilServant.Id}, Name: {civilServant.FirstName} {civilServant.LastName}, Date of Birth: {civilServant.DateOfBirth.ToShortDateString()}, Department: {civilServant.Department}, Position: {civilServant.Position}, Salary: {civilServant.Salary}");
            }
        }

        // Search civil servants by name
        public void SearchCivilServantsByName(string name)
        {
            var results = civilServants.Where(c => c.FirstName.Contains(name) || c.LastName.Contains(name));

            if (results.Any())
            {
                Console.WriteLine("Search Results:");
                foreach (CivilServant civilServant in results)
                {
                    Console.WriteLine($"ID: {civilServant.Id}, Name: {civilServant.FirstName} {civilServant.LastName}, Date of Birth: {civilServant.DateOfBirth.ToShortDateString()}, Department: {civilServant.Department}, Position: {civilServant.Position}, Salary: {civilServant.Salary}");
                }
            }
            else
            {
                Console.WriteLine("No matching civil servants found.");
            }
        }

        public static void Main(string[] args)
        {
            CivilServantManagementSystem system = new CivilServantManagementSystem();

            // Add some initial civil servants
            system.AddCivilServant("John", "Doe", new DateTime(1980, 1, 1), "Finance", "Accountant", 50000);
            system.AddCivilServant("Jane", "Smith", new DateTime(1985, 5, 15), "IT", "Software Engineer", 65000);

            // Display all civil servants
            system.DisplayAllCivilServants();

            // Update a civil servant's salary
            system.UpdateCivilServant(1, salary: 60000);

            // Delete a civil servant
            system.DeleteCivilServant(1);

            // Display all civil servants again
            system.DisplayAllCivilServants();

            // Search for civil servants by name
            system.SearchCivilServantsByName("Jane");

            Console.ReadKey();
        }
    }
}
