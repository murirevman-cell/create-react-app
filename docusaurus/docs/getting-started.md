import React, { useState } from 'react';

const PlacedLabors = () => {
  // Mock data - In a real app, this comes from your database (API)
  const [labors] = useState([
    { id: 1, name: "Abebe Kebede", passport: "EP123456", country: "Saudi Arabia", status: "Deployed", date: "2023-10-12" },
    { id: 2, name: "Mulugeta Tesfaye", passport: "EP987654", country: "UAE", status: "In Process", date: "2023-11-05" },
    { id: 3, name: "Sara Mohammed", passport: "EP456789", country: "Qatar", status: "Deployed", date: "2023-09-20" },
  ]);

  const [searchTerm, setSearchTerm] = useState("");

  const filteredLabors = labors.filter(labor => 
    labor.name.toLowerCase().includes(searchTerm.toLowerCase()) || 
    labor.passport.includes(searchTerm)
  );

  return (
    <div className="p-6 bg-gray-50 min-h-screen">
      {/* Header Section */}
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-2xl font-bold text-gray-800">Placed Labors List</h1>
        <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700">
          + Add New Placement
        </button>
      </div>

      {/* Filter/Search Bar */}
      <div className="bg-white p-4 rounded-lg shadow-sm mb-6 flex gap-4">
        <input 
          type="text" 
          placeholder="Search by name or passport..." 
          className="border p-2 rounded w-full md:w-1/3"
          onChange={(e) => setSearchTerm(e.target.value)}
        />
        <select className="border p-2 rounded bg-white">
          <option>All Statuses</option>
          <option>Deployed</option>
          <option>In Process</option>
        </select>
      </div>

      {/* Data Table */}
      <div className="bg-white rounded-lg shadow overflow-hidden">
        <table className="w-full text-left border-collapse">
          <thead className="bg-gray-100 border-b">
            <tr>
              <th className="p-4 font-semibold text-gray-600">Full Name</th>
              <th className="p-4 font-semibold text-gray-600">Passport No.</th>
              <th className="p-4 font-semibold text-gray-600">Destination</th>
              <th className="p-4 font-semibold text-gray-600">Status</th>
              <th className="p-4 font-semibold text-gray-600">Date Placed</th>
              <th className="p-4 font-semibold text-gray-600">Action</th>
            </tr>
          </thead>
          <tbody>
            {filteredLabors.map(labor => (
              <tr key={labor.id} className="border-b hover:bg-gray-50 transition">
                <td className="p-4">{labor.name}</td>
                <td className="p-4 font-mono text-sm">{labor.passport}</td>
                <td className="p-4">{labor.country}</td>
                <td className="p-4">
                  <span className={`px-2 py-1 rounded-full text-xs ${
                    labor.status === 'Deployed' ? 'bg-green-100 text-green-700' : 'bg-yellow-100 text-yellow-700'
                  }`}>
                    {labor.status}
                  </span>
                </td>
                <td className="p-4 text-gray-500">{labor.date}</td>
                <td className="p-4">
                  <button className="text-blue-600 hover:underline">View Details</button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
};

export default PlacedLabors;
