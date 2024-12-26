// src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import { Provider } from 'react-redux';
import store from './redux/store';
import './index.css';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

// src/redux/store.js
import { configureStore } from '@reduxjs/toolkit';
import companyReducer from './slices/companySlice';
import communicationReducer from './slices/communicationSlice';
import notificationReducer from './slices/notificationSlice';

export default configureStore({
  reducer: {
    companies: companyReducer,
    communications: communicationReducer,
    notifications: notificationReducer,
  },
});

// src/redux/slices/companySlice.js
import { createSlice } from '@reduxjs/toolkit';

const companySlice = createSlice({
  name: 'companies',
  initialState: [],
  reducers: {
    addCompany(state, action) {
      state.push(action.payload);
    },
    editCompany(state, action) {
      const index = state.findIndex(c => c.id === action.payload.id);
      if (index !== -1) state[index] = action.payload;
    },
    deleteCompany(state, action) {
      return state.filter(c => c.id !== action.payload);
    },
  },
});

export const { addCompany, editCompany, deleteCompany } = companySlice.actions;
export default companySlice.reducer;

// src/components/Admin/AdminDashboard.js
import React, { useState } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { addCompany, editCompany, deleteCompany } from '../../redux/slices/companySlice';

const AdminDashboard = () => {
  const dispatch = useDispatch();
  const companies = useSelector((state) => state.companies);
  const [companyData, setCompanyData] = useState({ name: '', location: '', linkedin: '', emails: '', phone: '', comments: '', periodicity: '' });

  const handleSubmit = (e) => {
    e.preventDefault();
    if (companyData.id) {
      dispatch(editCompany(companyData));
    } else {
      dispatch(addCompany({ ...companyData, id: Date.now() }));
    }
    setCompanyData({ name: '', location: '', linkedin: '', emails: '', phone: '', comments: '', periodicity: '' });
  };

  return (
    <div className="p-4">
      <h1 className="text-xl font-bold mb-4">Admin Dashboard</h1>
      <form onSubmit={handleSubmit} className="mb-4">
        <input type="text" placeholder="Company Name" value={companyData.name} onChange={(e) => setCompanyData({ ...companyData, name: e.target.value })} className="border p-2 mb-2 w-full" required />
        <input type="text" placeholder="Location" value={companyData.location} onChange={(e) => setCompanyData({ ...companyData, location: e.target.value })} className="border p-2 mb-2 w-full" required />
        <input type="text" placeholder="LinkedIn" value={companyData.linkedin} onChange={(e) => setCompanyData({ ...companyData, linkedin: e.target.value })} className="border p-2 mb-2 w-full" />
        <input type="text" placeholder="Emails" value={companyData.emails} onChange={(e) => setCompanyData({ ...companyData, emails: e.target.value })} className="border p-2 mb-2 w-full" />
        <input type="text" placeholder="Phone" value={companyData.phone} onChange={(e) => setCompanyData({ ...companyData, phone: e.target.value })} className="border p-2 mb-2 w-full" />
        <textarea placeholder="Comments" value={companyData.comments} onChange={(e) => setCompanyData({ ...companyData, comments: e.target.value })} className="border p-2 mb-2 w-full" />
        <input type="text" placeholder="Periodicity" value={companyData.periodicity} onChange={(e) => setCompanyData({ ...companyData, periodicity: e.target.value })} className="border p-2 mb-2 w-full" />
        <button type="submit" className="bg-blue-500 text-white p-2 rounded">{companyData.id ? 'Edit Company' : 'Add Company'}</button>
      </form>

      <div>
        <h2 className="text-lg font-bold mb-2">Company List</h2>
        <ul>
          {companies.map((company) => (
            <li key={company.id} className="mb-2 flex justify-between items-center">
              <span>{company.name}</span>
              <div>
                <button onClick={() => setCompanyData(company)} className="bg-yellow-500 text-white p-2 rounded mr-2">Edit</button>
                <button onClick={() => dispatch(deleteCompany(company.id))} className="bg-red-500 text-white p-2 rounded">Delete</button>
              </div>
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
};

export default AdminDashboard;

// src/App.js
import React from 'react';
import AdminDashboard from './components/Admin/AdminDashboard';

const App = () => {
  return (
    <div>
      <AdminDashboard />
    </div>
  );
};

export default App;
