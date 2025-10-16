import React from "react";
import { useState } from "react";

const EmployeeTable = () => {
  const [employees, setEmployees] = useState([
    { name: "Alice", dept: "HR", salary: 50000 },
    { name: "Bob", dept: "Engineering", salary: 80000 },
    { name: "Charlie", dept: "Finance", salary: 60000 },
    { name: "Diana", dept: "Engineering", salary: 75000 },
  ]);

  const [sortConfig, setSortConfig] = useState({ key: null, direction: "asc" });

  const handleSort = (key) => {
    let direction = "asc";
    if (sortConfig.key === key && sortConfig.direction === "asc") {
      direction = "desc";
    }

    const sortedData = [...employees].sort((a, b) => {
      if (a[key] < b[key]) return direction === "asc" ? -1 : 1;
      if (a[key] > b[key]) return direction === "asc" ? 1 : -1;
      return 0;
    });

    setEmployees(sortedData);
    setSortConfig({ key, direction });
  };

  return (
    <div className="p-6">
      <h2 className="text-xl font-semibold mb-4">Employee Table</h2>
      <table className="min-w-full border border-gray-300 rounded-lg shadow">
        <thead className="bg-gray-200">
          <tr>
            <th
              className="cursor-pointer px-4 py-2"
              onClick={() => handleSort("name")}
            >
              Name {sortConfig.key === "name" ? (sortConfig.direction === "asc" ? "▲" : "▼") : ""}
            </th>
            <th
              className="cursor-pointer px-4 py-2"
              onClick={() => handleSort("dept")}
            >
              Department {sortConfig.key === "dept" ? (sortConfig.direction === "asc" ? "▲" : "▼") : ""}
            </th>
            <th
              className="cursor-pointer px-4 py-2"
              onClick={() => handleSort("salary")}
            >
              Salary {sortConfig.key === "salary" ? (sortConfig.direction === "asc" ? "▲" : "▼") : ""}
            </th>
          </tr>
        </thead>
        <tbody>
          {employees.map((emp, index) => (
            <tr key={index} className="text-center border-t hover:bg-gray-100 transition">
              <td className="px-4 py-2">{emp.name}</td>
              <td className="px-4 py-2">{emp.dept}</td>
              <td className="px-4 py-2">${emp.salary}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default EmployeeTable;
