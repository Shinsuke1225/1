// App.js
import React, { useState } from 'react';
import ReservationForm from './ReservationForm';

function App() {
  const [reservations, setReservations] = useState([]);

  const addReservation = (newReservation) => {
    setReservations([...reservations, newReservation]);
  };

  return (
    <div className="App">
      <h1>Little Lemon </h1>
      <ReservationForm onAddReservation={addReservation} />
      <h2>目前預訂：</h2>
      <ul>
        {reservations.map((reservation, index) => (
          <li key={index}>
            {reservation.name} - {reservation.date} - {reservation.time}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;


// ReservationForm.js
import React, { useState } from 'react';

function ReservationForm({ onAddReservation }) {
  const [name, setName] = useState('');
  const [date, setDate] = useState('');
  const [time, setTime] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    const newReservation = { name, date, time };
    onAddReservation(newReservation);
    setName('');
    setDate('');
    setTime('');
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="姓名"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <input
        type="date"
        value={date}
        onChange={(e) => setDate(e.target.value)}
      />
      <input
        type="time"
        value={time}
        onChange={(e) => setTime(e.target.value)}
      />
      <button type="submit">預訂</button>
    </form>
  );
}

export default ReservationForm;
