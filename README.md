import { useState } from "react";

export default function CricketWebsite() { const [matches, setMatches] = useState([ { id: 1, teams: "RCB vs GT", date: "2 April 2025", time: "7:30 PM", score: "0/0", status: "Upcoming", type: "Domestic" }, { id: 2, teams: "RCB vs CSK", date: "4 April 2025", time: "7:30 PM", score: "0/0", status: "Upcoming", type: "International" }, ]); const [filter, setFilter] = useState("All"); const [newMatch, setNewMatch] = useState({ teams: "", date: "", time: "", score: "0/0", status: "Upcoming", type: "Domestic" });

const filteredMatches = filter === "All" ? matches : matches.filter(match => match.type === filter);

const addMatch = () => { setMatches([...matches, { ...newMatch, id: matches.length + 1 }]); setNewMatch({ teams: "", date: "", time: "", score: "0/0", status: "Upcoming", type: "Domestic" }); };

return ( <div className="min-h-screen flex flex-col items-center bg-gray-100"> <header className="w-full bg-blue-600 text-white p-4 text-center font-bold text-xl"> Cricket Live - Founder: Akash Sharma </header>

<div className="p-4 w-full max-w-md bg-white rounded-xl shadow-md mt-4">
    <h1 className="text-xl font-bold text-center mb-4">Upcoming Matches</h1>
    <div className="flex justify-center gap-4 mb-4">
      <button className="px-3 py-1 bg-blue-500 text-white rounded" onClick={() => setFilter("All")}>All</button>
      <button className="px-3 py-1 bg-green-500 text-white rounded" onClick={() => setFilter("International")}>International</button>
      <button className="px-3 py-1 bg-yellow-500 text-white rounded" onClick={() => setFilter("Domestic")}>Domestic</button>
    </div>

    <ul className="space-y-3">
      {filteredMatches.map(match => (
        <li key={match.id} className="p-3 bg-gray-100 shadow rounded">
          <h2 className="text-lg font-semibold">{match.teams}</h2>
          <p className="text-sm text-gray-600">{match.date} - {match.time}</p>
          <p className="text-sm font-bold">Score: {match.score} | Status: {match.status}</p>
          <span className="text-xs text-gray-500">{match.type}</span>
        </li>
      ))}
    </ul>
  </div>

  <div className="p-4 w-full max-w-md bg-white rounded-xl shadow-md mt-4">
    <h2 className="text-lg font-bold">Admin Panel</h2>
    <input type="text" placeholder="Teams" className="border p-1 w-full" value={newMatch.teams} onChange={(e) => setNewMatch({ ...newMatch, teams: e.target.value })} />
    <input type="text" placeholder="Date" className="border p-1 w-full mt-2" value={newMatch.date} onChange={(e) => setNewMatch({ ...newMatch, date: e.target.value })} />
    <input type="text" placeholder="Time" className="border p-1 w-full mt-2" value={newMatch.time} onChange={(e) => setNewMatch({ ...newMatch, time: e.target.value })} />
    <input type="text" placeholder="Score" className="border p-1 w-full mt-2" value={newMatch.score} onChange={(e) => setNewMatch({ ...newMatch, score: e.target.value })} />
    <input type="text" placeholder="Status" className="border p-1 w-full mt-2" value={newMatch.status} onChange={(e) => setNewMatch({ ...newMatch, status: e.target.value })} />
    <select className="border p-1 w-full mt-2" value={newMatch.type} onChange={(e) => setNewMatch({ ...newMatch, type: e.target.value })}>
      <option value="Domestic">Domestic</option>
      <option value="International">International</option>
    </select>
    <button className="mt-2 px-3 py-1 bg-blue-500 text-white rounded w-full" onClick={addMatch}>Add Match</button>
  </div>

  <div className="fixed bottom-0 w-full bg-gray-800 text-white p-3 text-center font-semibold">
    Sticky Ads - Your Ad Here
  </div>
</div>

); }

